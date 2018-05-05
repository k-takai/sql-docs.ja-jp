---
title: XML for Analysis への準拠 (XMLA) |Microsoft ドキュメント
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- compliance [XML for Analysis]
- XML for Analysis, compliance
- XMLA, extended functionality
- XML for Analysis, extended functionality
- XMLA, compliance
- extending XML for Analysis
ms.assetid: d987d320-5581-4454-ad45-68e3a22175b6
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b801e87576ae4ecf47f6ed828d35eac06c44a94d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="xml-for-analysis-compliance-xmla"></a>XML for Analysis への準拠 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  XML for Analysis 1.1 仕様は、World Wide Web 上に存在するデータ ソースへのアクセスをサポートするオープン スタンダードを記述します。 このトピックの詳細レベルでサポートされている XML for Analysis 1.1 仕様に準拠して[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]です。  
  
## <a name="compliant-items"></a>準拠項目  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、XML for Analysis 1.1 仕様にリストされたすべての必須項目に準拠しています。 それに加えて、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は XML for Analysis 1.1 仕様に記述された以下のオプション項目を実装しています。  
  
|アイテム|仕様|実装|  
|----------|-------------------|--------------------|  
|セッション サポート|XML for Analysis 1.1 仕様の「Support for Statefulness in XML for Analysis」セクションに記載されている SOAP ヘッダー要素。|リストされているすべての SOAP ヘッダー要素は、仕様に記述されているとおりに [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] でサポートされます。|  
  
## <a name="extensions"></a>拡張機能  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は XML for Analysis 1.1 仕様の拡張機能として、次のような追加機能も提供します。  
  
|アイテム|仕様|実装|  
|----------|-------------------|--------------------|  
|プロトコル ネゴシエーション|XML for Analysis 1.1 仕様には情報が含まれていません。|によって追加された ProtocolCapabilities ヘッダー要素[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]プロトコル機能のネゴシエーションをサポートするためにします。|  
|Discover メソッドでサポートされる XML for Analysis (XMLA) コマンド|以下のコマンドが XML for Analysis 1.1 仕様によってサポートされています。<br /><br /> [Statement 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|以下のコマンドが [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] によってサポートされています。<br /><br /> [Alter 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)<br /><br /> [要素をバックアップ&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)<br /><br /> [要素をバッチ&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)<br /><br /> [BeginTransaction 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)<br /><br /> [Cancel 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)<br /><br /> [ClearCache 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)<br /><br /> [CommitTransaction 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)<br /><br /> [要素を作成する&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)<br /><br /> [Delete 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)<br /><br /> [DesignAggregations 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)<br /><br /> [Drop 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)<br /><br /> [要素を挿入&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)<br /><br /> [要素をロック&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)<br /><br /> [MergePartitions 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)<br /><br /> [NotifyTableChange 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)<br /><br /> [要素を処理&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)<br /><br /> [Restore 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)<br /><br /> [RollbackTransaction 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)<br /><br /> [Statement 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)<br /><br /> [Subscribe 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)<br /><br /> [要素 & #40; を同期します。XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)<br /><br /> [要素のロック解除&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)<br /><br /> [Update 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)<br /><br /> [UpdateCells 要素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|表形式の行セットでの列エラー|XML for Analysis 1.1 仕様にはリストされていません。|[エラー](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)要素はによって使用[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]に含まれる列要素のエラーを報告する、[行](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)要素。|  
  
## <a name="see-also"></a>参照  
 [XML for Analysis & #40 です。XMLA & #41;参照](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  