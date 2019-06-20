---
title: 매개 변수가 있는 명령의 작업 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4001ac5b449609683293cd3174dc4410cabf4c4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701869"
---
# <a name="operation-of-parameterized-commands"></a>매개 변수화된 명령 작업
대규모 자식을 사용 하 여 작업 하는 경우 **레코드 집합**, 특히 부모의 크기에 비해 **레코드 집합**, 하지만 몇 가지 자식 장에서 액세스할 필요가 것이 보다 효율적으로 사용할를 매개 변수가 있는 명령입니다.  
  
 A *매개 변수가 없는 명령* 전체 부모와 자식 검색 **레코드 집합**, 부모에 게 장 열을 추가 하 고 다음 각 부모 행에 대 한 관련된 자식 장 참조 할당 .  
  
 A *명령은 매개 변수화* 전체 부모를 검색 **레코드 집합**, 하지만 장만 검색 **레코드 집합** 장 열에 액세스 하는 경우. 검색 전략의이 차이는 상당한 성능 이점을 얻을 수 있습니다.  
  
 예를 들어, 다음을 지정할 수 있습니다.  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 부모 및 자식 테이블에는 일반적인 cust_id에 열 이름이*합니다.* 합니다 *자식* 에 "?" 자리 표시자를 RELATE 절에서 참조 하는 (즉, "... 매개 변수 0")입니다.  
  
> [!NOTE]
>  매개 변수 절 셰이프 명령 구문은 관련이 있습니다. 두 ADO와 사용 하 여 연결 되어 있지 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체 또는 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션입니다.  
  
 매개 변수가 있는 모양 명령을 실행 하는 경우 결과 다음과 같습니다.  
  
1.  *상위 명령* 실행 되 고 부모 반환 **레코드 집합** Customers 테이블에서.  
  
2.  장 열이 부모에 추가 됩니다 **레코드 집합**합니다.  
  
3.  부모 행의 장 열에 액세스할 때 합니다 *자식* 매개 변수의 값으로는 customer.cust_id의 값을 사용 하 여 실행 됩니다.  
  
4.  3 단계에서 만든 데이터 공급자 행 집합의 모든 행 자식을 채우는 데 사용 됩니다 **레코드 집합**합니다. 이 예는 cust_id customer.cust_id 값과 동일한는 Orders 테이블의 모든 행입니다. 기본적으로 자식 **Recordset**s 클라이언트에서 부모에 대 한 모든 참조 될 때까지 캐시 됩니다 **Recordset** 릴리스됩니다. 이 동작을 변경 하려면 설정 합니다 **Recordset** [동적 속성](../../../ado/reference/ado-api/ado-dynamic-property-index.md) **캐시 자식 행** 를 **False**합니다.  
  
5.  검색된 된 자식 행에 대 한 참조 (자식 장, 즉 **레코드 집합**) 부모의 현재 행의 장 열에 배치 됩니다 **레코드 집합**합니다.  
  
6.  3 ~ 5 단계는 다른 행의 장 열에 액세스할 때 반복 됩니다.  
  
 합니다 **캐시 자식 행** 동적 속성 **True** 기본적으로 합니다. 캐싱 동작을 쿼리 매개 변수 값에 따라 달라 집니다. 단일 매개 변수, 자식 쿼리에서 **레코드 집합** 지정된 된 매개 변수의 값 사이의 값을 가진 자식에 대 한 요청 캐시 됩니다. 다음 코드에서는이 보여 줍니다.  
  
```  
SCmd = "SHAPE {select * from customer} " & _  
         "APPEND({select * from orders where cust_id = ?} " & _  
         "RELATE cust_id TO PARAMETER 0) AS chpCustOrder"  
Rst1.Open sCmd, Cnn1  
Set RstChild = Rst1("chpCustOrder").Value  
Rst1.MoveNext      ' Next cust_id passed to Param 0, & new rs fetched   
                   ' into RstChild.  
Rst1.MovePrevious  ' RstChild now holds cached rs, saving round trip.  
```  
  
 두 개 이상의 매개 변수를 사용 하 여 쿼리에서 캐시 된 자식 매개 변수 값을 모든 캐시 된 값과 일치 하는 경우에 사용 됩니다.  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>매개 변수가 있는 명령 및 복잡 한 부모-자식 관계  
 동등 조인 형식 계층의 성능 향상을 위해 매개 변수가 있는 명령을 사용 하는 것 외에도 매개 변수가 있는 명령은 더 복잡 한 부모-자식 관계를 지원 하기 위해 사용할 수 있습니다. 예를 들어 두 개의 테이블을 사용 하 여 거의 리그 데이터베이스: 구성 된 팀 (team_id, 팀 _ 이름) 및 (날짜, home_team visiting_team) 게임의 기타 하나입니다.  
  
 이러한 방식으로 팀 및 게임 테이블에 연결할 방법이 없기 매개 변수가 없는 계층을 사용 하는 자식 **레코드 집합** 전체 일정을 포함 하는 각 팀에 대 한 합니다. 홈 일정 또는 road 일정을 하나만 포함 하는 장을 만들 수 있습니다. RELATE 절 폼의 부모-자식 관계를 제한 하기 때문에 이것이 (p c 1 = cc1) AND (p c 2 = p c 2). 따라서 "관련 team_id TO home_team, team_id TO visiting_team" 명령을 포함 하는 경우 얻게만 게임 자체 팀 재생 된 위치입니다. 필요한 것은 "(team_id=home_team) 또는 (team_id visiting_team =)", 하지만 셰이프 공급자 OR 절을 지원 하지 않습니다.  
  
 원하는 결과 얻으려면 매개 변수가 있는 명령을 사용할 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 이 예제에서는 필요한 결과 얻기 위해 SQL WHERE 절의 뛰어난 유연성.  
  
> [!NOTE]
>  WHERE 절을 사용 하 여 매개 변수에 사용할 수 없습니다 SQL 데이터 형식을 text, ntext 및 image에 대 한 또는 오류가 발생 하는 경우 다음과 같은 설명을 포함: `Invalid operator for data type`합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)   
 [공식적인 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
