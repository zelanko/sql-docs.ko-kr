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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81988d34dca38d5c041ff9f87e9674d7c97d76cc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282451"
---
# <a name="outer-joins"></a>외부 조인
ODBC는 SQL-92 left, right 및 full outer join 구문을 지원 합니다. 외부 조인의 이스케이프 시퀀스는  
  
 **{oj** _외부 조인_**}**  
  
 여기서 *outer join* 은  
  
 *테이블-참조* {**LEFT &#124; RIGHT &#124; FULL} 외부 조인** {*table-reference* &#124; *outer join* **}** _(검색 조건)_  
  
 테이블 *참조* 는 테이블 이름을 지정 하 고, *검색 조건은* *테이블 참조*사이의 조인 조건을 지정 합니다.  
  
 외부 조인 요청은 **FROM** 키워드 뒤와 **WHERE** 절 (있는 경우) 앞에 나와야 합니다. 전체 구문에 대 한 자세한 내용은 부록 C: SQL 문법의 [외부 조인 이스케이프 시퀀스](../../../odbc/reference/appendixes/outer-join-escape-sequence.md) 를 참조 하세요.  
  
 예를 들어 다음 SQL 문은 모든 고객을 나열 하는 동일한 결과 집합과 열린 주문이 있는 표시를 만듭니다. 첫 번째 문은 이스케이프 시퀀스 구문을 사용 합니다. 두 번째 문은 Oracle의 네이티브 구문을 사용 하며 상호 운용할 수 없습니다.  
  
```  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM {oj Customers LEFT OUTER JOIN Orders ON Customers.CustID=Orders.CustID}  
   WHERE Orders.Status='OPEN'  
  
SELECT Customers.CustID, Customers.Name, Orders.OrderID, Orders.Status  
   FROM Customers, Orders  
   WHERE (Orders.Status='OPEN') AND (Customers.CustID= Orders.CustID(+))  
```  
  
 데이터 소스 및 드라이버에서 지 원하는 외부 조인의 유형을 확인 하기 위해 응용 프로그램은 SQL_OJ_CAPABILITIES 플래그를 사용 하 여 **SQLGetInfo** 를 호출 합니다. 지원 될 수 있는 외부 조인 유형은 왼쪽, 오른쪽, 전체 또는 중첩 된 외부 조인입니다. **ON** 절의 열 이름이 **outer join** 절에 있는 해당 테이블 이름과 순서가 같지 않은 외부 조인 외부 조인과 함께 내부 조인 모든 ODBC 비교 연산자를 사용 하 여 outer join을 사용 합니다. SQL_OJ_CAPABILITIES 정보 유형이 0을 반환 하는 경우에는 outer join 절이 지원 되지 않습니다.
