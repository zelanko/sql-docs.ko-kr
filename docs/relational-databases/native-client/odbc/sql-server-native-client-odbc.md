---
title: ODBC
description: SQL Server는 odbc를 SQL Server Native Client ODBC 드라이버를 사용 하 여 SQL Server와 통신 하는 C 및 c + + 응용 프로그램에 대 한 네이티브 API로 지원 합니다.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLNCLI, ODBC
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], ODBC
- SQL Server Native Client ODBC driver
- ODBC
- SQL Server Native Client, ODBC
- ODBC, about SQL Server Native Client ODBC driver
ms.assetid: 811d5ba3-a2b8-48c0-adbc-8c91f041f458
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aa462e10c92e94582fb127667127a3f7c50a98ce
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467624"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client(ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC는 관계형 데이터베이스 또는 ISAM(Indexed Sequential Access Method) 데이터베이스의 데이터에 액세스하는 데 사용되는 API(응용 프로그래밍 인터페이스)의 표준 정의입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 통신하는 C 및 C++ 애플리케이션을 작성하기 위한 네이티브 API 중 하나인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 통해 ODBC를 지원합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 사용하여 작성한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로그램은 C 함수 호출을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 통신합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관련 버전의 ODBC 함수는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 구현되어 있습니다. 드라이버는 SQL 문을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 전달하고 문의 결과를 애플리케이션에 반환합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 Microsoft Win32 ODBC 3.51 사양을 준수하며 이전 버전의 ODBC로 작성된 애플리케이션을 ODBC 3.51 사양에 정의된 방식에 따라 지원합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 원본 이름 및 64비트 운영 체제](../../../relational-databases/native-client/odbc/data-source-names-and-64-bit-operating-systems.md)  
  
-   [SQL Server Native Client ODBC 드라이버 애플리케이션 만들기](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
-   [SQL Server &#40;ODBC&#41;와 통신 ](../../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [ODBC&#41;&#40;쿼리 실행 ](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [ODBC&#41;&#40;결과 처리 ](../../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
-   [ODBC&#41;&#40;커서 사용 ](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [ODBC&#41;&#40;트랜잭션 수행 ](./performing-transactions-in-odbc.md)  
  
-   [오류 및 메시지 처리](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [저장 프로시저 실행](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [카탈로그 함수 사용](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  
  
-   [ODBC&#41;&#40;대량 복사 작업 수행 ](../../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [text 및 image 열 관리](../../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [ODBC 드라이버 성능 프로파일링](../../../relational-databases/native-client/odbc/profiling-odbc-driver-performance.md)  
  
-   [ODBC&#41;&#40;테이블 반환 매개 변수 ](../../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [ODBC&#41;&#40;날짜 및 시간 기능 향상 ](../../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [ODBC&#41;를 &#40;하는 대량 CLR User-Defined 형식 ](../../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)  
  
-   [ODBC&#41;&#40;FILESTREAM 지원 ](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [클라이언트 연결의 SPN&#40;서비스 사용자 이름&#41;&#40;ODBC&#41;](../../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [스파스 열 &#40;ODBC&#41;지원 ](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)  
  
-   [ODBC&#41; 참조 &#40;SQL Server Native Client]()  
  
-   [ODBC 방법 도움말 항목](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 프로그래밍](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [SQL Server Native Client 설치](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
