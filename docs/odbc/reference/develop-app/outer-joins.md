---
title: 외부 조인 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd35a8bd0e2a9280d16614a3979dc2af05487e42
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619611"
---
# <a name="outer-joins"></a>외부 조인
ODBC는 SQL-92 left, right 및 full outer join 구문을 지원합니다. 외부 조인 이스케이프 시퀀스는  
  
 **{oj** *외부-조인 *}**  
  
 여기서 *외부 조인* 는  
  
 *테이블 참조* {0}**왼쪽 &#124; 오른쪽 &#124; 전체} 외부 조인** {0}*테이블 참조* &#124; *외부 조인*} **ON**  *검색 조건*  
  
 *테이블 참조* 테이블 이름을 지정 하 고 *검색 조건* 간에 조인 조건을 지정 합니다 *테이블 참조*합니다.  
  
 외부 조인 요청을 뒤에 나타나야 합니다.는 **FROM** 키워드 및 하기 전에 **여기서** 절 (있는 경우). 전체 구문 정보를 참조 하세요. [외부 조인 이스케이프 시퀀스](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) 부록 c: SQL 문법에서입니다.  
  
 예를 들어, 다음 SQL 문을 모든 고객을 나열 하 고 열린 주문의 표시 하는 동일한 결과 집합을 만듭니다. 첫 번째 문은 이스케이프 시퀀스가 구문을 사용 합니다. 두 번째 문은 Oracle에 대 한 기본 구문을 사용 하 고 상호 운용은 불가능 합니다.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 응용 프로그램이 호출 데이터 소스와 드라이버를 지 원하는 외부 조인 형식을 결정할 **SQLGetInfo** 는 SQL_OJ_CAPABILITIES를 사용 하 여 플래그를 지정 합니다. 왼쪽, 오른쪽, 전체 또는 중첩 된 외부 조인; 지원 될 수 있는 외부 조인 유형 외부 조인에 열 이름에 **ON** 절에서 해당 테이블 이름으로 동일한 순서 없는 합니다 **OUTER JOIN** 절; 외부 조인이; 및 외부 조인을 사용 하 여 함께 내부 조인 모든 ODBC 비교 연산자입니다. SQL_OJ_CAPABILITIES 정보 유형 0을 반환 하는 경우에 외부 조인 절 없이 지원 됩니다.
