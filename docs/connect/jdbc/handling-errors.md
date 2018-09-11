---
title: 오류 처리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eee315022a94795dd27ae8ae7fee6cc784912bec
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42783897"
---
# <a name="handling-errors"></a>오류 처리
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 사용하면 모든 데이터베이스 오류 조건이 [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) 클래스를 통해 Java 응용 프로그램에 예외로 반환됩니다. 다음 SQLServerException 클래스의 메서드는 java.sql.SQLException 및 java.lang.Throwable에서 상속되며, 발생한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류에 대한 세부 정보를 반환하는 데 사용합니다.  
  
-   getSQLState는 표준 X/Open 또는 SQL99 예외의 상태 코드를 반환합니다.  
  
-   getErrorCode는 특정 데이터베이스 오류 번호를 반환합니다.  
  
-   getMessage는 예외의 전체 텍스트를 반환합니다. 오류 메시지 텍스트에는 문제에 대한 설명이 나와 있으며, 표시될 때 오류 메시지에 삽입된 개체 이름 같은 정보에 대한 자리 표시자가 자주 포함되어 있습니다.  
  
-   getNextException 반환할 예외 개체가 없는 경우 다음 SQLServerException 개체 또는 null을 반환 합니다.  
  
 다음 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대해 열린 연결을 함수로 전달하고, FROM 절이 없는 잘못된 형식의 SQL 문을 생성합니다. 그런 다음 이 문을 실행하고 SQL 예외를 처리합니다.  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 관련 문제 진단](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
