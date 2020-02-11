---
title: CREATE GLOBAL CUBE 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d678622c67a83c279cce094b849829e668af30cb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892157"
---
# <a name="mdx-data-definition---create-global-cube"></a>MDX 데이터 정의 - CREATE GLOBAL CUBE


  논리적 지속형 큐브를 서버에 있는 큐브의 하위 큐브에 따라 만들고 채웁니다. 논리적 지속형 큐브에 대한 연결 시에는 서버 연결이 필요하지 않습니다. 로컬 큐브에 대 한 자세한 내용은 [로컬 큐브 &#40;Analysis Services 다차원 데이터&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/olap-physical/local-cubes-analysis-services-multidimensional-data)를 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE GLOBAL CUBE local_cube_name STORAGE 'Cube_Location'   
FROM source_cube_name (<param list>)  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= < dim DM from clause> | <reg dim from clause>   
  
<dim DM from clause>::= dm_model_name> COLUMN column_name   
  
<dim reg from clause>::= dimension_name  
  
<dim content def>::= ( <level list> [,<grouping list>] [,<member slice list>] [,<default member>] )  
  
<level list>::= <level def> [, <level list>]  
  
<level def>::= LEVEL level_name [<level type> ] [AS level_name] [<level content def>]  
  
<level content def>::= ( <property list> ) | NO_PROPERTIES  
  
<level type>::= GROUPING  
  
<property list>::= <property def> [, <property list>]  
  
<property def>::= PROPERTY property_name   
  
<grouping list>::= <grouping entity> [,<grouping list>]  
  
<grouping entity>::= GROUP group_level_name.group_name (<mixed list>)  
  
<grp mixed list>::= <grp mixed element> [,<grp mixed list>]  
  
<grp mixed element>::= <grouping entity> | <member def>  
  
<member slice list>::= <member list>  
  
<member list>::= <member def> [, <member list>]  
  
<member def>::= MEMBER member_name  
  
<default member>::= DEFAULT_MEMBER AS MDX_expression  
  
<visibility qualifier>::= HIDDEN   
```  
  
## <a name="syntax-elements"></a>구문 요소  
 local_cube_name  
 로컬 큐브의 이름입니다.  
  
 'Cube_Location'  
 로컬에 저장된 큐브의 이름과 경로입니다.  
  
 source_cube_name  
 로컬 큐브가 기준으로 하는 큐브의 이름입니다.  
  
 source_cube_name.measure_name  
 로컬 큐브에 포함되는 원본 측정값의 정규화된 이름입니다. 측정값 차원의 계산 멤버는 허용되지 않습니다.  
  
 measure_name  
 로컬 큐브에 있는 측정값의 이름입니다.  
  
 source_cube_name.dimension_name  
 로컬 큐브에 포함되는 원본 차원의 정규화된 이름입니다.  
  
 dimension_name  
 로컬 큐브에 있는 차원의 이름입니다.  
  
 FROM \<dim from 절>  
 파생된 차원 정의에 대해서만 유효한 지정입니다.  
  
 NOT_RELATED_TO_FACTS  
 파생된 차원 정의에 대해서만 유효한 지정입니다.  
  
 \<수준 유형>  
 파생된 차원 정의에 대해서만 유효한 지정입니다.  
  
## <a name="remarks"></a>설명  
 로컬 큐브는 측정값을 정의 하는 definedin 용어입니다. 다음과 같은 두 가지 유형의 차원이 있습니다.  
  
-   원본 차원 - 하나 이상 원본 큐브의 일부인 차원입니다.  
  
-   파생된 차원 - 새 분석 기능을 제공하는 차원입니다. 파생된 차원은 세로 또는 가로로 분리되거나 차원 멤버의 사용자 지정 그룹화를 포함하는 원본 차원을 기반으로 정의된 일반 차원일 수 있습니다. 또한 파생된 차원은 데이터 마이닝 모델을 기반으로 하는 데이터 마이닝 차원일 수 있습니다.  
  
> [!NOTE]  
>  차원 키워드는 차원이나 계층을 참조할 수 있습니다.  
  
 로컬 큐브에서는 다음 태스크를 수행할 수 있습니다.  
  
-   원본 큐브에 있는 차원을 제거합니다.  
  
-   차원에 계층을 추가하거나 제거합니다.  
  
-   측정값 그룹이나 특정 측정값을 제거합니다.  
  
 CREATE GLOBAL CUBE 문은 다음 규칙을 따릅니다.  
  
-   CREATE GLOBAL CUBE 문은 계산 측정값 또는 동작과 같은 모든 명령을 로컬 큐브로 자동으로 복사합니다. 명령에 부모 큐브를 명시적으로 참조하는 MDX(Multidimensional Expressions) 식이 포함된 경우 로컬 큐브는 해당 명령을 실행할 수 없습니다. 이 문제를 방지 하려면 명령에 대 한 MDX 식을 정의할 때 **Currentcube** 키워드를 사용 합니다. **Currentcube** 키워드는 MDX 식 내에서 큐브를 참조할 때 현재 큐브 컨텍스트를 사용 합니다.  
  
-   로컬 큐브 파일에 있는 기존 글로벌 큐브로부터 만든 글로벌 큐브는 동일한 로컬 큐브 파일에 저장할 수 없습니다. 예를 들어 SalesLocal1이라는 글로벌 큐브를 만들고 이 큐브를 C:\SalesLocal.cub 파일에 저장한다고 가정하십시오. 그런 다음 C:\SalesLocal.cub 파일에 연결하여 SalesLocal2라는 두 번째 글로벌 큐브를 만듭니다. 이제 SalesLocal2 글로벌 큐브를 C:\SalesLocal.cub 파일에 저장하려고 하면 오류가 발생합니다. 하지만 SalesLocal2 글로벌 큐브를 다른 로컬 큐브 파일에 저장할 수는 있습니다.  
  
-   글로벌 큐브는 고유 카운트 측정값을 지원하지 않습니다. 고유 카운트 측정값이 포함된 큐브는 비가산적이기 때문에 CREATE GLOBAL CUBE 문에서는 고유 카운트 측정값을 만들거나 사용할 수 없습니다.  
  
-   로컬 큐브에 측정값을 추가하는 경우 추가되는 측정값과 관련된 차원도 하나 이상 포함해야 합니다.  
  
-   로컬 큐브에 부모-자식 계층을 추가하는 경우 부모-자식 계층의 수준과 필터는 무시되고 전체 부모-자식 계층이 포함됩니다.  
  
-   멤버 속성은 로컬 큐브에서 지원되지 않습니다.  
  
-   큐브 뷰에서 로컬 큐브를 만들 수 없습니다.  
  
-   로컬 큐브에 반가산적 측정값을 포함할 때는 다음과 같은 규칙이 적용됩니다.  
  
    -   추가되는 측정값의 AggregateFunction 속성이 ByAccount이면 Account 차원을 포함해야 합니다.  
  
    -   추가되는 AggregateFunction 속성 측정값이 FirstChild, LastChild, FirstNonEmpty, LastNonEmpty 또는 AverageOfChildren이면 전체 Time 차원을 포함해야 합니다.  
  
-   데이터 마이닝 차원은 로컬 큐브에 추가할 수 없습니다.  
  
-   참조 차원은 일반 차원으로 구체화되고 추가됩니다.  
  
-   다 대 다 차원을 포함할 때는 다음과 같은 규칙이 적용됩니다.  
  
    -   전체 다 대 다 차원을 추가해야 합니다.  
  
    -   중간 측정값 그룹을 추가해야 합니다.  
  
    -   다 대 다 관계에 포함된 두 측정값 그룹에 공통적인 모든 차원을 전체적으로 추가해야 합니다.  
  
 다음 예에서는 Reseller Sales Amount 측정값, Reseller 차원 및 Date 차원만 포함하는 Adventure Works 큐브의 로컬 지속형 버전을 만드는 방법을 보여 줍니다.  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller1.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
   )  
```  
  
 다음 예에서는 로컬 큐브를 만들 때의 분리 방법을 보여 줍니다. 생성된 글로벌 큐브는 Fiscal Year 수준의 2005 멤버에 의해 수직으로 분리되고 Fiscal Year 및 Month 수준에 의해 수평으로 분리된 Adventure Works 큐브를 기반으로 합니다.  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller2.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
      (  
LEVEL [Fiscal Year],  
LEVEL [Month],  
MEMBER [Date].[Fiscal].[Fiscal Year].&[2005]  
      )  
   )  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 데이터 정의 문은 MDX를 &#40;&#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [CREATE SESSION CUBE 문 &#40;MDX&#41;](../mdx/mdx-data-definition-create-session-cube.md)  
  
  
