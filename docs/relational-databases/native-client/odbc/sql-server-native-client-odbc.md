---
title: SQL Server Native Client (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client|ODBC
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 396c9b277c95efa8d1f281392a0d53352253600b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43105519"
---
# <a name="sql-server-native-client-odbc"></a>SQL Server Native Client(ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  ODBC는 관계형 데이터베이스 또는 ISAM(Indexed Sequential Access Method) 데이터베이스의 데이터에 액세스하는 데 사용되는 API(응용 프로그래밍 인터페이스)의 표준 정의입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 통신하는 C 및 C++ 응용 프로그램을 작성하기 위한 네이티브 API 중 하나인 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 통해 ODBC를 지원합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 사용하여 작성한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로그램은 C 함수 호출을 통해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 통신합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 관련 버전의 ODBC 함수는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에 구현되어 있습니다. 드라이버는 SQL 문을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 전달하고 문의 결과를 응용 프로그램에 반환합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 Microsoft Win32 ODBC 3.51 사양을 준수하며 이전 버전의 ODBC로 작성된 응용 프로그램을 ODBC 3.51 사양에 정의된 방식에 따라 지원합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 원본 이름 및 64비트 운영 체제](../../../relational-databases/native-client/odbc/data-source-names-and-64-bit-operating-systems.md)  
  
-   [SQL Server Native Client ODBC 드라이버 응용 프로그램 만들기](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
-   [SQL Server와의 통신 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
-   [쿼리 실행 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
-   [결과 처리 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
  
-   [커서를 사용 하 여 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
-   [트랜잭션 수행 &#40;ODBC&#41;](http://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
-   [오류 및 메시지 처리](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
-   [저장 프로시저 실행](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
-   [카탈로그 함수 사용](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  
  
-   [대량 복사 작업 수행 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
-   [text 및 image 열 관리](../../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
-   [ODBC 드라이버 성능 프로파일링](../../../relational-databases/native-client/odbc/profiling-odbc-driver-performance.md)  
  
-   [테이블 반환 매개 변수 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
-   [날짜 및 시간 기능 향상 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
-   [큰 CLR 사용자 정의 형식 &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)  
  
-   [FILESTREAM 지원 &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/filestream-support-odbc.md)  
  
-   [서비스 사용자 이름 &#40;Spn&#41; 클라이언트 연결의 &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [스파스 열 지원 &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)  
  
-   [SQL Server Native Client &#40;ODBC&#41; 참조](http://msdn.microsoft.com/library/06b7edee-8636-49d9-9b5c-2c710bf4fa2d)  
  
-   [ODBC 방법 도움말 항목](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 프로그래밍](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [SQL Server Native Client 설치](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
