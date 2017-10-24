---
title: "UnionAggregate (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UnionAggregate
- UnionAggregate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UnionAggregate method (geography)
ms.assetid: 1a3aeef1-5b0e-4ae8-aeb7-c4aab22f42ab
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b98e5b8ff7f9c9c544b905e68eefa3669710112b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="unionaggregate-geography-data-type"></a>UnionAggregate(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

geography 개체 집합에서 통합 연산을 수행합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
UnionAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>인수  
 *geography_operand*  
 이 **geography** 의 집합을 보유 하는 형식 테이블 열 **geography** 통합 연산을 수행할 개체입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
## <a name="remarks"></a>주의  
 메서드 반환 **null** 입력에 다른 srid가 하는 경우. 참조 [Spatial Reference Identifier &#40; Srid &#41; ](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
 메서드는 무시 **null** 입력 합니다.  
  
> [!NOTE]  
>  메서드 반환 **null** 경우는 모든 입력 값 **null**합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 수행는 `UnionAggregate` 집합이 **geography** 도시 안의 위치 점입니다.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::UnionAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

