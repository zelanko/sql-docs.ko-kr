---
title: "Discover 메서드 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 09/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Discover Method
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#
- http://schemas.microsoft.com/analysisservices/2003/engine#
- microsoft.xml.analysis.discover
- urn:schemas-microsoft-com:xml-analysis#Discover
- Discover
helpviewer_keywords:
- Discover method
ms.assetid: 0eb52d88-c081-416e-a229-610e4373b0b3
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 60a101afa2953d62e2910b4523a0213e4e786490
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="xml-elements---methods---discover"></a>XML 요소 방법-검색
  인스턴스에서 특정 개체에 대 한 정보 또는 사용 가능한 데이터베이스 목록과 같은 정보를 검색 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다. **Discover** 메서드로 검색되는 데이터는 해당 메서드로 전달되는 매개 변수의 값에 따라 달라집니다.  
  
 **네임스페이스** urn:schemas-microsoft-com:xml-analysis  
  
 **SOAP 동작** "urn:schemas-microsoft-com:xml-analysis:Discover"  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Discover>  
   <RequestType>...</RequestType>  
   <Restrictions>...</Restrictions>  
   <Properties>...</Properties>  
</Discover>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[속성](../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md), [RequestType](../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md), [제한 사항](../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 **Discover** 에 대 한 메타 데이터를 요청 하는 메서드 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 및 개체입니다. XMLA를 사용 하 여 메타 데이터가 반환 되는지 [행 집합](../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) 데이터 형식입니다.  
 
> [!TIP] 
> XML 명령에 익숙하지에서 XMLA 쿼리 템플릿 클릭는 **쿼리** Management studio에서 쿼리를 작성 하 고 매개 변수를 추가 하려면 도구 모음입니다. 자세한 내용은 [Use Analysis Services Templates in SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)을 참조하세요. 
  
## <a name="example"></a>예제  
 다음 코드 샘플에서는 클라이언트 보냅니다는 **Discover** 호출에서 큐브 목록을 요청 하는 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 샘플 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스:  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>MDSCHEMA_CUBES</RequestType>  
   <Restrictions>  
      <RestrictionList>  
         <CATALOG_NAME>Adventure Works DW Multidimensional 2012</CATALOG_NAME>  
      </RestrictionList>  
   </Restrictions>  
   <Properties>  
      <PropertyList>  
         <DataSourceInfo>Provider=MSOLAP;Data Source=local;</DataSourceInfo>  
         <Catalog>Adventure Works DW Multidimensional 2012</Catalog>  
         <Format>Tabular</Format>  
      </PropertyList>  
   </Properties>  
</Discover>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [XML 데이터 형식 &#40; XMLA &#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [방법 &#40; 실행 XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)   
 [방법 &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [XML 요소 &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Analysis Services 스키마 행 집합](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  

