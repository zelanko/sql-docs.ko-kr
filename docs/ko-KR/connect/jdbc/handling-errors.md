---
title: 오류 처리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33f9c9daa495c26b1a1e35869016f0e7382d9d1a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="handling-errors"></a>오류 처리
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  사용 하는 경우는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], 모든 데이터베이스 오류 조건이 예외를 사용 하 여 Java 응용 프로그램에 반환 되는 [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) 클래스입니다. SQLServerException 클래스의 다음 메서드는 java.sql.SQLException 및 java.lang.Throwable에서 상속 에 대 한 특정 정보를 반환 하는 데 사용 될 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 발생 한 오류:  
  
-   getSQLState는 표준 X / Open 또는 SQL99 상태 코드는 예외를 반환합니다.  
  
-   getErrorCode 특정 데이터베이스 오류 번호를 반환합니다.  
  
-   getMessage 예외의 전체 텍스트를 반환합니다. 오류 메시지 텍스트에는 문제에 대한 설명이 나와 있으며, 표시될 때 오류 메시지에 삽입된 개체 이름 같은 정보에 대한 자리 표시자가 자주 포함되어 있습니다.  
  
-   getNextException 반환할 예외 개체가 없는 경우 다음 SQLServerException 개체 또는 null을 반환 합니다.  
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스에 함수에 전달 하 고 FROM 절이 없는 잘못 된 형식의 SQL 문을 생성 합니다. 그런 다음 이 문을 실행하고 SQL 예외를 처리합니다.  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 관련 문제 진단](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
