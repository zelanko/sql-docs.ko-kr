---
title: "DRILLTHROUGH를 사용 하 여 원본 데이터 검색 (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DRILLTHROUGH statement
- retrieving data
- queries [MDX], DRILLTHROUGH statement
- data retrieval [MDX]
ms.assetid: fe0ab170-25a9-45a8-a377-f71a67f77018
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9470c5edd50bab3622ad73f3e3404a4747b07dd7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-data-manipulation---retrieve-source-data-using-drillthrough"></a>MDX 데이터 조작 드릴스루를 사용 하 여 원본 데이터 검색
  MDX(Multidimensional Expressions)는 [DRILLTHROUGH](../../../mdx/mdx-data-manipulation-drillthrough.md)문을 사용하여 큐브 셀의 원본 데이터에서 행 집합을 검색합니다.  
  
 큐브에서 **DRILLTHROUGH** 문을 실행하려면 해당 큐브에 대한 드릴스루 동작을 정의해야 합니다. 드릴스루 동작을 정의하려면 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]의 큐브 디자이너에서 **동작** 창의 도구 모음에서 **새 드릴스루 동작**을 클릭하십시오. 새 드릴스루 동작에서 동작 이름, 대상, 조건 및 **DRILLTHROUGH** 문이 반환하는 열을 지정하십시오.  
  
## <a name="drillthrough-statement-syntax"></a>DRILLTHROUGH 문 구문  
 **DRILLTHROUGH** 문의 구문은 다음과 같습니다.  
  
```  
<drillthrough> ::= DRILLTHROUGH [<Max_Rows>] [<First_Rowset>] <MDX select> [<Return_Columns>]  
   < Max_Rows> ::= MAXROWS <positive number>  
   <First_Rowset> ::= FIRSTROWSET <positive number>  
   <Return_Columns> ::= RETURN <member or attribute> [, <member or attribute>]  
```  
  
 **SELECT** 절은 검색할 원본 데이터를 포함하는 큐브를 식별합니다. 이 **SELECT** 절은 **SELECT** 절에서 각 축에 한 개의 멤버만 지정할 수 있다는 점 이외에는 통상적인 MDX **SELECT** 문과 동일합니다. 한 개의 축에 멤버를 두 개 이상 지정하면 오류가 발생합니다.  
  
 `<Max_Rows>` 구문은 반환된 각 행 집합의 최대 행 수를 지정합니다. 데이터 원본에 연결하는 데 사용되는 OLE DB 공급자가 **DBPROP_MAXROWS**를 지원하지 않으면 `<Max_Rows>` 설정은 무시됩니다.  
  
 `<First_Rowset>` 구문은 행 집합이 먼저 반환되는 파티션을 식별합니다.  
  
 `<Return_Columns>` 구문은 반환할 기본 데이터베이스 열을 식별합니다.  
  
## <a name="drillthrough-statement-example"></a>DRILLTHROUGH 문 예  
 다음 예에서는 **DRILLTHROUGH** 문의 사용 방법을 설명합니다. 이 예에서 DRILLTHROUGH 문은 상점 차원(slicer 축)을 따라 Store, Product 및 Time 차원 리프를 쿼리한 다음 부서 측정값 그룹, 부서 ID 및 직원의 이름을 반환합니다.  
  
```  
DRILLTHROUGH  
Select {Leaves(Store), Leaves(Product), Leaves(Time),*} on 0  
From Stores  
RETURN [Department MeasureGroup].[Department Id], [Employee].[First Name]  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 조작&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  

