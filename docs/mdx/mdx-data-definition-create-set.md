---
title: CREATE SET 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4d1e58d016649c3c21a056a82315bd0d0fb3564f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248380"
---
# <a name="mdx-data-definition---create-set"></a>MDX 데이터 정의 - CREATE SET


  현재 큐브의 세션 범위를 사용하여 명명된 집합을 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE [SESSION] [ STATIC | DYNAMIC ] [HIDDEN] SET   
   CURRENTCUBE | Cube_Name  
      .Set_Name AS 'Set_Expression'  
      [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브의 이름을 지정하는 유효한 문자열 식입니다.  
  
 *Set_Name*  
 만들려는 명명된 집합의 이름을 지정하는 유효한 문자열 식입니다.  
  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
 *Property_Name*  
 집합 속성의 이름을 지정하는 유효한 문자열입니다.  
  
 *Property_Value*  
 집합 속성의 값을 정의하는 유효한 스칼라 식입니다.  
  
## <a name="remarks"></a>Remarks  
 명명된 집합은 다시 사용할 수 있도록 만드는 일련의 차원 멤버(또는 집합을 정의하는 식)입니다. 예를 들어 명명된 집합을 사용하면 판매량 기준으로 상위 10개의 판매점 집합으로 구성되는 차원 멤버 집합을 정의할 수 있습니다. 정적으로 또는 같은 함수를 사용 하 여이 집합을 정의할 수 있습니다 [TopCount](../mdx/topcount-mdx.md)합니다. 그런 다음에는 상위 10개의 판매점이 필요할 때마다 이 명명된 집합을 사용할 수 있습니다.  
  
 CREATE SET 문은 세션을 통해 사용할 수 있는 상태로 유지되는 명명된 집합을 만들기 때문에 세션의 여러 쿼리에서 사용될 수 있습니다. 자세한 내용은 [세션 범위 계산 멤버 &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md)합니다.  
  
 또한 단일 쿼리에서 사용할 명명된 집합을 정의할 수 있습니다. 이러한 집합을 정의하려면 SELECT 문에서 WITH 절을 사용합니다. WITH 절에 대 한 자세한 내용은 참조 하세요. [명명 된 집합 만들기 &#40;mdx&#41; &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md)합니다.  
  
 합니다 *Set_Expression* 절에는 MDX 구문을 지 원하는 함수가 포함 될 수 있습니다. SESSION 절을 지정하지 않는 CREATE SET 문으로 만든 집합에는 세션 범위가 포함됩니다. 쿼리 범위의 집합을 만들려면 WITH 절을 사용합니다.  
  
 현재 연결된 큐브가 아닌 다른 큐브를 지정하면 오류가 발생합니다. 따라서 큐브 이름에서 CURRENTCUBE를 사용하여 현재 큐브를 표시해야 합니다.  
  
## <a name="scope"></a>범위  
 사용자 정의 집합은 다음 표에 나열된 범위 중 하나에서 발생할 수 있습니다.  
  
 쿼리 범위  
 집합의 표시 여부 및 수명은 쿼리에 따라 결정됩니다. 집합은 개별 쿼리에서 정의됩니다. 쿼리 범위는 세션 범위보다 우선합니다. 자세한 내용은 [명명 된 집합 만들기 &#40;mdx&#41; &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md)합니다.  
  
 세션 범위  
 집합의 표시 여부 및 수명은 집합이 생성될 때의 세션에 따라 결정됩니다. (수명 보다 작은 경우 세션 기간을 DROP SET 문이 집합에서 실행 되는 경우) CREATE SET 문은 세션 범위로 집합을 만듭니다. 쿼리 범위의 집합을 만들려면 WITH 절을 사용합니다.  
  
### <a name="example"></a>예제  
 다음 예에서는 Core Products라는 집합을 만듭니다. 그런 다음 SELECT 쿼리를 통해 새로 만든 집합을 호출합니다. CREATE SET 문은 SELECT 쿼리를 실행하기 전에 실행해야 합니다. CREATE SET 문과 SELECT 쿼리를 동시에 실행할 수는 없습니다.  
  
```  
CREATE SET [Adventure Works].[Core Products] AS '{[Product].[Category].[Bikes]}'  
  
SELECT [Core Products] ON 0  
  FROM [Adventure Works]  
```  
  
## <a name="set-evaluation"></a>집합 계산  
 집합 계산은 서로 다르게 발생하도록 정의할 수 있습니다. 집합을 만들 때 한 번만 발생하도록 정의하거나 집합을 사용할 때마다 발생하도록 정의할 수 있습니다.  
  
 STATIC  
 CREATE SET 문을 계산할 때 집합이 한 번만 계산됨을 나타냅니다.  
  
 DYNAMIC  
 쿼리에서 사용할 때마다 집합이 계산됨을 나타냅니다.  
  
## <a name="set-visibility"></a>집합 표시 유형  
 큐브를 쿼리하는 다른 사용자에게 집합을 표시하거나 표시하지 않을 수 있습니다.  
  
 HIDDEN  
 큐브를 쿼리하는 사용자에게 집합을 표시하지 않도록 지정합니다.  
  
## <a name="standard-properties"></a>표준 속성  
 각 집합에는 기본 속성 집합이 있습니다. 클라이언트 응용 프로그램을 연결할 때 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 관리자의 선택에 따라 기본 속성이 지원 되거나 지원 가능 하 게 됩니다.  
  
|속성 식별자|의미|  
|-------------------------|-------------|  
|CAPTION|클라이언트 응용 프로그램이 집합에 대한 캡션으로 사용하는 문자열입니다.|  
|DISPLAY_FOLDER|클라이언트 응용 프로그램이 집합을 표시하기 위해 사용하는 표시 폴더의 경로를 식별하는 문자열입니다. 폴더 수준 구분 기호는 클라이언트 응용 프로그램에서 정의합니다. 도구 및 클라이언트에서 제공한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 백슬래시 (\\)가 수준 구분 기호입니다. 정의 집합에 대해 여러 표시 폴더를 제공하려면 세미콜론(;)을 사용하여 폴더를 구분하십시오.|  
  
## <a name="see-also"></a>관련 항목  
 [DROP SET 문 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-set.md)   
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
