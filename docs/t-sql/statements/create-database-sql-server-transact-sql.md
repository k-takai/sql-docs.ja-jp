---
title: CREATE DATABASE (SQL Server Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATABASE_TSQL
- DATABASE
- CONTAINMENT_TSQL
- CREATE DATABASE
- CREATE_DATABASE_TSQL
- CONTAINS_FILESTREAM_TSQL
- CONTAINS FILESTREAM
- CONTAINMENT
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server database snapshots], creating
- databases [SQL Server], creating
- model database [SQL Server], database creation
- mounted drives [SQL Server]
- CREATE DATABASE
- CREATE DATABASE statement
- file creation [SQL Server]
- creating databases
- containment
- filegroups [SQL Server], database creation
- database creation [SQL Server], CREATE DATABASE statement
- moving databases
- attaching databases [SQL Server], CREATE DATABASE...FOR ATTACH
ms.assetid: 29ddac46-7a0f-4151-bd94-75c1908c89f8
caps.latest.revision: 212
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 356a00b1c83220e0be211ee0357d2736533a3906
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="create-database-sql-server-transact-sql"></a>CREATE DATABASE (SQL Server Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  新しいデータベースとデータベースを格納するファイルを作成するか、データベース スナップショットを作成するか、以前作成されたデータベースのデタッチされたファイルからデータベースをアタッチします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  

データベースの作成    

```  
CREATE DATABASE database_name   
[ CONTAINMENT = { NONE | PARTIAL } ]  
[ ON   
      [ PRIMARY ] <filespec> [ ,...n ]   
      [ , <filegroup> [ ,...n ] ]   
      [ LOG ON <filespec> [ ,...n ] ]   
]   
[ COLLATE collation_name ]  
[ WITH  <option> [,...n ] ]  
[;]  
  
<option> ::=  
{  
      FILESTREAM ( <filestream_option> [,...n ] )  
    | DEFAULT_FULLTEXT_LANGUAGE = { lcid | language_name | language_alias }  
    | DEFAULT_LANGUAGE = { lcid | language_name | language_alias }  
    | NESTED_TRIGGERS = { OFF | ON }  
    | TRANSFORM_NOISE_WORDS = { OFF | ON}  
    | TWO_DIGIT_YEAR_CUTOFF = <two_digit_year_cutoff>   
    | DB_CHAINING { OFF | ON }  
    | TRUSTWORTHY { OFF | ON }  
}  
  
<filestream_option> ::=  
{  
      NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }  
    | DIRECTORY_NAME = 'directory_name'   
}  
  
<filespec> ::=   
{  
(  
    NAME = logical_file_name ,  
    FILENAME = { 'os_file_name' | 'filestream_path' }   
    [ , SIZE = size [ KB | MB | GB | TB ] ]   
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]   
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB | % ] ]  
)  
}  
  
<filegroup> ::=   
{  
FILEGROUP filegroup name [ [ CONTAINS FILESTREAM ] [ DEFAULT ] | CONTAINS MEMORY_OPTIMIZED_DATA ]  
    <filespec> [ ,...n ]  
}  
  
<service_broker_option> ::=  
{  
    ENABLE_BROKER  
  | NEW_BROKER  
  | ERROR_BROKER_CONVERSATIONS  
}  
  
```  
 
データベースのアタッチ    

```  
CREATE DATABASE database_name   
    ON <filespec> [ ,...n ]   
    FOR { { ATTACH [ WITH <attach_database_option> [ , ...n ] ] }  
        | ATTACH_REBUILD_LOG }  
[;]  
  
<attach_database_option> ::=  
{  
      <service_broker_option>  
    | RESTRICTED_USER  
    | FILESTREAM ( DIRECTORY_NAME = { 'directory_name' | NULL } )  
}   
```  
  
データベース スナップショットの作成    

```  
CREATE DATABASE database_snapshot_name   
    ON   
    (  
        NAME = logical_file_name,  
        FILENAME = 'os_file_name'   
    ) [ ,...n ]   
    AS SNAPSHOT OF source_database_name  
[;]  
```  
  
## <a name="arguments"></a>引数  
 *database_name*  
 新規データベースの名前です。 データベース名は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で一意であり、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。  
  
 ログ ファイルに論理名が指定されていない場合を除き、*database_name* には、最大 128 文字まで指定できます。 ログ ファイルの論理名が指定されていない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、*database_name* にサフィックスを付加することにより、ログの *logical_file_name* および *os_file_name* を生成します。 生成された論理ファイル名が 128 文字を超えないようにするため、*database_name* は 123 文字に制限されます。  
  
 データ ファイル名が指定されていない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、*logical_file_name* および *os_file_name* の両方に *database_name* を使用します。 既定のパスはレジストリから取得されます。 既定のパスを変更するには、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] の **[サーバーのプロパティ] ([データベースの設定] ページ)** を使用します。 既定のパスを変更するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動する必要があります。  
  
 CONTAINMENT = { NONE | PARTIAL }  

