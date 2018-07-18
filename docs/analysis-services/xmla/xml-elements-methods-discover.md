---
title: Discover 메서드 (XMLA) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 921afc6d17a0eddcba48e5a6a6064810a3b3b6ef
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979106"
---
# <a name="xml-elements---methods---discover"></a>XML 요소-메서드-검색
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Analysis Services 인스턴스에서 특정 개체에 대 한 세부 정보나 사용 가능한 데이터베이스 목록과 같은 정보를 검색합니다. **Discover** 메서드로 검색되는 데이터는 해당 메서드로 전달되는 매개 변수의 값에 따라 달라집니다.  
  
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
  
## <a name="element-characteristics"></a>요소 특성  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[속성](../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)하십시오 [RequestType](../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md), [제한 사항](../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 합니다 **Discover** 메서드 인스턴스 및 개체에 대 한 메타 데이터를 요청 합니다. XMLA를 사용 하 여 메타 데이터가 반환 되는지 [행 집합](../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) 데이터 형식입니다.  
 
> [!TIP] 
> XML 명령을 사용 하 여 잘 모르는 경우에서 XMLA 쿼리 템플릿을 클릭 합니다 **쿼리** Management studio에서 쿼리를 작성 하 고 매개 변수를 추가 하려면 도구 모음입니다. 자세한 내용은 [Use Analysis Services Templates in SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)을 참조하세요. 
  
## <a name="example"></a>예제  
 클라이언트가 보내는 다음 코드 샘플에서는 합니다 **Discover** 호출에서 큐브 목록을 요청 하는 [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] 예제 Analysis Services 데이터베이스:  
  
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
  
## <a name="see-also"></a>참고자료
 [XML 데이터 형식 &#40;XMLA&#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [메서드를 실행 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)   
 [메서드 &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [XML 요소 &#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Analysis Services 스키마 행 집합](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
