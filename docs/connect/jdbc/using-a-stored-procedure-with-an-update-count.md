---
title: 업데이트 횟수가 있는 저장 프로시저 사용 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 64cf4877-5995-4bfc-8865-b7618a5c8d01
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 851974955b9311efc149ecdff310bfbb1d8869fc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026931"
---
# <a name="using-a-stored-procedure-with-an-update-count"></a>업데이트 횟수가 있는 저장 프로시저 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터를 수정하기 위해 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스를 제공합니다. SQLServerCallableStatement 클래스를 사용하면 데이터베이스에 있는 데이터를 수정하고 영향을 받은 행 수(업데이트 횟수라고도 함)를 반환하는 저장 프로시저를 호출할 수 있습니다.

SQLServerCallableStatement 클래스를 사용하여 저장 프로시저에 대한 호출을 설정한 후에는 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 또는 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 메서드를 사용하여 저장 프로시저를 호출할 수 있습니다. executeUpdate 메서드는 저장 프로시저에 의해 영향을 받은 행 수가 포함된 **int** 값을 반환하지만 execute 메서드는 그렇지 않습니다. execute 메서드를 사용하여 영향을 받은 행 수를 가져오려면 저장 프로시저를 실행한 후 [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) 메서드를 호출합니다.

> [!NOTE]  
> JDBC 드라이버가 발생 가능성이 있는 모든 트리거가 반환한 업데이트 횟수를 포함하여 모든 업데이트 횟수를 반환하게 하려면 lastUpdateCount 연결 문자열 속성을 "false"로 설정합니다. lastUpdateCount 속성에 대한 자세한 내용은 [연결 속성 설정](../../connect/jdbc/setting-the-connection-properties.md)을 참조하세요.

이에 대한 예로 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 다음 테이블 및 저장 프로시저를 만들고 예제 데이터도 삽입합니다.

```sql
CREATE TABLE TestTable
   (Col1 int IDENTITY,
    Col2 varchar(50),
    Col3 int);  

CREATE PROCEDURE UpdateTestTable  
   @Col2 varchar(50),  
   @Col3 int  
AS  
BEGIN  
   UPDATE TestTable  
   SET Col2 = @Col2, Col3 = @Col3  
END;  
INSERT INTO dbo.TestTable (Col2, Col3) VALUES ('b', 10);  
```

다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대해 열린 연결을 함수로 전달하고, execute 메서드를 사용하여 UpdateTestTable 저장 프로시저를 호출한 다음, getUpdateCount 메서드를 사용하여 저장 프로시저에 의해 영향을 받은 행 수를 반환합니다.

[!code[JDBC#UsingSprocWithUpdateCount1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_0_1.java)]

## <a name="see-also"></a>참고 항목

[저장 프로시저가 있는 문 사용](../../connect/jdbc/using-statements-with-stored-procedures.md)
