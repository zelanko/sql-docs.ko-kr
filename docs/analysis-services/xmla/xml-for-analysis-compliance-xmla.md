---
title: "XML for Analysis 호환성 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- compliance [XML for Analysis]
- XML for Analysis, compliance
- XMLA, extended functionality
- XML for Analysis, extended functionality
- XMLA, compliance
- extending XML for Analysis
ms.assetid: d987d320-5581-4454-ad45-68e3a22175b6
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f86d674ec86788741e098d8cfe37462cdffaec6b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="xml-for-analysis-compliance-xmla"></a>XMLA(XML for Analysis) 호환성
  XMLA 1.1 사양에는 World Wide Web에 존재하는 데이터 원본에 대한 데이터 액세스를 지원하는 개방형 표준이 기술되어 있습니다. 이 항목에서 지원 되는 XML for Analysis 1.1 사양 준수 수준을 자세히 설명 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="compliant-items"></a>호환 항목  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 XMLA 1.1 사양에 나열된 모든 필수 항목을 따릅니다. 또한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 XMLA 사양에 설명된 다음과 같은 선택적 항목을 구현합니다.  
  
|항목|사양|구현|  
|----------|-------------------|--------------------|  
|세션 지원|XMLA 1.1 사양의 "Support for Statefulness in XML for Analysis(XMLA의 상태 유지 지원)" 섹션에 나열된 SOAP 헤더 요소|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 나열된 모든 SOAP 헤더 요소가 사양에 설명된 대로 지원됩니다.|  
  
## <a name="extensions"></a>확장 프로그램  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 또한 XMLA 1.1 사양을 확장하여 다음과 같은 추가 기능을 지원합니다.  
  
|항목|사양|구현|  
|----------|-------------------|--------------------|  
|프로토콜 협상|XML for Analysis 1.1 사양에는 해당 정보가 없습니다.|ProtocolCapabilities 헤더 요소에서 추가한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로토콜 기능 협상을 지원 하도록 합니다.|  
|Discover 메서드에서 지원되는 XMLA(XML for Analysis) 명령|XMLA 1.1 사양에서는 다음과 같은 명령이 지원됩니다.<br /><br /> [Statement 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 다음과 같은 명령이 지원됩니다.<br /><br /> [Alter 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)<br /><br /> [요소 &#40; 백업 XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)<br /><br /> [일괄 처리 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)<br /><br /> [BeginTransaction 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)<br /><br /> [Cancel 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)<br /><br /> [ClearCache 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)<br /><br /> [CommitTransaction 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)<br /><br /> [요소 &#40; 만들기 XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)<br /><br /> [요소 &#40; 삭제 XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)<br /><br /> [DesignAggregations 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)<br /><br /> [Drop 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)<br /><br /> [요소 &#40; 삽입 XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)<br /><br /> [Lock 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)<br /><br /> [MergePartitions 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)<br /><br /> [NotifyTableChange 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)<br /><br /> [Process 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)<br /><br /> [요소 &#40; 복원 XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)<br /><br /> [RollbackTransaction 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)<br /><br /> [Statement 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)<br /><br /> [구독 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)<br /><br /> [요소 &#40; 동기화 XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)<br /><br /> [요소 &#40; 잠금 해제 XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)<br /><br /> [Update 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)<br /><br /> [UpdateCells 요소 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|테이블 형식의 행 집합에 있는 열 오류|XMLA 1.1 사양에는 해당 항목이 없습니다.|[오류](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) 요소를 사용 하 여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 포함 된 열 요소에 대 한 오류 보고는 [행](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) 요소입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [XMLA&#40;XML for Analysis&#41; 참조](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
