---
title: 셀 요소 (MDDataSet) (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ba73a6ea5926de6f445c5ca5cec8142b3e196bd
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34576275"
---
# <a name="cell-element-mddataset-xmla"></a>Cell 요소(MDDataSet)(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  부모에 포함 된 단일 셀에 대 한 정보를 포함 [CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CellData>  
   <Cell CellOrdinal="unsignedInt">  
      <!-- Zero or more cell property values -->  
      <!-- or -->  
      <Error>...</Error>  
   </Cell>  
</CellData>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|InclusionThresholdSetting|  
|기본값|InclusionThresholdSetting|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md)|  
|자식 요소|0 개 이상의 셀 속성 값 또는 [오류](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|CellOrdinal|필요한 **unsignedInt** 특성입니다. 다차원 데이터 집합에 있는 셀의 서수 위치입니다.|  
  
## <a name="remarks"></a>Remarks  
 부모에 **루트** 요소는 **축** 요소 뒤는 **CellData** 요소, **셀** 포함 하는 요소 다차원 데이터 집합에 반환 된 각 셀에 대 한 속성 값입니다. **셀** 요소에 포함 된 **CellOrdinal** 각 셀 속성 값에 대 한 요소와 다차원 데이터 집합에 있는 셀의 서 수 위치 0부터 시작을 나타내는 특성 셀과 연결 합니다. 각 셀 속성 값은 **셀** 요소는 별도 XML 요소로 정의 됩니다. 에 정의 된 셀 속성의 값은 XML 요소 및 셀 속성의 이름에 포함 된 데이터는 **CellInfo** 부모 root 요소에서의 요소는 XML 요소의 이름에 해당 합니다.  
  
 다음은 셀 속성 값의 구문입니다.  
  
```  
<CellProperty xsi:type="string">value</CellProperty>  
```  
  
 셀 속성 값의 데이터 형식은 VALUE 셀 속성에만 지정됩니다. 다른 셀 속성의 데이터 형식에 포함 된 셀 속성 정의 의해 결정 됩니다는 **CellInfo** 요소입니다. 기본값이 지정 된 셀 속성 값 요소가 제외 될 수 있습니다 (포함 하 여 한 **기본** 에 포함 된 셀 속성 정의 대 한 요소는 **CellInfo** 요소) 셀 속성에 대 한 기본 값이 지정 하 고 셀 속성의 값은 null입니다.  
  
## <a name="cell-property-errors"></a>셀 속성 오류  
 셀 속성 값 지정된 된 셀에 대 한 반환 되지 않도록 하는 계산 오류 등의 Analysis Services 인스턴스에서 발생 하는 오류로 인해 반환할 수 없는 경우는 **오류** 요소 내용을 대체는 셀 속성에 있습니다. 다음 XML 예는 셀 속성 오류를 보여 줍니다.  
  
```  
<Cell CellOrdinal="0">  
   <Value xsi:type="xsd:double">  
      <Error>  
         <ErrorCode>2148497527</ErrorCode>  
         <Description>Unknown error</Description>  
      </Error>  
   </Value>  
</Cell>  
```  
  
## <a name="calculating-cell-ordinal-values"></a>셀 서수 값 계산  
 축 참조 셀이 되어 계산할 수에 따라 한 **CellOrdinal** 특성 값입니다. 이론적으로 셀 매겨집니다 데이터 집합의 데이터 집합을 한 *p*-차원 배열 여기서 *p* 축 수는 있습니다. 셀은 행 중심의 순서로 번호가 매겨집니다.  
  
 열에 측정값 4개 및 행에 4개 분기와 2개 주가 크로스 조인된 쿼리를 요청한다고 가정해 봅니다. 데이터 집합 결과 다음에 **CellOrdinal** 굵은 텍스트로 표시 되는 데이터 집합 결과의 부분에 대 한 속성은 {9, 10, 11, 13, 14, 15, 17, 18, 19} 집합입니다. 셀은 행 중심 순서 대로 번호가 매겨집니다 때문에 집합은 부터는 **CellOrdinal** 왼쪽된 위 셀에 대 한 0입니다.  
  
|State|Quarter|Unit sales|Store cost|Store sales|Sales count|  
|-----------|-------------|----------------|----------------|-----------------|-----------------|  
|California|Q1|16890|14431.09|36175.2|5498|  
||Q 2|18052|15332.02|38396.75|5915|  
||Q 3|18370|**15672.83**|**39394.05**|**6014**|  
||Q 4|21436|**18094.5**|**45201.84**|**7015**|  
|Oregon|Q1|19287|**16081.07**|**40170.29**|**6184**|  
||Q 2|15079|12678.96|31772.88|4799|  
||Q 3|16940|14273.78|35880.46|5432|  
||Q 4|16353|13738.68|34453.44|5196|  
|Washington|Q1|30114|25240.08|63282.86|9906|  
||Q 2|29479|24953.25|62496.64|9654|  
||Q 3|30538|25958.26|64997.38|10007|  
||Q 4|34235|29172.72|73016.34|11217|  
  
 그림의 공식을 적용하면 축 k = 0에는 Uk = 4 멤버가 있고, 축 k = 1에는 Uk = 8 튜플이 있습니다. P = 2는 쿼리의 전체 축 개수입니다. {California, Q3, Store Cost}인 셀을 S0으로 정하면 초기 합은 i = 0 또는 1입니다. i = 0이면 {Store Cost}의 축 0에서 튜플 서수는 1입니다. i = 1이면 {CA, Q3}의 튜플 서수는 2입니다.  
  
 에 대 한 i = 0, Ei = 1, 따라서 예를 i = 0 합은 1 * 1 = 1 및 i = 1, 합은 2 (튜플 서 수) 4 시간 (Ei 값 1로 계산 \* 4), 또는 8입니다. 그러면 1 + 8의 합 9가 해당 셀의 셀 서수가 됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 구조는 **셀** 요소를 VALUE, FORMATTED_VALUE 및 FORMAT_STRING 셀 각 셀에 대 한 속성 값입니다.  
  
```  
<CellData>  
   <Cell CellOrdinal="0">  
      <Value xsi:type="xsd:double">16890</Value>  
      <FmtValue>16,890.00</FmtValue>  
      <FormatString>Standard</FormatString>  
   </Cell>  
   <Cell CellOrdinal="1">  
      <Value xsi:type="xsd:int">50</Value>  
      <FmtValue>50</FmtValue>  
      <FormatString>Standard</FormatString>  
   </Cell>  
   <Cell CellOrdinal="2">  
      <Value xsi:type="xsd:double">36175.2</Value>  
      <FmtValue>$36,175.20</FmtValue>  
      <FormatString>Currency</FormatString>  
   </Cell>  
</CellData>  
```  
  
## <a name="see-also"></a>참고자료
 [MDDataSet 데이터 형식 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)   
 [속성 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
