---
title: 외부 조인 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequences [ODBC]
- escape sequences [ODBC], outer join
ms.assetid: be1a0203-5da9-4871-9566-4bd3fbc0895c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15ab82f5623bad7d3c82729dfd9077ac967301e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914358"
---
# <a name="outer-joins"></a>외부 조인
ODBC는 sql-92 left, right 및 완전 외부 조인 구문을 지원합니다. 외부 조인에 대 한 이스케이프 시퀀스는  
  
 **{oj** *외부-조인 * * *을 (를)**  
  
 여기서 *외부 조인* 은  
  
 *테이블 참조* {**왼쪽 &#124; 오른쪽 &#124; 전체을 (를) 외부 조인** {*테이블 참조* &#124; *외부 조인*} **ON**  *검색 조건*  
  
 *테이블 참조* 테이블 이름을 지정 하 고 *검색 조건* 간의 조인 조건을 지정는 *테이블 참조*합니다.  
  
 외부 조인 요청이 뒤에 나타나야 합니다는 **FROM** 키워드 및 하기 전에 **여기서** 절 (있는 경우). 전체 구문 정보에 대 한 참조 [외부 조인 이스케이프 시퀀스](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) 부록 c: SQL 문법에 있습니다.  
  
 예를 들어 다음 SQL 문을 모든 고객을 나열 되 고 열기는 orders가 표시 하는 동일한 결과 집합을 만듭니다. 첫 번째 문은 이스케이프 시퀀스 구문을 사용합니다. 두 번째 문은 Oracle에서는 기본 구문을 사용 하 고 상호 운용 되지 않습니다.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 데이터 소스와 드라이버가 지 원하는 외부 조인의 종류를 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** 는 SQL_OJ_CAPABILITIES와 플래그를 지정 합니다. 지원 될 수 있는 외부 조인 유형에 왼쪽, 오른쪽, 전체 또는 중첩 된 외부 조인; 외부 조인에 열 이름에 **ON** 절에서 각 테이블 이름와 순서가 동일 하지 않은 **OUTER JOIN** 절; 외부 조인이; 및 외부 조인을 사용 하 여 함께 내부 조인 모든 ODBC 비교 연산자입니다. SQL_OJ_CAPABILITIES 정보 유형 0을 반환 하면 외부 조인 절 없이 사용할 수 있습니다.
