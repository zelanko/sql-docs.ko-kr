---
title: CollectionAggregate(geography Data Type) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CollectionAggregate method (geography)
ms.assetid: e49a644a-dbf2-46c3-98f5-4b3ec197e2ad
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3f081e7c3bb990ae28bcd035008719b90e7b7ae6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600091"
---
# <a name="collectionaggregate-geography-data-type"></a>CollectionAggregate(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

**geography** 객체 집합에서 **GeometryCollection** 인스턴스를 만듭니다.
  
## <a name="syntax"></a>구문  
  
```  
  
ConvexHullAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>인수  
 *geography_operand*  
 **GeometryCollection** 인스턴스에 나열될 **geography** 객체 집합을 나타내는 **geography** 형식 테이블 열입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
## <a name="exception"></a>예외  
 유효하지 않은 입력 값이 있는 경우 `FormatException`을 발생시킵니다. [STIsValid&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md) 참조  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 입력이 비어 있거나 입력에 다른 SRID가 있는 경우 **null**을 반환합니다. [Spatial Reference Identifier&#40;SRIDs&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md) 참조  
  
 이 메서드는 **null** 입력을 무시합니다.  
  
> [!NOTE]  
>  이 메서드는 모든 입력 값이 **null**인 경우 **null**을 반환합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 **geography** 개체 집합을 포함하는 `GeometryCollection` 인스턴스를 반환합니다.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT geography::CollectionAggregate(SpatialLocation).ToString() AS SpatialLocation  
 FROM Person.Address  
 WHERE City LIKE ('Bothell')
 ```  
  
## <a name="see-also"></a>참고 항목  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
