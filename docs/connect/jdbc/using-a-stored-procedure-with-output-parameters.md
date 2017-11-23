---
title: "저장된 프로시저를 사용 하 여 출력 매개 변수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
caps.latest.revision: "29"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 7dc04aac6bf9ec53b72705322ebe7f056caf8bfb
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="using-a-stored-procedure-with-output-parameters"></a>출력 매개 변수가 있는 저장 프로시저 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  A [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 호출할 수 있는 저장된 프로시저는 하나를 반환 하는 하나 또는 호출 응용 프로그램에 다시 OUT 매개 변수는 저장된 프로시저 사용 하 여 데이터를 반환 하는 매개 변수를 추가 합니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 제공는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 이러한 종류의 저장된 프로시저를 호출 하 고 반환 되는 데이터를 처리 하는 데 사용할 수 있는 클래스입니다.  
  
 JDBC 드라이버를 사용 하 여 이러한 종류의 저장된 프로시저를 호출할 때 사용 해야 합니다는 `call` 와 함께 SQL 이스케이프 시퀀스는 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다. 에 대 한 구문은 `call` OUT 매개 변수가 있는 이스케이프 시퀀스는 다음과 같습니다.  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  SQL 이스케이프 시퀀스에 대 한 자세한 내용은 참조 [SQL 이스케이프 시퀀스를 사용 하 여](../../connect/jdbc/using-sql-escape-sequences.md)합니다.  
  
 생성할 때는 `call` 이스케이프 시퀀스를 사용 하 여 OUT 매개 변수를 지정 된? 입력 매개 변수를 지정합니다. 이 문자는 저장 프로시저에서 반환될 매개 변수 값에 대한 자리 표시자로 사용됩니다. 사용 하 여 각 매개 변수의 데이터 형식을 지정 해야 하는 OUT 매개 변수 값을 지정 하는 [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 저장된 프로시저를 실행 하기 전에 SQLServerCallableStatement 클래스의 메서드.  
  
 RegisterOutParameter 메서드에 OUT 매개 변수를 사용 해야 네이티브 중 하나로 매핑됩니다 java.sql.Types에 포함 된 JDBC 데이터 형식 중 하나를 지정 하는 값 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다. JDBC에 대 한 자세한 내용은 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식을 참조 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)합니다.  
  
 RegisterOutParameter 메서드와 OUT 매개 변수 값을 전달 하는 경우에 매개 변수를 되지만 매개 변수의 서 수 위치 또는 저장된 프로시저에서 매개 변수의 이름에 사용할 데이터 형식 뿐만 아니라 지정 해야 합니다. 예를 들어, 저장 프로시저에 하나의 출력 매개 변수가 들어 있는 경우 서수 값은 1이 됩니다. 또한 저장 프로시저에 출력 매개 변수가 두 개이면 첫 번째 서수 값은 1이고 두 번째 서수 값은 2가 됩니다.  
  
> [!NOTE]  
>  JDBC 드라이버는 CURSOR, SQLVARIANT, TABLE 및 타임 스탬프의 사용을 지원 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] OUT 매개 변수 데이터 형식입니다.  
  
 예를 들어에서 다음과 같은 저장된 프로시저를 만들는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
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
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스는 함수에 전달 된 및 [실행](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드는 GetImmediateManager 저장 프로시저를 호출 하는:  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
      CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");  
      cstmt.setInt(1, 5);  
      cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
      cstmt.execute();  
      System.out.println("MANAGER ID: " + cstmt.getInt(2));  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
 다음 예에서는 서수 위치를 사용하여 매개 변수를 식별합니다. 서수 위치 대신 이름을 사용하여 매개 변수를 식별할 수도 있습니다. 다음 코드 예에서는 이전 예를 수정하여 Java 응용 프로그램에서 명명된 매개 변수를 사용하는 방법을 설명합니다. 매개 변수 이름은 저장 프로시저의 정의에 있는 매개 변수 이름에 해당합니다.  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
      CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");  
      cstmt.setInt("employeeID", 5);  
      cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
      cstmt.execute();  
      System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
      cstmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
```  
  
 }  
  
> [!NOTE]  
>  이 예에서는 SQLServerCallableStatement 클래스의 execute 메서드를 사용 하 여 저장된 프로시저를 실행 합니다. 이 메서드를 사용하는 이유는 저장 프로시저에서 결과 집합을 반환하지 않았기 때문입니다. 팩트 테이블 하는 경우는 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 메서드를 사용 합니다.  
  
 저장 프로시저는 업데이트 횟수 및 다중 결과 집합을 반환할 수 있습니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] OUT 매개 변수를 검색 하기 전에 다중 결과 집합 및 업데이트 횟수를 검색 이것은 JDBC 3.0 사양을 따릅니다. 즉, 응용 프로그램의 모든 결과 집합 개체를 검색 하 고 업데이트 횟수 CallableStatement.getter 방법을 사용 하 여 OUT 매개 변수를 검색 하기 전에 해야 합니다. 그렇지 않으면 결과 집합 개체와 이미 검색 되지 않은 업데이트 회수 손실 됩니다 OUT 매개 변수를 검색 하는 경우. 업데이트 횟수에 대 한 자세한 내용 및 다중 결과 집합에 대 한 참조 [저장 프로시저를 사용 하 여 업데이트 횟수로](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) 및 [를 사용 하 여 여러 결과 집합은](../../connect/jdbc/using-multiple-result-sets.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [저장 프로시저가 있는 문 사용](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
