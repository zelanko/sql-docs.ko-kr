---
title: Recommendation 요소 (DTA) | Microsoft Docs
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
- Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: affac3964b25761341c5ac39e3987a107636fae1
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="recommendation-element-dta"></a>Recommendation 요소(DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]사용자 지정 구성의 일부인 가상 인덱스에 대 한 정보를 포함 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Configuration>  
    ...code removed here...  
    <Table>  
      <Name>...</Name>  
      <Recommendation>  
      ...code removed here...  
      </Recommendation>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 각 **Table** 요소에 한 번만 사용할 수 있습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Table 요소 스키마 &#40; DTA &#41;](../../tools/dta/table-element-for-schema-dta.md)|  
|**자식 요소**|[Create 요소&#40;DTA&#41;](../../tools/dta/create-element-dta.md)<br /><br /> **Drop** 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.|  
  
## <a name="remarks"></a>주의  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **RecommendationTypecomplexType** 입니다. 이 요소는 가상 구성에 대한 인덱스를 지정하는 데 사용됩니다. 이 **Recommendation** 요소와 분할을 지정하는 데 사용할 수 있는 다른 형식(**RecommendationPType**) 또는 뷰(**RecommendationViewType**)를 혼동하지 마세요. 이러한 다른 **Recommendation** 요소 유형에 대한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?linkid=43100)를 참조하세요.  
  
## <a name="example"></a>예제  
 이 요소의 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 샘플&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
