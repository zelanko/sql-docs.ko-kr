---
title: "ColumnID 요소 (ColumnBinding) (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ColumnID Element (ColumnBinding)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ColumnID
helpviewer_keywords: ColumnID element
ms.assetid: f4edf532-7e40-4ee2-9b5e-48b3c3de7a74
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d13ccee573076a8b56071601d86c693240621d1c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="columnid-element-columnbinding-assl"></a>ColumnID 요소(ColumnBinding)(ASSL)
  데이터 항목이 바인딩되는 테이블 내 열 ID를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ColumnBinding>  
   ...  
   <ColumnID>...</ColumnID>  
   ...  
</ColumnBinding>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|문자열|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타날 수 있는 필수 요소.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **ColumnID** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.ColumnBinding>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
