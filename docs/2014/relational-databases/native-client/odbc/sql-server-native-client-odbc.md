---
title: SQL Server Native Client (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 570c0574357d9315f0e6b153f3eeabac79ec673b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63055663"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client(ODBC)
  ODBC는 관계형 데이터베이스 또는 ISAM(Indexed Sequential Access Method) 데이터베이스의 데이터에 액세스하는 데 사용되는 API(응용 프로그래밍 인터페이스)의 표준 정의입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 통신하는 C 및 C++ 애플리케이션을 작성하기 위한 네이티브 API 중 하나인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 통해 ODBC를 지원합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 사용하여 작성한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로그램은 C 함수 호출을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 통신합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관련 버전의 ODBC 함수는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 구현되어 있습니다. 드라이버는 SQL 문을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 전달하고 문의 결과를 애플리케이션에 반환합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 Microsoft Win32 ODBC 3.51 사양을 준수하며 이전 버전의 ODBC로 작성된 애플리케이션을 ODBC 3.51 사양에 정의된 방식에 따라 지원합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 원본 이름 및 64비트 운영 체제](data-source-names-and-64-bit-operating-systems.md)  
  
-   [SQL Server Native Client ODBC 드라이버 응용 프로그램 만들기](creating-a-driver-application.md)  
  
-   [SQL Server와의 통신 &#40;ODBC&#41;](../../native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [쿼리 실행 &#40;ODBC&#41;](../../native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [결과 처리 &#40;ODBC&#41;](../../native-client-odbc-results/processing-results-odbc.md)  
  
-   [커서를 사용 하 여 &#40;ODBC&#41;](../../native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [트랜잭션 수행 &#40;ODBC&#41;](../../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
-   [오류 및 메시지 처리](../../native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [저장 프로시저 실행](../../native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [카탈로그 함수 사용](using-catalog-functions.md)  
  
-   [대량 복사 작업 수행 &#40;ODBC&#41;](../../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [text 및 image 열 관리](../../native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [ODBC 드라이버 성능 프로파일링](profiling-odbc-driver-performance.md)  
  
-   [테이블 반환 매개 변수 &#40;ODBC&#41;](../../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../../native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [큰 CLR 사용자 정의 형식 &#40;ODBC&#41;](large-clr-user-defined-types-odbc.md)  
  
-   [FILESTREAM 지원 &#40;ODBC&#41;](filestream-support-odbc.md)  
  
-   [서비스 사용자 이름 &#40;Spn&#41; 클라이언트 연결의 &#40;ODBC&#41;](service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [스파스 열 지원 &#40;ODBC&#41;](sparse-columns-support-odbc.md)  
  
-   [SQL Server Native Client &#40;ODBC&#41; 참조](../../../database-engine/dev-guide/sql-server-native-client-odbc-reference.md)  
  
-   [ODBC 방법 도움말 항목](../../native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 프로그래밍](../sql-server-native-client-programming.md)   
 [SQL Server Native Client 설치](../applications/installing-sql-server-native-client.md)  
  
  