**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 データベースの包含状態を指定します。 NONE = 非包含データベース PARTIAL = 部分的包含データベース  
  
 ON  
 データベースのデータ部分の格納に使用するディスク ファイル (データ ファイル) を明示的に定義するように指定します。 プライマリ ファイル グループのデータ ファイルを定義する \<filespec> 項目のコンマ区切りリストが続く場合は、ON にします。 プライマリ ファイル グループ内のファイルのリストに続き、ユーザー ファイル グループおよびユーザー ファイル グループに属するファイルを定義する省略可能な \<filegroup> 項目のコンマ区切りリストを記述できます。  
  
 PRIMARY  
 関連付けられた \<filespec> リストによってプライマリ ファイルを定義するように指定します。 プライマリ ファイル グループ内の \<filespec> エントリに最初に指定されたファイルが、プライマリ ファイルとなります。 データベースはプライマリ ファイルを 1 つだけ保有することができます。 詳細については、「 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)」を参照してください。  
  
 PRIMARY を指定しないと、CREATE DATABASE ステートメントに記述された最初のファイルがプライマリ ファイルになります。  
  
 LOG ON  
 データベース ログの格納に使用するディスク ファイル (ログ ファイル) を明示的に定義するように指定します。 LOG ON に続けて、ログ ファイルを定義する \<filespec> 項目のコンマ区切りリストを記述します。 LOG ON が指定されていない場合、データベースのすべてのデータ ファイルのサイズの合計の 25%、または、512 KB のいずれか大きい方のサイズのログ ファイルが 1 つ自動的に作成されます。 このファイルは既定のログ ファイルの場所に保存されます。 この場所については、「[データ ファイルとログ ファイルの既定の場所の表示または変更 &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)」を参照してください。  
  
 LOG ON はデータベース スナップショットでは指定できません。  
  
 COLLATE *collation_name*  
 データベースの既定の照合順序を指定します。 照合順序名には、Windows 照合順序名または SQL 照合順序名を指定できます。 指定しない場合は、データベースに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの既定の照合順序が割り当てられます。 照合順序名は、データベース スナップショットでは指定できません。  
  
 照合順序名は、FOR ATTACH 句または FOR ATTACH_REBUILD_LOG 句と共に指定することはできません。 アタッチされたデータベースの照合順序を変更する方法の詳細については、この [Microsoft Web サイト](http://go.microsoft.com/fwlink/?linkid=16419&kbid=325335)を参照してください。  
  
 Windows と SQL の照合順序名については、「[COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)」を参照してください。  
  
> [!NOTE]  
>  包含データベースは、非包含データベースとは異なる方法で照合されます。 詳細については、「[包含データベースの照合順序](../../relational-databases/databases/contained-database-collations.md)」を参照してください。  
  
 WITH \<option>  
 -   **\<filestream_options>** 
  
     NON_TRANSACTED_ACCESS = { **OFF** | READ_ONLY | FULL }  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     データベースに対する非トランザクション FILESTREAM アクセスのレベルを指定します。  
  
    |ReplTest1|Description|  
    |-----------|-----------------|  
    |OFF|非トランザクション アクセスは無効です。|  
    |READONLY|このデータベース内の FILESTREAM データは、非トランザクション プロセスによって読み取ることができます。|  
    |FULL|FILESTREAM FileTable に対する完全な非トランザクション アクセスは有効です。|  
  
     DIRECTORY_NAME = \<directory_name> **Applies to**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] through [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     Windows と互換性のあるディレクトリ名です。 この名前は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内のすべての Database_Directory 名の中で一意である必要があります。 一意性の比較では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 照合順序の設定とは関係なく、大文字と小文字は区別されません。 このオプションは、このデータベース内に FileTable を作成する前に設定する必要があります。  
  
 次のオプションは、CONTAINMENT が PARTIAL に設定されている場合にのみ使用できます。 CONTAINMENT が NONE に設定されている場合、エラーが発生します。  
  
-   **DEFAULT_FULLTEXT_LANGUAGE = \<lcid> | \<language name> | \<language alias>**  
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the default full-text language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) for a full description of this option.  
  
-   **DEFAULT_LANGUAGE = \<lcid> | \<language name> | \<language alias>**  
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the default language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) for a full description of this option.  
  
-   **NESTED_TRIGGERS = { OFF | ON}**  
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the nested triggers Server Configuration Option](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) for a full description of this option.  
  
-   **TRANSFORM_NOISE_WORDS = { OFF | ON}**  
  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)for a full description of this option.  
  
-   **TWO_DIGIT_YEAR_CUTOFF = { 2049 | \<any year between 1753 and 9999> }**  
  
     年を表す 4 桁の数字。 既定値は 2049 です。 このオプションの詳細については、「[two digit year cutoff サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)」を参照してください。  
  
