---
title: "복잡 한 문을 처리 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6b807a45-a8b5-4b1c-8b7b-d8175c710ce0
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bf7d2c48d091c013a351ae1f0421f172e33bb37e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="handling-complex-statements"></a>복잡한 문 처리
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  사용 하는 경우는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 런타임에 동적으로 생성 되는 문을 포함 하 여 복잡 한 문을 처리 해야 할 수 있습니다. 복잡한 문은 대개 업데이트, 삽입 및 삭제를 포함하여 다양한 태스크를 수행합니다. 또한 이러한 유형의 문은 다중 결과 집합과 출력 매개 변수를 반환할 수 있습니다. 이 경우 문을 실행하는 Java 코드에서 반환되는 개체 및 데이터의 형식과 수를 미리 알지 못할 수 있습니다.  
  
 JDBC 드라이버에서는 복합한 문을 효과적으로 처리하기 위해 반환되는 개체 및 데이터를 쿼리하는 다양한 메서드를 제공하여 응용 프로그램에서 이를 올바르게 처리할 수 있도록 합니다. 복잡 한 문을 처리 하는 열쇠입니다는 [실행](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스입니다. 이 메서드는 반환 된 **부울** 값입니다. 값이 true인 경우 문에서 처음 반환되는 결과는 결과 집합입니다. 값이 false이면 처음 반환되는 결과는 업데이트 횟수입니다.  
  
 개체 또는 반환 된 데이터의 형식을 알고 있는 경우 하나를 사용할 수 있습니다는 [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) 또는 [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) 메서드를 해당 데이터를 처리 합니다. 다음 개체 또는 복잡 한 문에서 반환 되는 데이터를 계속 하려면는 [getMoreResults](../../connect/jdbc/reference/getmoreresults-method.md) 메서드.  
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스는 함수에 전달 된, SQL 문이 저장된 프로시저 호출을 결합 하는 복잡 한 문을 생성를 실행 한 다음은 `do` 루프는 모든 결과 집합 및 업데이트 횟수 반환 되는 처리 하는 데 사용 합니다.  
  
 [!code[JDBC#HandlingComplexStatements1](../../connect/jdbc/codesnippet/Java/handling-complex-statements_1.java)]  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버에서 문 사용](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  

