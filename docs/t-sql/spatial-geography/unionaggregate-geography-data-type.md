---
description: UnionAggregate(geography 데이터 형식)
title: UnionAggregate(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UnionAggregate
- UnionAggregate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UnionAggregate method (geography)
ms.assetid: 1a3aeef1-5b0e-4ae8-aeb7-c4aab22f42ab
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 6a31d700c51a4d6bc5836de7d904fdbc3e4644c4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488250"
---
# <a name="unionaggregate-geography-data-type"></a>UnionAggregate(geography 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

geography 개체 집합에서 통합 연산을 수행합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
UnionAggregate ( geography_operand )  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *geography_operand*  
 통합 연산을 수행할 **geography** 개체 집합을 보관하는 **geography** 형식 테이블 열입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
## <a name="remarks"></a>설명  
 메서드가 입력에 다른 SRID가 있을 경우 **null**을 반환합니다. [공간 참조 식별자 &#40;SRID&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)를 참조하세요.  
  
 이 메서드는 **null** 입력을 무시합니다.  
  
> [!NOTE]  
>  이 메서드는 모든 입력 값이 **null**인 경우 **null**을 반환합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 한 도시 안의 **geography** 위치 지점 집합에서 `UnionAggregate`를 수행합니다.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::UnionAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>참고 항목  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
