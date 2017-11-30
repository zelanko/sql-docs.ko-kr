---
title: "CREATE MEMBER 문 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_MEMBER
- CREATE MEMBER
- Member
- CREATE
dev_langs: kbMDX
helpviewer_keywords:
- CREATE MEMBER statement
- calculated members [MDX]
ms.assetid: 49379217-be2c-4139-a206-1168078b9b76
caps.latest.revision: "55"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 44a329213b7bbe39167e8f0c6b85e473d2d58411
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2017
---
# <a name="mdx-data-definition---create-member"></a>MDX 데이터 정의-멤버를 만들려면
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  계산 멤버를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
CREATE [ SESSION ] [HIDDDEN] [ CALCULATED ] MEMBER CURRENTCUBE | Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>인수  
 *Cube_Name*  
 멤버를 만들 큐브의 이름을 지정하는 유효한 문자열 식입니다.  
  
 *Member_Name*  
 멤버 이름을 지정하는 유효한 문자열 식입니다. 측정값 차원이 아닌 차원의 멤버를 만들려면 정규화된 이름을 지정합니다. 정규화된 멤버 이름을 제공하지 않으면 측정값 차원에 멤버가 생성됩니다.  
  
 *MDX_Expression*  
 유효한 MDX 식입니다.  
  
 *Property_Name*  
 계산 멤버 속성의 이름을 지정하는 유효한 문자열입니다.  
  
 *Property_Value*  
 계산 멤버 속성의 값을 정의하는 유효한 스칼라 식입니다.  
  
