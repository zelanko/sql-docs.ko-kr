---
title: 오류 및 메시지 처리 | Microsoft Docs
description: 응용 프로그램이 성공 또는 실패 및 자세한 정보를 포함 하 여 ODBC 함수를 호출할 때 반환 되는 진단 정보에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, about error handling
- errors [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], about messages
- ODBC error handling
- SQL_INVALID_HANDLE return code
- errors [ODBC], about error handling
- messages [ODBC]
ms.assetid: 74ea9630-e482-4a46-bb45-f5234f079b48
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 64e6226c5f8260979b5cf83245f56bf77b9ff759
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998511"
---
# <a name="handling-errors-and-messages"></a>오류 및 메시지 처리
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  애플리케이션이 ODBC 함수를 호출하면 드라이버가 함수를 실행하고 반환 코드와 진단 레코드라는 두 가지 방법으로 진단 정보를 반환합니다. 반환 코드는 ODBC 함수의 전반적인 성공 또는 실패를 나타내고, 진단 레코드는 함수에 대한 자세한 정보를 제공합니다. 진단 레코드에는 헤더 레코드 및 상태 레코드가 포함됩니다. 함수가 성공하더라도 한 개 이상의 진단 레코드, 즉 헤더 레코드가 반환됩니다.  
  
 진단 정보는 개발 과정에서 잘못된 핸들이나 하드 코딩된 SQL 문의 구문 오류와 같은 프로그래밍 오류를 파악하는 데 사용됩니다. 이 밖에도 런타임에 데이터 잘림, 규칙 위반 및 사용자가 입력한 SQL 문의 구문 오류와 같은 런타임 오류 및 경고를 파악하는 데도 사용됩니다. 프로그램 논리는 일반적으로 반환 코드에 기반을 둡니다.  
  
 예를 들어 응용 프로그램이 **Sqlfetch** 를 호출 하 여 결과 집합의 행을 검색 한 후 반환 코드는 결과 집합의 끝에 도달 했는지 (SQL_NO_DATA), 정보 메시지가 반환 되었는지 (SQL_SUCCESS_WITH_INFO) 또는 오류가 발생 한 경우 (SQL_ERROR)를 나타냅니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버가 SQL_SUCCESS 이외의 값을 반환 하는 경우 응용 프로그램은 **SQLGetDiagRec** 를 호출 하 여 정보 또는 오류 메시지를 검색할 수 있습니다. 둘 이상의 메시지가 있는 경우 **SQLGetDiagRec** 를 사용 하 여 메시지 집합을 위아래로 스크롤합니다.  
  
 반환 코드 SQL_INVALID_HANDLE은 항상 프로그래밍 오류를 나타내며 런타임에 발생하지 않도록 해야 합니다. 다른 모든 반환 코드는 런타임 정보를 나타내며 SQL_ERROR는 프로그래밍 오류를 나타내는 경우가 있습니다.  
  
 원래 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 API 인 C 용 db-library를 사용 하면 응용 프로그램에서 오류 또는 메시지를 반환 하는 콜백 오류 처리 및 메시지 처리 함수를 설치할 수 있습니다. PRINT, RAISERROR, DBCC 및 SET과 같은 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 결과를 결과 집합이 아닌 DB-Library 메시지 처리기 함수로 반환합니다. 그러나 ODBC API에는 이러한 콜백 기능이 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT odbc 드라이버가에서 반환 된 메시지를 검색 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] odbc 반환 코드를 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR로 설정 하 고 메시지를 하나 이상의 진단 레코드로 반환 합니다. 따라서 ODBC 응용 프로그램은 이러한 반환 코드를 신중 하 게 테스트 하 고 **SQLGetDiagRec** 를 호출 하 여 메시지 데이터를 검색 해야 합니다.  
  
 오류 추적에 대한 자세한 내용은 [데이터 액세스 추적](https://go.microsoft.com/fwlink/?LinkId=125805)을 참조하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 추가된 오류 추적의 향상된 기능에 대한 자세한 내용은 [확장 이벤트 로그의 진단 정보 액세스](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)를 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [메시지를 생성하는 문 처리](../../relational-databases/native-client-odbc-error-messages/processing-statements-that-generate-messages.md)  
  
-   [진단 레코드 및 필드](../../relational-databases/native-client-odbc-error-messages/diagnostic-records-and-fields.md)  
  
-   [원시 오류 번호](../../relational-databases/native-client-odbc-error-messages/native-error-numbers.md)  
  
-   [SQLSTATE &#40;ODBC 오류 코드&#41;](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)  
  
-   [오류 메시지](../../relational-databases/native-client-odbc-error-messages/error-messages.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
