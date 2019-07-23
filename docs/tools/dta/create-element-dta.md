---
title: Create 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Create element (DTA)
ms.assetid: 9d076c90-f933-45f4-b6d9-447793f6528b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3541a007b51d5813a6bc42a977ec31fedf5bab87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104990"
---
# <a name="create-element-dta"></a>Create 요소(DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|각 물리적 디자인 구조 유형(인덱스, 통계 또는 힙 구조)에 한 번만 지정해야 합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Recommendation 요소&#40;DTA&#41;](../../tools/dta/recommendation-element-dta.md)|  
|**자식 요소**|[Index 요소&#40;DTA&#41;](../../tools/dta/index-element-dta.md)<br /><br /> **Statistics** 요소(자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://schemas.microsoft.com/sqlserver/) 참조)<br /><br /> **Heap** 요소(자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](https://schemas.microsoft.com/sqlserver/) 참조)|  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **CreateTypecomplexType** 입니다. 이 요소는 사용자 지정 구성에 대한 인덱스, 통계 및 힙 구조를 만드는 데 사용됩니다. 이 **Create** 요소를 뷰(**CreateViewType**) 또는 분할(**CreatePType**)을 만드는 데 사용할 수 있는 다른 유형과 혼동하지 마세요. 이러한 기타 [Create](https://schemas.microsoft.com/sqlserver/) 요소 유형에 대한 내용은 **데이터베이스 엔진 튜닝 관리자 XML 스키마** 를 참조하세요.  
  
## <a name="example"></a>예제  
 이 요소의 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 샘플&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
