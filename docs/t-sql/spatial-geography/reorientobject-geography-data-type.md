---
title: "ReorientObject (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- ReorientObject
- ReorientObject_TSQL
dev_langs: TSQL
helpviewer_keywords: ReorientObject method (geography)
ms.assetid: e2a1a4f1-211b-4e82-abed-03fc7140a83c
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 181781aa4cd76ee41a6c4b5e7a3ca8255d6f9a4e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="reorientobject-geography-data-type"></a>ReorientObject(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  반환 된 **geography** 내부 영역과 외부 영역이 서로 바뀐를 사용 하 여 인스턴스.  
  
 이 **geography** 데이터 형식 메서드 지원 **FullGlobe** 인스턴스 또는 반구 보다 큰 공간 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
.ReorientObject (geography)  
```  
  
## <a name="arguments"></a>인수  
 *geography*  
 다른 **geography** 인스턴스 `ReorientObject()` 가 호출 됩니다.  
  
## <a name="return-value"></a>반환 값  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>주의  
 이 메서드는 모두의 링 방향은 변경 **다각형** 에 **GeometryCollection** 제거 하거나 변경 하지 않는 있지만 **포인트** 또는 **Linestrings** 지정한 컬렉션에 있습니다.  
  
 경우는 **GeometryCollection** 전달이 메서드에 컬렉션의 각 인스턴스는 방향이 다시 지정 되지만 컬렉션 전체의 방향은 변경 되지 않습니다.  
  
## <a name="examples"></a>예  
  
```  
DECLARE @R GEOGRAPHY = GEOGRAPHY::Parse('Polygon((-10 -10, -10 10, 10 10, 10 -10, -10 -10))');  
SELECT @R.ReorientObject().STAsText();  
--Result: POLYGON ((10 10, -10 10, -10 -10, 10 -10, 10 10))  
```  
  
## <a name="see-also"></a>관련 항목:  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
