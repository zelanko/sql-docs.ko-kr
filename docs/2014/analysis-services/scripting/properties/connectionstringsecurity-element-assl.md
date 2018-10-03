---
title: ConnectionStringSecurity 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ConnectionStringSecurity Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ConnectionStringSecurity
helpviewer_keywords:
- ConnectionStringSecurity element
ms.assetid: f25c4448-bb0d-4945-bc84-9c015eefa0eb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6237271e3952c05c9c7b231332454aaf2aa0c3ed
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219433"
---
# <a name="connectionstringsecurity-element-assl"></a>ConnectionStringSecurity 요소(ASSL)
  보안을 위해 데이터 원본 연결 문자열에서 사용자 암호를 제거할지 여부를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataSource>  
   ...  
   <ConnectionStringSecurity>...</ConnectionStringSecurity>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DataSource](../objects/datasource-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 있는 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*PasswordRemoved*|암호가 연결 문자열에서 제거되었습니다.|  
|*Unchanged*|연결 문자열이 수정되지 않았습니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `ConnectionStringSecurity`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.ConnectionStringSecurity>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
