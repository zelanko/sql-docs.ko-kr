---
title: Shape COMPUTE 절 | Microsoft Docs
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
ms.openlocfilehash: fa6862808643f3d687fa406cb3fc2aa23c9b7d7b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924140"
---
# <a name="shape-compute-clause"></a>셰이프 COMPUTE 절
Shape COMPUTE 절은 열이 자식 **레코드 집합**에 대 한 참조로 구성 된 부모 **레코드 집합**을 생성 합니다. 내용에 장, 새 열 또는 계산 된 열 또는 자식 **레코드** 집합에 대 한 집계 함수를 실행 한 결과 또는 이전에 지정한 **레코드 집합**에서 집계 함수를 실행 한 결과 선택적 BY 절에 나열 된 자식 **레코드 집합** 의 모든 열  
  
## <a name="syntax"></a>구문  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>Description  
 이 절의 부분은 다음과 같습니다.  
  
 *자식-명령*  
 다음 중 하나로 구성 됩니다.  
  
-   자식 **레코드 집합** 개체를 반환 하는{}중괄호 ("") 내의 쿼리 명령입니다. 명령은 기본 데이터 공급자에 대해 실행 되며 해당 구문은 해당 공급자의 요구 사항에 따라 달라 집니다. ADO에 특정 쿼리 언어가 필요 하지는 않지만 일반적으로 SQL 언어입니다.  
  
-   기존 모양의 **레코드 집합**의 이름입니다.  
  
-   다른 shape 명령입니다.  
  
-   테이블 키워드와 데이터 공급자의 테이블 이름이 차례로 나옵니다.  
  
 *자식 별칭*  
 자식 명령에서 반환 된 **레코드 집합** 을 참조 하는 데 사용 되는 별칭 *입니다.* *자식 별칭* 은 COMPUTE 절의 열 목록에 필요 하며 부모 및 자식 **레코드 집합** 개체 간의 관계를 정의 합니다.  
  
 *추가 된 열 목록*  
 각 요소가 생성 된 부모에서 열을 정의 하는 목록입니다. 각 요소에는 장 열, 새 열, 계산 열 또는 자식 **레코드 집합**에 대 한 집계 함수로 생성 된 값이 포함 됩니다.  
  
 *그룹 필드 목록*  
 자식에서 행을 그룹화 하는 방법을 지정 하는 부모 및 자식 **레코드 집합** 개체의 열 목록입니다.  
  
 *Grp-필드 목록의* 각 열에 대해 자식 및 부모 **레코드 집합** 개체에 해당 하는 열이 있습니다. 부모 **레코드 집합**의 각 행에 대해 *그룹 필드 목록* 열에는 고유한 값이 있고 부모 행에서 참조 하는 자식 **레코드 집합** 은 부모 행과 동일한 값을 *갖는 자식* 행 으로만 구성 됩니다.  
  
 BY 절이 포함 된 경우 자식 **레코드 집합**의 행은 COMPUTE 절의 열을 기준으로 그룹화 됩니다. 부모 **레코드 집합** 은 자식 **레코드 집합**의 각 행 그룹에 대해 하나의 행을 포함 합니다.  
  
 BY 절을 생략 하면 전체 자식 **레코드 집합이** 단일 그룹으로 처리 되 고 부모 **레코드 집합** 에는 정확히 한 개의 행이 포함 됩니다. 해당 행은 전체 하위 **레코드 집합**을 참조 합니다. BY 절을 생략 하면 전체 하위 **레코드 집합**에 대 한 "총합계" 집계를 계산할 수 있습니다.  
  
 예를 들면 다음과 같습니다.  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 계산 또는 추가를 사용 하 여 부모 **레코드 집합** 을 구성 하는 방법에 관계 없이 자식 **레코드 집합**에 연결 하는 데 사용 되는 챕터 열이 포함 됩니다. 원하는 경우 부모 **레코드 집합** 에 자식 행에 대 한 집계 (SUM, MIN, MAX 등)가 포함 된 열이 포함 될 수도 있습니다. 부모 및 자식 **레코드 집합** 모두에는 **레코드 집합**의 행에 식이 포함 된 열이 포함 될 수 있으며 처음에는 비어 있는 열도 포함 될 수 있습니다.  
  
