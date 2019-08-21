---
title: 입력 매개 변수가 있는 저장 프로시저 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8f491b70-7d1b-42bd-964f-9a8b86af5eaa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c84e4081b9369d504d173387c6944b06d927c9c
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026900"
---
# <a name="using-a-stored-procedure-with-input-parameters"></a>입력 매개 변수가 있는 저장 프로시저 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

호출할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저는 데이터를 저장 프로시저에 전달하는 데 사용할 수 있는 입력 매개 변수가 하나 이상인 저장 프로시저입니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 이러한 종류의 저장 프로시저를 호출하여 반환되는 데이터를 처리하는 데 사용할 수 있는 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스를 제공합니다.

JDBC 드라이버를 사용하여 입력 매개 변수가 포함된 저장 프로시저를 호출하는 경우에는 `call` SQL 이스케이프 시퀀스와 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 메서드를 함께 사용해야 합니다. 입력 매개 변수가 있는 `call` 이스케이프 시퀀스의 구문은 다음과 같습니다.

`{call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> SQL 이스케이프 시퀀스에 대 한 자세한 내용은 [sql 이스케이프 시퀀스 사용](../../connect/jdbc/using-sql-escape-sequences.md)을 참조 하세요.

`call` 이스케이프 시퀀스를 만드는 경우 물음표(?) 문자를 사용하여 입력 매개 변수를 지정합니다. 이 문자는 저장 프로시저로 전달될 매개 변수 값에 대한 자리 표시자로 사용됩니다. 매개 변수의 값을 지정 하려면 SQLServerPreparedStatement 클래스의 setter 메서드 중 하나를 사용할 수 있습니다. 사용할 수 있는 setter 메서드는 입력 매개 변수의 데이터 형식에 따라 결정됩니다.

setter 메서드에 값을 전달할 때는 매개 변수에 사용할 실제 값은 물론 저장 프로시저에서 해당 매개 변수의 서수 위치도 지정해야 합니다. 예를 들어 저장 프로시저에 단일 입력 매개 변수가 들어 있는 경우 서수 값은 1이 됩니다. 또한 저장 프로시저에 입력 매개 변수가 두 개이면 첫 번째 서수 값은 1이고 두 번째 서수 값은 2가 됩니다.

입력 매개 변수가 있는 저장 프로시저를 호출하는 방법의 예로 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 uspGetEmployeeManagers 저장 프로시저를 사용합니다. 이 저장 프로시저는 정수인 EmployeeID라는 단일 입력 매개 변수를 허용하고 지정한 EmployeeID를 토대로 직원 및 해당 관리자의 재귀 목록을 반환합니다. 이 저장 프로시저를 호출하는 Java 코드는 다음과 같습니다.

```java
public static void executeSprocInParams(Connection con) throws SQLException {  
    try(PreparedStatement pstmt = con.prepareStatement("{call dbo.uspGetEmployeeManagers(?)}"); ) {  

        pstmt.setInt(1, 50);  
        ResultSet rs = pstmt.executeQuery();  

        while (rs.next()) {  
            System.out.println("EMPLOYEE:");  
            System.out.println(rs.getString("LastName") + ", " + rs.getString("FirstName"));  
            System.out.println("MANAGER:");  
            System.out.println(rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));  
            System.out.println();  
        }  
    }
}
```

## <a name="see-also"></a>관련 항목:

[저장 프로시저가 있는 문 사용](../../connect/jdbc/using-statements-with-stored-procedures.md)
