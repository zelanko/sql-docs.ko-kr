---
title: EnvelopeAngle(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeAngle
- EnvelopeAngle_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAngle method
ms.assetid: 14a7ba15-168c-4b08-ba3d-951d73092ac7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e3289956dd79c852eef6534ad1f72623ad4dcaa6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68066460"
---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  `EnvelopeCenter()`에서 반환하는 지점과 **geography** 인스턴스에 있는 지점 사이의 최대 각도를 도 단위로 반환합니다.  
  
 이 **geography** 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
EnvelopeAngle( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **float**  
  
 CLR 반환 형식: **SqlDouble**  
  
## <a name="remarks"></a>설명  
 이 메서드는 **geography** 인스턴스에 있는 지점을 도 단위로 반환합니다. EnvelopeCenter()와 함께 사용할 경우 `EnvelopeAngle()`은 **geography** 인스턴스의 경계 원을 반환합니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 이 메서드는 **FullGlobe** 인스턴스로 확장되었습니다.  
  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]의 `EnvelopeAngle()`에 적용된 반구 제한이 제거되었습니다. 그러나 각도가 90도보다 큰 인스턴스의 경우 180도가 반환됩니다. **geography** 인스턴스가 둘 이상의 반구에 걸쳐 있을 경우 `EnvelopeAngle()`이 정확하지 않습니다.  
  
## <a name="examples"></a>예  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';   
SELECT @g.EnvelopeAngle();  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeCenter &#40;geography 데이터 형식 &#41;](../../t-sql/spatial-geography/envelopecenter-geography-data-type.md)  
  
  
