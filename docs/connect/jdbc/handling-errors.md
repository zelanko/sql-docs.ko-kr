---
title: 오류 처리 | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a69bf1d98d666b0b4b76be604abc31e28958adb4
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66781703"
---
# <a name="handling-errors"></a>오류 처리
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 사용하면 모든 데이터베이스 오류 조건이 [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) 클래스를 통해 Java 애플리케이션에 예외로 반환됩니다. 다음 SQLServerException 클래스의 메서드는 java.sql.SQLException 및 java.lang.Throwable에서 상속되며, 발생한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류에 대한 세부 정보를 반환하는 데 사용합니다.  
  
-   `getSQLState()`는 표준 X/Open 또는 SQL99 예외의 상태 코드를 반환합니다.
  
-   `getErrorCode()`는 특정 데이터베이스 오류 번호를 반환합니다.
  
-   `getMessage()`는 예외의 전체 텍스트를 반환합니다. 오류 메시지 텍스트에는 문제에 대한 설명이 나와 있으며, 표시될 때 오류 메시지에 삽입된 개체 이름 같은 정보에 대한 자리 표시자가 자주 포함되어 있습니다.
  
-   `getNextException()`은 다음 `SQLServerException` 개체를 반환하거나 반환할 예외 개체가 없는 경우 null을 반환합니다.

-   `getSQLServerError()` 반환 된 `SQLServerError` SQL Server에서 수신 된 예외에 대 한 자세한 정보를 포함 하는 개체입니다. 이 메서드가 없는 서버 오류가 발생 하는 경우 null을 반환 합니다.

다음 메서드는 `SQLServerError` 클래스는 서버에서 생성 된 오류에 대 한 추가 세부 정보를 가져오는 데 사용할 수 있습니다.

-   `SQLServerError.getErrorMessage()` 서버에서 받은 오류 메시지를 반환 합니다.

-   `SQLServerError.getErrorNumber()` 오류의 형식을 식별 하는 숫자를 반환 합니다.

-   `SQLServerError.getErrorState()` 오류, 경고 또는 "데이터 없음" 메시지를 나타내는 SQL Server에서 숫자 오류 코드를 반환 합니다.

-   `SQLServerError.getErrorSeverity()` 수신 된 오류의 심각도 반환 합니다.

-   `SQLServerError.getServerName()` 오류를 생성 하는 SQL Server의 인스턴스를 실행 하는 컴퓨터의 이름을 반환 합니다.

-   `SQLServerError.getProcedureName()` 저장된 프로시저 또는 오류를 발생 시킨 원격 프로시저 호출 (RPC)의 이름을 반환 합니다.

-   `SQLServerError.getLineNumber()` TRANSACT-SQL 명령 일괄 처리 또는 오류를 생성 하는 저장된 프로시저의 줄 번호를 반환 합니다.
  
 다음 예제에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대해 열린 연결을 함수로 전달하고, FROM 절이 없는 잘못된 형식의 SQL 문을 생성합니다. 그런 다음 이 문을 실행하고 SQL 예외를 처리합니다.  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 관련 문제 진단](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
