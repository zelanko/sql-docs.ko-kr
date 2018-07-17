---
title: EnvelopeCenter(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- EnvelopeCenter
- EnvelopeCenter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeCenter method
ms.assetid: dee9d807-faad-45b8-b3f3-7e8aa7d07147
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8ad66188870d99c31f93404fcc8422339c6e94b0
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36246255"
---
# <a name="envelopecenter-geography-data-type-"></a>EnvelopeCenter(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geography** 인스턴스에 대한 경계 원의 중심으로 사용할 수 있는 지점을 반환합니다.  
  
 경계 원을 결정하기 위해 이 인스턴스의 각 지점은 지구 중심에서 지구 표면에 있는 해당 지점까지의 벡터로 표시됩니다. 경계 원의 중심점은 모든 벡터의 평균을 구하여 계산합니다. **polygon** 인스턴스 또는 **linestring** 인스턴스에 있는 폐쇄형 루프의 경우 첫 번째 지점과 마지막 지점이 한 번만 사용됩니다.  
  
 이 **geography** 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 **지점**을 반환합니다. `EnvelopeAngle()`과 함께 사용할 경우 `EnvelopeCenter()`는 **geography** 인스턴스의 경계 원을 반환합니다.  
  
> [!NOTE]  
>  `EnvelopeCenter()`는 **geography** 인스턴스의 경계 원을 반환하지만 이 경계 원이 가장 작은 경계 원이 아닐 수 있습니다. 반면에 **geometry** 인스턴스에 **geometry** 데이터 형식 메서드 `STEnvelope()`를 적용하면 가장 작은 경계 상자가 반환됩니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상에서는 이 인스턴스의 봉투를 나타내는 원의 중심을 **지점**으로 반환합니다. `EnvelopeAngle()` = 180으로 정의된 모든 큰 개체의 경우 `EnvelopeCenter()`는 (90,0)을 반환합니다.  
  
 이 메서드는 정확하지 않습니다.  
  
## <a name="examples"></a>예  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeAngle &#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
