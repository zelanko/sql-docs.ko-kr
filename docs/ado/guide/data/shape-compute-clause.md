---
title: "COMPUTE 절 셰이프 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0c20aec7585c33a7165fac4e93b446e4ce3aaf4e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="shape-compute-clause"></a>셰이프 COMPUTE 절
부모를 생성 하는 셰이프 COMPUTE 절 **레코드 집합**, 열이 있는 자식에 대 한 참조를 이루어져 **레코드 집합**선택적 요소 내용이 장, 새로 만들었거나, 또는 계산된 열, 열 또는 자식 요소에서 집계 함수를 실행 한 결과 **레코드 집합** 또는 이전에 모양의 **레코드 집합**; 및 모든 열을 자식 **레코드 집합** 에 나열 된 절에 의해 선택 사항입니다.  
  
## <a name="syntax"></a>구문  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>Description  
 이 절의 일부는 다음과 같습니다.  
  
 *자식 명령*  
 다음 중 하나를 구성 됩니다.  
  
-   자식 항목을 반환 하는 쿼리 명령이 중괄호 ("{") 안에 **레코드 집합** 개체입니다. 기본 데이터 공급자에는 명령이 실행 될 하 고 해당 공급자의 요구 사항에 해당 구문에 따라 달라 집니다. ADO 특별 한 쿼리 언어 필요 하지 않지만 SQL 언어 같아야 합니다.  
  
-   기존 모양 이름 **레코드 집합**합니다.  
  
-   다른 도형 명령입니다.  
  
-   데이터 공급자에 있는 테이블의 이름이 차례로 나옵니다 테이블 키워드입니다.  
  
 *자식 별칭*  
 별칭 참조 하는 데는 **레코드 집합** 에서 반환 되는 *자식 명령입니다.* *자식 별칭* COMPUTE 절에 있는 열의 목록에이 필요 하 고 부모와 자식 간의 관계를 정의 **레코드 집합** 개체입니다.  
  
 *열 추가-목록*  
 각 요소는 생성 된 부모 열을 정의 목록입니다. 장 열, 새 열, 계산된 열 또는 자식 요소에서 집계 함수를 결과 값을 포함 하는 각 요소 **레코드 집합**합니다.  
  
 *그룹 필드 목록*  
 부모 및 자식 열 목록 **레코드 집합** 자식에서 행을 그룹화 하는 방법을 지정 하는 개체입니다.  
  
 각 열에 대해서는 *그룹-필드 목록에서* 자식 및 부모에 해당 열이 **레코드 집합** 개체입니다. 부모의 각 행에 대해 **레코드 집합**, *그룹 필드 목록* 열의 고유 값이 있고 자식 **레코드 집합** 부모 참조 자식 행 으로만 구성 행을 갖는 *그룹 필드 목록* 열 동일한 부모 행 값을 갖습니다.  
  
 BY 절을 선택한 경우 자식 **레코드 집합**의 행은 COMPUTE 절에 열을 기준으로 그룹화 됩니다. 부모 **레코드 집합** 에 자식 있는 행의 각 그룹에 대해 하나의 행이 포함 됩니다 **레코드 집합**합니다.  
  
 BY 절을 생략 하면 전체 자식 **레코드 집합** 단일 그룹 및 부모도 처리 **레코드 집합** 정확히 한 개의 행이 포함 됩니다. 해당 행은 전체 자식 참조 **레코드 집합**합니다. BY 절을 생략 하면 전체 자식 통해 "총합계" 집계를 계산 하 **레코드 집합**합니다.  
  
 예를 들어 다음과 같이 사용할 수 있습니다.  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 어떤 방식으로 관계 없이 부모 **레코드 집합** 형식이 자식 관련 시키는 데 사용 되는 장 열 포함 됩니다 (COMPUTE를 사용 하 여 또는 APPEND를 사용 하 여) **레코드 집합**합니다. 원하는 경우, 부모 **레코드 집합** 자식 행에 대해 집계 (SUM, MIN, MAX, 및 등)를 포함 하는 열이 포함 될 수 있습니다. 부모와 자식 **레코드 집합** 의 행에는 식을 포함 하는 열이 포함 될는 **레코드 집합**뿐만 아니라 새로운과 처음 있는 열이 비어 있습니다.  
  
