---
title: 매개 변수가 있는 SQL 문을 사용 하 여 | Microsoft Docs
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
ms.assetid: 3202b88f-ce13-44dd-982c-c6a3b0260378
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c18852f5f1d30378e97c7754b074dd965b7325d0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-an-sql-statement-with-parameters"></a>매개 변수가 있는 SQL 문 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  에 데이터로 작업 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 매개 변수를 포함 하는 SQL 문을 사용 하 여 사용할 수 있습니다는 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) 의 메서드는 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 는 반환하는클래스[ SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 요청 된 데이터를 포함 하는 합니다. 이 수행 하려면 먼저 만들어야 합니다는 SQLServerPreparedStatement 개체를 사용 하 여는 [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) 의 메서드는 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 클래스입니다.  
  
 SQL 문을 생성할 때 물음표(?)를 사용하여 입력 매개 변수를 지정하면 SQL 문으로 전달될 매개 변수 값에 대한 자리 표시자로 사용됩니다. 매개 변수에 대해 값을 지정 하려면 SQLServerPreparedStatement 클래스의 setter 메서드 중 하나를 사용할 수 있습니다. 사용하는 setter 메서드는 SQL 문에 전달할 값의 데이터 형식에 따라 결정됩니다.  
  
 setter 메서드에 값을 전달할 때는 SQL 문에 사용할 실제 값은 물론 SQL 문에서 해당 매개 변수의 서수 위치도 지정해야 합니다. 예를 들어 단일 매개 변수를 포함 하는 SQL 문의 서 수 값 1이 됩니다. 문에 두 개의 매개 변수가 있으면 두 번째 서 수 값은 2가 됩니다 하는 동안 첫 번째 서 수 값이 1 됩니다.  
  
 다음 예에서는 열린 연결에에서는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 예제 데이터베이스에 전달 함수에, 준비 된 문의 SQL 구현 되 고 단일 문자열 매개 변수 값과 함께 실행 하 고 다음 결과 결과 집합에서 읽습니다.  
  
 [!code[JDBC#UsingSQLWithParams1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-w_1_1.java)]  
  
## <a name="see-also"></a>관련 항목:  
 [SQL에 문 사용](../../connect/jdbc/using-statements-with-sql.md)  
  
  
