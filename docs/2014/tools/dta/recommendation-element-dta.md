---
title: 권장 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Recommendation element
ms.assetid: 679ea535-865a-4633-a4d3-5b3090515158
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bcc0a95028b1f107f15752692d3dcad090fbe8b1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62659586"
---
# <a name="recommendation-element-dta"></a>Recommendation 요소(DTA)
  사용자 지정 구성의 일부인 가상 인덱스에 대한 정보를 포함합니다.  
  
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
  
|특성|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 각 `Table` 요소에 한 번만 사용할 수 있습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Schema의 Table 요소&#40;DTA&#41;](table-element-for-schema-dta.md)|  
|**자식 요소**|[Create 요소&#40;DTA&#41;](create-element-dta.md)<br /><br /> `Drop`요소인. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.|  
  
## <a name="remarks"></a>설명  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **RecommendationTypecomplexType** 입니다. 이 요소는 가상 구성에 대한 인덱스를 지정하는 데 사용됩니다. 이 `Recommendation` 요소를 분할(`RecommendationPType`) 또는 뷰(`RecommendationViewType`)를 지정하는 데 사용할 수 있는 다른 유형과 혼동하지 마십시오. 이러한 다른 `Recommendation` 요소 형식에 대 한 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://go.microsoft.com/fwlink/?linkid=43100)를 참조 하세요.  
  
## <a name="example"></a>예제  
 이 요소의 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 샘플&#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
