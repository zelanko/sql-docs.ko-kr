---
title: 외부 조인 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81988d34dca38d5c041ff9f87e9674d7c97d76cc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282451"
---
# <a name="outer-joins"></a>외부 조인
ODBC는 SQL-92 왼쪽, 오른쪽 및 전체 외부 조인 구문을 지원합니다. 외부 조인에 대한 이스케이프 시퀀스는  
  
 **{oj** _외부 조인_**}**  
  
 *외부 조인이* 있는 위치  
  
 *테이블 참조* {**왼쪽 &#124; 오른쪽 &#124; FULL} 외부 조인** { 테이블*참조* &#124; *외부 조인*} **on** _검색 조건_  
  
 *테이블 참조는* 테이블 이름을 지정하고 *검색 조건은* *테이블 참조*사이의 조인 조건을 지정합니다.  
  
 외부 조인 요청은 **FROM** 키워드 다음과 **WHERE** 절(있는 경우)앞에 나타나야 합니다. 전체 구문 정보는 부록 C: SQL 문법의 [외부 조인 이스케이프 시퀀스를](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) 참조하십시오.  
  
 예를 들어 다음 SQL 문은 모든 고객을 나열하고 미달 주문이 있는 것을 표시하는 동일한 결과 집합을 만듭니다. 첫 번째 문은 이스케이프 시퀀스 구문을 사용합니다. 두 번째 문은 Oracle의 기본 구문을 사용하며 상호 운용할 수 없습니다.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 데이터 원본 및 드라이버 가 지원하는 외부 조인 유형을 확인하려면 응용 프로그램에서 **sqlGetInfo를** SQL_OJ_CAPABILITIES 플래그를 호출합니다. 지원될 수 있는 외부 조인 유형은 왼쪽, 오른쪽, 전체 또는 중첩된 외부 조인입니다. 외부 조인은 **ON** 절의 열 이름이 **OUTER JOIN** 절의 해당 테이블 이름과 동일한 순서를 갖지 않습니다. 외부 조인과 함께 내부 조인; 및 외부 는 모든 ODBC 비교 연산자를 사용하여 조인합니다. SQL_OJ_CAPABILITIES 정보 유형이 0을 반환하는 경우 외부 조인 절이 지원되지 않습니다.