-   **DB_CHAINING { OFF | ON }**  
  
     ON が指定されている場合、データベースを、複数データベースの組み合わせ所有権のソース データベースまたは対象データベースとして使用できます。  
  
     OFF の場合、データベースは、複数データベースの組み合わせ所有権に参加することはできません。 既定値は OFF です。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスでは、cross db ownership chaining サーバー オプションが 0 (OFF) の場合に、この設定が認識されます。 cross db ownership chaining が 1 (ON) の場合は、このオプションの値にかかわらず、すべてのユーザー データベースが複数データベースの組み合わせ所有権に参加できます。 このオプションは、[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を使用して設定します。  
  
     このオプションを設定するには、sysadmin 固定サーバー ロールのメンバーシップが必要です。 master、model、tempdb のシステム データベースでは、DB_CHAINING オプションを設定することはできません。  
  
-   **TRUSTWORTHY { OFF | ON }**  
  
     ON が指定されている場合、権限借用のコンテキストを使用するデータベース モジュール (ビュー、ユーザー定義関数、ストアド プロシージャなど) は、データベース外のリソースにアクセスできます。  
  
     OFF の場合、権限借用のコンテキスト内のデータベース モジュールは、データベース外のリソースにアクセスできません。 既定値は OFF です。  
  
     データベースがアタッチされている場合は常に、TRUSTWORTHY は OFF に設定されます。  
  
     既定では、msdb データベースを除くすべてのシステム データベースで TRUSTWORTHY は OFF に設定されています。 model および tempdb データベースでは、この値は変更できません。 master データベースでは、TRUSTWORTHY オプションを ON に設定しないことを強くお勧めします。  
  
     このオプションを設定するには、sysadmin 固定サーバー ロールのメンバーシップが必要です。  
  
 FOR ATTACH [ WITH \< attach_database_option > ] 既存のオペレーティング システム ファイルのセットを[アタッチ](../../relational-databases/databases/database-detach-and-attach-sql-server.md)することによりデータベースを作成するように指定します。 プライマリ ファイルを指定する \<filespec> エントリが必要です。 他に必要な \<filespec> エントリは、データベースが最初に作成されたとき、または最後にアタッチされたときからパスが変わったファイルのエントリだけです。 これらのファイルの \<filespec> エントリを指定する必要があります。  
  
 FOR ATTACH では、以下のことが必要です。  
  
-   すべてのデータ ファイル (MDF および NDF) が有効であること  
  
-   ログ ファイルが複数存在する場合は、これらがすべて使用可能であること  
  
 読み取り/書き込みデータベースに現在利用できないログ ファイルが 1 つある場合、アタッチ操作の前に、ユーザーも、開かれたトランザクションもない状態でデータベースをシャットダウンすると、FOR ATTACH は自動的にログ ファイルを再構築し、プライマリ ファイルを更新します。 これに対し、読み取り専用データベースの場合、プライマリ ファイルを更新できないため、ログは再構築されません。 したがって、ログが利用できない読み取り専用データベースをアタッチする場合、ログ ファイルまたはファイルを FOR ATTACH 句に指定する必要があります。  
  
> [!NOTE]  
>  新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で作成したデータベースは、それ以前のバージョンでアタッチすることはできません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、アタッチされるデータベースに含まれているフルテキスト ファイルも、すべてデータベースと共にアタッチされます。 フルテキスト カタログの新しいパスを指定するには、フルテキストのオペレーティング システム ファイル名を含めずに新しい場所を指定します。 詳細については、「例」のセクションを参照してください。  
  
 "ディレクトリ名" の FILESTREAM オプションを含むデータベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにアタッチすると、Database_Directory 名が一意であることを確認する要求が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に対して行われます。 Database_Directory 名が一意でない場合は、アタッチ操作は失敗し、"FILESTREAM Database_Directory 名 \<名前> は、この SQL Server インスタンスで一意ではありません" というエラーが出力されます。 このエラーを回避するには、省略可能なパラメーターの *directory_name* をこの操作に渡す必要があります。  
  
 FOR ATTACH はデータベース スナップショットでは指定できません。  
  
 FOR ATTACH は RESTRICTED_USER オプションを指定できます。 RESTRICTED_USER モードでは、db_owner 固定データベース ロールと、dbcreator 固定サーバー ロールおよび sysadmin 固定サーバー ロールのメンバーのみが、データベースに接続できます。ただし、接続ユーザー数に制限はありません。 修飾されていないユーザーによる試行が拒否されます。  
  
 データベースで [!INCLUDE[ssSB](../../includes/sssb-md.md)] を使用する場合は、FOR ATTACH 句で WITH \<service_broker_option> を使用します。 
  
 \<service_broker_option> [!INCLUDE[ssSB](../../includes/sssb-md.md)] のメッセージの配信と、データベースの [!INCLUDE[ssSB](../../includes/sssb-md.md)] 識別子を制御します。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] オプションは、FOR ATTACH 句が使用されている場合にのみ指定できます。  
  
 ENABLE_BROKER  
 指定したデータベースに対して [!INCLUDE[ssSB](../../includes/sssb-md.md)] を有効にします。 つまり、メッセージ配信が開始され、sys.databases カタログ ビューで is_broker_enabled が TRUE に設定されます。 データベースは、既存の [!INCLUDE[ssSB](../../includes/sssb-md.md)] 識別子を保持します。  
  
 NEW_BROKER  
 sys.databases と復元されたデータベースの両方に新しい service_broker_guid 値を作成し、すべてのメッセージ交換エンドポイントをクリーンアップして終了します。 ブローカーは有効ですが、リモートのメッセージ交換エンドポイントにメッセージは送信されません。 古い [!INCLUDE[ssSB](../../includes/sssb-md.md)] 識別子を参照するルートは、新しい識別子を使用して作成し直す必要があります。  
  
 ERROR_BROKER_CONVERSATIONS  
 データベースがアタッチまたは復元されていることを示すエラーと共に、すべてのメッセージ交換を終了します。 ブローカーはこの操作が完了するまで無効になり、その後、有効になります。 データベースは、既存の [!INCLUDE[ssSB](../../includes/sssb-md.md)] 識別子を保持します。  
  
 レプリケートされたデータベースをアタッチするとき、そのデータベースがデタッチではなくコピーされたものである場合は、次の点を考慮してください。  
  
-   元のデータベースと同じサーバー インスタンスおよびバージョンにデータベースをアタッチする場合は、必要な追加手順はありません。  
  
-   同じサーバー インスタンスのアップグレードされたバージョンにデータベースをアタッチする場合は、アタッチ操作が完了した後、[sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md) を実行してレプリケーションをアップグレードする必要があります。  
  
-   バージョンに関係なく、別のサーバー インスタンスにデータベースをアタッチする場合は、アタッチ操作が完了した後、[sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) を実行してレプリケーションを削除する必要があります。  
  
