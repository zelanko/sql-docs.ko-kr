---
title: 업데이트 횟수가 있는 저장된 프로시저를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 64cf4877-5995-4bfc-8865-b7618a5c8d01
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d858b255d5bdd6ce74509d36f4d0497220350694
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-a-stored-procedure-with-an-update-count"></a>업데이트 횟수가 있는 저장 프로시저 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  데이터를 수정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 저장된 프로시저를 사용 하 여 데이터베이스의 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 제공는 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스입니다. SQLServerCallableStatement 클래스를 사용 하 여 데이터베이스에 포함 된 데이터를 수정 하는 저장된 프로시저를 호출할 수 있으며 업데이트 횟수 라고도, 영향을 받는 행의 수를 반환할 수 있습니다.  
  
 저장된 프로시저에 대 한 호출에서 SQLServerCallableStatement 클래스를 사용 하 여 설정한 후 호출할 수 있습니다는 저장된 프로시저 중 하나를 사용 하 여는 [실행](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 또는 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 메서드. ExecuteUpdate 메서드는 반환 된 **int** 값 execute 메서드에서 않고 저장된 프로시저에 영향을 받은 행 수를 포함 하는 그렇지 않습니다. Execute 메서드를 사용 하 고 영향을 받는 행 수를 확인 하고자 하는 경우 호출할 수 있습니다는 [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) 메서드 후 저장된 프로시저를 실행 합니다.  
  
> [!NOTE]  
>  JDBC 드라이버가 발생 가능성이 있는 모든 트리거가 반환한 업데이트 횟수를 포함하여 모든 업데이트 횟수를 반환하게 하려면 lastUpdateCount 연결 문자열 속성을 "false"로 설정합니다. LastUpdateCount 속성이 사용에 대 한 자세한 내용은 참조 [연결 속성을 설정할](../../connect/jdbc/setting-the-connection-properties.md)합니다.  
  
 예를 들어 다음 테이블 및 저장된 프로시저를 만들고 있는 샘플 데이터를 삽입할 수도 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
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
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스는 함수에 전달 된 UpdateTestTable 저장 프로시저를 호출 하 고 execute 메서드를 사용 하 고 다음 getUpdateCount 메서드를 사용 하 되는 행의 개수를 반환 저장된 프로시저에 의해 영향을 합니다.  
  
 [!code[JDBC#UsingSprocWithUpdateCount1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_0_1.java)]  
  
## <a name="see-also"></a>관련 항목:  
 [저장 프로시저가 있는 문 사용](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  
