---
title: 반환 상태가 있는 저장된 프로시저를 사용 하 여 | Microsoft Docs
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
ms.assetid: 4b126e95-8458-41d6-af37-fc6662859f19
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd23673239d184117d39da3a47b909cf4ddca9ef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-a-stored-procedure-with-a-return-status"></a>반환 상태가 있는 저장 프로시저 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 상태나 결과 및 매개 변수를 반환 하 호출할 수 있는 저장된 프로시저입니다. 이러한 매개 변수는 대개 저장 프로시저의 성공 또는 실패를 나타내는 데 사용됩니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 제공는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 이러한 종류의 저장된 프로시저를 호출 하 고 반환 하는 데이터를 처리할 수 있는 클래스입니다.  
  
 사용 해야 하는 JDBC 드라이버를 사용 하 여 이러한 종류의 저장된 프로시저를 호출 하는 경우는 `call` 와 함께에서 SQL 이스케이프 시퀀스는 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스 . 에 대 한 구문에서 `call` 반환 상태 매개 변수가 있는 이스케이프 시퀀스는 다음:  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  SQL 이스케이프 시퀀스에 대 한 자세한 내용은 참조 [SQL 이스케이프 시퀀스를 사용 하 여](../../connect/jdbc/using-sql-escape-sequences.md)합니다.  
  
 생성할 때는 `call` 이스케이프 시퀀스를 사용 하 여 반환 상태 매개 변수에 지정 된? 입력 매개 변수를 지정합니다. 이 문자는 저장 프로시저에서 반환될 매개 변수 값에 대한 자리 표시자로 사용됩니다. 사용 하 여 매개 변수의 데이터 형식을 지정 해야 하는 반환 상태 매개 변수에 대 한 값을 지정 하는 [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 저장된 프로시저를 실행 하기 전에 SQLServerCallableStatement 클래스의 메서드.  
  
> [!NOTE]  
>  SQL Server 데이터베이스와 JDBC 드라이버를 사용할 때 registerOutParameter 메서드의 반환 상태 매개 변수에 지정한 값은 항상 java.sql.Types.INTEGER 데이터 형식을 사용 하 여 지정할 수 있는 정수 됩니다.  
  
 또한 registerOutParameter 메서드 반환 상태 매개 변수에 대 한 값을 전달 하는 경우에 매개 변수 뿐만 아니라 저장된 프로시저 호출에서 매개 변수의 서 수 위치에 사용할 데이터 형식 뿐만 아니라를 지정 해야 합니다. 반환 상태 매개 변수인 경우, 항상 저장 프로시저 호출에서 첫 번째 매개 변수이므로 해당 서수 위치는 항상 1입니다. SQLServerCallableStatement 클래스에 특정 매개 변수를 나타내기 위해 매개 변수의 이름을 사용 하 여에 대 한 지원을 제공 하지만 반환 상태 매개 변수에 대 한 매개 변수의 서 수 위치 번호만을 사용할 수 있습니다.  
  
 예를 들어에서 다음과 같은 저장된 프로시저를 만들는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
CREATE PROCEDURE CheckContactCity  
   (@cityName CHAR(50))  
AS  
BEGIN  
   IF ((SELECT COUNT(*)  
   FROM Person.Address  
   WHERE City = @cityName) > 1)  
   RETURN 1  
ELSE  
   RETURN 0  
END  
```  
  
 이 저장 프로시저에서는 cityName 매개 변수에 지정된 도시가 Person.Address 테이블에 있는지 여부에 따라 1 또는 0의 상태 값을 반환합니다.  
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스는 함수에 전달 된 및 [실행](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드 CheckContactCity 저장 프로시저를 호출 하는:  
  
 [!code[JDBC#UsingSprocWithReturnStatus1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_1_1.java)]  
  
## <a name="see-also"></a>관련 항목:  
 [저장 프로시저가 있는 문 사용](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