## <a name="remarks"></a>주의  
 CREATE MEMBER 문은 세션 전체에서 사용할 수 있는 계산 멤버를 정의하므로 세션 중에 여러 쿼리에서 사용할 수 있습니다. 자세한 내용은 참조 [Creating Session-Scoped 계산 멤버 &#40; Mdx&#41; ](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md).  
  
 또한 단일 쿼리에서 사용할 계산 멤버를 정의할 수 있습니다. 단일 쿼리로 제한된 계산 멤버를 정의하려면 SELECT 문에서 WITH 절을 사용합니다. 자세한 내용은 참조 [Creating Query-Scoped 계산 멤버 &#40; Mdx&#41; ](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
 *Property_Name* 표준 나 선택적 계산된 멤버 속성이 속성 중 하나를 참조할 수 있습니다. 표준 멤버 속성은 이 항목의 후반부에 나열되어 있습니다. 없이 CREATE MEMBER로 만든 계산 멤버는 **세션** 값 세션 범위를 가집니다. 또한 계산 멤버 정의 내부의 문자열은 큰따옴표로 구분됩니다. 이것은 문자열이 작은따옴표로 구분되어야 한다고 지정하는 OLE DB에 의해 정의된 메서드와는 다릅니다.  
  
 현재 연결된 큐브가 아닌 다른 큐브를 지정하면 오류가 발생합니다. 따라서 큐브 이름에서 CURRENTCUBE를 사용하여 현재 큐브를 표시해야 합니다.  
  
 OLE DB에 의해 정의되는 멤버 속성에 대한 자세한 내용은 OLE DB 설명서를 참조하십시오.  
  
## <a name="scope"></a>범위  
 계산 멤버는 다음 테이블에 나열된 범위 중 하나에서 발생할 수 있습니다.  
  
 쿼리 범위  
 계산 멤버의 표시 여부 및 수명은 쿼리로 제한됩니다. 계산 멤버는 개별 쿼리에서 정의됩니다. 쿼리 범위는 세션 범위보다 우선합니다. 자세한 내용은 참조 [Creating Query-Scoped 계산 멤버 &#40; Mdx&#41; ](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
 세션 범위  
 계산 멤버의 표시 여부 및 수명은 계산 멤버를 만들 때의 세션에 따라 결정됩니다. DROP MEMBER 문이 계산 멤버에서 실행되는 경우 수명은 세션 기간보다 짧습니다. CREATE MEMBER 문은 세션 범위로 계산 멤버를 만듭니다.  
  
### <a name="scope-isolation"></a>범위 격리  
 큐브 MDX(Multidimensional Expressions) 스크립트에 계산 멤버가 포함되어 있으면 기본적으로 세션 범위 계산 및 쿼리 정의 계산이 해결되기 전에 계산 멤버가 해결됩니다.  
  
> [!NOTE]  
>  특정 시나리오에는 [(MDX)](../mdx/aggregate-mdx.md) 함수 및 [VisualTotals (MDX)](../mdx/visualtotals-mdx.md) 함수가이 동작을 노출 하지 않습니다.  
  
 이 동작을 사용하면 특정 계산 구현을 고려할 필요 없이 일반 클라이언트 응용 프로그램에서 복잡한 계산이 포함된 큐브 작업을 수행할 수 있습니다. 하지만, 특정 시나리오에 필요할 수 있습니다는 큐브에 및 둘 다에서 세션 또는 특정 계산 하기 전에 쿼리 범위 계산된 멤버를 실행 하는 **집계** 함수 및 **VisualTotals** 함수 적용 됩니다. 이를 위해서는 SCOPE_ISOLATION 계산 속성을 사용하십시오.  
  
#### <a name="example"></a>예제  
 다음 스크립트는 올바른 결과를 생성하기 위해 SCOPE_ISOLATION 계산 속성이 필요한 경우의 예입니다.  
  
 **큐브의 MDX 스크립트:**  
  
```  
CREATE MEMBER CURRENTCUBE.Measures.ProfitRatio AS 'Measures.[Store Sales]/Measures.[Store Cost]', SOLVE_ORDER = 10  
```  
  
 **MDX 쿼리:**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
 이전 쿼리의 원하는 결과는 WA를 제외한 미국의 매장 비용 대비 WA를 제외한 미국의 매출 비율입니다. 이전 쿼리는 원하는 결과를 반환하지 않고 미국 비율에서 WA 비율을 뺀 값을 반환하는데 이 결과는 의미가 없습니다.  원하는 결과를 얻으려면 SCOPE_ISOLATION 계산 속성을 사용합니다.  
  
 **SCOPE_ISOLATION 계산 속성을 사용 하 여 MDX 쿼리:**  
  
```  
WITH MEMBER [Customer].[Customers].[USA]. USAWithoutWA AS  
[Customer].[Customers].[Country].&[USA] - [Customer].[Customers].[State Province.&[WA], SOLVE_ORDER=5  
,SCOPE_ISOLATION=CUBE  
SELECT {USAWithoutWA} ON 0 FROM SALES  
WHERE ProfitRatio  
```  
  
## <a name="standard-properties"></a>표준 속성  
 각 계산 멤버에는 기본 속성 집합이 있습니다. 클라이언트 응용 프로그램에 연결 되어 있을 때 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 기본 속성은 지원 되거나 지원 가능 하 게 관리자의 선택에 따라 합니다.  
  
 큐브 정의에 따라 멤버 속성을 추가로 사용할 수도 있습니다. 다음 속성은 큐브의 차원 수준에 관한 정보를 나타냅니다.  
  
|속성 식별자|의미|  
|-------------------------|-------------|  
|SOLVE_ORDER|계산 멤버가 다른 계산 멤버를 참조하는 경우(즉, 계산 멤버가 서로 교차하는 경우) 계산 멤버를 확인하는 순서입니다.|  
|FORMAT_STRING|셀 값을 표시할 때 클라이언트 응용 프로그램이 사용할 수 있는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office 스타일 서식 문자열입니다.|  
|VISIBLE|계산 멤버를 스키마 행 집합에서 볼 수 있는지 여부를 나타내는 값입니다.  계산 된 집합에 멤버를 추가할 수는 [AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md) 함수입니다. 0이 아닌 값은 계산 멤버를 볼 수 있음을 나타냅니다. 이 속성에 대 한 기본값은 *Visible*합니다.<br /><br /> 볼 수 없는 계산 멤버(이 값이 0으로 설정된 계산 멤버)는 일반적으로 더 복잡한 계산 멤버에서 중간 단계로 사용됩니다. 이런 계산 멤버는 측정값과 같은 다른 종류의 멤버가 참조할 수도 있습니다.|  
|NON_EMPTY_BEHAVIOR|빈 셀을 확인할 때 계산 멤버의 동작을 결정하는 데 사용하는 측정값 또는 집합입니다.<br /><br /> **\*\*경고 \* \***  이 속성은 사용 되지 않습니다. 이 속성을 설정하지 마세요. 자세한 내용은 [SQL Server 2016에서 사용되지 않는 Analysis Services 기능](../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md)을 참조하세요.|  
|CAPTION|클라이언트 응용 프로그램이 멤버에 대한 캡션으로 사용하는 문자열입니다.|  
|DISPLAY_FOLDER|클라이언트 응용 프로그램이 멤버를 표시하기 위해 사용하는 표시 폴더의 경로를 식별하는 문자열입니다. 폴더 수준 구분 기호는 클라이언트 응용 프로그램에서 정의합니다. 도구 및에서 제공 하는 클라이언트에 대 한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], 백슬래시 (\\)가 수준 구분 기호입니다. 정의 멤버에 대해 여러 표시 폴더를 제공하려면 세미콜론(;)을 사용하여 폴더를 구분하십시오.|  
|ASSOCIATED_MEASURE_GROUP|이 멤버를 연결할 측정값 그룹의 이름입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [DROP MEMBER 문 &#40; Mdx&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [UPDATE MEMBER 문 &#40; Mdx&#41;](../mdx/mdx-data-definition-update-member.md)   
 [MDX 데이터 정의 문 &#40; Mdx&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
