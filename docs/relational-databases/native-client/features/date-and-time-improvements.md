---
title: "日付と時刻の強化 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 9b1d0d9d-1f6e-4399-8f61-e23f9a486a7a
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 843ce549dbd36f8fcbde8c61ade8cee2bc7163ca
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2017
---
# <a name="date-and-time-improvements"></a>日付と時刻の強化
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  このトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に追加された日付と時刻のデータ型の [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client サポートについて説明します。  
  
 日付/時刻の強化の詳細については、次を参照してください。[日付と時刻の強化 &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)と[日付と時刻の強化 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)です。  
  
 この機能を説明するサンプル アプリケーションについては、次を参照してください。 [SQL Server データ プログラミング サンプル](http://msftdpprodsamples.codeplex.com/)です。  
  
## <a name="usage"></a>使用方法  
 ここでは、新しい日付型と時刻型のさまざまな使用方法について説明します。  
  
### <a name="use-date-as-a-distinct-data-type"></a>個別のデータ型として日付を使用する  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 以降、日付型と時刻型のサポートの強化により、SQL_TYPE_DATE ODBC 型 (ODBC 2.0 アプリケーションの場合は SQL_DATE) と DBTYPE_DBDATE OLE DB 型をより効果的に使用できるようになります。  
  
### <a name="use-time-as-a-distinct-data-type"></a>個別のデータ型として時刻を使用する  
 OLE DB には既に、有効桁数が 1 秒のデータ型として DBTYPE_DBTIME があります。このデータ型には時刻のみが含まれます。 この型は、ODBC の SQL_TYPE_TIME (ODBC 2.0 アプリケーションの場合は SQL_TIME) に相当します。  
  
 新しい[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]時刻データ型は小数秒の精度が 100 ナノ秒です。 新しい型にはその必要があります[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client: DBTYPE_DBTIME2 (OLE DB) と SQL_SS_TIME2 (ODBC)。 秒の小数部を含まない時刻を使用するように記述された既存のアプリケーションでは、time(0) 列を使用できます。 アプリケーションがメタデータに返される型に依存しない場合は、既存の OLE DB DBTYPE_TIME 型と ODBC SQL_TYPE_TIME 型、およびそれに対応する構造体が正常に動作します。  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>秒の有効桁数が拡張された個別のデータ型として時刻を使用する  
 プロセス制御や製造アプリケーションなど、アプリケーションによっては、有効桁数が 100 ナノ秒までの時刻データを処理できる必要があります。 このための新しい型が DBTYPE_DBTIME2 (OLE DB) と SQL_SS_TIME2 (ODBC) です。  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>秒の有効桁数が拡張された Datetime を使用する  
 OLE DB では既に、有効桁数が 1 ナノ秒までの型が定義されています。 ただし、この型は既に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既存のアプリケーションで使用されており、このようなアプリケーションでは、有効桁数を 1/300 秒までしか想定していません。 新しい**datetime2(3)**型は、既存の datetime 型と直接的な互換性はありません。 これがアプリケーションの動作に影響するというリスクがある場合、アプリケーションは新しい DBCOLUMN フラグを使用して、実際のサーバーの種類を判断する必要があります。  
  
 ODBC DB でも既に、有効桁数が 1 ナノ秒までの型が定義されています。 ただし、この型は既に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既存のアプリケーションで使用されており、このようなアプリケーションでは、有効桁数を 3 ミリ秒までしか想定していません。 新しい**datetime2(3)**型は、既存の直接的な互換性がない**datetime**型です。 **datetime2(3)**精度は 1 ミリ秒、および**datetime** 1/300 秒の有効桁数です。 ODBC では、アプリケーションが SQL_DESC_TYPE_NAME 記述子フィールドで使用されているサーバーの種類を判断できます。 したがって、既存の型 SQL_TYPE_TIMESTAMP (ODBC 2.0 アプリケーションの場合は SQL_TIMESTAMP) は両方の型に使用できます。  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>秒の有効桁数とタイム ゾーンが拡張された Datetime を使用する  
 アプリケーションによっては、タイム ゾーン情報を含む datetime 値が必要です。 これは、新しい型 DBTYPE_DBTIMESTAMPOFFSET (OLE DB) および SQL_SS_TIMESTAMPOFFSET (ODBC) でサポートされています。  
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>既存の変換と一貫性のあるクライアント側変換で Date/Time/Datetime/Datetimeoffset データを使用する  
 ODBC 標準では、既存の date 型、time 型、および timestamp 型の間の変換のしくみについて説明します。 このような変換は、[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] で導入されたすべての日付型と時刻型との間の変換を含めるように一貫して拡張されます。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の機能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  