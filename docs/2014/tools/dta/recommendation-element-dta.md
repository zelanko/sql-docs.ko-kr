---
title: Recommendation 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 58535397a152ff1198cbb4cf713a6d0ec04a7eed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088317"
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
  
|특징|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 각각에 대해 한 번만 사용할 수 `Table` 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[스키마에 대 한 요소를 표에서 &#40;DTA&#41;](table-element-for-schema-dta.md)|  
|**자식 요소**|[Create 요소 &#40;DTA&#41;](create-element-dta.md)<br /><br /> `Drop` 요소입니다. 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?linkid=43100)를 참조하십시오.|  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **RecommendationTypecomplexType** 입니다. 이 요소는 가상 구성에 대한 인덱스를 지정하는 데 사용됩니다. 이 혼동 하지 마십시오 `Recommendation` 분할을 지정 하는 데 사용할 수 있는 다른 유형과 요소 (`RecommendationPType`) 또는 뷰 (`RecommendationViewType`). 이러한 기타 방법에 대 한 정보에 대 한 `Recommendation` 요소 형식 참조는 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://go.microsoft.com/fwlink/?linkid=43100)합니다.  
  
## <a name="example"></a>예제  
 이 요소의 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 샘플&#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  