---
title: 저장 프로시저 실행 | Microsoft Docs
description: 저장 프로시저는 데이터베이스에 저장된 실행 가능한 개체입니다. SQL Server는 저장 프로시저와 확장 저장 프로시저를 지원 합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- stored procedures [ODBC], running
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], executing
ms.assetid: 866b6dd3-2acd-4dfb-aeca-a0352b2d4c6a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2d28d9647c974dc4607ebd3498f0add4eede487a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97437551"
---
# <a name="running-stored-procedures"></a>저장 프로시저 실행
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  저장 프로시저는 데이터베이스에 저장된 실행 가능한 개체입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 다음과 같은 프로시저를 지원합니다.  
  
-   저장 프로시저:  
  
     실행 가능한 단일 프로시저로 미리 컴파일된 하나 이상의 SQL 문입니다.  
  
-   확장 저장 프로시저:  
  
     SQL Server 개방형 Data Services API에 확장 저장 프로시저에 대해 작성된 C 또는 C++ DLL(동적 연결 라이브러리)입니다. 개방형 Data Services API는 C 또는 C++ 코드를 포함하도록 저장 프로시저의 기능을 확장합니다.  
  
 문을 실행할 때 클라이언트 애플리케이션에서 직접 문을 실행하거나 준비하는 대신 데이터 원본의 저장 프로시저를 호출하면 다음과 같은 이점이 있습니다.  
  
-   성능 향상  
  
     프로시저가 생성될 때 SQL 문이 구문 분석되고 컴파일됩니다. 프로시저를 실행할 때는 이러한 오버헤드가 발생하지 않습니다.  
  
-   네트워크 오버헤드 감소  
  
     네트워크를 통해 복잡한 쿼리를 전송하는 대신 프로시저를 실행하면 네트워크 트래픽을 줄일 수 있습니다. ODBC 애플리케이션이 ODBC { CALL } 구문을 사용하여 저장 프로시저를 실행하는 경우 ODBC 드라이버가 추가 최적화를 수행하므로 매개 변수 데이터를 변환하지 않아도 됩니다.  
  
-   일관성 향상  
  
     조직의 규칙을 저장 프로시저와 같은 중앙 리소스에 구현하면 이러한 규칙을 한 번에 코딩, 테스트 및 디버그할 수 있습니다. 프로그래머는 직접 구현을 개발하는 대신 이러한 테스트된 저장 프로시저를 사용할 수 있습니다.  
  
-   정확도 향상  
  
     저장 프로시저는 일반적으로 숙련된 프로그래머가 작성하기 때문에 기술 수준이 서로 다른 프로그래머들이 여러 차례 개발하는 코드보다 효율적이고 오류가 적은 경우가 많습니다.  
  
-   기능 추가  
  
     확장 저장 프로시저는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 제공되지 않는 C 및 C++ 기능을 사용할 수 있습니다.  
  
     저장 프로시저를 호출 하는 방법에 대 한 예제는 [ODBC&#41;&#40;반환 코드 및 출력 매개 변수 처리 ](../../relational-databases/native-client-odbc-how-to/running-stored-procedures-process-return-codes-and-output-parameters.md)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [저장 프로시저 호출](../../relational-databases/native-client-odbc-stored-procedures/calling-a-stored-procedure.md)  
  
-   [저장 프로시저 호출 일괄 처리](../../relational-databases/native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)  
  
-   [저장 프로시저 결과 처리](../../relational-databases/native-client-odbc-stored-procedures/processing-stored-procedure-results.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;SQL Server Native Client &#40;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [저장 프로시저 실행 방법 항목 ODBC&#41;&#40;](../native-client-odbc-how-to/running-stored-procedures-call-stored-procedures.md)  
  
