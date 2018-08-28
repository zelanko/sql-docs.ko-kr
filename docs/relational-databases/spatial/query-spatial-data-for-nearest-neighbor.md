---
title: 가장 인접한 항목의 공간 데이터 쿼리 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: spatial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7af4ad5d-484e-45b4-aa16-83c33b358bb6
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 87a2742a2b856d8734e355aa3de2c126c14e025a
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43059978"
---
# <a name="query-spatial-data-for-nearest-neighbor"></a>가장 인접한 항목의 공간 데이터 쿼리
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  공간 데이터에 사용되는 일반적인 쿼리는 가장 인접한 항목 쿼리입니다. 가장 인접한 항목 쿼리는 특정 공간 개체에 가장 가까운 공간 개체를 찾는 데 사용됩니다. 예를 들어 웹 사이트에 대한 상점 로케이터는 고객 위치와 가장 가까운 상점 위치를 찾아야 하는 경우가 많습니다.  
  
 가장 인접한 항목 쿼리는 여러 가지의 유효한 쿼리 형식으로 작성할 수 있지만 가장 인접한 항목 쿼리에서 공간 인덱스를 사용하는 경우 다음 구문을 사용해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
SELECT TOP ( number )  
        [ WITH TIES ]  
        [ * | expression ]   
        [, ...]  
    FROM spatial_table_reference, ...   
        [ WITH   
            (   
                [ INDEX ( index_ref ) ]   
                [ , SPATIAL_WINDOW_MAX_CELLS = <value>]   
                [ ,... ]   
            )   
        ]  
    WHERE   
        column_ref.STDistance ( @spatial_ object )   
            {   
                [ IS NOT NULL ] | [ < const ] | [ > const ]   
                | [ <= const ] | [ >= const ] | [ <> const ] ]   
            }  
            [ AND { other_predicate } ]   
    }  
    ORDER BY column_ref.STDistance ( @spatial_ object ) [ ,...n ]  
[ ; ]  
  
```  
  
## <a name="nearest-neighbor-query-and-spatial-indexes"></a>가장 인접한 항목 쿼리 및 공간 인덱스  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 **TOP** 및 **ORDER BY** 절은 공간 데이터 열에서 가장 인접한 항목 쿼리를 수행하는 데 사용됩니다. **ORDER BY** 절은 공간 열 데이터 형식의 `STDistance()` 메서드에 대한 호출을 포함합니다. **TOP** 절은 쿼리에 대해 반환하는 개체 수를 나타냅니다.  
  
 가장 인접한 항목 쿼리에서 공간 인덱스를 사용하려면 다음 요구 사항을 충족해야 합니다.  
  
1.  공간 인덱스가 공간 열 중 하나에 있어야 하며 `STDistance()` 메서드가 해당 열을 **WHERE** 및 **ORDER BY** 절에 사용해야 합니다.  
  
2.  **TOP** 절은 **PERCENT** 문을 포함할 수 없습니다.  
  
3.  **WHERE** 절은 `STDistance()` 메서드를 포함해야 합니다.  
  
4.  **WHERE** 절에 조건자가 여러 개 있는 경우 `STDistance()` 메서드를 포함하는 조건자는 다른 조건자와 **AND** 결합으로 연결되어야 합니다. `STDistance()` 메서드는 **WHERE** 절의 선택적 부분에 있을 수 없습니다.  
  
5.  **ORDER BY** 절의 첫 번째 식은 `STDistance()` 메서드를 사용해야 합니다.  
  
6.  `STDistance()` ORDER BY **절의 첫 번째** 식에 대한 정렬 순서는 **ASC**여야 합니다.  
  
7.  `STDistance` 에서 **NULL** 을 반환하는 모든 행은 필터링되어야 합니다.  
  
> [!WARNING]  
>  **geography** 또는 **geometry** 데이터 형식을 인수로 사용하는 메서드는 이 두 데이터 형식의 SRID가 서로 동일하지 않는 경우 **NULL** 을 반환합니다.  
  
 가장 인접한 항목 쿼리에 사용되는 인덱스에는 새 공간 인덱스 공간 분할(tessellation)을 사용하는 것이 좋습니다. 공간 인덱스 공간 분할(tessellation)에 대한 자세한 내용은 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)여야 합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 공간 인덱스를 사용할 수 있는 가장 인접한 항목 쿼리를 보여 줍니다. 이 예에서는 `Person.Address` 데이터베이스의 `AdventureWorks2012` 테이블을 사용합니다.  
  
```sql  
USE AdventureWorks2012  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
WHERE SpatialLocation.STDistance(@g) IS NOT NULL  
ORDER BY SpatialLocation.STDistance(@g);  
  
```  
  
 가장 인접한 항목 쿼리에서 공간 인덱스를 사용하는 방법을 확인하기 위해 SpatialLocation 열에 대한 공간 인덱스를 만듭니다. 공간 인덱스를 만드는 방법은 [Create, Modify, and Drop Spatial Indexes](../../relational-databases/spatial/create-modify-and-drop-spatial-indexes.md)를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 공간 인덱스를 사용할 수 없는 가장 인접한 항목 쿼리를 보여 줍니다.  
  
```sql  
USE AdventureWorks2012  
GO  
DECLARE @g geography = 'POINT(-121.626 47.8315)';  
SELECT TOP(7) SpatialLocation.ToString(), City FROM Person.Address  
ORDER BY SpatialLocation.STDistance(@g);  
  
```  
  
 이 쿼리에는 구문 섹션에서 지정한 형식의 **를 사용하는** WHERE `STDistance()` 절이 부족하므로 쿼리에서 공간 인덱스를 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [공간 데이터&#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
