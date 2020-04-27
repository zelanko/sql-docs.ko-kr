---
title: Schema의 Table 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Table element [DTA]
ms.assetid: a59e8319-05d1-47f3-af39-7d970ab8e7dc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8b3a72f800643afa5e7edf6bdfa9928196f5da2d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63138785"
---
# <a name="table-element-for-schema-dta"></a>Schema의 Table 요소(DTA)
  튜닝에 사용할 테이블을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Schema>  
...code removed here...  
    <Table>...</Table>  
```  
  
## <a name="element-attributes"></a>요소 특성  
  
|attribute|Description|  
|---------------|-----------------|  
|`NumberOfRows`|선택 사항입니다. 여러 다른 크기의 테이블을 시뮬레이트할 수 있게 하는 정수입니다.|  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특성|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|1 ~ 007e; 255 자 사이의 **문자열**입니다.|  
|**기본값**|없음|  
|**내용과**|선택 사항입니다. 작업에 적합한 수만큼 테이블을 나열합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Database의 Schema 요소&#40;DTA&#41;](schema-element-for-database-dta.md)|  
|**자식 요소**|[Table의 Name 요소&#40;DTA&#41;](name-element-for-table-dta.md)|  
  
## <a name="remarks"></a>설명  
 `Table` 요소를 지정하지 않을 경우 데이터베이스 엔진 튜닝 관리자는 지정된 데이터베이스의 모든 테이블을 튜닝할 수 있다고 가정합니다.  
  
## <a name="example"></a>예제  
 사용 예를 보려면 [Server 요소&#40;DTA&#41;](server-element-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
