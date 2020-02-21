---
title: 복잡한 문 처리 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6b807a45-a8b5-4b1c-8b7b-d8175c710ce0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ebd2aee0990b744df1420e88f8cc79870b350f2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027996"
---
# <a name="handling-complex-statements"></a>복잡한 문 처리
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 사용하는 경우 런타임에 동적으로 생성되는 문을 포함하여 복잡한 문을 처리해야 할 수 있습니다. 복잡한 문은 대개 업데이트, 삽입 및 삭제를 포함하여 다양한 태스크를 수행합니다. 또한 이러한 유형의 문은 다중 결과 집합과 출력 매개 변수를 반환할 수 있습니다. 이 경우 문을 실행하는 Java 코드에서 반환되는 개체 및 데이터의 형식과 수를 미리 알지 못할 수 있습니다.  
  
 JDBC 드라이버에서는 복합한 문을 효과적으로 처리하기 위해 반환되는 개체 및 데이터를 쿼리하는 다양한 메서드를 제공하여 애플리케이션에서 이를 올바르게 처리할 수 있도록 합니다. 복잡한 문을 처리하는 기능의 핵심은 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스의 [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드입니다. 이 메서드는 **boolean** 값을 반환합니다. 값이 true인 경우 문에서 처음 반환되는 결과는 결과 집합입니다. 값이 false이면 처음 반환되는 결과는 업데이트 횟수입니다.  
  
 반환된 개체 또는 데이터의 형식을 알고 있으면 [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) 또는 [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) 메서드를 사용하여 해당 데이터를 처리할 수 있습니다. 복잡한 문에서 이후에 반환되는 개체 또는 데이터를 처리하는 데는 [getMoreResults](../../connect/jdbc/reference/getmoreresults-method.md) 메서드를 사용합니다.  
  
 다음 예제에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 대해 열린 연결을 함수로 전달하고, 저장 프로시저 호출과 SQL 문이 결합된 복잡한 문을 생성하여 실행한 다음, `do` 루프를 사용하여 반환되는 모든 결과 집합 및 업데이트 횟수를 처리합니다.  
  
 [!code[JDBC#HandlingComplexStatements1](../../connect/jdbc/codesnippet/Java/handling-complex-statements_1.java)]  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버에서 문 사용](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  
