---
title: 결과 처리 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], about result sets
- SQLRowCount function
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- COMPUTE clause
- result sets [ODBC]
- COMPUTE BY clause
ms.assetid: 61a8db19-6571-47dd-84e8-fcc97cb60b45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb490ab23d146dc8131c16e22b0d63f07b79d482
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058313"
---
# <a name="processing-results-odbc"></a>결과 처리(ODBC)
  응용 프로그램이 SQL 문을 제출하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 결과 데이터를 하나 이상의 결과 집합으로 반환합니다. 결과 집합은 쿼리 조건과 일치하는 행과 열 집합입니다. SELECT 문, 카탈로그 함수 및 일부 저장 프로시저는 응용 프로그램에서 사용할 수 있는 결과 집합을 테이블 형식으로 생성합니다. 실행한 SQL 문이 저장 프로시저, 여러 명령이 포함된 일괄 처리 또는 키워드가 포함된 SELECT 문이면 처리할 결과 집합이 여러 개가 됩니다.  
  
 또한 ODBC 카탈로그 함수는 데이터를 검색할 수 있습니다. 예를 들어 [SQLColumns](../native-client-odbc-api/sqlcolumns.md) 데이터 원본의 열에 대 한 데이터를 검색 합니다. 이러한 결과 집합에는 0개 이상의 행이 포함될 수 있습니다.  
  
 GRANT 또는 REVOKE와 같은 다른 SQL 문은 결과 집합을 반환하지 않습니다. 이러한 문의 경우에서 반환 코드 **SQLExecute** 또는 **SQLExecDirect** 는 일반적으로 나서야 문이 성공적으로 수행 합니다.  
  
 각 INSERT, UPDATE 및 DELETE 문은 수정 내용이 적용되는 행 수만 포함된 결과 집합을 반환합니다. 이 개수는 응용 프로그램 때 사용할 수 있는 호출 이루어집니다 [SQLRowCount](../native-client-odbc-api/sqlrowcount.md)합니다. ODBC 3입니다. *x* 응용 프로그램은 호출 **SQLRowCount** 결과 검색 하려면 설정 하거나 [SQLMoreResults](../native-client-odbc-api/sqlmoreresults.md) 취소 하 합니다. 사용 하 여 각 수정 문의에서 결과 집합을 처리 해야 하는지 응용 프로그램에서 일괄 처리 또는 여러 INSERT, UPDATE 또는 DELETE 문이 포함 된 저장된 프로시저를 실행할 때 **SQLRowCount** 를사용하여취소또는**SQLMoreResults**합니다. 일괄 처리나 저장 프로시저에 SET NOCOUNT ON 문을 포함하여 이 개수를 취소할 수 있습니다.  
  
 Transact-SQL에는 SET NOCOUNT 문이 포함되어 있습니다. SQL Server 문에 의해 영향을 받는 행의 수를 반환 하지 않습니다에서 NOCOUNT 옵션을 설정 하 고 **SQLRowCount** 0을 반환 합니다. 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 버전에서는 드라이버별 [SQLGetStmtAttr](../native-client-odbc-api/sqlgetstmtattr.md) 옵션인 SQL_SOPT_SS_NOCOUNT_STATUS를 NOCOUNT 옵션을 on 또는 off 인지 보고 합니다. 언제 든 지 **SQLRowCount** SQL_SOPT_SS_NOCOUNT_STATUS를 테스트 해야 응용 프로그램에 0을 반환 합니다. 경우 SQL_NC_ON 반환 되는 값이 0 **SQLRowCount** 만 SQL Server 행 수를 반환 하지 않은 나타냅니다. SQL_NC_OFF가 반환 하는 경우는 NOCOUNT가 off 의미 및 0 값 **SQLRowCount** 문이 어떤 행에 영향을 주지 않았습니다 나타냅니다. 응용 프로그램의 값을 표시 되지 않아야 **SQLRowCount** SQL_SOPT_SS_NOCOUNT_STATUS가 sql_nc_off 인 경우. 큰 일괄 처리나 저장 프로시저에는 여러 개의 SET NOCOUNT 문이 포함될 수 있으므로 프로그래머는 SQL_SOPT_SS_NOCOUNT_STATUS가 일정하게 유지된다고 가정할 수 없습니다. 옵션을 테스트할 때마다 **SQLRowCount** 0을 반환 합니다.  
  
 다른 몇 개의 Transact-SQL 문은 데이터를 결과 집합이 아닌 메시지로 반환합니다. 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 이러한 메시지를 수신 응용 프로그램에 정보 메시지를 사용할 수 있는지 알립니다를 SQL_SUCCESS_WITH_INFO를 반환 합니다. 응용 프로그램을 호출할 수 있습니다 **SQLGetDiagRec** 이러한 메시지를 검색 합니다. 이런 방식으로 작동하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 다음과 같습니다.  
  
-   DBCC  
  
-   SET SHOWPLAN(이전 버전의 SQL Server에서 사용 가능)  
  
-   SET STATISTICS  
  
-   PRINT  
  
-   RAISERROR  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 심각도가 11 이상인 RAISERROR에서 SQL_ERROR를 반환 합니다. RAISERROR의 심각도가 19이면 연결도 삭제됩니다.  
  
 SQL 문의 결과 집합을 처리하기 위해 응용 프로그램은 다음 작업을 수행합니다.  
  
-   결과 집합의 특징을 확인합니다.  
  
-   열을 프로그램 변수에 바인딩합니다.  
  
-   단일 값, 전체 행의 값 또는 여러 행의 값을 검색합니다.  
  
-   테스트를 통해 추가 결과 집합이 있는지 확인하고, 있는 경우 루프백하여 새 결과 집합의 특징을 확인합니다.  
  
 데이터 원본에서 행을 검색하고 응용 프로그램에 반환하는 프로세스를 인출이라고 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [결과 집합의 특징을 확인 &#40;ODBC&#41;](determining-the-characteristics-of-a-result-set-odbc.md)  
  
-   [저장소 할당](assigning-storage.md)  
  
-   [결과 데이터 페치](fetching-result-data.md)  
  
-   [데이터 형식 매핑 &#40;ODBC&#41;](mapping-data-types-odbc.md)  
  
-   [데이터 형식 사용](data-type-usage.md)  
  
-   [문자 데이터 자동 변환](autotranslation-of-character-data.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [결과 처리 방법 도움말 항목 &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)  
  
  