## <a name="operation"></a>작업(Operation)  
 자식 *명령은* 공급자에 게 실행 되어 자식 **레코드 집합**을 반환 합니다.  
  
 COMPUTE 절은 부모 **레코드 집합**의 열을 지정 합니다 .이 열은 자식 **레코드 집합**, 하나 이상의 집계, 계산 식 또는 새 열에 대 한 참조일 수 있습니다. BY 절이 있는 경우 정의 하는 열도 부모 **레코드 집합**에 추가 됩니다. BY 절은 자식 **레코드 집합** 의 행을 그룹화 하는 방법을 지정 합니다.  
  
 예를 들어 상태, 구/군/시 및 인구 필드로 구성 된 인구 통계 라는 테이블이 있다고 가정 합니다. (테이블의 채우기 수치는 한 가지 예로만 제공 됩니다.)  
  
|시스템 상태|City|모집단|  
|-----------|----------|----------------|  
|WA|Seattle|70만|  
|또는|Medford|200,000|  
|또는|Portland|400,000|  
|CA|Los Angeles|80만|  
|CA|샌디에이고|60만|  
|WA|Tacoma|500,000|  
|또는|Corvallis|300,000|  
  
 이제 다음 셰이프 명령을 실행 합니다.  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 이 명령은 두 수준이 있는 모양 있는 **레코드 집합** 을 엽니다. 부모 수준은 집계 열 (`SUM(rs.population)`), 자식 **레코드 집합** `rs`을 참조 하는 열 () 및 자식 **레코드 집합** (`state`)을 그룹화 하는 열을 포함 하는 생성 된 **레코드 집합** 입니다. 자식 수준은 쿼리 명령 (`select * from demographics`)에서 반환 하는 **레코드 집합** 입니다.  
  
 자식 **레코드 집합** 정보 행은 상태별로 그룹화 되지만 그렇지 않은 경우에는 특정 순서로 그룹화 되지 않습니다. 즉, 그룹이 사전순 또는 숫자로 정렬 되지 않습니다. 부모 **레코드 집합** 을 정렬 하려는 경우에는 **레코드 집합 정렬** 메서드를 사용 하 여 부모 **레코드 집합**의 순서를 지정할 수 있습니다.  
  
 이제 열린 부모 **레코드 집합** 을 탐색 하 고 자식 세부 정보 **레코드 집합** 개체에 액세스할 수 있습니다. 자세한 내용은 [계층적 레코드 집합의 행에 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)를 참조 하세요.  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>결과 부모 및 자식 세부 정보 레코드 집합  
  
### <a name="parent"></a>Parent  
  
|합계 (rs. 표본의|rs|시스템 상태|  
|---------------------------|--------|-----------|  
|130만|자식 1에 대 한 참조|CA|  
|120만|자식 2에 대 한 참조|WA|  
|110만|Child3에 대 한 참조|또는|  
  
## <a name="child1"></a>Child1  
  
|시스템 상태|City|모집단|  
|-----------|----------|----------------|  
|CA|Los Angeles|80만|  
|CA|샌디에이고|60만|  
  
## <a name="child2"></a>Child2  
  
|시스템 상태|City|모집단|  
|-----------|----------|----------------|  
|WA|Seattle|70만|  
|WA|Tacoma|500,000|  
  
## <a name="child3"></a>Child3  
  
|시스템 상태|City|모집단|  
|-----------|----------|----------------|  
|또는|Medford|200,000|  
|또는|Portland|400,000|  
|또는|Corvallis|300,000|  
  
## <a name="see-also"></a>참고 항목  
 [계층적 레코드 집합의 행 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [데이터 셰이핑 개요](../../../ado/guide/data/data-shaping-overview.md)   
 [Field 개체](../../../ado/reference/ado-api/field-object.md)   
 [공식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [데이터 셰이핑에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 절](../../../ado/guide/data/shape-append-clause.md)   
 [Shape 명령 일반](../../../ado/guide/data/shape-commands-in-general.md)   
 [Value 속성 (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic for Applications 기능](../../../ado/guide/data/visual-basic-for-applications-functions.md)
