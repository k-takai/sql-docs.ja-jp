---
title: "Unicode |Microsoft ドキュメント"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7ec40cc841c073fe66f9537687516f044048a0fc
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="unicode"></a>Unicode
Unicode では、多くの言語で、文字のエンコードを定義します。  
  
 Unicode 規格の詳細については、次を参照してください。 [Unicode コンソーシアムの「](http://www.unicode.org)です。  
  
 Unicode では、ユニバーサル文字セットを定義します。 Windows の ANSI コード ページでは、通常 1 つの言語の文字を含む、文字セットを定義します。 異なるコード ページを使用するために必要なアプリケーションを作成しにくい場合があります。  
  
 Unicode では、コード ページは必要ありません。 すべてのコード ポイントは、一部の言語の 1 文字にマップされます。  
  
 現時点では、ODBC をサポートしているエンコードのみ Unicode では、文字を表現する 16 ビット整数 (固定長) を使用している UCS 2 です。 Unicode では、さまざまな言語で動作するアプリケーションができます。  
  
 ODBC 3.5 (またはそれ以降) ドライバー マネージャーは、Unicode に対応します。 2 つの主要な領域に影響します。 関数呼び出しと、文字列データ型。 ドライバー マネージャー マップ関数の文字列引数と文字列データは、アプリケーションおよびドライバーによって必要に応じては Unicode に対応するか、ANSI が有効なをどちらもできます。 これら 2 つの領域は、のセクションで詳しく説明[Unicode 関数の引数](../../../odbc/reference/develop-app/unicode-function-arguments.md)と[Unicode データ](../../../odbc/reference/develop-app/unicode-data.md)です。  
  
 ODBC 3.5 (またはそれ以降) のドライバー マネージャーは、Unicode アプリケーションと ANSI アプリケーションの両方で Unicode ドライバーの使用をサポートします。 ANSI アプリケーションと ANSI ドライバーの使用もサポートします。 ドライバー マネージャーは、Unicode アプリケーションの場合、ANSI ドライバーの使用の制限の Unicode から ANSI へマッピングを提供します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [Unicode 関数の引数](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Unicode データ](../../../odbc/reference/develop-app/unicode-data.md)