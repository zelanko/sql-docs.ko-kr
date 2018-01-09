---
title: "진단 레코드 및 필드 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-error-messages
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- header records [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], diagnostic records
- ODBC error handling, diagnostic records
- SQLGetDiagField function
- diagnostic records [ODBC]
- errors [ODBC], diagnostic records
- fields [ODBC]
- status information [ODBC]
ms.assetid: 4949530c-62d1-4f1a-b592-144244444ce0
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ced62a96f94fa4cb929f295f7a390c60b42e15d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="diagnostic-records-and-fields"></a>진단 레코드 및 필드
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  진단 레코드는 ODBC 환경, 연결, 문 또는 설명자 핸들과 연결되어 있습니다. ODBC 함수가 SQL_SUCCESS 또는 SQL_INVALID_HANDLE이 아닌 반환 코드를 생성하는 경우 해당 함수에서 호출된 핸들에 정보 또는 오류 메시지가 포함된 진단 레코드가 연결되어 있습니다. 이러한 레코드는 해당 핸들을 사용하여 다른 함수를 호출할 때까지 유지되며, 이때 레코드가 삭제됩니다. 한 번에 핸들에 연결할 수 있는 진단 레코드 수에는 제한이 없습니다.  
  
 두 가지 유형의 진단 레코드(헤더 및 상태)가 있습니다. 헤더 레코드는 레코드 0이고, 상태 레코드가 있을 경우 레코드 1 이상이 됩니다. 진단 레코드에는 헤더 레코드 및 상태 레코드에 대한 여러 필드가 포함됩니다. ODBC 구성 요소에서 해당 진단 레코드 필드를 정의할 수도 있습니다.  
  
 헤더 레코드의 필드에는 반환 코드, 행 수, 상태 레코드 수, 실행된 문 유형 등 함수 실행에 대한 일반 정보가 포함됩니다. ODBC 함수에서 SQL_INVALID_HANDLE을 반환하지 않을 경우 헤더 레코드는 항상 생성됩니다. 헤더 레코드의 필드의 전체 목록은 참조 하십시오. [SQLGetDiagField](../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md)합니다.  
  
 상태 레코드의 필드에는 SQLSTATE, 원시 오류 번호, 진단 메시지, 열 번호 및 행 번호를 비롯하여 ODBC 드라이버 관리자, 드라이버 또는 데이터 원본에서 반환된 특정 오류 또는 경고에 대한 정보가 포함됩니다. 상태 레코드는 함수에서 SQL_ERROR, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_NEED_DATA 또는 SQL_STILL_EXECUTING을 반환하는 경우에만 생성됩니다. 상태 레코드의 필드의 전체 목록은 참조 하십시오. **SQLGetDiagField**합니다.  
  
 **SQLGetDiagRec** 해당 ODBC SQLSTATE, 원시 오류 번호 및 진단 메시지 필드와 함께 단일 진단 레코드를 검색 합니다. 이 기능은 ODBC 2와 비슷합니다. *x***SQLError** 함수입니다. ODBC 3의 가장 간단한 오류 처리 함수입니다. *x* 반복 해 서 호출 **SQLGetDiagRec** 부터는 *RecNumber* 매개 변수를 증가 및 1로 설정 *RecNumber* 될 때까지 1 씩 **SQLGetDiagRec** SQL_NO_DATA를 반환 합니다. 이것은 ODBC 2입니다. *x* 응용 프로그램 호출 **SQLError** SQL_NO_DATA_FOUND가 반환 될 때까지 합니다.  
  
 ODBC 3입니다. *x* ODBC 2 보다 훨씬 더 많은 진단 정보를 지원 합니다. *x*합니다. 이 정보를 사용 하 여 검색 된 진단 레코드의 추가 필드에 저장 됩니다 **SQLGetDiagField**합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 검색할 수 있는 드라이버별 진단 필드에 **SQLGetDiagField**합니다. 이러한 드라이버별 필드의 레이블은 sqlncli.h에서 정의됩니다. 해당 레이블을 사용하여 각 진단 레코드와 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 상태, 심각도 수준, 서버 이름, 프로시저 이름 및 줄 번호를 검색합니다. 또한 sqlncli.h에는 드라이버는 응용 프로그램을 호출 하는 경우 TRANSACT-SQL 문을 식별 하는 데 사용 하는 코드 정의가 **SQLGetDiagField** 와 *DiagIdentifier* SQL_DIAG_DYNAMIC_로 설정 FUNCTION_CODE 합니다.  
  
 **SQLGetDiagField** 기본 드라이버에서 캐시 한 오류 정보를 사용 하 여 ODBC 드라이버 관리자에서 처리 됩니다. ODBC 드라이버 관리자는 성공적으로 연결될 때까지 드라이버별 진단 필드를 캐시하지 않습니다. **SQLGetDiagField** 성공적으로 연결 완료 되기 전에 드라이버별 진단 필드를 가져오려는 호출 되 면 SQL_ERROR를 반환 합니다. ODBC 연결 함수에서 SQL_SUCCESS_WITH_INFO를 반환할 경우 해당 연결 함수의 드라이버별 진단 필드를 아직 사용할 수 없습니다. 호출을 시작할 수 **SQLGetDiagField** 다른 ODBC를 변경한 후에 드라이버별 진단 필드에 대 한 연결 함수 뒤에 함수 호출 합니다.  
  
 대부분의 오류 보고는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 진단할 수 있는 효과적으로 반환 하는 정보를 사용 하 여 **SQLGetDiagRec**합니다. 하지만 일부 경우에서는 오류를 진단할 때 드라이버별 진단 필드에서 반환된 정보가 중요합니다. ODBC 오류 처리기를 사용 하 여 응용 프로그램에 대 한 코드를 작성할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버는 것이 좋습니다를 사용 하도록 **SQLGetDiagField** 검색할 최소한 SQL_DIAG_SS_MSGSTATE는 및 SQL_DIAG_SS_SEVERITY 드라이버 관련 필드입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 코드의 여러 위치에서 특정 오류가 발생할 수 있는 경우 SQL_DIAG_SS_MSGSTATE를 통해 Microsoft 지원 엔지니어가 오류 발생 위치를 구체적으로 확인할 수 있으므로 문제 진단에 도움이 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [오류 및 메시지 처리](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
