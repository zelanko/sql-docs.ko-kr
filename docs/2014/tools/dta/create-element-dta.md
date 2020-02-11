---
title: Create 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Create element (DTA)
ms.assetid: 9d076c90-f933-45f4-b6d9-447793f6528b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7ec9ad9569326e4a9b3e890af4b5f909e36e5c5b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63149485"
---
# <a name="create-element-dta"></a>Create 요소(DTA)
  인덱스, 통계 또는 힙 구조에 대한 정보를 사용자 지정 구성에 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Recommendation>  
    <Create>  
    ...code removed here...  
    </Create>  
</Recommendation>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특성|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|각 물리적 디자인 구조 유형(인덱스, 통계 또는 힙 구조)에 한 번만 지정해야 합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Recommendation 요소&#40;DTA&#41;](recommendation-element-dta.md)|  
|**자식 요소**|[Index 요소&#40;DTA&#41;](index-element-dta.md)<br /><br /> `Statistics`요소 (자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://schemas.microsoft.com/sqlserver/) 참조)<br /><br /> `Heap`요소 (자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://schemas.microsoft.com/sqlserver/) 참조)|  
  
## <a name="remarks"></a>설명  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **CreateTypecomplexType** 입니다. 이 요소는 사용자 지정 구성에 대한 인덱스, 통계 및 힙 구조를 만드는 데 사용됩니다. 이 `Create` 요소를 뷰(`CreateViewType`) 또는 분할(`CreatePType`)을 만드는 데 사용할 수 있는 다른 유형과 혼동하지 마십시오. 이러한 다른 `Create` 요소 형식에 대 한 자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://schemas.microsoft.com/sqlserver/) 를 참조 하세요.  
  
## <a name="example"></a>예제  
 이 요소의 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 샘플&#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
