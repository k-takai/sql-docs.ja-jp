---
title: SQL Server Usage Feedback Collection の Local Audit | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Local Audit
ms.assetid: a0665916-7789-4f94-9086-879275802cf3
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 983b5a1e1597aee61400b121d19aa8436512b06a
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2018
ms.locfileid: "34770768"
---
# <a name="local-audit-for-sql-server-usage-feedback-collection"></a>SQL Server Usage Feedback Collection の Local Audit

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

## <a name="introduction"></a>概要

Microsoft SQL Server は、お客様のコンピューターまたはデバイスに関する情報を収集して送信するインターネット対応の機能を備えています。 これは*標準的なコンピューター情報*と呼ばれています。 [SQL Server Usage Feedback Collection](http://support.microsoft.com/kb/3153756) の Local Audit コンポーネントは、サービスで収集されたデータを保存先フォルダーに出力します。このデータは、Microsoft に送信されるデータ (ログ) です。 Local Audit の目的は、Microsoft がこの機能で収集するすべてのデータをユーザーがコンプライアンス、法規制、またはプライバシーの検証目的で確認できるようにすることです。  

SQL Server 2016 CU2 以降、Local Audit は SQL Server Database Engine and Analysis Services (SSAS) のインスタンス レベルで構成できるようになりました。 SQL Server 2016 CU4 および SQL Server 2016 SP1 では、Local Audit は SQL Server Integration Services (SSIS) に対しても有効になります。 セットアップ中にインストールされる他の SQL Server コンポーネントと、セットアップ後にダウンロードまたはインストールされる SQL Server ツールには、使用状況フィードバック収集用の Local Audit 機能はありません。 

## <a name="prerequisites"></a>Prerequisites 

各 SQL Server インスタンスで Local Audit を有効にする前提条件は次のとおりです。 

1. インスタンスには SQL Server 2016 RTM CU2 以降の修正プログラムが適用されている。 Integration Services の場合、インスタンスには SQL 2016 RTM CU4 または SQL 2016 SP1 の修正プログラムが適用されている。

1. ユーザーはシステム管理者であるか、レジストリ キーの追加および変更、フォルダーの作成、フォルダー セキュリティの管理、および Windows サービスの停止/開始を行うアクセス権を持つロールである必要があります。  

## <a name="pre-configuration-steps-prior-to-turning-on-local-audit"></a>Local Audit を有効にする前の事前構成手順 

Local Audit を有効にする前に、システム管理者には次の準備が必要です。

1. SQL Server インスタンス名と SQL Server CEIP テレメトリ サービス ログオン アカウントを把握する。 

1. Local Audit ファイル用の新しいフォルダーを構成する。

1. SQL Server CEIP テレメトリ サービス ログオン アカウントにアクセス許可を付与する。

1. Local Audit ターゲット ディレクトリを構成するレジストリ キー設定を作成する。 


### <a name="get-the-sql-server-ceip-service-logon-account"></a>SQL Server CEIP サービス ログイン アカウントを取得する 

次の手順で、SQL Server CEIP テレメトリ サービス ログイン アカウントを取得します
 
1. **サービス** コンソールを起動します。 これを行うには、キーボードで **Windows キーを押しながら R キー**を押し、**[実行]** ダイアログ ボックスを開きます。 次に、テキスト フィールドに「*services.msc*」と入力し、**[OK]** を選択して**サービス** コンソールを起動します。  

2. 目的のサービスに移動します。 たとえば、データベース エンジンの場合、**SQL Server CEIP サービス** **(*Your-Instance-Name*)** を探します。 Analysis Services の場合、**SQL Server Analysis Services CEIP** **(*Your-Instance-Name*)** を探します。 Integration Services の場合は、**SQL Server Integration Services CEIP サービス**を探します。

3. サービスを右クリックし、 **[プロパティ]** を選択します。 

4. **[ログオン]** タブを選択します。ログオン アカウントは **[このアカウント]** に表示されます。 

### <a name="configure-a-new-folder-for-the-local-audit-files"></a>Local Audit ファイル用の新しいフォルダーを構成する。    

Local Audit がログを出力する新しいフォルダー (Local Audit ディレクトリ) を作成します。 たとえば、データベース エンジンの既定インスタンスの Local Audit ディレクトリの完全なパスは、*C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\* です。 
 
  >[!NOTE] 
  >監査機能や修正プログラムによって SQL Server に問題が発生する可能性を防ぐには、SQL Server インストール パス以外の Local Audit のディレクトリ パスを構成してください。

  ||設計上の決定|推奨|  
  |------|-----------------|----------|  
  |![チェック ボックス](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "チェック ボックス")|空き領域 |データベース数が約 10 個で中程度のワークロードの場合、インスタンスごとにデータベースあたり約 2 MB のディスク領域で計画を立てます。|  
|![チェック ボックス](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "チェック ボックス")|別のディレクトリ | 各インスタンス用にディレクトリを作成します。 たとえば、`MSSQLSERVER` という SQL Server インスタンス用には *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\* を使用します。 こうすることでファイルの管理が簡単になります。
|![チェック ボックス](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "チェック ボックス")|別のディレクトリ |サービスごとに別のフォルダーを使用します。 たとえば、1 つのインスタンス名について、データベース エンジン用に 1 つのフォルダーを用意します。 Analysis Services のインスタンスで同じインスタンス名を使用する場合は、Analysis Services 用に別のフォルダーを作成します。 データベース エンジンと Analysis Services の両インスタンスを同じフォルダーに構成すると、すべての Local Audit で両インスタンスのログが同じログ ファイルに出力されます。| 
|![チェック ボックス](../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "チェック ボックス")|SQL Server CEIP テレメトリ サービス ログオン アカウントにアクセス許可を付与する|SQL Server CEIP テレメトリ サービス ログイン アカウントに対する **フォルダーの内容の一覧表示**、 **読み取り** 、および **書き込み** の各アクセス権を有効にします|


### <a name="grant-permissions-to-the-sql-server-ceip-telemetry-service-logon-account"></a>SQL Server CEIP テレメトリ サービス ログオン アカウントにアクセス許可を付与する
  
1. **エクスプローラー**で、新しいフォルダーがある場所に移動します。

1. 新しいフォルダーを右クリックし、 **[プロパティ]** をクリックします。 

1. **[セキュリティ]** タブの **[編集]** を選択し、権限を管理します。

1. **[追加]** を選択し、SQL Server CEIP テレメトリ サービスの資格情報を入力します。 たとえば、 `NT Service\SQLTELEMETRY`があります。

1. **[名前の確認]** を選択して入力した名前を検証し、**[OK]** を選択します。

1. **[権限]** ダイアログ ボックスで、SQL Server CEIP テレメトリ サービスのログオン アカウントを選択し、**[フォルダーの内容の一覧表示]**、**[読み取り]**、**[書き込み]** を選択します。

1. **[OK]** を選択すると、権限の変更が直ちに適用されます。 
  
### <a name="create-a-registry-key-setting-to-configure-local-audit-target-directory"></a>Local Audit ターゲット ディレクトリを構成するレジストリ キー設定を作成する

1. regedit を起動します。

1. 目的の CPE パスに移動します。

   | [バージョンのオプション] | ***データベース エンジン*** - レジストリ キー |
   | :------ | :----------------------------- |
   | 2016    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL**13**.*Your-Instance-Name*\\CPE |
   | 2017    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSSQL**14**.*Your-Instance-Name*\\CPE |
   | &nbsp; | &nbsp; |

   | [バージョンのオプション] | ***Analysis Services*** - レジストリ キー |
   | :------ | :------------------------------- |
   | 2016    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS**13**.*Your-Instance-Name*\\CPE |
   | 2017    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\MSAS**14**.*Your-Instance-Name*\\CPE |
   | &nbsp; | &nbsp; |

  | [バージョンのオプション] | ***Integration Services*** - レジストリ キー |
  | :------ | :---------------------------------- |
  | 2016    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\**130** |
  | 2017    | HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Microsoft SQL Server\\**140** |
  | &nbsp; | &nbsp; |

1. CPE パスを右クリックし、**[新規]** を選択します。 **[文字列値]** を選択します。

1. 新しいレジストリ キーに `UserRequestedLocalAuditDirectory`と名前を付けます。 
 
## <a name="turning-local-audit-on-or-off"></a>Local Audit の有効/無効を切り替える

事前構成手順を完了したら、Local Audit を有効にすることができます。 有効にするには、システム管理者アカウント、またはレジストリ キーを変更するアクセス権を持つ同様のロールを使用し、次の手順に従って Local Audit の有効/無効を切り替えます。 

1. **regedit**を起動します。  

1. 目的の CPE [パス](#create-a-registry-key-setting-to-configure-local-audit-target-directory)に移動します。 

1. **[UserRequestedLocalAuditDirectory]** を右クリックし、*[変更]* を選択します。 

1. Local Audit を有効にするには、Local Audit のパスを入力します (例: *C:\\SQLCEIPAudit\\MSSQLSERVER\\DB\\*)。
 
    Local Audit を無効にするには、**[UserRequestedLocalAuditDirectory]** の値を空にします。

1. **regedit**を閉じます。 

SQL Server CEIP が既に実行中の場合、Local Audit 設定は直ちに認識されます。 SQL Server CEIP サービスを開始するには、システム管理者、または Windows サービスを開始または停止するアクセス権を持つユーザーが、次の手順を実行します。 

1. **サービス** コンソールを起動します。 これを行うには、キーボードで **Windows キーを押しながら R キー**を押し、**[実行]** ダイアログ ボックスを開きます。 次に、テキスト フィールドに「*services.msc*」と入力し、**[OK]** を選択して**サービス** コンソールを起動します。  

1. 目的のサービスに移動します。 

    - データベース エンジンの場合、「**SQL Server CEIP サービス (*Your-Instance-Name*)**」を使用します。     
    - Analysis Services の場合、「**SQL Server Analysis Services CEIP (*Your-Instance-Name*)**」を使用します。
    - Integration Services の場合、 
        - SQL 2016 の場合、「*SQL Server Integration Services CEIP サービス 13.0*」を使用します。
        - SQL 2017 の場合、「*SQL Server Integration Services CEIP サービス 14.0*」を使用します。

1. サービスを右クリックし、[再起動] を選択します。 

1. サービスの状態が "**実行中**" であることを確認します。 

Local Audit では、1 日に 1 つのログ ファイルが生成されます。 ログ ファイルは `<YYYY-MM-DD>.json`の形式です。 たとえば、 *2016-07-12.json*というファイル名です。 保存先ディレクトリにその日のファイルが既にある場合、Local Audit のログはそのファイルに付加されます。 既存のファイルがない場合、その日の新しいファイルが作成されます。 

  >[!NOTE]
  > Local Audit を有効にしてから、初めてログ ファイルに出力されるまでに最長 5 分間かかることがあります。 

## <a name="maintenance"></a>メンテナンス 

1. Local Audit から出力されるファイルのディスク使用量を制限するには、Local Audit ディレクトリをクリーンアップして古い不要なファイルを削除するポリシーまたは定期ジョブを設定します。  

2. Local Audit ディレクトリ パスには適切なユーザーのみがアクセスできるようにセキュリティで保護します。 ログ ファイルには、[フィードバックを Microsoft に送信するように SQL Server 2016 を構成する](http://support.microsoft.com/kb/3153756)方法に関するページで説明されている情報が含まれています。 このファイルに対するアクセス権では、組織のほとんどのメンバーに読み取りを禁止することが推奨されます。  

## <a name="data-dictionary-of-local-audit-output-data-structure"></a>Local Audit 出力データ構造のデータ辞書 

- Local Audit ログ ファイルは JSON 形式です。 **emitTime**で Microsoft に送信されるデータ ポイントを表すオブジェクト (行) のセットが含まれます。
- 各行は、 **schemaVersion**に指定された特定のスキーマに従います。
- 各行は、 **sessionID**に指定された SQLCEIP サービス セッションの出力です。
- 行は、 **sequence**に指定された順に出力されます。
- 各データ ポイント行には、**queryIdentifier** の出力が含まれています。この出力は、**traceName** に指定されたトレースの種類に関連する T-SQL クエリ、XE セッション、またはメッセージの可能性があります。
- **queryIdentifiers** はグループ化され、 **querySetVersion**を使用してバージョン管理されます。
- **data** には、**queryTimeInTicks** を使用した対応するクエリ実行の出力が含まれます。
- T-SQL クエリの**queryIdentifiers** によって、クエリに T-SQL クエリ定義が格納されます。

| 論理的な Local Audit 情報階層 | 関連する列 |
| ------ | -------|
| Header | emitTime、schemaVersion 
| Machine | operatingSystem 
| Instance | instanceUniqueID, correlationID, clientVersion 
| Session | sessionID、traceName 
| [クエリ] | sequence、querySetVersion、queryIdentifier、query、queryTimeInTicks 
| data |  data 

### <a name="namevalue-pairs-definition-and-examples"></a>名前/値ペアの定義と例 

以下の列は、Local Audit ファイル出力の順を表しています。 以下の複数列の匿名化された値に対して、SHA 256 による一方向のハッシュが使用されています。  

| [オブジェクト名] | [説明] | 値の例
|-------|--------| ----------|
|instanceUniqueID| 匿名のインスタンス識別子。 | 888770C4D5A8C6729F76F33D472B28883AE518C92E1999888B171A085059FD 
|schemaVersion| SQLCEIP のスキーマ バージョン |  3 
|emitTime |データ ポイントの生成時間 (UTC) | 2016-09-08T17:20:22.1124269Z 
|sessionID | SQLCEIP サービスを提供するセッション識別子 | 89decf9a-ad11-485c-94a7-fefb3a02ed86 
|correlationId | 追加の識別子のプレース ホルダー | 0 
|sequence | セッション内で送信されたデータ ポイントのシーケンス番号 | 15 
|clientVersion | SQL Server インスタンスのバージョン | 13.0.2161.3 ((SQL16_RTM_QFE-CU).160907-1223) 
|operatingSystem | SQL Server インスタンスがインストールされている OS バージョン | Microsoft Windows Server 2012 R2 Datacenter 
|querySetVersion | クエリ定義グループのバージョン | 1.0.0.0 
|traceName | トレースのカテゴリ: (SQLServerXeQueries、SQLServerPeriodicQueries、SQLServerOneSettingsException) | SQLServerPeriodicQueries 
|queryIdentifier | クエリの識別子 | SQLServerProperties.002 
|data   | T-SQL クエリ、XE セッション、またはアプリケーションの出力として queryIdentifier で収集された情報の出力 |  [{"Collation": "SQL_Latin1_General_CP1_CI_AS","SqlFTinstalled": "0" "SqlIntSec": "1","IsSingleUser": "0","SqlFilestreamMode": "0","SqlPbInstalled": "0","SqlPbNodeRole": "","SqlVersionMajor": "13","SqlVersionMinor": "0","SqlVersionBuild": "2161","ProductBuildType": "","ProductLevel": "RTM","ProductUpdateLevel": "CU2","ProductUpdateReference": "KB3182270","ProductRevision": "3","SQLEditionId": "-1534726760","IsClustered": "0","IsHadrEnabled": "0","SqlAdvAInstalled": "0","PacketReceived": "1210","Version": "Microsoft SQL Server 2016 (RTM-CU2) (KB3182270) - 13.0.2161.3 (X64) \n\tSep  7 2016 14:24:16 \n\tCopyright (c) Microsoft Corporation\n\tStandard Edition (64-bit) on Windows Server 2012 R2 Datacenter 6.3 \u003cX64\u003e (Build 9600: ) (Hypervisor)\n"}],
|Query| 該当する場合、データを生成した queryIdentifier に関連する T-SQL クエリ定義。        このコンポーネントは、SQL Server CEIP サービスでアップロードされません。 ユーザー専用の参照コンポーネントとして Local Audit に含まれています。| SELECT\n      SERVERPROPERTY(\u0027Collation\u0027) AS [Collation],\n      SERVERPROPERTY(\u0027IsFullTextInstalled\u0027) AS [SqlFTinstalled],\n      SERVERPROPERTY(\u0027IsIntegratedSecurityOnly\u0027) AS [SqlIntSec],\n      SERVERPROPERTY(\u0027IsSingleUser\u0027) AS [IsSingleUser],\n      SERVERPROPERTY (\u0027FileStreamEffectiveLevel\u0027) AS [SqlFilestreamMode],\n      SERVERPROPERTY(\u0027IsPolybaseInstalled\u0027) AS [SqlPbInstalled],\n      SERVERPROPERTY(\u0027PolybaseRole\u0027) AS [SqlPbNodeRole],\n      SERVERPROPERTY(\u0027ProductMajorVersion\u0027) AS [SqlVersionMajor],\n      SERVERPROPERTY(\u0027ProductMinorVersion\u0027) AS [SqlVersionMinor],\n      SERVERPROPERTY(\u0027ProductBuild\u0027) AS [SqlVersionBuild],\n      SERVERPROPERTY(\u0027ProductBuildType\u0027) AS ProductBuildType,\n      SERVERPROPERTY(\u0027ProductLevel\u0027) AS ProductLevel,\n      SERVERPROPERTY(\u0027ProductUpdateLevel\u0027) AS ProductUpdateLevel,\n      SERVERPROPERTY(\u0027ProductUpdateReference\u0027) AS ProductUpdateReference,\n      RIGHT(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)),CHARINDEX(\u0027.\u0027, REVERSE(CAST(SERVERPROPERTY(\u0027ProductVersion\u0027) AS NVARCHAR(30)))) - 1) AS ProductRevision,\n      SERVERPROPERTY(\u0027EditionID\u0027) AS SQLEditionId,\n      SERVERPROPERTY(\u0027IsClustered\u0027) AS IsClustered,\n      SERVERPROPERTY(\u0027IsHadrEnabled\u0027) AS IsHadrEnabled,\n      SERVERPROPERTY(\u0027IsAdvancedAnalyticsInstalled\u0027) AS [SqlAdvAInstalled],\n      @@PACK_RECEIVED AS PacketReceived,\n      @@VERSION AS Version
|queryTimeInTicks | 次のトレース カテゴリのクエリを実行するためにかかる期間: (SQLServerXeQueries、SQLServerPeriodicQueries) |  0 
 
### <a name="trace-categories"></a>トレース カテゴリ 
現在、次のトレース カテゴリを収集します。 

- **SQLServerXeQueries**: 拡張イベント セッションで収集されたデータ ポイントが含まれます。
- **SQLServerPeriodicQueries**: SQL Server インスタンスで実行される定期的なクエリで収集されたデータ ポイントが含まれます。
- **SQLServerPerDBPeriodicQueries**: SQL Server インスタンスの最大 30 データベースに対して実行される定期的なクエリで収集されたデータ ポイントが含まれます。
- **SQLServerOneSettingsException**: スキーマやクエリ セットの更新に関連する例外メッセージが含まれます。
- **DigitalProductID**: SQL Server インスタンスの匿名化された (SHA-256) ハッシュ デジタル プロダクト ID を集約するデータ ポイントが含まれます。 

### <a name="local-audit-file-examples"></a>Local Audit ファイルの例



次に Local Audit の JSON ファイル出力の例を示します。

```JSON
[
  {
    "instanceUniqueId": "888770C4D5A8C6729F76F33D472B28883AE518C92E1999888B171A085059FD",
    "isSSEIInstance": "0",
    "schemaVersion": "5",
    "emitTime": "2018-05-04T15:27:59.7031518Z",
    "sessionId": "c3cd1b56-ab61-462f-8363-8881779aa223",
    "correlationId": 0,
    "sequence": 18,
    "clientVersion": "14.0.3025.34 ((SQLServer2017-CU6).180410-0033)",
    "isInternalMachine": "1",
    "operatingSystem": "Microsoft Windows 10 Enterprise",
    "querySetVersion": "14.0.3025.34",
    "traceName": "SQLServerPeriodicQueries",
    "queryIdentifier": "SQLServerProperties.002",
    "data": [
      {
        "Collation": "SQL_Latin1_General_CP1_CI_AS",
        "SqlFTinstalled": "0",
        "SqlIntSec": "1",
        "IsSingleUser": "0",
        "SqlFilestreamMode": "2",
        "SqlPbInstalled": "1",
        "SqlPbNodeRole": "Head",
        "SqlVersionMajor": "14",
        "SqlVersionMinor": "0",
        "SqlVersionBuild": "3025",
        "ProductBuildType": "",
        "ProductLevel": "RTM",
        "ProductUpdateLevel": "CU6",
        "ProductUpdateReference": "KB4101464",
        "ProductRevision": "34",
        "SQLEditionId": "1872460670",
        "IsClustered": "0",
        "IsHadrEnabled": "0",
        "SqlAdvAInstalled": "1",
        "PacketReceived": "422",
        "Version": "Microsoft SQL Server 2017 (RTM-CU6) (KB4101464) - 14.0.3025.34 (X64) \n\tApr  9 2018 18:00:41 \n\tCopyright (C) 2017 Microsoft Corporation\n\tEnterprise Edition: Core-based Licensing (64-bit) on Windows 10 Enterprise 10.0 <X64> (Build 16299: )\n"
      }
    ],
    "query": "SELECT\n      SERVERPROPERTY('Collation') AS [Collation],\n      SERVERPROPERTY('IsFullTextInstalled') AS [SqlFTinstalled],\n      SERVERPROPERTY('IsIntegratedSecurityOnly') AS [SqlIntSec],\n      SERVERPROPERTY('IsSingleUser') AS [IsSingleUser],\n      SERVERPROPERTY ('FileStreamEffectiveLevel') AS [SqlFilestreamMode],\n      SERVERPROPERTY('IsPolybaseInstalled') AS [SqlPbInstalled],\n      SERVERPROPERTY('PolybaseRole') AS [SqlPbNodeRole],\n      SERVERPROPERTY('ProductMajorVersion') AS [SqlVersionMajor],\n      SERVERPROPERTY('ProductMinorVersion') AS [SqlVersionMinor],\n      SERVERPROPERTY('ProductBuild') AS [SqlVersionBuild],\n      SERVERPROPERTY('ProductBuildType') AS ProductBuildType,\n      SERVERPROPERTY('ProductLevel') AS ProductLevel,\n      SERVERPROPERTY('ProductUpdateLevel') AS ProductUpdateLevel,\n      SERVERPROPERTY('ProductUpdateReference') AS ProductUpdateReference,\n      RIGHT(CAST(SERVERPROPERTY('ProductVersion') AS NVARCHAR(30)),CHARINDEX('.', REVERSE(CAST(SERVERPROPERTY('ProductVersion') AS NVARCHAR(30)))) - 1) AS ProductRevision,\n      SERVERPROPERTY('EditionID') AS SQLEditionId,\n      SERVERPROPERTY('IsClustered') AS IsClustered,\n      SERVERPROPERTY('IsHadrEnabled') AS IsHadrEnabled,\n      SERVERPROPERTY('IsAdvancedAnalyticsInstalled') AS [SqlAdvAInstalled],\n      @@PACK_RECEIVED AS PacketReceived,\n      @@VERSION AS Version",
    "queryTimeInTicks": 0
  },
  {
    "instanceUniqueId": "8884F770C4D5A8C6729F76F33D472B28883AE518C92E1999888B171A085059FD",
    "isSSEIInstance": "0",
    "schemaVersion": "5",
    "emitTime": "2018-05-04T15:28:00.9025999Z",
    "sessionId": "c3cd1b56-ab61-462f-8363-8881779aa223",
    "correlationId": 0,
    "sequence": 23,
    "clientVersion": "14.0.3025.34 ((SQLServer2017-CU6).180410-0033)",
    "isInternalMachine": "1",
    "operatingSystem": "Microsoft Windows 10 Enterprise",
    "querySetVersion": "14.0.3025.34",
    "traceName": "SQLServerPeriodicQueries",
    "queryIdentifier": "OsSysInfo.003",
    "data": [
      {
        "LogicalCPUCount": "8",
        "HyperthreadRatio": "8",
        "PhysicalMemoryMB": "32710.902343",
        "SQLServerStartTime": "05/04/2018 08:22:30",
        "AffinityTypeDesc": "AUTO",
        "VirtualMachineType": "0",
        "SocketCount": "1",
        "CoresPerSocket": "4",
        "NumaNodeCount": "1",
        "ContainerType": "0",
        "ContainerDescription": "NONE"
      }
    ],
    "query": "SELECT\n      cpu_count AS LogicalCPUCount,\n      hyperthread_ratio AS HyperthreadRatio,\n      physical_memory_kb/1024.0 AS PhysicalMemoryMB,\n      sqlserver_start_time AS SQLServerStartTime,\n      affinity_type_desc AS AffinityTypeDesc,\n      virtual_machine_type AS VirtualMachineType,\n      socket_count as SocketCount,\n      cores_per_socket as CoresPerSocket,\n      numa_node_count as NumaNodeCount,\n      container_type as ContainerType,\n      container_type_desc as ContainerDescription\n      FROM sys.dm_os_sys_info WITH(nolock)",
    "queryTimeInTicks": 0
  }
]
```
## <a name="frequently-asked-questions"></a>よく寄せられる質問

**DBA で Local Audit ログ ファイルを読み取るにはどうすればよいですか?**
Local Audit ログ ファイルは JSON 形式で出力されます。 各行は、Microsoft にアップロードされた 1 件のテレメトリを表す JSON オブジェクトになります。 フィールドには、わかりやすい名前を付けることをお勧めします。

**DBA で Usage Feedback Collection を無効にするとどうなりますか?**
Local Audit ファイルが出力されなくなります。

**インターネット接続がない場合やコンピューターがファイアウォールの背後にある場合はどうなりますか?**
SQL Server 2016 の使用状況のフィードバックは Microsoft に送信されなくなります。 構成が正しければ、Local Audit ログの出力は試行されます。

**DBA で Local Audit を無効にするにはどうすればよいですか?**
UserRequestedLocalAuditDirectory レジストリ キー エントリを削除します。

**Local Audit ログ ファイルを読み取ることができるのは誰ですか?**
組織内で、Local Audit ディレクトリにアクセス権を持つ全員です。

**指定したディレクトリに出力されたログ ファイルを DBA で管理するにはどうすればよいですか?**
ディスク領域を消費しすぎないように、ディレクトリ内にあるファイルのクリーンアップを DBA で自動管理する必要があります。

**この JSON 出力を読み取るために使用できるクライアントまたはツールはありますか?**
出力は、メモ帳、Visual Studio、JSON リーダーなど任意のツールで読み取ることができます。
また、JSON ファイルを読み取り、以下の図のように SQL Server 2016 インスタンスのデータを分析することもできます。 SQL Server で JSON ファイルを読み取る方法の詳細については、「 [Importing JSON files into SQL Server using OPENROWSET (BULK) and OPENJSON (Transact-SQL)](http://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/10/07/bulk-importing-json-files-into-sql-server/)」(OPENROWSET (BULK) と OPENJSON (Transact-SQL) を使用して JSON ファイルを SQL Server にインポートする) を参照してください。

```Transact-SQL
DECLARE @JSONFile AS VARCHAR(MAX)

-- Read the JSON file into variable 
SELECT @JSONFile = BulkColumn 
FROM OPENROWSET (BULK 'C:\SQLCEIPAudit\MSSQLSERVER\2016-09-08.json', SINGLE_CLOB) MyFile 

-- Check if the JSON file has been read properly and if it's in a JSON format
SELECT 
    @JSONFile LocalAuditOutput, 
    ISJSON(@JSONFile) IsFileInJSONFormat

-- Get the query identifier, query and the data (output of the query)   
SELECT 
    sequence,
    queryIdentifier,
    query,
    data
FROM OPENJSON(@JSONFile) 
    WITH (sessionId VARCHAR(64)
         ,sequence INT
         ,queryIdentifier VARCHAR(128)
         ,query VARCHAR(MAX)
         ,data NVARCHAR(MAX) AS JSON)
-- Get specific details about the output of "DatabaseProperties.001" query  
SELECT 
    QueryIdentifier,
    DatabaseID,
    CompatibilityLevel,
    IsQueryStoreOn
FROM OPENJSON(@JSONFile) 
    WITH (sessionId VARCHAR(64)
         ,sequence INT
         ,queryIdentifier VARCHAR(128)
         ,query VARCHAR(MAX)
         ,data NVARCHAR(MAX) AS JSON) 
    CROSS APPLY OPENJSON(data) 
        WITH (   DatabaseID varchar(128) '$.database_id'
                ,CompatibilityLevel varchar(128) '$.compatibility_level'
                ,IsQueryStoreOn varchar(128) '$.QS'
             )
WHERE queryIdentifier = 'DatabaseProperties.001'
```

## <a name="see-also"></a>参照
[SSMS Usage Feedback Collection の Local Audit](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-telemetry-ssms)
