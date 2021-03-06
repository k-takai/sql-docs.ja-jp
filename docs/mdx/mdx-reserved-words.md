---
title: MDX の予約語 |Microsoft ドキュメント
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5eec141a82b4cf7aca5fd8c112249c362a1242d4
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34742291"
---
# <a name="mdx-reserved-words"></a>MDX の予約語


  次の表に、多次元式 (MDX) で使用する予約語を示します。 これらの語を、MDX のキューブ名などの識別子やユーザー定義関数名の一部として使用することはできません。  
  
|||||  
|-|-|-|-|  
|ABSOLUTE|DESC|LEAVES|SELF_BEFORE_AFTER|  
|ACTIONPARAMETERSET|DESCENDANTS|LEVEL|SESSION|  
|ADDCALCULATEDMEMBERS|DESCRIPTION|LEVELS|SET|  
|AFTER|DIMENSION|LINKMEMBER|SETTOARRAY|  
|AGGREGATE|DIMENSIONS|LINREGINTERCEPT|SETTOSTR|  
|ALL|DISTINCT|LINREGPOINT|SORT|  
|ALLMEMBERS|DISTINCTCOUNT|LINREGR2|STDDEV|  
|ANCESTOR|DRILLDOWNLEVEL|LINREGSLOPE|STDDEVP|  
|ANCESTORS|DRILLDOWNLEVELBOTTOM|LINREGVARIANCE|STDEV|  
|AND|DRILLDOWNLEVELTOP|LOOKUPCUBE|STDEVP|  
|AS|DRILLDOWNMEMBER|MAX|STORAGE|  
|ASC|DRILLDOWNMEMBERBOTTOM|MEASURE|STRIPCALCULATEDMEMBERS|  
|ASCENDANTS|DRILLDOWNMEMBERTOP|MEDIAN|STRTOMEMBER|  
|AVERAGE|DRILLUPLEVEL|MEMBER|STRTOSET|  
|AXIS|DRILLUPMEMBER|MEMBERS|STRTOTUPLE|  
|BASC|DROP|MEMBERTOSTR|STRTOVAL|  
|BDESC|EMPTY|MIN|STRTOVALUE|  
|BEFORE|END|MTD|SUBSET|  
|BEFORE_AND_AFTER|ERROR|NAME|SUM|  
|BOTTOMCOUNT|EXCEPT|NAMETOSET|TAIL|  
|BOTTOMPERCENT|EXCLUDEEMPTY|NEST|THIS|  
|BOTTOMSUM|EXTRACT|NEXTMEMBER|TOGGLEDRILLSTATE|  
|BY|FALSE|NO_ALLOCATION|TOPCOUNT|  
|CACHE|FILTER|NO_PROPERTIES|TOPPERCENT|  
|CALCULATE|FIRSTCHILD|NON|TOPSUM|  
|CALCULATION|FIRSTSIBLING|NONEMPTYCROSSJOIN|TOTALS|  
|CALCULATIONCURRENTPASS|FOR|NOT_RELATED_TO_FACTS|TREE|  
|CALCULATIONPASSVALUE|FREEZE|NULL|TRUE|  
|CALCULATIONS|FROM|ON|TUPLETOSTR|  
|CALL|GENERATE|OPENINGPERIOD|TYPE|  
|CELL|GLOBAL|OR|UNION|  
|CELLFORMULASETLIST|GROUP|PAGES|UNIQUE|  
|CHAPTERS|GROUPING|PARALLELPERIOD|UNIQUENAME|  
|CHILDREN|HEAD|PARENT|UPDATE|  
|CLEAR|HIDDEN|PASS|USE|  
|CLOSINGPERIOD|HIERARCHIZE|PERIODSTODATE|USE_EQUAL_ALLOCATION|  
|COALESCEEMPTY|HIERARCHY|POST|USE_WEIGHTED_ALLOCATION|  
|COLUMN|IGNORE|PREDICT|USE_WEIGHTED_INCREMENT|  
|COLUMNS|IIF|PREVMEMBER|USERNAME|  
|CORRELATION|INCLUDEEMPTY|PROPERTIES|VALIDMEASURE|  
|COUNT|INDEX|PROPERTY|Value|  
|COUSIN|INTERSECT|QTD|VAR|  
|COVARIANCE|IS|RANK|VARIANCE|  
|COVARIANCEN|ISANCESTOR|RECURSIVE|VARIANCEP|  
|CREATE|ISEMPTY|RELATIVE|VARP|  
|CREATEPROPERTYSET|ISGENERATION|ROLLUPCHILDREN|VISUAL|  
|CREATEVIRTUALDIMENSION|ISLEAF|ROOT|VISUALTOTALS|  
|CROSSJOIN|ISSIBLING|ROWS|WHERE|  
|CUBE|ITEM|SCOPE|WITH|  
|CURRENT|LAG|SECTIONS|WTD|  
|CURRENTCUBE|LASTCHILD|SELECT|XOR|  
|CURRENTMEMBER|LASTPERIODS|SELF|YTD|  
|DEFAULT_MEMBER|LASTSIBLING|SELF_AND_AFTER||  
|DEFAULTMEMBER|LEAD|SELF_AND_BEFORE||  
  
## <a name="see-also"></a>参照  
 [予約済みキーワード&#40;MDX 構文&#41;](../mdx/reserved-keywords-mdx-syntax.md)   
 [MDX 言語リファレンス&#40;MDX&#41;](../mdx/mdx-language-reference-mdx.md)  
  
  
