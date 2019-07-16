---
title: 오류 및 메시지 처리 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4a4d87ccae235aee1a11e58aff60fe8e34d6205
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207089"
---
# <a name="handling-errors-and-messages"></a>오류 및 메시지 처리
  응용 프로그램이 ODBC 함수를 호출 하는 경우 드라이버는 함수를 실행 하 고 두 가지 방법으로 진단 정보를 반환 합니다. 반환 코드를 전반적인 성공 또는 실패는 ODBC 함수의 나타내고 진단 레코드는 함수에 대 한 자세한 정보를 제공 합니다. 진단 레코드에는 헤더 레코드 및 상태 레코드가 포함됩니다. 함수가 성공하더라도 한 개 이상의 진단 레코드, 즉 헤더 레코드가 반환됩니다.  
  
 진단 정보는 개발 과정에서 잘못된 핸들이나 하드 코딩된 SQL 문의 구문 오류와 같은 프로그래밍 오류를 파악하는 데 사용됩니다. 이 밖에도 런타임에 데이터 잘림, 규칙 위반 및 사용자가 입력한 SQL 문의 구문 오류와 같은 런타임 오류 및 경고를 파악하는 데도 사용됩니다. 프로그램 논리는 일반적으로 반환 코드에 기반을 둡니다.  
  
 예를 들어, 응용 프로그램 호출 **SQLFetch** 결과 집합의 행을 검색 하려면 반환 코드를 나타냅니다 (SQL_NO_DATA)을 결과 집합의 끝에 도달한 있는지 여부를 모든 정보 메시지 (SQL_SUCCESS_ 반환 된 경우 WITH_INFO), 아니면 오류가 (SQL_ERROR) 발생 했습니다.  
  
 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버가 SQL_SUCCESS 이외의 반환, 응용 프로그램에서 호출할 수 있습니다 **SQLGetDiagRec** 검색 다른 정보 또는 오류 메시지입니다. 사용 하 여 **SQLGetDiagRec** 메시지 경우 둘 이상의 메시지 집합을 위아래로 스크롤할 수 있습니다.  
  
 반환 코드 SQL_INVALID_HANDLE은 항상 프로그래밍 오류를 나타내며 런타임에 발생하지 않도록 해야 합니다. 다른 모든 반환 코드는 런타임 정보를 나타내며 SQL_ERROR는 프로그래밍 오류를 나타내는 경우가 있습니다.  
  
 원래 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 API 인 C 언어용 Db-library 허용 콜백 오류 처리를 설치할 응용 프로그램 및 해당 반환 오류 또는 메시지가 메시지 처리 함수입니다. PRINT, RAISERROR, DBCC 및 SET과 같은 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 결과를 결과 집합이 아닌 DB-Library 메시지 처리기 함수로 반환합니다. 그러나 ODBC API에는 이러한 콜백 기능이 없습니다. 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버에서 다시 보낸 메시지를 검색 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ODBC 반환 코드를 SQL_SUCCESS_WITH_INFO 또는 SQL_ERROR를 설정 하 고 메시지를 하나 이상의 진단 레코드를 반환 합니다. 따라서 ODBC 응용 프로그램을 신중 하 게 테스트 해야 이러한 반환 코드 및 호출에 대 한 **SQLGetDiagRec** 메시지 데이터를 검색 합니다.  
  
 오류 추적에 대한 자세한 내용은 [데이터 액세스 추적](https://go.microsoft.com/fwlink/?LinkId=125805)을 참조하십시오. 오류 추적에 추가 된 향상 된 기능에 대 한 내용은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]를 참조 하십시오 [확장 이벤트 로그의 진단 정보 액세스](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [메시지를 생성하는 문 처리](processing-statements-that-generate-messages.md)  
  
-   [진단 레코드 및 필드](diagnostic-records-and-fields.md)  
  
-   [원시 오류 번호](native-error-numbers.md)  
  
-   [SQLSTATE &#40;ODBC 오류 코드&#41;](sqlstate-odbc-error-codes.md)  
  
-   [오류 메시지](error-messages.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
