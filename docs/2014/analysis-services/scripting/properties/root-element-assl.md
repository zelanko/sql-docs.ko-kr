---
title: 루트 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Root Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Root
helpviewer_keywords:
- Root element
ms.assetid: ad3319d5-c3f0-49e3-b9c0-2fb77945c512
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 15b5ca79a25ec58bcdaf8bf6e76a2f4bb71ae710
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177573"
---
# <a name="root-element-assl"></a>Root 요소(ASSL)
  데이터 원본의 데이터(행 집합)를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<PushedDataSource>  
   ...  
   <Root>...</Root>  
   ...  
</PushedDataSource>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|행 집합|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[PushedDataSource](../data-type/datasource-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
