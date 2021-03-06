---
title: Stat メソッド |Microsoft ドキュメント
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
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26dd4f3fa7de49f51c32fd97e184ee356cb16f35
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="stat-method"></a>Stat メソッド
に関する情報を取得、[ストリーム](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクト。  
  
## <a name="syntax"></a>構文  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>戻り値  
 A**長い**操作のステータスを示す値。  
  
#### <a name="parameters"></a>パラメーター  
 *StatStg*  
 ストリームに関する情報が格納される STATSTG 構造体。 実装、 **Stat** ADO ストリーム オブジェクトによって使用されるメソッドがすべての構造体のフィールドでいっぱいになりません。  
  
 *StatFlag*  
 このメソッドで返されない一部のメンバーこれにより、メモリ割り当て操作が節約 STATSTG の構造体を指定します。 値は、STATFLAG 列挙体から取得されます。 STATFLAG 列挙体は 2 つの値  
  
|定数|値|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>解説  
 Stat ADO ストリーム オブジェクトに対して実装されるメソッドのバージョンは、STATSTG 構造体の次のフィールドに入力します。  
  
 *pwcsName*  
 StatFlag 値 STATFLAG_NONAME と 1 つが利用可能な場合、ストリームの名前を含む文字列が指定されませんでした。  
  
 *cbSize*  
 ストリームまたはバイト配列のバイト単位のサイズを指定します。  
  
 *mtime*  
 このストレージ、ストリーム、またはバイト配列の最終変更時刻を示します。  
  
 *ctime*  
 このストレージ、ストリーム、またはバイト配列の作成時間を示します。  
  
 *atime*  
 このストレージ、ストリームまたはバイト配列の最終アクセス時間を示します。  
  
 STATFLAG_NONAME が StatFlag パラメーターで指定されている場合、ストリームの名前は返されません。  
  
 STATFLAG_NONAME が StatFlag パラメーターで指定されていない、使用できる現在のストリーム名がない場合は、この値は E_NOTIMPL になります。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
