---
title: "Rowset 데이터 형식 (XMLA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Rowset Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Rowset
- http://schemas.microsoft.com/analysisservices/2003/engine#Rowset
- Rowset
helpviewer_keywords:
- Rowset data type
ms.assetid: a3e6e227-2d53-4530-b369-afa8b4df0a40
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 352dc0e626e3214b37f5047957f8fa1f68aace55
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="rowset-data-type-xmla"></a>Rowset 데이터 형식(XMLA)
  나타내는 파생된 데이터 형식을 정의 [루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) 에서 테이블 형식 데이터를 반환 하는 요소는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) 또는 [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) 메서드를 호출 합니다.  
  
 **Namespace** :-microsoft-com:xml-분석: 행 집합  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <!-- The following elements extend Resultset -->  
   <!-- Optional schema elements -->  
   <row>...</row>  
</root>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|[결과 집합](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[행](../../../analysis-services/xmla/xml-elements-properties/row-element-xmla.md)|  
|파생 요소|[루트](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
  
## <a name="remarks"></a>주의  
 XML은 요소 및 특성 이름에 특정 문자를 허용하지 않습니다. 이 명명 제약 조건을 해결 하기 위해 XML for Analysis (XMLA)에서 정의한 인코딩을 지원 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. XML 1.0 사양에 따라 유효 하지 않은 XML 이름 문자가 포함 된 열 이름에 대 한 XMLA 유효 하지 않은 유니코드 문자를 인코딩하는 데 해당 16 진수 값을 사용 합니다. 16 진수 값은 _x로 이스케이프 됩니다*HHHH*\_여기서 *HHHH* 는 최상위 비트 우선 순서에 있는 문자에 대 한 4 자리 16 진수 ucs-2 코드를 나타냅니다. 예를 들어 XMLA은 "Order Details" 이름에서 공백을 해당 16진수 코드로 바꾸어 Order_x0020_Details로 인코딩합니다.  
  
 인코딩을 하면 XSL(Extensible Stylesheet Language) 변환이 어려워질 수 있습니다. 인코딩되지 않은 열 이름, 실제 빠른 조회를 지원 하기 위해, 추가 된 **sql: field**다음 예제와 같이 각 열에 대 한 XML 행 집합 스키마로 특성:  
  
```  
<xsd:element name="Order_x0020_Details" type="string" sql:field="Order Details" />  
```  
  
> [!NOTE]  
>  **sql: field** 특성이 `"urn:schemas-microsoft-com:xml-sql"` 네임 스페이스입니다.  
  
## <a name="expressing-a-null-value"></a>Null 값 표현  
 행에서 열에 Null 값을 표현하는 방법은 두 가지가 있습니다.  
  
-   누락된 열 요소는 열이 Null임을 의미합니다.  
  
-   열 요소는 `xsi:nil='true'` 특성을 사용하여 해당 열에 Null 값이 있음을 나타낼 수 있습니다.  
  
 예를 들어 행에 Store_Name이라는 단일 열이 있고 해당 열 값이 NULL인 경우 누락 된 열 요소로 나타낼 수 Store_Name 열 값:를 사용 하 여 Store_Name 열 값을 나타낼 수 있습니다 또는 `xsi:nil='true'` 특성:  
  
```  
<row>  
   <Store_name xsi:nil='true'/>  
</row>  
```  
  
## <a name="example"></a>예제  
  
## <a name="xmla-rowset-for-flat-data"></a>플랫 데이터의 XMLA 행 집합  
 플랫 데이터의 경우 쿼리별 열 이름은 스키마에서 요소 이름으로 정의됩니다. 또한 `<row>` 태그 쌍이 각 행을 묶습니다.  
  
 다음 예에서는 플랫 데이터의 XMLA 행 집합 형식을 보여 줍니다.  
  
```  
<return>  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   </xsd:element>  
      <xsd:complexType name="row">  
         <xsd:choice maxOccurs="unbounded" minOccurs="0">  
            <xsd:element name="CATALOG_NAME" type="xsd:string" sql:field="CATALOG_NAME"></xsd:element>  
            <xsd:element name="DESCRIPTION" type="xsd:string" sql:field="DESCRIPTION"></xsd:element>  
            <xsd:element name="ROLES" type="xsd:string" sql:field="ROLES"></xsd:element>  
            <xsd:element name="DATE_MODIFIED" type="xsd:time" sql:field="DATE_MODIFIED"></xsd:element>  
         </xsd:choice>  
      </xsd:complexType>  
   </xsd:schema>  
   <row>  
      <CATALOG_NAME>FoodMart 2000</CATALOG_NAME>  
      <DESCRIPTION></DESCRIPTION>  
      <ROLES>All Users</ROLES>  
      <DATE_MODIFIED>3/11/2001 6:49:36 PM</DATE_MODIFIED>  
   </row>  
   ...  
</root>  
```  
  
## <a name="xmla-rowset-for-hierarchical-data"></a>계층적 데이터의 XMLA 행 집합  
 일부 행 집합은 계층적 데이터 또는 중첩된 행 집합을 포함합니다. 데이터 마이닝 쿼리에서 반환된 행 집합은 계층적입니다. 계층적 데이터의 경우 행 구조는 변경되지 않지만 데이터별 스키마는 중첩된 데이터를 포함하는 요소 하위 유형을 정의합니다.  
  
 다음 예에서는 계층적 데이터의 XMLA 행 집합 형식을 보여 줍니다. 이 예에서 중첩된 데이터를 포함하는 요소 하위 유형은 `<NODE_DISTRIBUTION>`입니다.  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
   xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <xsd:complexType name="row">  
         <xsd:choice maxOccurs="unbounded" minOccurs="0">  
            <xsd:sequence maxOccurs="unbounded" minOccurs="0">  
               <xsd:element name="NODE_DISTRIBUTION" sql:field="NODE_DISTRIBUTION">  
                  <xsd:complexType>  
                     <xsd:choice maxOccurs="unbounded" minOccurs="0">  
                        <xsd:element name="ATTRIBUTE_NAME" type="xsd:string" sql:field="ATTRIBUTE_NAME"></xsd:element>  
                        <xsd:element name="ATTRIBUTE_VALUE" type="xsd:string" sql:field="ATTRIBUTE_VALUE"></xsd:element>  
                        <xsd:element name="SUPPORT" type="xsd:double" sql:field="SUPPORT"></xsd:element>  
                        <xsd:element name="PROBABILITY" type="xsd:double" sql:field="PROBABILITY"></xsd:element>  
                        <xsd:element name="VARIANCE" type="xsd:double" sql:field="VARIANCE"></xsd:element>  
                        <xsd:element name="VALUETYPE" type="xsd:int" sql:field="VALUETYPE"></xsd:element>  
                     </xsd:choice>  
                  </xsd:complexType>  
               </xsd:element>  
            </xsd:sequence>  
            <xsd:element name="MODEL_CATALOG" type="xsd:string" sql:field="MODEL_CATALOG"></xsd:element>  
            <xsd:element name="MODEL_SCHEMA" type="xsd:string" sql:field="MODEL_SCHEMA"></xsd:element>  
            <xsd:element name="MODEL_NAME" type="xsd:string" sql:field="MODEL_NAME"></xsd:element>  
            <xsd:element name="ATTRIBUTE_NAME" type="xsd:string" sql:field="ATTRIBUTE_NAME"></xsd:element>  
            <xsd:element name="NODE_NAME" type="xsd:string" sql:field="NODE_NAME"></xsd:element>  
            <xsd:element name="NODE_UNIQUE_NAME" type="xsd:string" sql:field="NODE_UNIQUE_NAME"></xsd:element>  
            <xsd:element name="NODE_TYPE" type="xsd:unsignedInt" sql:field="NODE_TYPE"></xsd:element>  
            <xsd:element name="NODE_GUID" type="xsd:string" sql:field="NODE_GUID"></xsd:element>  
            <xsd:element name="NODE_CAPTION" type="xsd:string" sql:field="NODE_CAPTION"></xsd:element>  
            <xsd:element name="CHILDREN_CARDINALITY" type="xsd:unsignedInt" sql:field="CHILDREN_CARDINALITY"></xsd:element>  
            <xsd:element name="PARENT_UNIQUE_NAME" type="xsd:string" sql:field="PARENT_UNIQUE_NAME"></xsd:element>  
            <xsd:element name="NODE_DESCRIPTION" type="xsd:string" sql:field="NODE_DESCRIPTION"></xsd:element>  
            <xsd:element name="NODE_RULE" type="xsd:string" sql:field="NODE_RULE"></xsd:element>  
            <xsd:element name="MARGINAL_RULE" type="xsd:string" sql:field="MARGINAL_RULE"></xsd:element>  
            <xsd:element name="NODE_PROBABILITY" type="xsd:double" sql:field="NODE_PROBABILITY"></xsd:element>  
            <xsd:element name="MARGINAL_PROBABILITY" type="xsd:double" sql:field="MARGINAL_PROBABILITY"></xsd:element>  
            <xsd:element name="NODE_SUPPORT" sql:type="xsd:double" sql:field="NODE_SUPPORT"></xsd:element>  
            <xsd:element name="MSOLAP_MODEL_COLUMN" sql:type="xsd:string" sql:field="MSOLAP_MODEL_COLUMN"></xsd:element>  
            <xsd:element name="MSOLAP_NODE_SCORE" sql:type="xsd:double" sql:field="MSOLAP_NODE_SCORE"></xsd:element>  
            <xsd:element name="MSOLAP_NODE_SHORT_CAPTION" sql:type="xsd:string" sql:field="MSOLAP_NODE_SHORT_CAPTION"></xsd:element>  
         </xsd:choice>  
      </xsd:complexType>  
   </xsd:schema>  
   <row>  
      <MODEL_CATALOG>FoodMart 2000</MODEL_CATALOG>  
      <MODEL_NAME>customer pattern discovery</MODEL_NAME>  
      <ATTRIBUTE_NAME>Customers.Name.Member Card</ATTRIBUTE_NAME>  
      <NODE_NAME>2147483652</NODE_NAME>  
      <NODE_UNIQUE_NAME>2147483652</NODE_UNIQUE_NAME>  
      <NODE_TYPE>2</NODE_TYPE>  
      <NODE_CAPTION>All</NODE_CAPTION>  
      <CHILDREN_CARDINALITY>8</CHILDREN_CARDINALITY>  
      <PARENT_UNIQUE_NAME>0</PARENT_UNIQUE_NAME>  
      <NODE_DESCRIPTION>All</NODE_DESCRIPTION>  
      <NODE_RULE></NODE_RULE>  
      <MARGINAL_RULE></MARGINAL_RULE>  
      <NODE_PROBABILITY>1</NODE_PROBABILITY>  
      <MARGINAL_PROBABILITY>1</MARGINAL_PROBABILITY>  
      <NODE_DISTRIBUTION>  
         <ATTRIBUTE_NAME>Customers.Name.Member Card</ATTRIBUTE_NAME>  
         <ATTRIBUTE_VALUE>missing</ATTRIBUTE_VALUE>  
         <SUPPORT>0</SUPPORT>  
         <PROBABILITY>0</PROBABILITY>  
         <VARIANCE>0</VARIANCE>  
         <VALUETYPE>1</VALUETYPE></NODE_DISTRIBUTION>  
      <NODE_DISTRIBUTION>  
         <ATTRIBUTE_NAME>Customers.Name.Member Card</ATTRIBUTE_NAME>  
         <ATTRIBUTE_VALUE>Bronze</ATTRIBUTE_VALUE>  
         <SUPPORT>3077</SUPPORT>  
         <PROBABILITY>0.551334886221107</PROBABILITY>  
         <VARIANCE>0</VARIANCE>  
         <VALUETYPE>4</VALUETYPE></NODE_DISTRIBUTION>  
      <NODE_DISTRIBUTION>  
         <ATTRIBUTE_NAME>Customers.Name.Member Card</ATTRIBUTE_NAME>  
         <ATTRIBUTE_VALUE>Golden</ATTRIBUTE_VALUE>  
         <SUPPORT>659</SUPPORT>  
         <PROBABILITY>0.118079197276474</PROBABILITY>  
         <VARIANCE>0</VARIANCE>  
         <VALUETYPE>4</VALUETYPE></NODE_DISTRIBUTION>  
      <NODE_DISTRIBUTION>  
         <ATTRIBUTE_NAME>Customers.Name.Member Card</ATTRIBUTE_NAME>  
         <ATTRIBUTE_VALUE>Normal</ATTRIBUTE_VALUE>  
         <SUPPORT>1332</SUPPORT>  
         <PROBABILITY>0.238666905572478</PROBABILITY>  
         <VARIANCE>0</VARIANCE>  
         <VALUETYPE>4</VALUETYPE></NODE_DISTRIBUTION>  
      <NODE_DISTRIBUTION>  
         <ATTRIBUTE_NAME>Customers.Name.Member Card</ATTRIBUTE_NAME>  
         <ATTRIBUTE_VALUE>Silver</ATTRIBUTE_VALUE>  
         <SUPPORT>513</SUPPORT>  
         <PROBABILITY>9.19190109299409E-02</PROBABILITY>  
         <VARIANCE>0</VARIANCE>  
         <VALUETYPE>4</VALUETYPE></NODE_DISTRIBUTION>  
      <NODE_SUPPORT>5581</NODE_SUPPORT>  
      <MSOLAP_MODEL_COLUMN>Customers.Name.Member Card</MSOLAP_MODEL_COLUMN>  
      <MSOLAP_NODE_SCORE>1948.401692055</MSOLAP_NODE_SCORE>  
      <MSOLAP_NODE_SHORT_CAPTION>All</MSOLAP_NODE_SHORT_CAPTION>  
</row>  
</root>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [XML 데이터 형식 &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  
