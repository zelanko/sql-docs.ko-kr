---
title: "CollectionAggregate (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: CollectionAggregate method (geography)
ms.assetid: e49a644a-dbf2-46c3-98f5-4b3ec197e2ad
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2a2bec127117014b61cf9c40966ad1c28c4cee1c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="collectionaggregate-geography-data-type"></a>CollectionAggregate(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

만듭니다는 **GeometryCollection** 집합에서 인스턴스 **geography** 개체입니다.
  
## <a name="syntax"></a>구문  
  
```  
  
ConvexHullAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>인수  
 *geography_operand*  
 **geography** 형식 테이블 열 집합을 나타내는 **geography** 에 나열할 개체는 **GeometryCollection** 인스턴스.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
## <a name="exception"></a>Exception  
 유효하지 않은 입력 값이 있는 경우 `FormatException`을 발생시킵니다. 참조 [STIsValid &#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)  
  
## <a name="remarks"></a>주의  
 메서드 반환 **null** 경우 입력이 비어 있거나 입력에 다른 srid가 있습니다. 참조 [Spatial Reference Identifier &#40; Srid &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 메서드는 무시 **null** 입력 합니다.  
  
> [!NOTE]  
>  메서드 반환 **null** 경우는 모든 입력 값 **null**합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 반환는 `GeometryCollection` 집합이 들어 있는 인스턴스 **geography** 개체입니다.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT geography::CollectionAggregate(SpatialLocation).ToString() AS SpatialLocation  
 FROM Person.Address  
 WHERE City LIKE ('Bothell')
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
