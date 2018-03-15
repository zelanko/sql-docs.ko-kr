---
title: "EnvelopeAggregate(geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EnvelopeAggregate_TSQL
- EnvelopeAggregate
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAggregate method (geography)
ms.assetid: 4947797f-edb8-490f-beca-37df9ec06954
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 62e288175b4c8f6f33e3996046fa24ffccaa8b2c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="envelopeaggregate-geography-data-type"></a>EnvelopeAggregate(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

지정된 **geography** 개체 집합에 대한 경계 개체를 반환합니다. 결과 **geography** 개체는 여러 원호 세그먼트를 포함합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
EnvelopeAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>인수  
 *geography_operand*  
 봉투 집계 연산을 수행할 **geography** 개체 집합을 보관하는 **geography** 형식 테이블 열입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
## <a name="remarks"></a>Remarks  
 결과 경계 개체가 반구보다 크면 **FullGlobe** 개체가 반환됩니다. 이 메서드는 정확하지 않습니다.  
  
 메서드가 입력에 다른 SRID가 있을 경우 **null**을 반환합니다. [공간 참조 식별자 &#40;SRID&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)를 참조하세요.  
  
 메서드가 **null** 입력을 무시합니다.  
  
> [!NOTE]  
>  메서드는 모든 입력 값이 **null**인 경우 **null**을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 한 도시 안의 **geography** 위치 지점 집합에서 `EnvelopeAggregate`를 수행합니다.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::EnvelopeAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>참고 항목  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
