---
title: "EnvelopeAggregate (geography 데이터 형식) | Microsoft Docs"
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
f1_keywords:
- EnvelopeAggregate_TSQL
- EnvelopeAggregate
dev_langs: TSQL
helpviewer_keywords: EnvelopeAggregate method (geography)
ms.assetid: 4947797f-edb8-490f-beca-37df9ec06954
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4653e69162ff3485450d5397a80428ca600a008d
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="envelopeaggregate-geography-data-type"></a>EnvelopeAggregate(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

제공된 된 집합에 대 한 경계 개체를 반환 **geography** 개체입니다. 그 결과 **geography** 여러 원호 세그먼트를 포함 하는 개체입니다.
  
## <a name="syntax"></a>구문  
  
```  
  
EnvelopeAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>인수  
 *geography_operand*  
 이 **geography** 의 집합을 보유 하는 형식 테이블 열 **geography** 개체 봉투 (envelope)를 수행할 집계 연산을 합니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
## <a name="remarks"></a>주의  
 A **FullGlobe** 결과 경계 개체가 반구 보다 큽니다. 개체가 반환 됩니다. 이 메서드는 정확하지 않습니다.  
  
 메서드 반환 **null** 입력에 다른 srid가 하는 경우. 참조 [Spatial Reference Identifier &#40; Srid &#41; ](../../relational-databases/spatial/spatial-reference-identifiers-srids.md).  
  
 메서드는 무시 **null** 입력 합니다.  
  
> [!NOTE]  
>  메서드 반환 **null** 경우는 모든 입력 값 **null**합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 수행는 `EnvelopeAggregate` 집합이 **geography** 도시 안의 위치 점입니다.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::EnvelopeAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>관련 항목:  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
