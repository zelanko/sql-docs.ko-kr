---
title: 출력 매개 변수가 있는 저장 프로시저 사용 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea98438694963986c31f0dbb7dddecfb5caa9da6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610831"
---
# <a name="using-a-stored-procedure-with-output-parameters"></a>출력 매개 변수가 있는 저장 프로시저 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

호출할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저는 OUT 매개 변수를 하나 이상 반환하는 저장 프로시저입니다. 여기서 매개 변수는 저장 프로시저에서 데이터를 호출 응용 프로그램으로 다시 반환하는 데 사용됩니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 이러한 종류의 저장 프로시저를 호출하여 반환되는 데이터를 처리하는 데 사용할 수 있는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스를 제공합니다.

JDBC 드라이버를 사용하여 이러한 종류의 저장 프로시저를 호출하는 경우에는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 메서드와 함께 `call` SQL 이스케이프 시퀀스를 사용해야 합니다. OUT 매개 변수가 있는 `call` 이스케이프 시퀀스의 구문은 다음과 같습니다.

`{call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> SQL 이스케이프 시퀀스에 대 한 자세한 내용은 참조 하세요. [SQL 이스케이프 시퀀스를 사용 하 여](../../connect/jdbc/using-sql-escape-sequences.md)입니다.

`call` 이스케이프 시퀀스를 만드는 경우 물음표(?) 문자를 사용하여 입력 매개 변수를 지정합니다. 이 문자는 저장 프로시저에서 반환될 매개 변수 값에 대한 자리 표시자로 사용됩니다. OUT 매개 변수에 대한 값을 지정하려면 저장 프로시저를 실행하기 전에 SQLServerCallableStatement 클래스의 [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 메서드를 사용하여 각 매개 변수의 데이터 형식을 지정해야 합니다.

registerOutParameter 메서드에서 OUT 매개 변수에 대해 지정하는 값은 java.sql.Types에 들어 있는 JDBC 데이터 형식 중 하나여야 합니다. 또한 이 값은 네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 중 하나에 매핑됩니다. JDBC에 대 한 자세한 내용은 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 참조 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)합니다.

OUT 매개 변수에 대한 registerOutParameter 메서드에 값을 전달하는 경우 해당 매개 변수에 사용할 데이터 형식은 물론 저장 프로시저 호출에서 매개 변수의 서수 위치 또는 매개 변수의 이름도 지정해야 합니다. 예를 들어, 저장 프로시저에 하나의 출력 매개 변수가 들어 있는 경우 서수 값은 1이 됩니다. 또한 저장 프로시저에 출력 매개 변수가 두 개이면 첫 번째 서수 값은 1이고 두 번째 서수 값은 2가 됩니다.

> [!NOTE]  
> JDBC 드라이버에서는 OUT 매개 변수로 CURSOR, SQLVARIANT, TABLE 및 TIMESTAMP와 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식을 사용할 수 없습니다.

이에 대한 예로 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 다음 저장 프로시저를 만듭니다.

```sql
CREATE PROCEDURE GetImmediateManager  
   @employeeID INT,  
   @managerID INT OUTPUT  
AS  
BEGIN  
   SELECT @managerID = ManagerID
   FROM HumanResources.Employee
   WHERE EmployeeID = @employeeID  
END
```

이 저장 프로시저에서는 정수인 지정한 입력 매개 변수(employeeID)를 토대로 하여 마찬가지로 정수인 단일 출력 매개 변수(managerID)를 반환합니다. 출력 매개 변수에 반환되는 값은 HumanResources.Employee 테이블에 들어 있는 EmployeeID를 토대로 한 ManagerID입니다.

다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대해 열린 연결을 함수로 전달하고 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드를 사용하여 GetImmediateManager 저장 프로시저를 호출합니다.

```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");) {  
        cstmt.setInt(1, 5);  
        cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt(2));  
    }  
}
```

다음 예에서는 서수 위치를 사용하여 매개 변수를 식별합니다. 서수 위치 대신 이름을 사용하여 매개 변수를 식별할 수도 있습니다. 다음 코드 예에서는 이전 예를 수정하여 Java 응용 프로그램에서 명명된 매개 변수를 사용하는 방법을 설명합니다. 매개 변수 이름은 저장 프로시저의 정의에 있는 매개 변수 이름에 해당합니다.

```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}"); ) {  
        cstmt.setInt("employeeID", 5);  
        cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
    }  
}
```

> [!NOTE]  
> 이러한 예제는 저장된 프로시저를 실행 하려면 SQLServerCallableStatement 클래스의 execute 메서드를 사용 합니다. 이 메서드를 사용하는 이유는 저장 프로시저에서 결과 집합을 반환하지 않았기 때문입니다. 저장 프로시저에서 결과 집합을 반환한 경우에는 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 메서드를 사용합니다.

저장 프로시저는 업데이트 횟수 및 다중 결과 집합을 반환할 수 있습니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 OUT 매개 변수를 검색하기 전에 다중 결과 집합 및 업데이트 횟수를 검색해야 한다는 JDBC 3.0 사양을 따릅니다. 즉, 응용 프로그램의 모든 결과 집합 개체를 검색 하 고 CallableStatement.getter 메서드를 사용 하 여 OUT 매개 변수를 검색 하기 전에 개수를 업데이트 해야 합니다. 그렇지 않으면 이미 검색되지 않은 ResultSet 개체와 업데이트 회수는 OUT 매개 변수를 검색할 때 손실됩니다. 업데이트 횟수에 대 한 자세한 정보 및 다중 결과 집합에 대 한 참조 [업데이트 횟수가 있는 저장 프로시저를 사용 하 여](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) 하 고 [사용 하 여 여러 결과 집합을](../../connect/jdbc/using-multiple-result-sets.md)입니다.

## <a name="see-also"></a>참고 항목

[저장 프로시저가 있는 문 사용](../../connect/jdbc/using-statements-with-stored-procedures.md)
