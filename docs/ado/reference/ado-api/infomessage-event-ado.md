---
title: "InfoMessage イベント (ADO) |Microsoft ドキュメント"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7f1e479b4dfb5b9cb557030e03afeac3f6278720
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="infomessage-event-ado"></a>InfoMessage イベント (ADO)
**InfoMessage**中に警告が発生するたびにイベントが呼び出された、 **ConnectionEvent**操作します。  
  
## <a name="syntax"></a>構文  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *pError*  
 [エラー](../../../ado/reference/ado-api/error-object.md)オブジェクト。 このパラメーターには、返されるエラーが含まれています。 複数のエラーが返された場合は、列挙、**エラー**それらを検索するコレクション。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状態値。 警告が発生した場合*adStatus*に設定されている**adStatusOK**と*pError*警告が含まれています。  
  
 このイベントが返される前に、このパラメーターを設定**adStatusUnwantedEvent**を後続の通知を防ぐためにします。  
  
 *pConnection*  
 A[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。 警告が発生した接続です。 開くときに警告が発生することがなど、**接続**オブジェクトまたはを実行する、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)上、**接続**です。  
  
## <a name="see-also"></a>参照  
 [ADO イベント モデルの例 (vc++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)