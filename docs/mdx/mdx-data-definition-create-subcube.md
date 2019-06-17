---
title: CREATE SUBCUBE 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2b505de916ba274ebb69137aa3f61fe384386829
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248309"
---
# <a name="mdx-data-definition---create-subcube"></a>MDX 데이터 정의 - CREATE SUBCUBE


  지정한 큐브 또는 하위 큐브의 큐브 공간을 지정한 하위 큐브로 다시 정의합니다. 이 문은 후속 작업의 큐브 공간을 변경합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE SUBCUBE Cube_Name AS Select_Statement  
                                                  | NON VISUAL ( Select_Statement )  
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 제한되는 큐브 또는 큐브 뷰의 이름을 지정하는 유효한 문자열 식입니다. 이 이름은 하위 큐브의 이름이 됩니다.  
  
 *Select_Statement*  
 WITH, NON EMPTY 또는 HAVING 절이 없으며 차원이나 셀 속성을 요청하지 않는 유효한 MDX SELECT 식입니다.  
  
 참조 [SELECT 문의 &#40;MDX&#41; ](../mdx/mdx-data-manipulation-select.md) Select 문에 대 한 자세한 구문 설명을 보려면에 대 한 하며 **NON VISUAL** 절.  
  
## <a name="remarks"></a>Remarks  
 하위 큐브의 정의에서 기본 멤버가 제외되는 경우 그에 따라 좌표도 변경됩니다. 집계될 수 있는 특성에 대해서는 기본 멤버가 [All] 멤버로 이동합니다. 집계될 수 없는 특성에 대해서는 기본 멤버가 하위 큐브에 있는 멤버로 이동합니다. 다음 표에는 하위 큐브 예와 기본 멤버 조합이 포함됩니다.  
  
|원래 기본 멤버|집계 가능|하위 SELECT|수정된 기본 멤버|  
|-----------------------------|-----------------------|---------------|----------------------------|  
|Time.Year.All|사용자 계정 컨트롤|{Time.Year.2003}|변경 안 함|  
|Time.Year 합니다. [1997]|사용자 계정 컨트롤|{Time.Year.2003}|Time.Year.All|  
|Time.Year 합니다. [1997]|아니요|{Time.Year.2003}|Time.Year 합니다. [2003]|  
|Time.Year 합니다. [1997]|사용자 계정 컨트롤|{Time.Year.2003, Time.Year.2004}|Time.Year.All|  
|Time.Year 합니다. [1997]|아니요|{Time.Year.2003, Time.Year.2004}|Time.Year.[2003] 또는<br /><br /> Time.Year.[2004]|  
  
 [All] 멤버는 항상 하위 큐브에 존재합니다.  
  
 하위 큐브가 삭제되면 하위 큐브의 컨텍스트에서 생성된 세션 개체도 삭제됩니다.  
  
 하위 큐브에 대 한 자세한 내용은 참조 하세요. [MDX로 하위 큐브 작성 &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx.md)합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 큐브 공간을 Canada의 멤버로 제한하는 하위 큐브를 만듭니다. 사용 하 여는 **멤버** Geography 사용자 정의 계층의 canada 국가 반환 수준 국가의 모든 멤버를 반환 하는 함수입니다.  
  
```  
CREATE SUBCUBE [Adventure Works] AS  
   SELECT [Geography].[Country].&[Canada] ON 0  
   FROM [Adventure Works]  
  
SELECT [Geography].[Country].[Country].MEMBERS ON 0  
   FROM [Adventure Works]  
  
```  
  
 다음 예에서는 큐브 공간을 Products.Category의 {Accessories, Clothing} 멤버 및 Resellers.[Business Type]의 {[Value Added Reseller], [Warehouse]}로 제한하는 하위 큐브를 만듭니다.  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works]`  
  
 다음 MDX를 사용하여 Products.Category 및 Resellers.[Business Type]의 모든 멤버에 대한 하위 큐브 쿼리:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 반환되는 결과는 다음과 같습니다.  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$2,031,079.39|$506,172.45|$1,524,906.93|  
|Value Added Reseller|$767,388.52|$175,002.81|$592,385.71|  
|Warehouse|$1,263,690.86|$331,169.64|$932,521.23|  
  
 NON VISUAL 절을 사용하여 하위 큐브를 삭제하고 다시 만들면 하위 큐브에 해당 멤버가 표시되는지 여부에 관계없이 Products.Category 및 Resellers.[Business Type]의 모든 멤버에 대한 순 합계가 포함된 하위 큐브가 만들어집니다.  
  
 `CREATE SUBCUBE [Adventure Works] AS`  
  
 `NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 위와 같은 MDX 쿼리 실행:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 다음과 같이 다른 결과가 반환됩니다.  
  
|||||  
|-|-|-|-|  
||All Products|Accessories|Clothing|  
|All Resellers|$80,450,596.98|$571,297.93|$1,777,840.84|  
|Value Added Reseller|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 [All Products] 및 [All Resellers]의 열 및 행에는 보이는 멤버뿐만 아니라 모든 멤버에 대한 합계가 포함됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX의 주요 개념&#40;Analysis Services&#41;](../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)   
 [MDX 스크립팅 문 &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)   
 [DROP SUBCUBE 문 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-subcube.md)   
 [SELECT 문 & #40; Mdx& #41;](../mdx/mdx-data-manipulation-select.md)  
  
  
