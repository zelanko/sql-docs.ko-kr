---
title: 셰이프 COMPUTE 절 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e1e268da5eb4c53b6270e474987c69b88383cd9b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700352"
---
# <a name="shape-compute-clause"></a>셰이프 COMPUTE 절
셰이프 COMPUTE 절 생성 부모 **레코드 집합**, 열이 있는 자식에 대 한 참조를 이루어진 **레코드 집합**; 내용이 새 장에서 또는 계산된 열, 열 또는 자식 요소에서 집계 함수를 실행 한 결과 **Recordset** 이전 가공 **레코드 집합**; 및 자식에서 모든 열 **레코드 집합** 에 나열 된 절에서 선택 사항입니다.  
  
## <a name="syntax"></a>구문  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>Description  
 이 절의 일부는 다음과 같습니다.  
  
 *child-command*  
 다음 중 하나로 구성 됩니다.  
  
-   중괄호 내에서 쿼리 명령 ("{}")를 반환 하는 자식 **레코드 집합** 개체입니다. 기본 데이터 공급자에 게 명령을 실행 하 고 해당 구문은 해당 공급자의 요구 사항에 따라 달라 집니다. ADO 특별 한 쿼리 언어 필요 하지 않지만 SQL 언어에서 일반적으로 됩니다.  
  
-   기존 모양의 이름을 **레코드 집합**합니다.  
  
-   다른 셰이프 명령입니다.  
  
-   데이터 공급자에서 테이블의 이름 뒤에 테이블 키워드입니다.  
  
 *child-alias*  
 참조 하는 데 별칭을 **레코드 집합** 반환한는 *자식 명령입니다.* 합니다 *자식 별칭* COMPUTE 절에 열 목록에서 필요 하 고 부모와 자식 간의 관계 정의 **레코드 집합** 개체입니다.  
  
 *appended-column-list*  
 각 요소는 생성 된 부모에서 열 정의 목록입니다. 장 열, 새 열, 계산된 열 또는 자식에 집계 함수에서 결과 값을 포함 하는 요소당 **레코드 집합**합니다.  
  
 *grp-field-list*  
 부모 및 자식 열 목록이 **레코드 집합** 자식에서 행을 그룹화 하는 방법을 지정 하는 개체입니다.  
  
 각 열에 대해 합니다 *grp-필드-목록* 자식 및 부모에 해당 열이 있는 **레코드 집합** 개체입니다. 상위의 각 행에 대해 **Recordset**, *grp 필드 목록* 열에 고유 값 및 자식 **레코드 집합** 부모 참조 행 으로만 이루어져 자식 행을 갖는 *grp 필드 목록* 열 부모 행을 동일한 값을 갖습니다.  
  
 BY 절이 포함 된 자식 **레코드 집합**의 행에서는 COMPUTE 절에서 열에 따라 그룹화 됩니다. 부모 **Recordset** 각 자식에서 행 그룹에 대해 하나의 행이 포함 됩니다 **Recordset**합니다.  
  
 BY 절을 생략 하는 경우 전체 자식 **Recordset** 부모 단일 그룹으로 취급 됩니다 **레코드 집합** 정확히 하나의 행이 포함 됩니다. 해당 행은 전체 자식 참조 **레코드 집합**합니다. 전체 하위를 통해 "총합계" 집계를 계산할 수 있습니다 BY 절을 생략 **레코드 집합**합니다.  
  
 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 방식에 관계 없이 부모 **Recordset** 형식이 장 열을 자식으로 연결 하는 데 사용 되는 계산을 사용 하 여, 추가 사용 하 여 포함 됩니다 **레코드 집합**합니다. 원한다 면 부모 **레코드 집합** 자식 행에 대해 집계 (SUM, MIN, MAX 및 등)를 포함 하는 열이 포함 될 수 있습니다. 부모와 자식 **레코드 집합** 행이 행에서 식을 포함 하는 열이 포함 될 합니다 **레코드 집합**뿐 아니라 새로운과 처음에 있는 열에서 빈 합니다.  
  
## <a name="operation"></a>연산  
 합니다 *하위 명령* 자식을 반환 하는 공급자에 게 발급 된 **레코드 집합**합니다.  
  
 COMPUTE 절에 지정 된 부모 열 **Recordset**, 자식에 대 한 참조를 일 수 있는 **레코드 집합**, 하나 이상의 집계, 계산 된 식 또는 새 열입니다. 부모 열 정의 추가 됩니다 BY 절에 있으면 **레코드 집합**합니다. BY 절을 지정 하는 방법의 자식 행 **레코드 집합** 그룹화 됩니다.  
  
 예를 들어 라는 테이블을 인구 통계, 상태, 도시 및 채우기 필드로 구성 되어 있는 있다고 가정 합니다. (테이블에서 인구 수치를 예제로만 제공 됩니다).  
  
|State|City|모집단|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|또는|Medford|200,000|  
|또는|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|샌디에이고|600,000|  
|WA|Tacoma|500,000|  
|또는|Corvallis|300,000|  
  
 이제이 shape 명령 실행:  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 이 명령은 모양의 **레코드 집합** 두 수준입니다. 부모 수준이 생성 된 **Recordset** 집계 열을 사용 하 여 (`SUM(rs.population)`), 자식 참조 열 **레코드 집합** (`rs`), 자식 그룹화열과**레코드 집합** (`state`). 자식 수준은 합니다 **Recordset** 쿼리 명령에서 반환 된 (`select * from demographics`).  
  
 자식 **레코드 집합** 상태별로 그룹화 하지만 특정 순서 없이 그렇지 않으면 세부 정보 행이 됩니다. 즉, 그룹 알파벳순 이나 숫자순 순서 대로 되지 않습니다. 부모를 하려는 경우 **레코드 집합** 정렬할를 사용할 수 있습니다 합니다 **레코드 집합 정렬** 부모를 주문 하는 방법 **레코드 집합**합니다.  
  
 이제 열린된 부모를 탐색할 수 있습니다 **Recordset** 자식 세부 정보에 액세스 하 고 **레코드 집합** 개체입니다. 자세한 내용은 [계층적 레코드 집합에서 행 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)합니다.  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>결과 부모 및 자식 세부 정보 레코드 집합  
  
### <a name="parent"></a>Parent  
  
|SUM (rs 합니다. 채우기)|rs|State|  
|---------------------------|--------|-----------|  
|1,300,000|Child1이에 대 한 참조|CA|  
|1,200,000|Child2에 대 한 참조|WA|  
|1,100,000|Child3에 대 한 참조|또는|  
  
## <a name="child1"></a>Child1  
  
|State|City|모집단|  
|-----------|----------|----------------|  
|CA|Los Angeles|800,000|  
|CA|샌디에이고|600,000|  
  
## <a name="child2"></a>Child2  
  
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
  
## <a name="see-also"></a>관련 항목  
 [계층적 레코드 집합의 행에 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [데이터 셰이핑 개요](../../../ado/guide/data/data-shaping-overview.md)   
 [Field 개체](../../../ado/reference/ado-api/field-object.md)   
 [공식적인 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [데이터 셰이프에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [셰이프 APPEND 절](../../../ado/guide/data/shape-append-clause.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)   
 [Value 속성 (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic for Applications 기능](../../../ado/guide/data/visual-basic-for-applications-functions.md)
