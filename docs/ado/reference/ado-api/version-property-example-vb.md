---
title: バージョン プロパティの例 (VB) |Microsoft ドキュメント
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
dev_langs:
- VB
helpviewer_keywords:
- Version property [ADO], Visual Basic example
ms.assetid: 708efd50-2905-4168-b7e4-91b2e9b23539
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c48b12324b24a03452e7520afe04579c2989252
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="version-property-example-vb"></a>バージョン プロパティの例 (VB)
この例では、[バージョン](../../../ado/reference/ado-api/version-property-ado.md)のプロパティ、[接続](../../../ado/reference/ado-api/connection-object-ado.md)ADO の現在のバージョンを表示するオブジェクト。 表示するいくつかの動的なプロパティを使用します。  
  
-   現在の DBMS 名とバージョン。  
  
-   OLE DB バージョンです。  
  
-   プロバイダー名とバージョン。  
  
-   ODBC のバージョンです。  
  
-   ODBC ドライバー名およびバージョンです。  
  
```  
'BeginVersionVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strVersionInfo As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    strVersionInfo = "ADO Version: " & Cnxn.Version & vbCr  
    strVersionInfo = strVersionInfo & "DBMS Name: " & Cnxn.Properties("DBMS Name") & vbCr  
    strVersionInfo = strVersionInfo & "DBMS Version: " & Cnxn.Properties("DBMS Version") & vbCr  
    strVersionInfo = strVersionInfo & "OLE DB Version: " & Cnxn.Properties("OLE DB Version") & vbCr  
    strVersionInfo = strVersionInfo & "Provider Name: " & Cnxn.Properties("Provider Name") & vbCr  
    strVersionInfo = strVersionInfo & "Provider Version: " & Cnxn.Properties("Provider Version") & vbCr  
  
    MsgBox strVersionInfo  
  
    ' clean up  
    Cnxn.Close  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndVersionVB  
```  
  
## <a name="see-also"></a>参照  
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Version プロパティ (ADO)](../../../ado/reference/ado-api/version-property-ado.md)