> [!NOTE]  
> アタッチは **vardecimal** ストレージ形式で動作しますが、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] を [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2 以降にアップグレードする必要があります。 vardecimal ストレージ形式を使用するデータベースを以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアタッチすることはできません。 **vardecimal** ストレージ形式の詳細については、「[データ圧縮](../../relational-databases/data-compression/data-compression.md)」を参照してください。  
  
 データベースが最初に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の新しいインスタンスにアタッチまたは復元されるとき、データベース マスター キー (サービス マスター キーにより暗号化されたもの) のコピーはまだサーバーに格納されていません。 **OPEN MASTER KEY** を使用して、データベース マスター キー (DMK) を暗号化解除する必要があります。 DMK の暗号化が解除されると、 **ALTER MASTER KEY REGENERATE** ステートメントを使用して、サービス マスター キー (SMK) で暗号化された DMK のコピーをサーバーに提供することにより、将来、自動的に暗号化解除することも可能となります。 データベースを以前のバージョンからアップグレードした場合、新しい AES アルゴリズムを使用するように DMK を再作成する必要があります。 DMK を再作成する方法については、「[ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)」を参照してください。 DMK キーを再作成して AES にアップグレードするのに必要な時間は、DMK によって保護されているオブジェクトの数によって異なります。 DMK キーを再作成して AES にアップグレードする作業は、1 回限りで済み、今後のキー ローテーション方法には影響を与えません。 アタッチを使用してデータベースをアップグレードする方法については、「[デタッチとアタッチを使用したデータベースのアップグレード &#40;Transact-SQL&#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md)」を参照してください。  
  
> [!IMPORTANT]  
> 不明なソースや信頼されていないソースからのデータベースはアタッチしないことをお勧めします。 こうしたデータベースには、意図しない [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを実行したり、スキーマまたは物理データベース構造を変更してエラーを発生させるような、悪意のあるコードが含まれている可能性があります。 不明または信頼できないソースのデータベースを使用する前に、運用サーバー以外のサーバーでそのデータベースに対し [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) を実行し、さらに、そのデータベースのストアド プロシージャやその他のユーザー定義コードなどのコードを調べます。  
  
> [!NOTE]  
> データベースをアタッチするときに、**TRUSTWORTHY** オプションおよび **DB_CHAINING** オプションによる効果は発生しません。  
  
 FOR ATTACH_REBUILD_LOG  
 既存のオペレーティング システム ファイルのセットをアタッチすることによりデータベースを作成するように指定します。 このオプションは読み取り/書き込みデータベースに限定されます。 プライマリ ファイルを指定する *\<filespec>* エントリが必要です。 1 つ以上のトランザクション ログ ファイルが見つからない場合、ログ ファイルは再構築されます。 ATTACH_REBUILD_LOG を指定すると、1 MB のログ ファイルが自動的に新規作成されます。 このファイルは既定のログ ファイルの場所に保存されます。 この場所については、「[データ ファイルとログ ファイルの既定の場所の表示または変更 &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)」を参照してください。  
  
> [!NOTE]  
>  ログ ファイルが利用可能な場合は、[!INCLUDE[ssDE](../../includes/ssde-md.md)]はログ ファイルを再構築せず、それらのファイルを使用します。  
  
 FOR ATTACH_REBUILD_LOG では、以下のことが必要です。  
  
-   データベースのクリーン シャットダウン  
  
-   すべてのデータ ファイル (MDF および NDF) が有効であること  
  
> [!IMPORTANT]  
> この操作により、連続したログ バックアップが中断されます。 操作が完了したら、データベース全体のバックアップを行うことをお勧めします。 詳細については、「 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)」を参照してください。  
  
 通常、FOR ATTACH_REBUILD_LOG は、大きなログを持つ読み取り/書き込みデータベースを別のサーバーにコピーする場合に使用します。このようなサーバーでは、コピーしたデータベースが、多くの場合読み取り操作に使用されます (または読み取り操作でのみ使用されます)。このため、元のデータベースほどログ領域を必要としません。  
  
 FOR ATTACH_REBUILD_LOG はデータベース スナップショットでは指定できません。  
  
 データベースのインポートおよびデタッチの詳細については、「[データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)」を参照してください。  
  
 \<filespec>  
 ファイル プロパティを制御します。  
  
 NAME *logical_file_name*  
 ファイルの論理名を指定します。 NAME は、FOR ATTACH 句の 1 つを指定する場合以外に、FILENAME が指定されるときに必要です。 FILESTREAM ファイル グループの名前を PRIMARY にすることはできません。  
  
 *logical_file_name*  
 ファイルを参照するときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用される論理名を指定します。 *Logical_file_name* は、データベース内で一意であり、[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。 この名前は、文字定数、UNICODE 定数、標準の識別子、区切られた識別子のいずれでもかまいません。  
  
 FILENAME { **'***os_file_name***'** | **'***filestream_path***'** }  
 オペレーティング システムの (物理) ファイル名を指定します。  
  
 **'** *os_file_name* **'**  
 ファイルを作成する際にオペレーティング システムが使用するパスとファイル名です。 ファイルは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているローカル サーバー、ストレージ エリア ネットワーク (SAN)、または、iSCSI ベースのネットワークのうちのいずれかのデバイスに存在する必要があります。 指定したパスは、CREATE DATABASE ステートメントを実行する前に存在する必要があります。 詳細については、「解説」の「データベース ファイルとファイル グループ」を参照してください。  
  
 ファイルに対して UNC パスが指定されている場合は、SIZE、MAXSIZE、および FILEGROWTH パラメーターを設定できます。  
  
 ファイルが未処理のパーティション上にある場合、*os_file_name* には、未処理になっている既存のパーティションのドライブ文字のみを指定する必要があります。 1 つの未処理のパーティションに作成できるのは 1 つのデータ ファイルだけです。  
  
 ファイルが読み取り専用のセカンダリ ファイルであるか、データベースが読み取り専用である場合を除き、データ ファイルを圧縮ファイル システム上に置かないでください。 ログ ファイルは、圧縮ファイル システム上に置くことはできません。  
  
 **'** *filestream_path* **'**  
 FILESTREAM ファイル グループの場合、FILENAME は FILESTREAM データが格納されるパスを参照します。 最後のフォルダーまでのパスが存在する必要がありますが、最後のフォルダーは存在できません。 たとえば、パス C:\MyFiles\MyFilestreamData を指定する場合は、ALTER DATABASE を実行するとき、C:\MyFiles は既に存在している必要がありますが、MyFilestreamData フォルダーは存在してはなりません。  
  
 ファイル グループとファイル (`<filespec>`) は、同じステートメントで作成する必要があります。  
  
 SIZE プロパティおよび FILEGROWTH プロパティは、FILESTREAM ファイル グループには適用されません。  
  
 SIZE *size*  
 ファイルのサイズを指定します。  
  
 *os_file_name* が UNC パスとして指定されている場合、SIZE を指定することはできません。 SIZE は、FILESTREAM ファイル グループには適用されません。  
  
 *size*  
 ファイルの初期サイズです。  
  
 プライマリ ファイルに *size* が指定されていない場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)] では、model データベースのプライマリ ファイルのサイズを使用します。 モデルの既定のサイズは 8 MB ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降) または 1 MB (それより前のバージョン) です。 セカンダリ データ ファイルまたはログ ファイルが指定されているにもかかわらず、そのファイルに対して *size* サイズが指定されていない場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)] では、そのファイルのサイズが 8 MB ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降) または 1 MB (それより前のバージョン) になります。 なお、プライマリ ファイルに対して指定するサイズは、model データベースのプライマリ ファイルのサイズ以上である必要があります。  
  
 サフィックスとして、KB、MB、GB、または TB を使用できます。 既定値は MB です。 整数を指定します。小数を含めないでください。 *size* は整数値です。 2,147,483,647 を超える値に対しては、より大きな単位を使用してください。  
  
 MAXSIZE *max_size*  
 ファイルのサイズの上限を指定します。 *os_file_name* が UNC パスとして指定されている場合、MAXSIZE を指定することはできません。  
  
 *max_size*  
 ファイルの最大サイズです。 サフィックスとして、KB、MB、GB、および TB を使用できます。 既定値は MB です。 整数を指定します。小数を含めないでください。 *max_size* を指定しないと、ファイルはディスク領域がなくなるまで拡張されます。 *max_size* は整数値です。 2,147,483,647 を超える値に対しては、より大きな単位を使用してください。  
  
 UNLIMITED  
 ディスクがいっぱいになるまでファイルを拡張するように指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、無制限に拡張するファイル固有のログの最大サイズは 2 TB で、データ ファイルの最大サイズは 16 TB です。  
  
