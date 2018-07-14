---
title: XML for Analysis 호환성 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- compliance [XML for Analysis]
- XML for Analysis, compliance
- XMLA, extended functionality
- XML for Analysis, extended functionality
- XMLA, compliance
- extending XML for Analysis
ms.assetid: d987d320-5581-4454-ad45-68e3a22175b6
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cc7a8da77b72f25a68764636fbe15bc2d9e4ae04
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267089"
---
# <a name="xml-for-analysis-compliance-xmla"></a>XMLA(XML for Analysis) 호환성
  XMLA 1.1 사양에는 World Wide Web에 존재하는 데이터 원본에 대한 데이터 액세스를 지원하는 개방형 표준이 기술되어 있습니다. 이 항목에서는에서 지원 되는 XML for Analysis 1.1 사양 준수 수준을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="compliant-items"></a>호환 항목  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 XMLA 1.1 사양에 나열된 모든 필수 항목을 따릅니다. 또한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 XMLA 사양에 설명된 다음과 같은 선택적 항목을 구현합니다.  
  
|항목|사양|구현|  
|----------|-------------------|--------------------|  
|세션 지원|XMLA 1.1 사양의 "Support for Statefulness in XML for Analysis(XMLA의 상태 유지 지원)" 섹션에 나열된 SOAP 헤더 요소|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 나열된 모든 SOAP 헤더 요소가 사양에 설명된 대로 지원됩니다.|  
  
## <a name="extensions"></a>확장 프로그램  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 또한 XMLA 1.1 사양을 확장하여 다음과 같은 추가 기능을 지원합니다.  
  
|항목|사양|구현|  
|----------|-------------------|--------------------|  
|프로토콜 협상|XML for Analysis 1.1 사양에는 해당 정보가 없습니다.|[ProtocolCapabilities](xml-elements-headers/protocolcapabilities-element-xmla.md) 헤더 요소를 추가 하 여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로토콜 기능 협상을 지원 하도록 합니다.|  
|Discover 메서드에서 지원되는 XMLA(XML for Analysis) 명령|XMLA 1.1 사양에서는 다음과 같은 명령이 지원됩니다.<br /><br /> -   [Statement 요소 &#40;XMLA&#41;](xml-elements-commands/statement-element-xmla.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 다음과 같은 명령이 지원됩니다.<br /><br /> -   [Alter 요소 &#40;XMLA&#41;](xml-elements-commands/alter-element-xmla.md)<br />-   [요소를 백업 &#40;XMLA&#41;](xml-elements-commands/backup-element-xmla.md)<br />-   [요소를 일괄 처리 &#40;XMLA&#41;](xml-elements-commands/batch-element-xmla.md)<br />-   [BeginTransaction 요소 &#40;XMLA&#41;](xml-elements-commands/begintransaction-element-xmla.md)<br />-   [Cancel 요소 &#40;XMLA&#41;](xml-elements-commands/cancel-element-xmla.md)<br />-   [ClearCache 요소 &#40;XMLA&#41;](xml-elements-commands/clearcache-element-xmla.md)<br />-   [CommitTransaction 요소 &#40;XMLA&#41;](xml-elements-commands/committransaction-element-xmla.md)<br />-   [요소를 만들 &#40;XMLA&#41;](xml-elements-commands/create-element-xmla.md)<br />-   [Delete 요소 &#40;XMLA&#41;](xml-elements-commands/delete-element-xmla.md)<br />-   [DesignAggregations 요소 &#40;XMLA&#41;](xml-elements-commands/designaggregations-element-xmla.md)<br />-   [Drop 요소 &#40;XMLA&#41;](xml-elements-commands/drop-element-xmla.md)<br />-   [요소를 삽입 &#40;XMLA&#41;](xml-elements-commands/insert-element-xmla.md)<br />-   [요소를 잠급니다 &#40;XMLA&#41;](xml-elements-commands/lock-element-xmla.md)<br />-   [MergePartitions 요소 &#40;XMLA&#41;](xml-elements-commands/mergepartitions-element-xmla.md)<br />-   [NotifyTableChange 요소 &#40;XMLA&#41;](xml-elements-commands/notifytablechange-element-xmla.md)<br />-   [요소를 처리할 &#40;XMLA&#41;](xml-elements-commands/process-element-xmla.md)<br />-   [Restore 요소 &#40;XMLA&#41;](xml-elements-commands/restore-element-xmla.md)<br />-   [RollbackTransaction 요소 &#40;XMLA&#41;](xml-elements-commands/rollbacktransaction-element-xmla.md)<br />-SetPasswordEncryptionKey 요소<br />-   [Statement 요소 &#40;XMLA&#41;](xml-elements-commands/statement-element-xmla.md)<br />-   [Subscribe 요소 &#40;XMLA&#41;](xml-elements-commands/subscribe-element-xmla.md)<br />-   [Synchronize 요소 &#40;XMLA&#41;](xml-elements-commands/synchronize-element-xmla.md)<br />-   [요소 잠금 해제 &#40;XMLA&#41;](xml-elements-commands/unlock-element-xmla.md)<br />-   [Update 요소 &#40;XMLA&#41;](xml-elements-commands/update-element-xmla.md)<br />-   [UpdateCells 요소 &#40;XMLA&#41;](xml-elements-commands/updatecells-element-xmla.md)|  
|테이블 형식의 행 집합에 있는 열 오류|XMLA 1.1 사양에는 해당 항목이 없습니다.|합니다 [오류](xml-elements-properties/error-element-xmla.md) 요소를 사용 하 여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 포함 된 열 요소에 대 한 오류를 보고 하는 [행](xml-elements-properties/error-element-xmla.md) 요소입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [XML for Analysis &#40;XMLA&#41; 참조](xml-for-analysis-xmla-reference.md)  
  
  
