---
title: "JDBC 드라이버와 함께 using 문을 | Microsoft Docs"
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
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a900a32cbaca2337930f7bb84aafcb634dcb508e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="using-statements-with-the-jdbc-driver"></a>JDBC 드라이버에서 문 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 에서 데이터로 작업할 데 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 여러 가지 방법으로 데이터베이스입니다. JDBC 드라이버는 데이터베이스에 대해 SQL 문을 실행하거나, 입력 및 출력 매개 변수를 모두 사용하여 데이터베이스에서 저장 프로시저를 호출하는 데 사용할 수 있습니다. 또한 JDBC 드라이버는 SQL 이스케이프 시퀀스, 업데이트 횟수, 자동 생성 키의 사용은 물론 일괄 작업에서의 업데이트 수행을 지원합니다.  
  
 데이터를 검색 하기 위한 세 가지 클래스를 제공 하는 JDBC 드라이버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스:  
  
1.  [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) -매개 변수가 없는 SQL 문을 실행 하는 데 사용 합니다.  
  
2.  [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) (SQLServerStatement에서 상속)-매개 변수가 포함 될 수 있는 실행 중인 컴파일된 SQL 문을 사용 합니다.  
  
3.  [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) (SQLServerPreparedStatement에서 상속)-매개 변수, 출력 매개 변수 또는 둘 다 포함 될 수 있는 저장된 프로시저 실행에 사용 됩니다.  
  
 이 섹션의 항목의 데이터로 작업 하려면 각 세 개의 문 클래스를 사용할 수는 방법에 대해 설명 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[SQL에 문 사용](../../connect/jdbc/using-statements-with-sql.md)|JDBC 드라이버와 함께 SQL 문을 사용 하 여의 데이터로 작업 하는 방법을 설명는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다.|  
|[저장 프로시저가 있는 문 사용](../../connect/jdbc/using-statements-with-stored-procedures.md)|JDBC 드라이버와 함께 저장된 프로시저를 사용 하 여의 데이터로 작업 하는 방법에 설명 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다.|  
|[다중 결과 집합 사용](../../connect/jdbc/using-multiple-result-sets.md)|JDBC 드라이버를 사용하여 다중 결과 집합에서 데이터를 검색하는 방법을 설명합니다.|  
|[SQL 이스케이프 시퀀스 사용](../../connect/jdbc/using-sql-escape-sequences.md)|날짜/시간 리터럴 및 함수 같은 SQL 이스케이프 시퀀스를 사용하는 방법을 설명합니다.|  
|[자동 생성 키 사용](../../connect/jdbc/using-auto-generated-keys.md)|자동 생성 키를 사용하는 방법을 설명합니다.|  
|[일괄 처리 작업 수행](../../connect/jdbc/performing-batch-operations.md)|JDBC 드라이버를 사용하여 일괄 작업을 수행하는 방법을 설명합니다.|  
|[복잡한 문 처리](../../connect/jdbc/handling-complex-statements.md)|JDBC 드라이버를 사용하여 다양한 태스크를 수행하고 서로 다른 데이터 형식을 반환할 수 있는 복잡한 문을 실행하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
