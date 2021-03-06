---
title: レポート サーバー アイテムに対して Windows SharePoint Services の組み込みのセキュリティを使用する | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: security
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- permissions [Reporting Services], SharePoint integrated mode
- SharePoint integration [Reporting Services], permissions
- security [Reporting Services], SharePoint integrated mode
ms.assetid: 9577e88d-c22b-4934-936f-e0f1400cedf5
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5155c5689a4c7a51f2d392e8560a2c87dbf44fdd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "33033229"
---
# <a name="use-built-in-security-in-windows-sharepoint-services-for-report-server-items"></a>レポート サーバー アイテムに対して Windows SharePoint Services の組み込みのセキュリティを使用する
  SharePoint は、SharePoint のサイトおよびライブラリにあるレポート サーバー アイテムへのアクセスに使用できる、組み込みのセキュリティ機能を提供します。 サイトおよびリストに対する権限がユーザーに割り当て済みである場合は、SharePoint とレポート サーバーの間の統合設定を構成すると、直ちにそのユーザーがレポート サーバーのアイテムおよび操作にアクセスできるようになります。  
  
## <a name="securable-items"></a>セキュリティ保護可能なアイテム  
 サイトやライブラリに対して定義する権限は、レポート サーバー アイテムへのアクセスを許可するために使用できます。 ただし、個々のアイテムのセキュリティを保護する場合は、次のコンテンツ タイプに対する権限を設定できます。  
  
|ファイルの種類|Description|  
|---------------|-----------------|  
|.rdl|レポート レイアウトおよびデータの取得に使用するコマンドを定義するレポート定義ファイルです。 レポートが処理されると、レポート定義はデータ ソース接続情報を使用してデータを取得します。 レポート定義がレポート ビルダーで作成されたアドホック レポートである場合、表示されたレポートに対するデータ探索スコープを設定するレポート モデル (.smdl) ファイルがレポートに付属しています。|  
|.smdl|データ構造およびデータ構造の関連付けを記述するレポート モデル ファイルです。 このファイルは、レポート ビルダーのレポートの作成および実行に使用します。|  
|.rsds|外部データ ソースへの接続情報を指定する共有データ ソース ファイルです。 レポート定義 (.rdl) およびレポート モデル (.smdl) ファイルによって使用されます。 レポート モデルは、常に .rsds ファイルを使用して基になるデータ ソースへの接続情報を取得します。 レポート定義では、.rsds ファイル、またはレポートのデータ ソース プロパティで定義された接続情報を使用できます。|  
|.rsc|レポート アイテムまたはデータ領域のレイアウトと構造を定義するレポート パーツ ファイルです。 このファイルを使用してレポート パーツをサーバーにパブリッシュすると、他のレポート作成者はレポート パーツ ギャラリーからアイテムを再利用できます。|  
|.rsd|データセットのクエリ構文とプロパティを定義する共有データセット ファイルです。 共有データセットは、レポートの外部から共有、格納、処理、およびキャッシュできます。|  
  
 スケジュール、サブスクリプション、およびレポート履歴はセキュリティ保護可能なアイテムではありません。 サイトまたはライブラリに対する権限を設定することによって、スケジュール、サブスクリプション、およびレポート履歴をユーザーが作成または使用できるかどうかを決定できます。ただし、これらのアイテムのセキュリティを直接保護することはできません。  
  
 個別のアイテムを保護するには、ライブラリのアイテムを選択し、下矢印をクリックして、 **[権限の管理]** をクリックします。 **[アクション]** メニューの **[権限を編集]** をクリックします。  
  