> [!NOTE]  
> FILESTREAM コンテナーに対してこのオプションを指定した場合、最大サイズはありません。 ディスクがいっぱいになるまでファイル サイズが拡張します。  
  
 FILEGROWTH *growth_increment*  
 ファイルを自動拡張するときの増加量を指定します。 ファイルの FILEGROWTH の設定を MAXSIZE の設定より大きくすることはできません。 *os_file_name* が UNC パスとして指定されている場合、FILEGROWTH を指定することはできません。 FILEGROWTH は、FILESTREAM ファイル グループには適用されません。  
  
 *growth_increment*  
 新しい領域が必要とされるたびにファイルに追加される領域の容量です。  
  
 値は MB、KB、GB、TB または % の単位で指定できます。 サフィックス MB、KB、または % を付けないで数値を指定した場合の既定値は MB です。 % を指定すると、1 回の増加量は、増加時のファイル サイズに指定されたパーセンテージを掛けた値になります。 指定されたサイズは、最も近い 64 KB 単位の値に丸められ、最小値は 64 KB になります。  
  
 0 は、自動拡張がオフで、領域を追加できないことを示します。  
  
 FILEGROWTH が指定されていない場合、既定値は次のとおりです。  
  
|[バージョンのオプション]|[既定値]|  
|-------------|--------------------|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降|データ 64 MB。 ログ ファイル 64 MB。|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降|データ 1 MB。 ログ ファイル 10%。|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] の前|データ 10%。 ログ ファイル 10%。|  
  
 \<filegroup>  
 ファイル グループ プロパティを制御します。 ファイル グループは、データベース スナップショットでは指定できません。  
  
 FILEGROUP *filegroup_name*  
 ファイル グループの論理名です。  
  
 *filegroup_name*  
 *filegroup_name* はデータベース内で一意である必要があり、システムで提示された名前である PRIMARY や PRIMARY_LOG にすることはできません。 この名前は、文字定数、UNICODE 定数、標準の識別子、区切られた識別子のいずれでもかまいません。 名前は、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。  
  
 CONTAINS FILESTREAM  
 ファイル グループで FILESTREAM バイナリ ラージ オブジェクト (BLOB) をファイル システムに格納することを指定します。  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] から [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 ファイル グループでメモリ最適化データをファイル システムに格納することを指定します。 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。 MEMORY_OPTIMIZED_DATA ファイル グループは、1 つのデータベースにつき 1 つしか許可されません。 メモリ最適化データを格納するファイルグループを作成するコード サンプルについては、「[メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャの作成](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)」を参照してください。  
  
 DEFAULT  
 指定されたファイル グループが、データベースの既定のファイル グループであることを指定します。  
  
 *database_snapshot_name*  
 新規データベース スナップショットの名前です。 データベース スナップショット名は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で一意であり、識別子のルールに従っている必要があります。 *database_snapshot_name* は 128 文字以下です。  
  
 ON **(** NAME **=***logical_file_name***,** FILENAME **='***os_file_name***')** [ **,**... *n* ]  
 データベース スナップショットを作成するには、ソース データベースのファイルのリストを指定します。 スナップショットが機能するためには、すべてのデータ ファイルは個別に指定する必要があります。 ただし、データベース スナップショットにログ ファイルは指定できません。 FILESTREAM ファイル グループは、データベース スナップショットではサポートされていません。 CREATE DATABASE ON 句に FILESTREAM データ ファイルが含まれていると、ステートメントが失敗してエラーが発生します。  
  
 NAME、FILENAME、およびそれらの値については、相当する \<filespec> 値の説明を参照してください。  
  
> [!NOTE]  
> データベース スナップショットを作成する場合、他の \<filespec> オプションおよびキーワード PRIMARY は許可されません。  
  
 AS SNAPSHOT OF *source_database_name*  
 作成されるデータベースが、*source_database_name* によって指定されたソース データベースのデータベース スナップショットであることを指定します。 スナップショットとソース データベースは同じインスタンス上に存在する必要があります。  
  
 詳細については、「解説」の「データベース スナップショット」を参照してください。  
  
## <a name="remarks"></a>Remarks  
 [master データベース](../../relational-databases/databases/master-database.md)は、ユーザー データベースが作成、変更、または削除されるたびにバックアップする必要があります。  
  
 CREATE DATABASE ステートメントは自動コミット モード (既定のトランザクション管理モード) で実行する必要があり、明示的または暗黙的なトランザクション モードでは許可されません。  
  
 1 つの CREATE DATABASE ステートメントを使用して、データベースおよびデータベースを格納するファイルを作成することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、次の手順を使用して CREATE DATABASE ステートメントを実装します。  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、[model データベース](../../relational-databases/databases/model-database.md)のコピーを使用して、データベースとそのメタデータを初期化します。  
  
2.  Service Broker GUID がデータベースに割り当てられます。  
  
3.  次に、[!INCLUDE[ssDE](../../includes/ssde-md.md)] は、データベース内の領域の使用状況を記録する内部データが格納されるページを除いて、データベースの残りの部分に空のページを挿入します。  
  
 インスタンスには、最大 32,767 個のデータベースを指定できます [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]です。  
  
 各データベースには、データベース内で特殊な操作を実行できる所有者が存在します。 所有者はデータベースを作成するユーザーです。 データベース所有者は、[sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md) を使用して変更できます。  

一部のデータベース機能は、データベースの機能をすべて利用するためにファイル システムに存在する機能または能力に依存しています。 ファイル システムの機能セットに依存する機能の例をいくつか挙げます。
- DBCC CHECKDB
- FileStream
- VSS とファイルのスナップショットを使用したオンライン バックアップ
- データベース スナップショットの作成
- メモリ最適化データ ファイル グループ
   
## <a name="database-files-and-filegroups"></a>データベース ファイルとファイル グループ  
 すべてのデータベースには、*プライマリ ファイル*と*トランザクション ログ ファイル*という少なくとも 2 つのファイル、および少なくとも 1 つのファイル グループがあります。 各データベースに、最大 32,767 のファイルと 32,767 のファイル グループを指定できます。  
  
 データベースを作成する際に、データ ファイルのサイズは、データベースに記述されるデータの最大量を基に可能な限り大きく設定しておきます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ファイルのストレージには、ストレージ エリア ネットワーク (SAN)、iSCSI ベースのネットワーク、または、ローカルにアタッチされたディスクを使用することをお勧めします。この構成により、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンスと信頼性を最適化することができるためです。  
  
## <a name="database-snapshots"></a>データベース スナップショット  
 CREATE DATABASE ステートメントを使用して、*ソース データベース*の読み取り専用の静的ビューである*データベース スナップショット*を作成できます。 データベース スナップショットは、スナップショットが作成された時点で存在していたソース データベースと、トランザクション的に一貫性があります。 ソース データベースは複数のスナップショットを持つことができます。  
  
> [!NOTE]  
> データベース スナップショットを作成する際、CREATE DATABASE ステートメントは、ログ ファイル、オフライン ファイル、復元ファイル、および現存しないファイルを参照することはできません。  
  
 データベース スナップショットの作成に失敗した場合、スナップショットは問題ありになります、削除する必要があります。 詳細については、「[DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)」を参照してください。  
  
 各スナップショットは、削除されるまで、DROP DATABASE を使用して保持されます。  
  
 詳細については、「[データベース スナップショット &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)」を参照してください。  
  
## <a name="database-options"></a>データベース オプション  
 データベースを作成するたびに、いくつかのデータベース オプションが自動的に設定されます。 これらのオプションの一覧については、「[ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)」を参照してください。  
  
## <a name="the-model-database-and-creating-new-databases"></a>model データベースと新しいデータベースの作成  
 [model データベース](../../relational-databases/databases/model-database.md)内にあるすべてのユーザー定義のオブジェクトは、新しく作成されたすべてのデータベースにコピーされます。 テーブル、ビュー、ストアド プロシージャ、データ型など、あらゆるオブジェクトを model データベースに追加し、新しく作成されたすべてのデータベースに含めることができます。  
  
 CREATE DATABASE *database_name* ステートメントがサイズ パラメーターを追加せずに指定されている場合、プライマリ データ ファイルは、model データベースのプライマリ ファイルと同じサイズになります。  
  
 FOR ATTACH が指定されていない限り、すべての新しいデータベースは、model データベースからデータベース オプションの設定を継承します。 たとえば、auto shrink データベース オプションは、model データベースにおいても、作成するどの新規データベースにおいても、**true** に設定されます。 model データベースのオプションを変更すると、これらの新しいオプション設定が、作成する新規のデータベースで使用されます。 model データベースの操作の変更は、既存のデータベースには影響を与えません。 CREATE DATABASE ステートメントで FOR ATTACH を指定すると、新しいデータベースは元のデータベースからデータベース オプションの設定を継承します。  
  
## <a name="viewing-database-information"></a>データベース情報の表示  
 カタログ ビュー、システム関数、およびシステム ストアド プロシージャを使用して、データベース、ファイルおよびファイル グループについての情報を返すことができます。 詳細については、「[システム ビュー &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 CREATE DATABASE、CREATE ANY DATABASE、または ALTER ANY DATABASE の各権限が必要です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス上のディスク使用量を管理するため、通常、データベースを作成する権限をいくつかのログイン アカウントに制限します。  
  
 次の例は、データベース ユーザー Fay にデータベースを作成する権限を与えます。  
  
```sql  
USE master;  
GO  
GRANT CREATE DATABASE TO [Fay];  
GO  
```  
  
### <a name="permissions-on-data-and-log-files"></a>データおよびログ ファイルに対する権限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、各データベースのデータ ファイルとログ ファイルに一定の権限が設定されます。 次の操作がデータベースに適用されるたびに、次の権限が設定されます。  
  
|||  
|-|-|  
|Created|変更して新しいファイルを追加|  
|アタッチ|バックアップ|  
|デタッチ|復元|  
  
 この権限は、開く権限のあるディレクトリにファイルが存在する場合に、そのファイルが誤って書き換えられるのを防ぎます。  
  
> [!NOTE]  
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] では、データ ファイルとログ ファイルの権限は設定されません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-database-without-specifying-files"></a>A. ファイルを指定せずにデータベースを作成する  
 次の例では、`mytest` データベースを作成し、対応するプライマリ ファイルおよびトランザクション ログ ファイルを作成します。 ステートメントに \<filespec> 項目が含まれていないため、データベースのプライマリ ファイルは、model データベースのプライマリ ファイルと同じサイズになります。 トランザクション ログは、512KB、またはプライマリ データ ファイルのサイズの 25% の値の大きい方に設定されます。 MAXSIZE が指定されていないため、ファイルはディスク上のすべての使用可能な領域いっぱいまで拡張することができます。 この例では、`mytest` という名前のデータベースが既に存在する場合はそれを削除してから、`mytest` データベースを作成する方法も示します。  
  
```sql  
USE master;  
GO  
IF DB_ID (N'mytest') IS NOT NULL
DROP DATABASE mytest;
GO
CREATE DATABASE mytest;  
GO  
-- Verify the database files and sizes  
SELECT name, size, size*1.0/128 AS [Size in MBs]   
FROM sys.master_files  
WHERE name = N'mytest';  
GO  
```  
  
### <a name="b-creating-a-database-that-specifies-the-data-and-transaction-log-files"></a>B. データ ファイルとトランザクション ログ ファイルを指定してデータベースを作成する  
 次の例では、`Sales` データベースを作成します。 PRIMARY キーワードが使用されていないので、最初のファイル (`Sales_dat`) がプライマリ ファイルになります。 `Sales_dat` ファイルの SIZE パラメーターに MB も KB も指定されていないため、ファイルは MB を使用し、メガバイト単位で割り当てられます。 `Sales_log` ファイルは、`SIZE` パラメーターに `MB` サフィックスが明示的に指定されているため、メガバイト単位で割り当てられます。  
  
```sql  
USE master;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
### <a name="c-creating-a-database-by-specifying-multiple-data-and-transaction-log-files"></a>C. 複数のデータ ファイルとトランザクション ログ ファイルを指定してデータベースを作成する  
 次の例では、3 つの `Archive` のデータ ファイルと 2 つの `100-MB` のトランザクション ログ ファイルがある `100-MB` データベースを作成します。 プライマリ ファイルはリストの最初のファイルであり、`PRIMARY` キーワードによって明示的に指定されます。 トランザクション ログ ファイルは、`LOG ON` キーワードに続けて指定されます。 `FILENAME` オプションでファイルに使用される拡張子のうち、`.mdf` はプライマリ データ ファイルに、`.ndf` はセカンダリ データ ファイルに、`.ldf` はトランザクション ログ ファイルに、それぞれ使用されます。 この例では、作成するデータベースは、`D:` データベースと同じ場所ではなく `master` ドライブに格納します。  
  
```sql  
USE master;  
GO  
CREATE DATABASE Archive   
ON  
PRIMARY    
    (NAME = Arch1,  
    FILENAME = 'D:\SalesData\archdat1.mdf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
    ( NAME = Arch2,  
    FILENAME = 'D:\SalesData\archdat2.ndf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
    ( NAME = Arch3,  
    FILENAME = 'D:\SalesData\archdat3.ndf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20)  
LOG ON   
   (NAME = Archlog1,  
    FILENAME = 'D:\SalesData\archlog1.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
   (NAME = Archlog2,  
    FILENAME = 'D:\SalesData\archlog2.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20) ;  
GO  
```  
  
### <a name="d-creating-a-database-that-has-filegroups"></a>D. ファイル グループのあるデータベースを作成する  
 次の例では、以下のファイル グループがある `Sales` データベースを作成します。  
  
-   `Spri1_dat` ファイルおよび `Spri2_dat` ファイルのあるプライマリ ファイル グループ。 これらのファイルの FILEGROWTH 増加量は、`15%` に指定されています。  
  
-   `SGrp1Fi1` ファイルおよび `SGrp1Fi2` ファイルのある、`SalesGroup1` というファイル グループ。  
  
-   `SGrp2Fi1` ファイルおよび `SGrp2Fi2` ファイルのある、`SalesGroup2` というファイル グループ。  
  
 この例では、データ ファイルとログ ファイルは、パフォーマンスを向上させるために別のディスクに格納します。  
  
```sql  
USE master;  
GO  
CREATE DATABASE Sales  
ON PRIMARY  
( NAME = SPri1_dat,  
    FILENAME = 'D:\SalesData\SPri1dat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 15% ),  
( NAME = SPri2_dat,  
    FILENAME = 'D:\SalesData\SPri2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 15% ),  
FILEGROUP SalesGroup1  
( NAME = SGrp1Fi1_dat,  
    FILENAME = 'D:\SalesData\SG1Fi1dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
( NAME = SGrp1Fi2_dat,  
    FILENAME = 'D:\SalesData\SG1Fi2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
FILEGROUP SalesGroup2  
( NAME = SGrp2Fi1_dat,  
    FILENAME = 'D:\SalesData\SG2Fi1dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
( NAME = SGrp2Fi2_dat,  
    FILENAME = 'D:\SalesData\SG2Fi2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'E:\SalesLog\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
### <a name="e-attaching-a-database"></a>E. データベースをアタッチする  
 次の例では、例 D で作成された `Archive` データベースをデタッチしてから、`FOR ATTACH` 句を使用してこのデータベースをアタッチします。 `Archive` は、複数のデータおよびログ ファイルを保有するように定義されています。 しかし、ファイルの場所が作成時から変更されていないため、`FOR ATTACH` 句に指定する必要があるのは、プライマリ ファイルのみです。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降では、アタッチされているデータベースの一部であるフルテキスト ファイルは、データベースと共にアタッチされます。  
  
```sql  
USE master;  
GO  
sp_detach_db Archive;  
GO  
CREATE DATABASE Archive  
      ON (FILENAME = 'D:\SalesData\archdat1.mdf')   
      FOR ATTACH ;  
GO  
```  
  
### <a name="f-creating-a-database-snapshot"></a>F. データベース スナップショットを作成する  
 次の例では、`sales_snapshot0600` データベース スナップショットを作成します。 データベース スナップショットは読み取り専用であるため、ログ ファイルは指定できません。 構文に準拠して、ソース データベース内のすべてのファイルが指定され、ファイル グループは指定されません。  
  
 この例で使用するソース データベースは、例 D で作成された `Sales` データベースです。  
  
```sql  
USE master;  
GO  
CREATE DATABASE sales_snapshot0600 ON  
    ( NAME = SPri1_dat, FILENAME = 'D:\SalesData\SPri1dat_0600.ss'),  
    ( NAME = SPri2_dat, FILENAME = 'D:\SalesData\SPri2dt_0600.ss'),  
    ( NAME = SGrp1Fi1_dat, FILENAME = 'D:\SalesData\SG1Fi1dt_0600.ss'),  
    ( NAME = SGrp1Fi2_dat, FILENAME = 'D:\SalesData\SG1Fi2dt_0600.ss'),  
    ( NAME = SGrp2Fi1_dat, FILENAME = 'D:\SalesData\SG2Fi1dt_0600.ss'),  
    ( NAME = SGrp2Fi2_dat, FILENAME = 'D:\SalesData\SG2Fi2dt_0600.ss')  
AS SNAPSHOT OF Sales ;  
GO  
```  
  
### <a name="g-creating-a-database-and-specifying-a-collation-name-and-options"></a>G. データベースを作成し、照合順序名とオプションを指定する  
 次の例では、`MyOptionsTest` データベースを作成します。 照合順序名が指定され、`TRUSTYWORTHY` および `DB_CHAINING` オプションが `ON` に設定されます。  
  
```sql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE French_CI_AI  
WITH TRUSTWORTHY ON, DB_CHAINING ON;  
GO  
--Verifying collation and option settings.  
SELECT name, collation_name, is_trustworthy_on, is_db_chaining_on  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
```  
  
### <a name="h-attaching-a-full-text-catalog-that-has-been-moved"></a>H. 移動されたフルテキスト カタログをアタッチする  
 次の例では、フルテキスト カタログ `AdvWksFtCat` を `AdventureWorks2012` のデータおよびログ ファイルと共にアタッチします。 この例では、フルテキスト カタログは、既定の場所から新しい場所、`c:\myFTCatalogs` に移されます。 データおよびログ ファイルは、それぞれの既定の場所に残ります。  
  
```sql  
USE master;  
GO  
--Detach the AdventureWorks2012 database  
sp_detach_db AdventureWorks2012;  
GO  
-- Physically move the full text catalog to the new location.  
--Attach the AdventureWorks2012 database and specify the new location of the full-text catalog.  
CREATE DATABASE AdventureWorks2012 ON   
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_data.mdf'),   
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_log.ldf'),  
    (FILENAME = 'c:\myFTCatalogs\AdvWksFtCat')  
FOR ATTACH;  
GO  
```  
  
### <a name="i-creating-a-database-that-specifies-a-row-filegroup-and-two-filestream-filegroups"></a>I. 1 つの ROW ファイル グループと 2 つの FILESTREAM ファイル グループを指定してデータベースを作成する  
 次の例では、`FileStreamDB` データベースを作成します。 データベースは、1 つの ROW ファイル グループと 2 つの FILESTREAM ファイル グループを使用して作成されます。 各ファイル グループには、1 つのファイルが含まれます。  
  
-   `FileStreamDB_data` には行データが含まれます。 これには、既定のパスを指定した 1 つのファイル `FileStreamDB_data.mdf` が含まれます。  
  
-   `FileStreamPhotos` には FILESTREAM データが含まれます。 これには、`FSPhotos` (`C:\MyFSfolder\Photos` にある) と `FSPhotos2` (`D:\MyFSfolder\Photos` にある) の 2 つの FILESTREAM データ コンテナーが含まれます。 また、既定の FILESTREAM ファイル グループとしてマークします。  
  
-   `FileStreamResumes` には FILESTREAM データが含まれます。 これには、1 つの FILESTREAM データ コンテナー `FSResumes` (`C:\MyFSfolder\Resumes` にある) が含まれます。  
  
```sql  
USE master;  
GO  
-- Get the SQL Server data path.  
DECLARE @data_path nvarchar(256);  
SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)  
                  FROM master.sys.master_files  
                  WHERE database_id = 1 AND file_id = 1);  
  
 -- Execute the CREATE DATABASE statement.   
EXECUTE ('CREATE DATABASE FileStreamDB  
ON PRIMARY   
    (  
    NAME = FileStreamDB_data   
    ,FILENAME = ''' + @data_path + 'FileStreamDB_data.mdf''  
    ,SIZE = 10MB  
    ,MAXSIZE = 50MB  
    ,FILEGROWTH = 15%  
    ),  
FILEGROUP FileStreamPhotos CONTAINS FILESTREAM DEFAULT  
    (  
    NAME = FSPhotos  
    ,FILENAME = ''C:\MyFSfolder\Photos''  
-- SIZE and FILEGROWTH should not be specified here.  
-- If they are specified an error will be raised.  
, MAXSIZE = 5000 MB  
    ),  
    (  
      NAME = FSPhotos2  
      , FILENAME = ''D:\MyFSfolder\Photos''  
      , MAXSIZE = 10000 MB  
     ),  
FILEGROUP FileStreamResumes CONTAINS FILESTREAM  
    (  
    NAME = FileStreamResumes  
    ,FILENAME = ''C:\MyFSfolder\Resumes''  
    )   
LOG ON  
    (  
    NAME = FileStream_log  
    ,FILENAME = ''' + @data_path + 'FileStreamDB_log.ldf''  
    ,SIZE = 5MB  
    ,MAXSIZE = 25MB  
    ,FILEGROWTH = 5MB  
    )'  
);  
GO  
```  
  
### <a name="j-creating-a-database-that-has-a-filestream-filegroup-with-multiple-files"></a>J. 複数のファイルを含む FILESTREAM ファイル グループのあるデータベースを作成する  
 次の例では、`BlobStore1` データベースを作成します。 データベースは、1 つの ROW ファイル グループと、`FS` という 1 つの FILESTREAM ファイル グループを使用して作成されます。 FILESTREAM ファイル グループには、`FS1` および `FS2` の 2 つのファイルが含まれています。 その後 `FS3` という 3 つ目のファイルが FILESTREAM ファイルグループに追加されると、データベースが変更されます。  
  
```sql  
USE master;  
GO  
  
CREATE DATABASE [BlobStore1]  
CONTAINMENT = NONE  
ON PRIMARY   
(   
    NAME = N'BlobStore1',   
    FILENAME = N'C:\BlobStore\BlobStore1.mdf',  
    SIZE = 100MB,  
    MAXSIZE = UNLIMITED,  
    FILEGROWTH = 1MB  
),   
FILEGROUP [FS] CONTAINS FILESTREAM DEFAULT   
(  
    NAME = N'FS1',  
    FILENAME = N'C:\BlobStore\FS1',  
    MAXSIZE = UNLIMITED  
),   
(  
    NAME = N'FS2',  
    FILENAME = N'C:\BlobStore\FS2',  
    MAXSIZE = 100MB  
)  
LOG ON   
(  
    NAME = N'BlobStore1_log',  
    FILENAME = N'C:\BlobStore\BlobStore1_log.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 1GB,  
    FILEGROWTH = 1MB  
);  
GO  
  
ALTER DATABASE [BlobStore1]  
ADD FILE  
(  
    NAME = N'FS3',  
    FILENAME = N'C:\BlobStore\FS3',  
    MAXSIZE = 100MB  
)  
TO FILEGROUP [FS];  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)   
 [Database Snapshots &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [データベース ファイルの移動](../../relational-databases/databases/move-database-files.md)   
 [データベース](../../relational-databases/databases/databases.md)   
 [バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  

