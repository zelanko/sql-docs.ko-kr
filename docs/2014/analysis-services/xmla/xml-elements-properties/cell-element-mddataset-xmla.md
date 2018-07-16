---
title: 셀 요소 (MDDataSet) (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Cell Element (MDDataSet)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cell
- http://schemas.microsoft.com/analysisservices/2003/engine#Cell
- urn:schemas-microsoft-com:xml-analysis#Cell
helpviewer_keywords:
- Cell element
ms.assetid: c4ea08a4-f653-4ade-be07-b91eb5b1ef32
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f07798a28c59597575de08bf5d0f3ea1d7087c8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37269509"
---
# <a name="cell-element-mddataset-xmla"></a>Cell 요소(MDDataSet)(XMLA)
  부모에 포함 된 단일 셀에 대 한 정보가 [CellData](celldata-element-xmla.md) 요소입니다.  
  
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
|부모 요소|[CellData](celldata-element-xmla.md)|  
|자식 요소|0 개 이상의 셀 속성 값 또는 [오류](error-element-xmla.md)|  
  
## <a name="attributes"></a>특성  
  
|attribute|Description|  
|---------------|-----------------|  
|CellOrdinal|필요한 `unsignedInt` 특성입니다. 다차원 데이터 집합에 있는 셀의 서수 위치입니다.|  
  
## <a name="remarks"></a>Remarks  
 부모 `root` 요소에서 `Axes` 요소는 다차원 데이터 집합에 반환된 각 셀의 속성 값을 포함하는 `CellData` 요소의 컬렉션인 `Cell` 요소 뒤에 나옵니다. `Cell` 요소는 다차원 데이터 집합에 있는 셀의 서수 위치(0부터 시작)를 나타내는 `CellOrdinal` 특성을 포함하고 해당 셀과 연결된 각 셀 속성 값 당 하나의 요소를 포함합니다. `Cell` 요소의 각 셀 속성 값은 개별 XML 요소로 정의됩니다. 셀 속성 값은 XML 요소에 포함된 데이터이고, 부모 루트 요소의 `CellInfo` 요소에 정의된 셀 속성 이름은 XML 요소 이름과 일치합니다.  
  
 다음은 셀 속성 값의 구문입니다.  
  
```  
<CellProperty xsi:type="string">value</CellProperty>  
```  
  
 셀 속성 값의 데이터 형식은 VALUE 셀 속성에만 지정됩니다. 다른 셀 속성의 데이터 형식은 `CellInfo` 요소에 포함된 셀 속성 정의에 의해 결정됩니다. 셀 속성에 기본값이 지정되었거나(`Default` 요소에 포함된 셀 속성 정의에 `CellInfo` 요소가 있음) 기본값이 지정되어 있지 않고 셀 속성 값이 Null인 경우 셀 속성 값 요소가 제외될 수 있습니다.  
  
## <a name="cell-property-errors"></a>셀 속성 오류  
 인스턴스에서 발생 하는 오류로 인해 셀 속성을 반환할 수 없는 경우 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에 값을 지정된 된 셀에 대해 반환 되는 것을 방지 하는 계산 오류와 같은 `Error` 요소 대체는 해당 셀 속성의 내용입니다. 다음 XML 예는 셀 속성 오류를 보여 줍니다.  
  
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
 셀의 축 참조를 `CellOrdinal` 특성 값에 기반하여 계산할 수 있습니다. 개념적으로 셀은 번호가 매겨진 데이터 집합의 데이터 집합 처럼를 *p*-차원 배열에 있는 *p* 는 축의 개수입니다. 셀은 행 중심의 순서로 번호가 매겨집니다.  
  
 열에 측정값 4개 및 행에 4개 분기와 2개 주가 크로스 조인된 쿼리를 요청한다고 가정해 봅니다. 다음 데이터 집합 결과에서 굵게 표시된 데이터 집합 결과 부분의 `CellOrdinal` 속성은 {9, 10, 11, 13, 14, 15, 17, 18, 19} 집합입니다. 집합인 이유는 왼쪽 위 셀부터 0 `CellOrdinal`로 시작하여 행 중심의 순서로 셀의 번호를 매기기 때문입니다.  
  
|State|Quarter|Unit sales|Store cost|Store sales|Sales count|  
|-----------|-------------|----------------|----------------|-----------------|-----------------|  
|California|Q1|16890|14431.09|36175.2|5498|  
||Q2|18052|15332.02|38396.75|5915|  
||Q3|18370|**15672.83**|**39394.05**|**6014**|  
||Q4|21436|**18094.5**|**45201.84**|**7015**|  
|Oregon|Q1|19287|**16081.07**|**40170.29**|**6184**|  
||Q2|15079|12678.96|31772.88|4799|  
||Q3|16940|14273.78|35880.46|5432|  
||Q4|16353|13738.68|34453.44|5196|  
|Washington|Q1|30114|25240.08|63282.86|9906|  
||Q2|29479|24953.25|62496.64|9654|  
||Q3|30538|25958.26|64997.38|10007|  
||Q4|34235|29172.72|73016.34|11217|  
  
 그림의 공식을 적용하면 축 k = 0에는 Uk = 4 멤버가 있고, 축 k = 1에는 Uk = 8 튜플이 있습니다. P = 2는 쿼리의 전체 축 개수입니다. {California, Q3, Store Cost}인 셀을 S0으로 정하면 초기 합은 i = 0 또는 1입니다. i = 0이면 {Store Cost}의 축 0에서 튜플 서수는 1입니다. i = 1이면 {CA, Q3}의 튜플 서수는 2입니다.  
  
 에 대 한 i = 0, Ei = 1, 따라서 i = 0 합은 1 * 1 = 1 및 있나요 = 1, 합은 2 (튜플 서 수) 4 시간 (는 Ei 값 1로 계산 \* 4), 또는 8. 그러면 1 + 8의 합 9가 해당 셀의 셀 서수가 됩니다.  
  
## <a name="example"></a>예제  
 다음 예는 각 셀의 VALUE, FORMATTED_VALUE 및 FORMAT_STRING 셀 속성 값을 포함하는 `Cell` 요소의 구조를 보여 줍니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [MDDataSet 데이터 형식 &#40;XMLA&#41;](../xml-data-types/mddataset-data-type-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
