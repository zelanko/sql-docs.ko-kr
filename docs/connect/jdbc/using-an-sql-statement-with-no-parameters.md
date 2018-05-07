---
title: 매개 변수가 없는 SQL 문을 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4b0728bd-059b-4b71-895c-999335bc7427
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd6fbcc2813fbd1e19078e94e4ba23b002e2818c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-an-sql-statement-with-no-parameters"></a>매개 변수가 없는 SQL 문 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  에 데이터로 작업 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 매개 변수를 포함 하는 SQL 문을 사용 하 여 사용할 수 있습니다는 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 의 메서드는 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 반환 하는 클래스는 [ SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 요청 된 데이터를 포함 하는 합니다. 이 수행 하려면 먼저 만들어야 합니다 SQLServerStatement 개체를 사용 하 여는 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다.  
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스에 전달 함수에, SQL 문을 생성 및 실행 하 고 다음 결과 결과 집합에서 읽습니다.  
  
 [!code[JDBC#UsingSQLWithNoParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_0_1.java)]  
  
 결과 집합을 사용 하는 방법에 대 한 자세한 내용은 참조 [JDBC 드라이버로 결과 집합 관리](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL에 문 사용](../../connect/jdbc/using-statements-with-sql.md)  
  
  
