---
title: DISCOVER_CSDL_METADATA 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ca80c243a7ee9c001f079f21908f803a99b75e1f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34028638"
---
# <a name="discovercsdlmetadata-rowset"></a>DISCOVER_CSDL_METADATA 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 데이터 모델(테이블 형식 또는 다차원)에 대한 정보를 반환하여 CSDLBI 형식(BI 포함 개념 스키마 정의 언어 주석)으로 모델의 정의를 제공합니다. CSDLBI는 CSDL을 기반으로 하며, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 서버와 [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] 클라이언트 간의 통신을 위한 엔터티 데이터 프레임워크에서 사용되는 XML 스키마입니다. BI(비즈니스 인텔리전스) 주석은 테이블 형식 모델과 모델 안의 개체에 대한 메타데이터를 추가로 제공합니다. 테이블 형식 데이터 모델에 대한 자세한 내용은 [비즈니스 인텔리전스에 대한 CSDL 주석&#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)을 참조하세요.  
  
 명령의 보안 컨텍스트에 따라 반환되는 행 집합이 달라집니다. 서버에서 CSDL 정의를 가져오려면 Analysis Services 인스턴스에 대해 읽기 권한이 있어야 합니다.  
  
 행 집합을 요청하는 클라이언트의 언어 식별자는 명령에 대한 연결 문자열에 포함되며, 행 집합에 포함되어 반환되는 일부 속성에 표시되는 언어에 영향을 줍니다.  언어 식별자의 영향을 받는 속성 및 설명에 대한 정보는 설명 섹션을 참조하십시오.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_CSDL_METADATA** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|**열 이름**|**유형 표시기**|**제한**|**설명**|  
|---------------------|------------------------|---------------------|---------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|예|CSDLBI 설명이 요청된 데이터베이스의 이름을 지정합니다. 생략하는 경우 현재 데이터베이스가 사용됩니다.<br /><br /> 이 제한은 모든 모델 유형에 필수입니다.|  
|**PERSPECTIVE_ID**|**DBTYPE_WSTR**|예|CATALOG_NAME으로 지정한 모델에 정의되어 있는 큐브 뷰 ID를 지정합니다.<br /><br /> 선택적 제한입니다. 모든 모델 유형에 적용됩니다.|  
|**PERSPECTIVE_NAME**|**DBTYPE_WSTR**|예|CATALOG_NAME에 의해 지정된 모델에 정의되어 있는 큐브 뷰 이름을 지정합니다.<br /><br /> 이 제한은 테이블 형식 모델에 큐브 뷰가 포함되거나 다차원 솔루션에 큐브 또는 큐브 뷰가 여러 개 포함된 경우에 필요합니다.|  
|**METADATA**|**DBTYPE_WSTR**|아니요|CSDLBI 스키마에 따라 데이터 원본 및 그 속성의 XML 정의를 포함하는 문자열입니다.|  
|**CUBE_ID**|**DBTYPE_WSTR**|예|문자열 식별자입니다.<br /><br /> 이 제한은 다차원 데이터베이스에 대한 선택 사항입니다. 큐브를 여러 개 사용할 수 있고 제한을 생략한 경우 기본 큐브가 반환됩니다.|  
  
## <a name="remarks"></a>주의  
 DISCOVER_CSDL_METADATA에는 다음과 같은 요구 사항이 있습니다.  
  
-   CATALOG_NAME 제한을 사용하여 데이터베이스를 지정하지 않으면 DISCOVER 요청이 실패합니다.  
  
-   테이블 형식 모델의 경우, 모델에 큐브 뷰가 둘 이상 있으면 큐브 뷰 ID가 필요합니다.  
  
-   다차원 모델의 경우 카탈로그 이름과 큐브(큐브 뷰) 이름이 모두 필요합니다.  
  
-   큐브 뷰가 제한으로 제공되면 모델에 대해 동일한 CSDL 행 집합이 반환됩니다. 단, 모델에 있지만 지정된 큐브 뷰에는 포함되지 않은 개체는 **Hidden** = True로 표시됩니다.  
  
-   테이블과 열의 경우 DISCOVER 요청은 항상 큐브 차원의 값을 출력합니다. 큐브 차원 속성이 설정되어 있지 않으면 이 요청은 차원의 값을 반환합니다.  
  
-   DISCOVER 요청은 의미 체계 오류가 포함된 측정값 또는 계산된 열을 반환할 수 없습니다.  
  
-   DISCOVER 요청은 속성 값이 없는 개체에 대한 정보를 반환하지 않습니다. 또한 DISCOVER 요청은 기본값을 사용하는 특성의 값을 반환하지 않습니다.  
  
 행 집합에 반환되는 XML 문자열에는 다음과 같은 언어 관련 속성 또는 값이 포함될 수 있습니다. 예를 들어 LCID가 0403(카탈로니아어)인 클라이언트로부터 행 집합을 요청하는 경우 속성에는 카탈로니아어에 해당하는 다음 값이 반환됩니다. 서버에서 번역을 사용할 수 없는 경우 서버의 기본 언어 문자열이 반환됩니다.  
  
-   Caption  
  
-   한정자  
  
-   SortDirection  
  
-   IsRightToLeft  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 다음 XMLA 쿼리는 AdventureWorks 2012 테이블 형식 모델 예제의 CSDL 표현을 반환합니다. 각 테이블 형식 솔루션은 모델 하나만 포함할 수 있으므로 PERSPECTIVE_NAME 제한을 비워 둘 수 있습니다. 하지만 이 모델은 큐브 뷰를 여러 개 포함합니다.  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>AdventureWorks2012Tabular</CATALOG_NAME>  
                <PERSPECTIVE_NAME>EMPLOYEE</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
</Discover>  
  
```  
  
## <a name="example"></a>예제  
 **다차원**  
  
 다음 XMLA 쿼리는 Contoso Operations 큐브의 CSDLBI 표현을 반환합니다. 다차원 데이터베이스를 쿼리하려면 VERSION 제한이 필요합니다. Contoso Retail 데이터베이스에는 큐브가 두 개 포함되므로 PERSPECTIVE_NAME 제한을 사용하여 Operations 큐브를 참조합니다.  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>Contoso_Retail</CATALOG_NAME>  
                <PERSPECTIVE_NAME>Operation</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
 </Discover>  
  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|3444B255-171E-4cb9-AD98-19E57888A75F|  
|ADOMDNAME|Csdl|  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 스키마 행 집합](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [Business Intelligence & #40;에 대 한 CSDL 주석 CSDLBI & #41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
  
