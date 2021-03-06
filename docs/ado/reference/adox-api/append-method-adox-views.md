---
title: Append メソッド (ADOX Views) |Microsoft ドキュメント
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::raw_Append
- Views::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6070fd58-3237-4c77-a966-5b39ce5d57e4
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d8d713be4cf193ba7cacf1957bdf51937b9ed4a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="append-method-adox-views"></a>Append メソッド (ADOX ビュー)
新たに作成[ビュー](../../../ado/reference/adox-api/view-object-adox.md)オブジェクトに追加され、[ビュー](../../../ado/reference/adox-api/views-collection-adox.md)コレクション。  
  
## <a name="syntax"></a>構文  
  
```  
  
Views.Append Name, Command  
```  
  
#### <a name="parameters"></a>パラメーター  
 *名前*  
 A**文字列**を作成するビューの名前を指定する値。  
  
 *Command*  
 ADO[コマンド](../../../ado/reference/ado-api/command-object-ado.md)を作成するビューを表すオブジェクト。  
  
## <a name="remarks"></a>解説  
 指定した属性と名前を持つデータ ソースに新しいビューを作成、**コマンド**オブジェクト。  
  
 ユーザーが指定したコマンド テキストを表す場合、ビューではなく、プロシージャ、動作は、プロバイダーによって異なります。 **追加**プロバイダーは永続的なコマンドをサポートしていない場合は失敗します。  
  
> [!NOTE]
>  For Microsoft Jet OLE DB プロバイダーを使用する場合、**ビュー**コレクション**Append**を指定するメソッドを使用できる、**プロシージャ**ではなく、**ビュー**で、*コマンド*パラメーター。 **プロシージャ**がデータ ソースに追加されに追加されます、**ビュー**コレクション。 後に、 **Append**場合は、**プロシージャ**と**ビュー**コレクションが更新されると、**プロシージャ**でしなくなる**ビュー**コレクションに表示されます、**プロシージャ**コレクション。  
  
## <a name="applies-to"></a>適用対象  
 [Views コレクション (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
  
## <a name="see-also"></a>参照  
 [ビューの追加メソッドの例 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Append メソッド (ADOX 列)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append メソッド (ADOX グループ)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append メソッド (ADOX インデックス)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append メソッド (ADOX キー)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append メソッド (ADOX プロシージャ)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append メソッド (ADOX テーブル)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append メソッド (ADOX Users)](../../../ado/reference/adox-api/append-method-adox-users.md)
