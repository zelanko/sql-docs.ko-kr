---
title: "CREATE SESSION CUBE 문 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_SESSION_CUBE
- SESSION
- CUBE
- SESSION CUBE
- CREATE SESSION CUBE
- CREATE SESSION
- CREATE
dev_langs:
- kbMDX
helpviewer_keywords:
- CREATE SESSION CUBE
- statements [MDX], CREATE SESSION CUBE
ms.assetid: 06b90f44-d943-4a52-b0d8-4bcbc57ed6ec
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 14556669f6c39977fa1f82d8fbe6a2edff927837
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="mdx-data-definition---create-session-cube"></a>MDX 데이터 정의-세션 큐브 만들기
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  기존 서버 큐브에서 세션 큐브를 만들고 채웁니다. 세션 큐브는 현재 세션 내에서만 볼 수 있고 다른 세션에서 찾아보거나 쿼리할 수 없습니다.  세션 큐브는 세션을 닫을 때 암시적으로 삭제됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE SESSION CUBE session_cube_name FROM <cube list> (<param list>)  
  
<cube list>::= source_cube_name [,<cube list>]  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= <reg dim from clause>   
  
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
 session_cube_name  
 세션 큐브의 이름입니다.  
  
 source_cube_name  
 세션 큐브가 기준으로 하는 큐브의 이름입니다.  
  
 source_cube_name.measure_name  
 세션 큐브에 포함되는 원본 측정값의 정규화된 이름입니다. 측정값 차원의 계산 멤버는 허용되지 않습니다.  
  
 measure_name  
 세션 큐브에 있는 측정값의 이름입니다.  
  
 source_cube_name.dimension_name  
 세션 큐브에 포함되는 원본 차원의 정규화된 이름입니다.  
  
 dimension_name  
 세션 큐브에 있는 차원의 이름입니다.  
  
 \<dim from 절 >  
 파생된 차원 정의에 대해서만 유효한 지정입니다.  
  
 NOT_RELATED_TO_FACTS  
 파생된 차원 정의에 대해서만 유효한 지정입니다.  
  
 \<수준 유형 >  
 파생된 차원 정의에 대해서만 유효한 지정입니다.  
  
## <a name="remarks"></a>주의  
 서버 및 로컬 큐브와 달리 세션 큐브는 세션 큐브를 만든 세션이 끝나면 지속되지 않습니다. 세션 큐브는 해당 세션 큐브를 정의하는 정의와 측정값으로 정의됩니다. 다음과 같은 두 가지 유형의 차원이 있습니다.  
  
-   원본 차원 - 하나 이상 원본 큐브의 일부인 차원입니다.  
  
-   파생된 차원 - 새 분석 기능을 제공하는 차원입니다. 파생된 차원은 세로 또는 가로로 분리되거나 차원 멤버의 사용자 지정 그룹화를 포함하는 원본 차원을 기반으로 정의된 일반 차원일 수 있습니다. 또한 파생된 차원은 데이터 마이닝 모델을 기반으로 하는 데이터 마이닝 차원일 수 있습니다.  
  
> [!NOTE]  
>  차원 키워드는 차원이나 계층을 참조할 수 있습니다.  
  
 세션 큐브는 주로 Microsoft Excel과 같은 클라이언트 응용 프로그램에서 동적으로 특성 멤버를 사용자 지정 멤버 그룹으로 그룹화하는 데 사용됩니다. 세션 큐브에서는 다음 태스크를 수행할 수 있습니다.  
  
-   원본 큐브에 있는 차원을 제거합니다.  
  
-   차원에 계층을 추가하거나 제거합니다.  
  
-   측정값 그룹이나 특정 측정값을 제거합니다.  
  
-   기존 특성에 대한 그룹을 만들기 위해 특성 바인딩을 기반으로 새 특성을 추가합니다.  
  
> [!IMPORTANT]  
>  세션 큐브 개체에 대한 보안은 기본 원본 개체로부터 상속됩니다. 세션 큐브는 동작 및 계산 스크립트와 같은 다른 개체도 상속 받습니다.  
  
 CREATE SESSION CUBE 문은 다음 규칙을 따릅니다.  
  
-   부모-자식 계층에 대해 그룹화를 수행할 수 없습니다.  
  
