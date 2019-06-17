---
title: TuningOptions 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3050ce285cc98386f6de6278bedd2520cb39ba36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061067"
---
# <a name="tuningoptions-element-dta"></a>TuningOptions 요소(DTA)
  특정 튜닝 세션에 대한 튜닝 옵션을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 사용할 경우 각 `DTAInput` 요소에 한 번만 사용할 수 있습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[DTAInput 요소&#40;DTA&#41;](dtainput-element-dta.md)|  
|**자식 요소**|`ReportSet` 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> `TuningLogTable` 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> `NumberOfEvents` 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> [TuningTimeInMin 요소&#40;DTA&#41;](tuningtimeinmin-element-dta.md)<br /><br /> [StorageBoundInMB 요소&#40;DTA&#41;](storageboundinmb-element-dta.md)<br /><br /> `MaxKeyColumnsInIndex` 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> `MaxColumnsInIndex` 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> `MinPercentageImprovement` 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> [TestServer 요소&#40;DTA&#41;](server-element-dta.md)<br /><br /> [FeatureSet 요소&#40;DTA&#41;](featureset-element-dta.md)<br /><br /> [Partitioning 요소&#40;DTA&#41;](partitioning-element-dta.md)<br /><br /> [DropOnlyMode 요소&#40;DTA&#41;](droponlymode-element-dta.md)<br /><br /> [KeepExisting 요소&#40;DTA&#41;](keepexisting-element-dta.md)<br /><br /> [OnlineIndexOperation 요소&#40;DTA&#41;](onlineindexoperation-element-dta.md)<br /><br /> [DatabaseToConnect 요소&#40;DTA&#41;](databasetoconnect-element-dta.md)<br /><br /> `IgnoreConstantsInWorkload` 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> `RetainShellDB` 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.|  
  
## <a name="example"></a>예제  
 에 대 한 예제는 `TuningOptions` 요소를 참조 합니다 [XML 입력 파일 샘플 &#40;DTA&#41;](xml-input-file-samples-dta.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
