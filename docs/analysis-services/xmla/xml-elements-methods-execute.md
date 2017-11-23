---
title: "Execute 메서드 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Execute Method
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- EXECUTE
- urn:schemas-microsoft-com:xml-analysis#
- http://schemas.microsoft.com/analysisservices/2003/engine#
- microsoft.xml.analysis.execute
- urn:schemas-microsoft-com:xml-analysis#Execute
helpviewer_keywords: Execute method
ms.assetid: 0fff5221-7164-4bbc-ab58-49cf04c52664
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a2743ccdbe0f2186db5721479c812f61adfcfe92
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="xml-elements---methods---execute"></a>XML 요소 방법-실행
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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타나는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[명령](../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md), [매개 변수](../../analysis-services/xmla/xml-elements-properties/parameters-element-xmla.md), [속성](../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **Execute** 메서드가에 제공 된 XMLA 명령을 실행는 **명령** 요소 중 하나를 사용 하 여 모든 결과 데이터를 XMLA 반환 [행 집합](../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) 데이터 형식 (테이블 형식 결과 설정) 또는 XMLA [MDDataSet](../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) 데이터 형식 (다차원 결과 집합입니다.)  
  
## <a name="example"></a>예제  
 다음 코드 예제는 MDX(Multidimensional Expressions) SELECT 문을 포함하는 **Execute** 메서드 호출의 예입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [XML 데이터 형식 &#40; XMLA &#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [방법 &#40; 검색 XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [방법 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [XML 요소 &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Analysis Services 스키마 행 집합](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
