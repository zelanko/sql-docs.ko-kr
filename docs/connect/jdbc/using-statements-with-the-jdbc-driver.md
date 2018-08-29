---
title: JDBC 드라이버에서 문 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 983cf2bcbdbfd91f10331310dbf4318cd5b3fb5e
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785816"
---
# <a name="using-statements-with-the-jdbc-driver"></a>JDBC 드라이버에서 문 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터를 다양한 방법으로 처리할 수 있습니다. JDBC 드라이버는 데이터베이스에 대해 SQL 문을 실행하거나, 입력 및 출력 매개 변수를 모두 사용하여 데이터베이스에서 저장 프로시저를 호출하는 데 사용할 수 있습니다. 또한 JDBC 드라이버는 SQL 이스케이프 시퀀스, 업데이트 횟수, 자동 생성 키의 사용은 물론 일괄 작업에서의 업데이트 수행을 지원합니다.  
  
JDBC 드라이버는 다음과 같은 세 개의 클래스를 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터를 검색합니다.  
  
1. [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) - 매개 변수가 없는 SQL 문을 실행하는 데 사용됩니다.  
  
2. [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) - SQLServerStatement에서 상속되며, 입력 매개 변수가 포함될 수 있는 컴파일된 SQL 문을 실행하는 데 사용됩니다.  
  
3. [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) - SQLServerPreparedStatement에서 상속되며, 입력 매개 변수, 출력 매개 변수 또는 두 매개 변수가 모두 포함될 수 있는 저장 프로시저를 실행하는 데 사용됩니다.  
  
 이 섹션의 항목에서는 이러한 세 개의 명령문 클래스를 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터를 사용하는 방법에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  

| 항목                                                                                                    | 설명                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [SQL에 문 사용](../../connect/jdbc/using-statements-with-sql.md)                             | JDBC 드라이버에서 SQL 문을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터를 사용하는 방법을 설명합니다.    |
| [저장 프로시저가 있는 문 사용](../../connect/jdbc/using-statements-with-stored-procedures.md) | JDBC 드라이버에서 저장 프로시저를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터를 사용하는 방법을 설명합니다. |
| [다중 결과 집합 사용](../../connect/jdbc/using-multiple-result-sets.md)                           | JDBC 드라이버를 사용하여 다중 결과 집합에서 데이터를 검색하는 방법을 설명합니다.                                                                       |
| [SQL 이스케이프 시퀀스 사용](../../connect/jdbc/using-sql-escape-sequences.md)                           | 날짜/시간 리터럴 및 함수 같은 SQL 이스케이프 시퀀스를 사용하는 방법을 설명합니다.                                                               |
| [자동 생성 키 사용](../../connect/jdbc/using-auto-generated-keys.md)                             | 자동 생성 키를 사용하는 방법을 설명합니다.                                                                                                     |
| [일괄 처리 작업 수행](../../connect/jdbc/performing-batch-operations.md)                         | JDBC 드라이버를 사용하여 일괄 작업을 수행하는 방법을 설명합니다.                                                                                      |
| [복잡한 문 처리](../../connect/jdbc/handling-complex-statements.md)                         | JDBC 드라이버를 사용하여 다양한 태스크를 수행하고 서로 다른 데이터 형식을 반환할 수 있는 복잡한 문을 실행하는 방법을 설명합니다.               |
  
## <a name="see-also"></a>참고 항목

[JDBC 드라이버 개요](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