-   ROLAP 차원에 대해 그룹화를 수행할 수 없습니다.  
  
-   연결된 차원에 대해 그룹화를 수행할 수 없습니다.  
  
-   사용자 지정 롤업이 있는 수준에 대해 그룹화를 수행할 수 없습니다.  
  
-   불연속화 특성 계층에 대해 그룹화를 수행할 수 없습니다.  
  
-   수준 간에 다 대 다 관계가 있는 계층(예: 연령 및 성별)인 비자연 계층에 대해 그룹화를 수행할 수 없습니다.  
  
-   MDX 스크립트에 있는 큐브 이름에 대한 명시적 참조는 세션 큐브에 다른 이름이 있으므로 그룹화에 의해 끊어집니다. 대신 CURRENTCUBE 키워드를 사용합니다.  
  
-   명시적 기본 멤버가 있는 차원에 대해 그룹화를 수행할 수 없습니다.  
  
-   그룹화를 수행하면 원래 서버 큐브의 세션 범위 계산 멤버는 삭제됩니다.  
  
-   서버 큐브의 큐브 차원에 대해 그룹화를 수행하면 동일한 차원을 기반으로 하는 모든 큐브 차원에 영향을 줍니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 Reseller Sales Amount 측정값, Reseller 차원, Product 차원, Geography 차원 및 Date 차원을 포함하는 Adventure Works 큐브의 세션 범위 버전을 만드는 방법을 보여 줍니다. 이 세션 큐브 내에 두 개의 그룹이 생성됩니다. 한 그룹에는 유럽 국가가 포함되고 다른 그룹에는 북아메리카 국가가 포함됩니다. 이 예제는 사용자가 멤버의 사용자 지정 그룹화를 만들 때 Microsoft Excel에서 실행하는 CREATE SESSION CUBE 문의 단순한 버전입니다.  
  
```  
CREATE SESSION CUBE [Adventure Works_XL_GROUPING1]   
   FROM [Adventure Works]   
   ( MEASURE [Adventure Works].[Internet Sales Amount]  
   ,MEASURE [Adventure Works].[Reseller Sales Amount]  
   ,DIMENSION [Adventure Works].[Date].[Calendar]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Year]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Semester]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Quarter]  
   ,DIMENSION [Adventure Works].[Date].[Month Name]  
   ,DIMENSION [Adventure Works].[Date].[Date]  
   ,DIMENSION [Adventure Works].[Geography].[Country]   
      HIDDEN AS _XL_GROUPING81  
   ,DIMENSION [Adventure Works].[Geography].[State-Province]  
   ,DIMENSION [Adventure Works].[Geography].[City]  
   ,DIMENSION [Adventure Works].[Geography].[Postal Code]  
   ,DIMENSION [Adventure Works].[Geography].[Geography]  
   ,DIMENSION [Adventure Works].[Product].[Product Categories]  
   ,DIMENSION [Adventure Works].[Product].[Category]  
   ,DIMENSION [Adventure Works].[Product].[Subcategory]  
   ,DIMENSION [Adventure Works].[Product].[Product]  
   ,DIMENSION [Adventure Works].[Product].[Product Key]  
   ,DIMENSION [Adventure Works].[Reseller].[Reseller]  
   ,DIMENSION [Adventure Works].[Reseller].[Geography Key]  
   ,DIMENSION [Geography].[Country]   
      NOT_RELATED_TO_FACTS FROM _XL_GROUPING81   
          ( LEVEL [(All)]  
         ,LEVEL [Country1] GROUPING  
         ,LEVEL [Country]  
            ,GROUP [Country1].[CountryXl_Grp_1]   
                ( MEMBER [Geography].[Country].&[Canada]  
                  ,MEMBER [Geography].[Country].&[United States] )  
            ,GROUP [Country1].[CountryXl_Grp_2]   
                ( MEMBER [Geography].[Country].&[France]  
                  ,MEMBER [Geography].[Country].&[Germany]  
                  ,MEMBER [Geography].[Country].&[United Kingdom] )   
            )   
   )  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 데이터 정의 문 &#40; Mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [GLOBAL CUBE 문 &#40; 만들기 Mdx&#41;](../mdx/mdx-data-definition-create-global-cube.md)  
  
  

