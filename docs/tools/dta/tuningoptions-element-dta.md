---
title: TuningOptions 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f82d39a90f515d4f70d9e48bef7f20996ba60f78
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="tuningoptions-element-dta"></a>TuningOptions 요소(DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]특정 튜닝 세션에 대 한 튜닝 옵션을 포함 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 사용할 경우 각 **DTAInput** 요소에 한 번만 사용할 수 있습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[DTAInput 요소 &#40; DTA &#41;](../../tools/dta/dtainput-element-dta.md)|  
|**자식 요소**|**ReportSet** 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> **TuningLogTable** 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> **NumberOfEvents** 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> [TuningTimeInMin 요소 &#40; DTA &#41;](../../tools/dta/tuningtimeinmin-element-dta.md)<br /><br /> [StorageBoundInMB 요소 &#40; DTA &#41;](../../tools/dta/storageboundinmb-element-dta.md)<br /><br /> **MaxKeyColumnsInIndex** 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> **MaxColumnsInIndex** 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> **MinPercentageImprovement** 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> [TestServer 요소 &#40; DTA &#41;](../../tools/dta/testserver-element-dta.md)<br /><br /> [FeatureSet 요소 &#40; DTA &#41;](../../tools/dta/featureset-element-dta.md)<br /><br /> [분할 요소 &#40; DTA &#41;](../../tools/dta/partitioning-element-dta.md)<br /><br /> [DropOnlyMode 요소 &#40; DTA &#41;](../../tools/dta/droponlymode-element-dta.md)<br /><br /> [KeepExisting 요소 &#40; DTA &#41;](../../tools/dta/keepexisting-element-dta.md)<br /><br /> [OnlineIndexOperation 요소 &#40; DTA &#41;](../../tools/dta/onlineindexoperation-element-dta.md)<br /><br /> [DatabaseToConnect 요소 &#40; DTA &#41;](../../tools/dta/databasetoconnect-element-dta.md)<br /><br /> **IgnoreConstantsInWorkload** 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.<br /><br /> **RetainShellDB** 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.|  
  
## <a name="example"></a>예제  
 **TuningOptions** 요소의 예제는 [XML 입력 파일 샘플&#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
