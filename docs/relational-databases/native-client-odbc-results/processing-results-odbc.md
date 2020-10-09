---
title: 결과 처리 (ODBC) | Microsoft Docs
description: ODBC 응용 프로그램에서 SQL 문을 제출할 때 SQL Server 반환 되는 데이터 처리에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 912a025e689343ffe3dce2ccc19dbec600576cd1
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867275"
---
# <a name="processing-results-odbc"></a>결과 처리(ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  애플리케이션이 SQL 문을 제출하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 결과 데이터를 하나 이상의 결과 집합으로 반환합니다. 결과 집합은 쿼리 조건과 일치하는 행과 열 집합입니다. SELECT 문, 카탈로그 함수 및 일부 저장 프로시저는 애플리케이션에서 사용할 수 있는 결과 집합을 테이블 형식으로 생성합니다. 실행한 SQL 문이 저장 프로시저, 여러 명령이 포함된 일괄 처리 또는 키워드가 포함된 SELECT 문이면 처리할 결과 집합이 여러 개가 됩니다.  
  
 또한 ODBC 카탈로그 함수는 데이터를 검색할 수 있습니다. 예를 들어 [Sqlcolumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md) 는 데이터 원본에 있는 열에 대 한 데이터를 검색 합니다. 이러한 결과 집합에는 0개 이상의 행이 포함될 수 있습니다.  
  
 GRANT 또는 REVOKE와 같은 다른 SQL 문은 결과 집합을 반환하지 않습니다. 이러한 문의 경우 **Sqlexecute** 또는 **sqlexecdirect** 의 반환 코드는 일반적으로 문이 성공 했음을 나타냅니다.  
  
 각 INSERT, UPDATE 및 DELETE 문은 수정 내용이 적용되는 행 수만 포함된 결과 집합을 반환합니다. 이 개수는 응용 프로그램이 [Sqlrowcount](../../relational-databases/native-client-odbc-api/sqlrowcount.md)를 호출할 때 사용할 수 있습니다. ODBC 3. *x* 응용 프로그램은 **sqlrowcount** 를 호출 하 여 결과 집합을 검색 하거나 [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md) 를 호출 하 여 취소 해야 합니다. 응용 프로그램이 여러 INSERT, UPDATE 또는 DELETE 문을 포함 하는 일괄 처리 또는 저장 프로시저를 실행 하는 경우 각 수정 문의 결과 집합을 **Sqlrowcount** 를 사용 하 여 처리 하거나 **SQLMoreResults**를 사용 하 여 취소 해야 합니다. 일괄 처리나 저장 프로시저에 SET NOCOUNT ON 문을 포함하여 이 개수를 취소할 수 있습니다.  
  
 Transact-SQL에는 SET NOCOUNT 문이 포함되어 있습니다. NOCOUNT 옵션을 on으로 설정 하면 SQL Server는 문의 영향을 받는 행 수를 반환 하지 않으며 **Sqlrowcount** 는 0을 반환 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버 버전은 NOCOUNT 옵션의 설정 또는 해제 여부를 보고 하는 드라이버 관련 [SQLGetStmtAttr](../../relational-databases/native-client-odbc-api/sqlgetstmtattr.md) 옵션인 SQL_SOPT_SS_NOCOUNT_STATUS를 소개 합니다. **Sqlrowcount** 가 0을 반환할 때마다 응용 프로그램이 SQL_SOPT_SS_NOCOUNT_STATUS를 테스트 해야 합니다. SQL_NC_ON 반환 되는 경우 **Sqlrowcount** 의 값이 0 이면 SQL Server 행 개수가 반환 되지 않았음을 나타냅니다. SQL_NC_OFF 반환 되는 경우에는 NOCOUNT가 OFF이 고 **Sqlrowcount** 의 값 0은 문이 행에 영향을 주지 않았음을 나타냅니다. SQL_SOPT_SS_NOCOUNT_STATUS SQL_NC_OFF 되 면 응용 프로그램에서 **Sqlrowcount** 값을 표시 해서는 안 됩니다. 큰 일괄 처리나 저장 프로시저에는 여러 개의 SET NOCOUNT 문이 포함될 수 있으므로 프로그래머는 SQL_SOPT_SS_NOCOUNT_STATUS가 일정하게 유지된다고 가정할 수 없습니다. **Sqlrowcount** 가 0을 반환할 때마다이 옵션을 테스트 해야 합니다.  
  
 다른 몇 개의 Transact-SQL 문은 데이터를 결과 집합이 아닌 메시지로 반환합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 이러한 메시지를 받을 때 정보 메시지를 사용할 수 있다는 것을 응용 프로그램에 알리기 위해 SQL_SUCCESS_WITH_INFO를 반환 합니다. 그런 다음 응용 프로그램은 **SQLGetDiagRec** 를 호출 하 여 이러한 메시지를 검색할 수 있습니다. 이런 방식으로 작동하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 다음과 같습니다.  
  
-   DBCC  
  
-   SET SHOWPLAN(이전 버전의 SQL Server에서 사용 가능)  
  
-   SET STATISTICS  
  
-   PRINT  
  
-   RAISERROR  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native CLIENT ODBC 드라이버는 심각도가 11 이상인 RAISERROR에 SQL_ERROR를 반환 합니다. RAISERROR의 심각도가 19이면 연결도 삭제됩니다.  
  
 SQL 문의 결과 집합을 처리하기 위해 애플리케이션은 다음 작업을 수행합니다.  
  
-   결과 집합의 특징을 확인합니다.  
  
-   열을 프로그램 변수에 바인딩합니다.  
  
-   단일 값, 전체 행의 값 또는 여러 행의 값을 검색합니다.  
  
-   테스트를 통해 추가 결과 집합이 있는지 확인하고, 있는 경우 루프백하여 새 결과 집합의 특징을 확인합니다.  
  
 데이터 원본에서 행을 검색하고 애플리케이션에 반환하는 프로세스를 인출이라고 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [ODBC&#41;&#40;결과 집합의 특징 확인 ](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
-   [스토리지 할당](../../relational-databases/native-client-odbc-results/assigning-storage.md)  
  
-   [결과 데이터 인출](../../relational-databases/native-client-odbc-results/fetching-result-data.md)  
  
-   [ODBC&#41;&#40;데이터 형식 매핑 ](../../relational-databases/native-client-odbc-results/mapping-data-types-odbc.md)  
  
-   [데이터 형식 사용](../../relational-databases/native-client-odbc-results/data-type-usage.md)  
  
-   [문자 데이터 자동 변환](../../relational-databases/native-client-odbc-results/autotranslation-of-character-data.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;SQL Server Native Client &#40;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [결과 처리 방법 도움말 항목 &#40;ODBC&#41;](../native-client-odbc-how-to/processing-results-process-results.md)  
  
