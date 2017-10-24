---
title: "EnvelopeAngle (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EnvelopeAngle
- EnvelopeAngle_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAngle method
ms.assetid: 14a7ba15-168c-4b08-ba3d-951d73092ac7
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cd410a6eb07c626c7674febad2a427bbd029f98a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  반환 되는 지점 사이의 최대 각도 반환 `EnvelopeCenter()` 의 점과 **geography** 도 인스턴스.  
  
 이 **geography** 데이터 형식 메서드 지원 **FullGlobe** 인스턴스 또는 반구 보다 큰 공간 인스턴스.  
  
## <a name="syntax"></a>구문  
  
```  
  
EnvelopeAngle( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]반환 형식: **float**  
  
 CLR 반환 형식: **SqlDouble**  
  
## <a name="remarks"></a>주의  
 요소를 반환 하는이 메서드는 **geography** 도 인스턴스. EnvelopeCenter()와 함께 사용할 경우 `EnvelopeAngle()` 의 경계 원을 반환는 **geography** 인스턴스.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)],이 메서드가 확장 되었습니다 **FullGlobe** 인스턴스.  
  
 에 적용 된 반구 제한이 `EnvelopeAngle()` 에 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 제거 되었습니다. 그러나 각도가 90도보다 큰 인스턴스의 경우 180도가 반환됩니다. `EnvelopeAngle()`이 정확 **geography** 인스턴스가 둘 이상의 반구에 걸쳐 있을 합니다.  
  
## <a name="examples"></a>예  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';   
SELECT @g.EnvelopeAngle();  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeCenter &#40; geography 데이터 형식 &#41;](../../t-sql/spatial-geography/envelopecenter-geography-data-type.md)  
  
  

