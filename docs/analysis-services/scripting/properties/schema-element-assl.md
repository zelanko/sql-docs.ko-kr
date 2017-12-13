---
title: "Schema 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Schema Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Schema
helpviewer_keywords: Schema element
ms.assetid: 4b6375fb-7ad8-4d5f-88b1-abd3da2654db
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c96773b2d1f1f42b195d41b98ac1646c997257c1
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="schema-element-assl"></a>Schema 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]데이터 원본 뷰의 스키마를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataSourceView>  
   ...  
   <Schema>...</Schema>  
   ...  
</DataSourceView>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|스키마|  
|기본값|없음|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **스키마** 에서 데이터 집합의 XML XSD (스키마 정의) 언어 형식을 사용 하 여 표시 되는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework에서 데이터 집합 및 데이터 정의 내에서 이러한 용도에 다른 사용자에 대 한 일부 확장명 언어 (DDL)입니다. 데이터 집합은 XSD에서 관계형 스키마로의 유연한 매핑을 정의하지만 XSD를 정규 형식으로 반환합니다. 이 정규 형식은 데이터 원본에서만 유효합니다.  
  
 부모에 해당 하는 요소 **스키마** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DataSourceView>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