## <a name="operation"></a>연산  
 *자식 명령* 공급자 자식을 반환는 발급 **레코드 집합**합니다.  
  
 COMPUTE 절에 지정 된 부모 열 **레코드 집합**, 자식에 대 한 참조가 발생할 수 있는 **레코드 집합**, 하나 이상의 집계, 계산 된 식 또는 새 열입니다. 열 정의 부모에도 추가 됩니다 BY 절이 없으면 **레코드 집합**합니다. BY 절은 지정 방법을 자식 행 **레코드 집합** 그룹화 됩니다.  
  
 예를 들어 한 테이블, 명명 된 인구 통계 상태, City, 및 채우기 필드 요소로 이루어진 있다고 가정 합니다. (테이블에 채우기 수치를 예제로만 제공 됩니다).  
  
|State|City|모집단|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|또는|Medford|200,000|  
|또는|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|샌디에고|600,000|  
|WA|Tacoma|500,000|  
|또는|Corvallis|300,000|  
  
 이제이 shape 명령을 실행 합니다.  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 이 명령은 엽니다는 셰이핑된 **레코드 집합** 두 수준입니다. 부모 수준으로 생성 된은 **레코드 집합** 집계 열이 있는 (`SUM(rs.population)`) 자식 참조 하는 열, **레코드 집합** (`rs`), 및 자식 그룹화에대한열**레코드 집합** (`state`). 자식 수준은 **레코드 집합** 쿼리 명령에서 반환 된 (`select * from demographics`).  
  
 자식 **레코드 집합** 상태별로 그룹화 된 하지만 임의의 순서로 그렇지 않으면 세부 행이 됩니다. 즉, 그룹 알파벳순 이나 숫자순 순서로 되지 않습니다. 부모를 원하는 경우 **레코드 집합** 정렬할 수를 사용할 수 있습니다는 **레코드 집합 정렬** 메서드를 부모 요청 **레코드 집합**합니다.  
  
 이제 열린된 부모를 탐색할 수 있습니다 **레코드 집합** 자식 세부 정보에 액세스 하 고 **레코드 집합** 개체입니다. 자세한 내용은 참조 [계층적 레코드 집합에서 행 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)합니다.  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>결과 부모 및 자식 세부 레코드 집합  
  
### <a name="parent"></a>Parent  
  
|SUM (rs 합니다. 채우기)|rs|State|  
|---------------------------|--------|-----------|  
|1,300,000|자식 1에 대 한 참조|CA|  
|1,200,000|자식 2에 대 한 참조|WA|  
|1,100,000|Child3에 대 한 참조|또는|  
  
## <a name="child1"></a>Child1  
  
|State|City|모집단|  
|-----------|----------|----------------|  
|CA|Los Angeles|800,000|  
|CA|샌디에고|600,000|  
  
## <a name="child2"></a>자식 2  
  
|State|City|모집단|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|WA|Tacoma|500,000|  
  
## <a name="child3"></a>Child3  
  
|State|City|모집단|  
|-----------|----------|----------------|  
|또는|Medford|200,000|  
|또는|Portland|400,000|  
|또는|Corvallis|300,000|  
  
## <a name="see-also"></a>관련 항목:  
 [계층적 레코드 집합의 행에 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [데이터 셰이핑 개요](../../../ado/guide/data/data-shaping-overview.md)   
 [Field 개체](../../../ado/reference/ado-api/field-object.md)   
 [형식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [데이터 모양 지정에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [셰이프 APPEND 절](../../../ado/guide/data/shape-append-clause.md)   
 [일반적으로 shape 명령](../../../ado/guide/data/shape-commands-in-general.md)   
 [Value 속성 (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic for Applications 기능](../../../ado/guide/data/visual-basic-for-applications-functions.md)
