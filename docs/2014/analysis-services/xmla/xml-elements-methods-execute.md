---
title: Execute 메서드 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Execute Method
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EXECUTE
- urn:schemas-microsoft-com:xml-analysis#
- http://schemas.microsoft.com/analysisservices/2003/engine#
- microsoft.xml.analysis.execute
- urn:schemas-microsoft-com:xml-analysis#Execute
helpviewer_keywords:
- Execute method
ms.assetid: 0fff5221-7164-4bbc-ab58-49cf04c52664
caps.latest.revision: 34
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 5c32261e06788f366a6c5ce5af24c508b87a6882
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081629"
---
# <a name="execute-method-xmla"></a>Execute 메서드(XMLA)
  인스턴스를 Analysis (XMLA) 명령에 대 한 XML 보냅니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다. 여기에는 서버의 데이터 검색 또는 업데이트와 같은 데이터 전송 관련 요청이 포함됩니다.  
  
 **네임스페이스** urn:schemas-microsoft-com:xml-analysis  
  
 **SOAP 동작** "urn:schemas-microsoft-com:xml-analysis:Execute"  
  
## <a name="syntax"></a>구문  
  
```  
  
<Execute>  
   <Command>...</Command>  
   <Properties>...</Properties>  
   <Parameters>...</Parameters>  
</Execute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타나는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[명령](xml-elements-properties/command-element-xmla.md), [매개 변수](xml-elements-properties/parameters-element-xmla.md), [속성](xml-elements-properties/properties-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Execute` 메서드가에 제공 된 XMLA 명령을 실행의 `Command` 요소 XMLA 결과 중 하나를 사용 하 여 데이터를 반환 하 고 [행 집합](xml-data-types/rowset-data-type-xmla.md) (테이블 형식 결과 집합 지원)에 대 한 데이터 형식이 나 XMLA [MDDataSet](xml-data-types/mddataset-data-type-xmla.md) 데이터 형식 (다차원 결과 집합입니다.)  
  
## <a name="example"></a>예제  
 다음 코드 예제는 MDX(Multidimensional Expressions) SELECT 문을 포함하는 `Execute` 메서드 호출의 예입니다.  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Statement>  
         SELECT [Measures].MEMBERS ON COLUMNS FROM [Adventure Works]  
      </Statement>  
   </Command>  
   <Properties>  
      <PropertyList>  
         <DataSourceInfo>Provider=MSOLAP;Data Source=local;</DataSourceInfo>  
         <Catalog>Adventure Works DW Multidimensional 2012</Catalog>  
         <Format>Multidimensional</Format>  
         <AxisFormat>ClusterFormat</AxisFormat>  
      </PropertyList>  
   </Properties>  
</Execute>  
```  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터 형식 &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [Discover 메서드 &#40;XMLA&#41;](xml-elements-methods-discover.md)   
 [메서드 &#40;XMLA&#41;](xml-elements-methods.md)   
 [XML 요소 &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Analysis Services 스키마 행 집합](../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  