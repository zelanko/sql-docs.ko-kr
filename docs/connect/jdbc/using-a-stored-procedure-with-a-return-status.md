---
title: 반환 상태가 있는 저장 프로시저 사용 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4b126e95-8458-41d6-af37-fc6662859f19
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0ae22a9fac4333271d564fb242803e4cc8eb0b4
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39661825"
---
# <a name="using-a-stored-procedure-with-a-return-status"></a>반환 상태가 있는 저장 프로시저 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

호출할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 저장 프로시저는 상태 또는 결과 및 매개 변수를 반환하는 프로시저입니다. 이러한 매개 변수는 대개 저장 프로시저의 성공 또는 실패를 나타내는 데 사용됩니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 이러한 종류의 저장 프로시저를 호출하여 반환되는 데이터를 처리하는 데 사용할 수 있는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스를 제공합니다.

JDBC 드라이버를 사용하여 이러한 종류의 저장 프로시저를 호출하는 경우에는 `call` SQL 이스케이프 시퀀스와 함께 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스의 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 메서드를 사용해야 합니다. 반환 상태 매개 변수가 있는 `call` 이스케이프 시퀀스의 구문은 다음과 같습니다.

`{[?=]call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> SQL 이스케이프 시퀀스에 대 한 자세한 내용은 참조 하세요. [SQL 이스케이프 시퀀스를 사용 하 여](../../connect/jdbc/using-sql-escape-sequences.md)입니다.

`call` 이스케이프 시퀀스를 만드는 경우 물음표(?) 문자를 사용하여 입력 매개 변수를 지정합니다. 이 문자는 저장 프로시저에서 반환될 매개 변수 값에 대한 자리 표시자로 사용됩니다. 반환 상태 매개 변수에 대한 값을 지정하려면 저장 프로시저를 실행하기 전에 SQLServerCallableStatement 클래스의 [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 메서드를 사용하여 매개 변수의 데이터 형식을 지정해야 합니다.

> [!NOTE]  
> SQL Server 데이터베이스에서 JDBC 드라이버를 사용하는 경우 registerOutParameter 메서드의 반환 상태 매개 변수에 대해 지정하는 값은 항상 정수이며, 이는 java.sql.Types.INTEGER 데이터 형식을 사용하여 지정할 수 있습니다.

또한 반환 상태 매개 변수에 대한 registerOutParameter 메서드에 값을 전달하는 경우 해당 매개 변수에 사용할 데이터 형식은 물론 저장 프로시저 호출에서 매개 변수의 서수 위치도 지정해야 합니다. 반환 상태 매개 변수인 경우, 항상 저장 프로시저 호출에서 첫 번째 매개 변수이므로 해당 서수 위치는 항상 1입니다. SQLServerCallableStatement 클래스가 특정 매개 변수를 나타내기 위해 매개 변수의 이름 사용을 지원하더라도 반환 상태 매개 변수에 대한 매개 변수의 서수 위치 번호만 사용할 수 있습니다.

이에 대한 예로 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 다음 저장 프로시저를 만듭니다.

```sql
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

다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대해 열린 연결을 함수로 전달하고 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드를 사용하여 CheckContactCity 저장 프로시저를 호출합니다.

[!code[JDBC#UsingSprocWithReturnStatus1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_1_1.java)]

## <a name="see-also"></a>참고 항목

[저장 프로시저가 있는 문 사용](../../connect/jdbc/using-statements-with-stored-procedures.md)