## <a name="using-built-in-groups-and-permission-levels-to-access-report-server-items"></a>組み込みのグループおよび権限レベルを使用したレポート サーバーのアイテムへのアクセス  
 権限の継承および標準の SharePoint グループを使用する場合は、レポート サーバーおよび SharePoint インスタンスの統合設定を構成すると、直ちにほとんどのレポート サーバーの操作にアクセスできるようになります。  
  
 SharePoint で提供される標準グループは、SharePoint サイトのドキュメントおよびページにどのようにアクセスできるかを決定する、定義済み権限レベルにマップされます。 標準グループおよび既定の権限レベルを使用する場合に、サイトが権限を継承するように構成されていると、次の方法で [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 機能を使用できます。  
  
|**SharePoint グループ**|**権限レベル**|**概要**|**レポート サーバー アクセス**|  
|---------------------------|--------------------------|-----------------|------------------------------|  
|**所有者**|フル コントロール|所有者には、レポート サーバーのアイテムと操作の作成、管理、およびセキュリティ保護を行う完全な権限があります。|サイト内のライブラリに格納されたすべてのレポート サーバー アイテムへのアクセスを制御する権限を設定します。 レポート モデル内の権限を設定します (モデル アイテム セキュリティとも呼ばれます)。 レポート ビューアー Web パーツをカスタマイズします。 レポートなどのアイテムをライブラリに追加します。 レポートなどのドキュメントに使用するアイテム プロパティを編集します。 レポートなどのアイテムを削除します。 データ探索にレポート モデルを使用するレポートなど、レポートを表示します。 レポートのパラメーターを設定します。 レポートの処理オプションを設定します。 レポート モデルを生成します。 レポート ビルダーでレポートを作成します。 共有データ ソースを作成および管理します。 任意のユーザーが所有するサブスクリプションを作成、変更、および削除します。 サイト全体で使用される共有スケジュールを作成および管理します。 レポート履歴など、ドキュメントのバージョンを作成および管理します。 レポート定義またはレポート モデルのソース ファイルをダウンロードします。 レポート定義、レポート モデル、共有データ ソース、またはリソースを置き換えます (アイテムのプロパティおよび権限は維持)。|  
|**メンバー**|投稿|メンバーは、新しいアイテムを作成し、アイテムのレポートおよびモデルをデザイン ツールから SharePoint ライブラリにパブリッシュすることができます。|レポートなどのアイテムをライブラリに追加します。 レポートなどのドキュメントに使用するアイテム プロパティを編集します。 レポートなどのアイテムを削除します。 データ探索にレポート モデルを使用するレポートなど、レポートを表示します。 レポート履歴スナップショットなど、ドキュメントの過去のバージョンを表示します (ユーザーには、レポート履歴が作成された元のレポートを開く権限が必要)。 レポートのパラメーターを設定します。 レポートの処理オプションを設定します。 レポート モデルを生成します。 レポート ビルダーでレポートを作成します。 共有データ ソースを作成および管理します。 そのユーザーが所有するサブスクリプションを作成、変更、および削除します。 サブスクリプションで共有スケジュールを使用します。 レポート履歴など、ドキュメントのバージョンを作成および管理します。 レポート定義またはレポート モデルのソース ファイルをダウンロードします。 レポート定義、レポート モデル、共有データ ソース、またはリソースを置き換えます (アイテムのプロパティおよび権限は維持)。|  
|**閲覧者**と**ビューアー**|Read|閲覧者はレポートを表示できます。|データ探索にレポート モデルを使用するレポートなど、レポートを表示します。|  
  
 組み込みのグループおよび権限レベルを使用しない場合、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 機能にアクセスするには、特定の権限が必要になります。 詳細については、「 [SharePoint Web アプリケーションのレポート サーバー操作に対する権限を設定する](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SharePoint サイトのレポート サーバー アイテムに対する権限の付与](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [SQL Server Reporting Services と SharePoint グループの役割とタスクの比較とアクセス許可](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)   
 [SharePoint Web アプリケーションのレポート サーバー操作に対するアクセス許可を設定する](../../reporting-services/security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md)   
 [SharePoint サイトのレポート サーバー アイテムに対する権限の付与](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
