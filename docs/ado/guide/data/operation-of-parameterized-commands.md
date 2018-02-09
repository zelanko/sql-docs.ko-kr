---
title: "작업 매개 변수가 있는 명령의 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d826d5407aabce4baa82b0952cff6c8344944e8
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="operation-of-parameterized-commands"></a>매개 변수가 있는 명령 작업을
큰 자식을 사용 하는 경우 **레코드 집합**, 특히 부모의 크기에 비해 **레코드 집합**만 몇 가지 자식 장 액세스할 필요 하지만 보다 효율적으로 사용할 찾을 수 있습니다는 매개 변수가 있는 명령입니다.  
  
 A *매개 변수가 없는 명령* 전체 부모와 자식 검색 **레코드 집합**부모에 게 장 열이 추가 하 고 다음 각 부모 행에 대 한 관련된 자식 장에 대 한 참조를 할당 .  
  
 A *명령에 매개 변수가* 전체 부모를 검색 **레코드 집합**, 하지만 장만 검색 **레코드 집합** 장 열에 액세스 하는 경우. 이 검색 방법의이 차이로 인해 성능이 크게 향상을 얻을 수 있습니다.  
  
 예를 들어 다음을 지정할 수 있습니다.  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 부모 및 자식 테이블에는 일반적인 cust_id에 열 이름이*합니다.* *자식 명령* 에 "?" RELATE 절에서 참조 하는 자리 표시자 (즉, "... 매개 변수 0")입니다.  
  
> [!NOTE]
>  매개 변수 절 shape 명령 구문을 하는 데에 적용 됩니다. 어느 ADO와 연결 되지 않은 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체 또는 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션입니다.  
  
 매개 변수가 있는 shape 명령을 실행 하는 경우 결과 다음과 같습니다.  
  
1.  *부모 명령이* 실행 되 고 부모 반환 **레코드 집합** Customers 테이블의 합니다.  
  
2.  장 열이 부모에 추가 **레코드 집합**합니다.  
  
3.  부모 행의 장 열에 액세스 하는 경우는 *자식 명령* 매개 변수의 값으로는 customer.cust_id의 값을 사용 하 여 실행 됩니다.  
  
4.  3 단계에서 만든 데이터 공급자 행 집합의 모든 행은 자식을 채우는 데 사용 되 **레코드 집합**합니다. 이 예제는 cust_id에 customer.cust_id의 값과 같으면는 Orders 테이블의 모든 행입니다. 기본적으로 자식 **레코드 집합**s 클라이언트에서 부모에 대 한 모든 참조 될 때까지 캐시 됩니다 **레코드 집합** 해제 됩니다. 이 동작을 변경 하려면 설정는 **레코드 집합** [동적 속성](../../../ado/reference/ado-api/ado-dynamic-property-index.md) **캐시 자식 행** 를 **False**합니다.  
  
5.  검색된 된 자식 행에 대 한 참조 (자식 장, 즉 **레코드 집합**) 부모의 현재 행의 장 열에 배치 **레코드 집합**합니다.  
  
6.  3-5 단계는 다른 행의 장 열에 액세스할 때 반복 됩니다.  
  
 **캐시 자식 행** 동적 속성이로 설정 되어 **True** 기본적으로 합니다. 캐싱 동작 쿼리의 매개 변수 값에 따라 달라 집니다. 단일 매개 변수, 자식 쿼리에서 **레코드 집합** 지정된 된 매개 변수의 값 사이의 값을 가진 자식에 대 한 요청 캐시 됩니다. 다음 코드에서는이 보여 줍니다.  
  
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
  
 두 개 이상의 매개 변수가 있는 쿼리에서 캐시 된 자식 모든 매개 변수 값에는 캐시 된 값과 일치 하는 경우에 사용 됩니다.  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>매개 변수가 있는 명령 및 복잡 한 부모-자식 관계  
 매개 변수가 있는 명령을 사용 하 여 동등 조인 유형 계층의 성능을 향상 시킬 수를 매개 변수화 된 명령은 더 복잡 한 부모-자식 관계를 지원 하기 위해 사용할 수 있습니다. 예를 들어 두 개의 테이블이 포함 된 작은 리그 데이터베이스가 있다고 가정: (team_id, 팀 _ 이름)는 팀 및 다른의 게임 (날짜, home_team, visiting_team)으로 구성 된 하나입니다.  
  
 방식으로 팀 및 게임 테이블 방법이 있으면 매개 변수가 없는 계층 구조를 사용 하는 자식 **레코드 집합** 각 팀 전체 일정이 포함에 대 한 합니다. 홈 일정 또는로 일정을 하나만 포함 하는 장을 만들 수 있습니다. RELATE 절 폼의 부모-자식 관계를 제한 하기 때문에 이것이 (pc1 cc1 =) AND (p c 2 = p c 2). 따라서 명령 "RELATE team_id TO home_team, team_id TO visiting_team"를 포함 하는 경우 얻을 수만 게임 자체 팀을 여기서 재생 합니다. 원하는 대로 "(team_id=home_team) 또는 (team_id visiting_team =)", 하지만 셰이프 공급자 OR 절을 지원 하지 않습니다.  
  
 원하는 결과 얻으려면 매개 변수가 있는 명령을 사용할 수 있습니다. 예를 들어  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 이 예제에서는 필요한 결과 얻기 위해 SQL WHERE 절은 보다 유연 하 게를 이용 합니다.  
  
> [!NOTE]
>  WHERE 절을 사용 하 여 매개 변수에 사용할 수 없습니다 SQL 데이터 형식을 text, ntext 및 image에 대 한 시기나 하는 오류가 발생 합니다 다음과 같은 설명이 포함 된: `Invalid operator for data type`합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 예제를 셰이핑](../../../ado/guide/data/data-shaping-example.md)   
 [형식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
