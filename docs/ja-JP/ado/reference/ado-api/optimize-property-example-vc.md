---
title: プロパティの例 (vc++) を最適化 |Microsoft ドキュメント
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Optimize property [ADO], VC++ example
ms.assetid: cb335455-b027-4f66-868d-d0d8b2175de1
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e986ec8517322f76bd421ab9b7071ffc464079e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="optimize-property-example-vc"></a>プロパティの例 (vc++) を最適化します。
この例で、[フィールド](../../../ado/reference/ado-api/field-object.md)オブジェクト ダイナミック**最適化**プロパティです。 **Zip**のフィールド、**作成者**テーブルに、 **Pubs**データベースのインデックスが付いていません。 設定、[最適化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)プロパティを**True**上、 **zip**フィールド承認のパフォーマンスを向上させるインデックスを作成する ADO、 [を見つける](../../../ado/reference/ado-api/find-method-ado.md)メソッドです。  
  
## <a name="example"></a>例  
  
```  
// Optimize_Property_Sample.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) { if FAILED(x) _com_issue_error(x); };  
void OptimizeX();  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   OptimizeX();  
   ::CoUninitialize();  
}  
  
void OptimizeX() {  
   _bstr_t strCnn("Provider='sqloledb'; Data Source='My_Data_Source'; Initial Catalog='pubs'; Integrated Security='SSPI';");  
  
   // Define ADO object pointers.  Initialize pointers on define.  
   // These are in the ADODB:: namespace.  
   _RecordsetPtr pRst = NULL;  
  
   try {  
      TESTHR(pRst.CreateInstance(__uuidof(Recordset)));  
  
      // Enable Index creation.  
      pRst->CursorLocation = adUseClient;  
      pRst->Open ("SELECT * FROM authors", strCnn, adOpenStatic, adLockReadOnly, adCmdText);  
  
      // Create the index  
      pRst->Fields->GetItem("zip")->Properties->GetItem("Optimize")->PutValue("True");  
  
      // Find Akiko Yokomoto  
      pRst->Find("zip = '94595'", 1, adSearchForward);  
      printf("%s %s    %s %s %s",  
         (LPSTR) (_bstr_t) pRst->Fields->GetItem("au_fname")->Value,  
         (LPSTR) (_bstr_t) pRst->Fields->GetItem("au_lname")->Value,  
         (LPSTR) (_bstr_t) pRst->Fields->GetItem("address")->Value,  
         (LPSTR) (_bstr_t) pRst->Fields->GetItem("city")->Value,  
         (LPSTR) (_bstr_t) pRst->Fields->GetItem("state")->Value);  
  
      // Delete the index  
      pRst->Fields->GetItem("zip")->Properties->GetItem("Optimize")->PutValue("False");  
   }  
   catch (_com_error &e) {  
      // Display errors, if any.  Pass connection pointer accessed from the Recordset.  
      _variant_t vtConnect = pRst->GetActiveConnection();  
  
      // GetActiveConnection returns connect string if connection  
      // is not open, else returns Connection object.  
      switch(vtConnect.vt) {  
      case VT_BSTR:  
         PrintComError(e);  
         break;  
      case VT_DISPATCH:  
         PrintProviderError(vtConnect);  
         break;  
      default:  
         printf("Errors occured.");  
         break;  
      }  
   }  
  
   // Clean up objects before exit.  
   if (pRst)  
      if (pRst->State == adStateOpen)  
         pRst->Close();  
}  
  
void PrintProviderError(_ConnectionPtr pConnection) {  
   // Print Provider Errors from Connection object.  
   // pErr is a record object in the Connection's Error collection.  
   ErrorPtr pErr = NULL;  
  
   if ( (pConnection->Errors->Count) > 0 ) {  
      long nCount = pConnection->Errors->Count;  
  
      // Collection ranges from 0 to nCount -1.  
      for ( long i = 0 ; i < nCount ; i++ ) {  
         pErr = pConnection->Errors->GetItem(i);  
         printf("\t Error number: %x\t%s", pErr->Number, pErr->Description);  
      }  
   }  
}  
  
void PrintComError(_com_error &e) {  
   _bstr_t bstrSource(e.Source());  
   _bstr_t bstrDescription(e.Description());  
  
   // Print COM errors.   
   printf("Error\n");  
   printf("\tCode = %08lx\n", e.Error());  
   printf("\tCode meaning = %s\n", e.ErrorMessage());  
   printf("\tSource = %s\n", (LPCSTR) bstrSource);  
   printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
```  
  
 **Akiko Yokomoto 3 Silver-2-xクルミ クリーク CA**   
## <a name="see-also"></a>参照  
 [Field オブジェクト](../../../ado/reference/ado-api/field-object.md)   
 [Optimize プロパティ - 動的 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)