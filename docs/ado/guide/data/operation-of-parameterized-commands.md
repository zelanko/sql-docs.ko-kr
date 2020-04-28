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
ms.openlocfilehash: e7d4399a8cf279ed2283061fff9064ffcc1adfba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924732"
---
# <a name="operation-of-parameterized-commands"></a>매개 변수화된 명령 작업
특히 부모 **레코드 집합**의 크기와 비교할 때 큰 자식 **레코드 집합**을 사용 하 여 작업 하는 경우 몇 개의 자식 챕터에만 액세스 해야 하는 경우 매개 변수가 있는 명령을 사용 하는 것이 더 효율적일 수 있습니다.  
  
 *매개 변수가 없는 명령은* 전체 부모 및 자식 **레코드 집합**을 검색 하 고, 부모에 챕터 열을 추가한 다음 각 부모 행에 대 한 관련 자식 챕터에 대 한 참조를 할당 합니다.  
  
 *매개 변수가 있는 명령은* 전체 부모 **레코드 집합**을 검색 하지만 장 열에 액세스할 때 장 **레코드 집합** 을 검색 합니다. 이러한 검색 전략의 차이로 인해 성능이 크게 향상 될 수 있습니다.  
  
 예를 들어 다음을 지정할 수 있습니다.  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 부모 및 자식 테이블에는 공용, *cust_id*열 이름이 있습니다. *하위 명령* 에는 RELATE 절에서 참조 하는 "?" 자리 표시 자가 있습니다. 매개 변수 0 ").  
  
> [!NOTE]
>  PARAMETER 절은 shape 명령 구문에만 관련 됩니다. ADO [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체 또는 [매개 변수](../../../ado/reference/ado-api/parameters-collection-ado.md) 컬렉션에 연결 되어 있지 않습니다.  
  
 매개 변수가 있는 shape 명령이 실행 되 면 다음 작업이 수행 됩니다.  
  
1.  *부모 명령이* 실행 되 고 Customers 테이블에서 부모 **레코드 집합** 을 반환 합니다.  
  
2.  부모 **레코드 집합**에 장 열이 추가 됩니다.  
  
3.  부모 행의 chapter 열에 액세스할 때 매개 변수의 값으로 cust_id 값을 사용 하 여 *자식 명령이* 실행 됩니다.  
  
4.  3 단계에서 만든 데이터 공급자 행 집합의 모든 행은 자식 **레코드 집합**을 채우는 데 사용 됩니다. 이 예에서는 Orders 테이블의 모든 행이 cust_id는 customer. cust_id의 값과 같습니다. 기본적으로 자식 **레코드 집합**은 부모 **레코드 집합** 에 대 한 모든 참조가 해제 될 때까지 클라이언트에 캐시 됩니다. 이 동작을 변경 하려면 **레코드 집합** [동적 속성](../../../ado/reference/ado-api/ado-dynamic-property-index.md) **캐시 자식 행** 을 **False**로 설정 합니다.  
  
5.  검색 된 자식 행, 즉 자식 **레코드 집합**의 챕터에 대 한 참조는 부모 **레코드 집합**의 현재 행에 있는 장 열에 배치 됩니다.  
  
6.  다른 행의 장 열에 액세스할 때 3-5 단계가 반복 됩니다.  
  
 **캐시 자식 행** 동적 속성은 기본적으로 **True** 로 설정 됩니다. 캐싱 동작은 쿼리의 매개 변수 값에 따라 달라 집니다. 단일 매개 변수를 사용 하는 쿼리에서 지정 된 매개 변수 값에 대 한 자식 **레코드 집합** 은 해당 값이 있는 자식에 대 한 요청 간에 캐시 됩니다. 다음 코드에서 이 과정을 보여 줍니다.  
  
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
  
 두 개 이상의 매개 변수가 있는 쿼리에서 캐시 된 자식은 모든 매개 변수 값이 캐시 된 값과 일치 하는 경우에만 사용 됩니다.  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>매개 변수가 있는 명령 및 복잡 한 부모 자식 관계  
 매개 변수가 있는 명령을 사용 하 여 동등 조인 형식 계층의 성능을 향상 시키는 것 외에도 매개 변수가 있는 명령을 사용 하 여 보다 복잡 한 부모-자식 관계를 지원할 수 있습니다. 예를 들어 두 개의 테이블을 포함 하는 약간의 리그 데이터베이스 (team_id, team_name) 및 기타 게임 (date, home_team, visiting_team)으로 구성 되어 있다고 가정 합니다.  
  
 매개 변수가 없는 계층 구조를 사용 하는 경우 각 팀의 자식 **레코드 집합** 에 전체 일정이 포함 되도록 팀과 게임 테이블을 연결할 수 있는 방법이 없습니다. 집 일정 또는도로 일정이 포함 된 챕터를 만들 수 있습니다. 이는 RELATE 절이 폼의 부모-자식 관계 (pc1 = cc1) 및 (pc2 = pc2)를 제한 하기 때문입니다. 따라서 명령에 "team_id 관련 된 home_team team_id visiting_team"가 있는 경우 팀이 자신을 재생 하는 게임만 표시 됩니다. 원하는 것은 "(team_id = home_team) 또는 (team_id = visiting_team)" 이지만 셰이프 공급자는 또는 절을 지원 하지 않습니다.  
  
 원하는 결과를 얻기 위해 매개 변수가 있는 명령을 사용할 수 있습니다. 예를 들면 다음과 같습니다.  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 이 예에서는 SQL WHERE 절의 유연성을 활용 하 여 필요한 결과를 얻을 수 있습니다.  
  
> [!NOTE]
>  WHERE 절을 사용 하는 경우 매개 변수는 text, ntext 및 image에 SQL 데이터 형식을 사용할 수 없습니다. 또는 오류는 다음 설명을 포함 하 `Invalid operator for data type`는 결과입니다..  
  
## <a name="see-also"></a>참고 항목  
 [데이터 셰이핑 예](../../../ado/guide/data/data-shaping-example.md)   
 [공식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
