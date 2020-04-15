---
title: SQLCancelHandle 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 059ed283032feb96ca5e6b12520682ccb034752a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299668"
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle 함수
**규칙**  
 버전 출시: ODBC 3.8  
  
 표준 준수: 없음  
  
 대부분의 ODBC 3.8(및 이후) 드라이버가 이 기능을 구현할 것으로 예상됩니다. 드라이버가 하지 않으면 *핸들* 매개 변수의 연결 핸들을 사용 하 여 **SQLCancelHandle** 호출 IM001의 SQLSTATE와 메시지 '드라이버이 이 기능을 지원하지 않습니다'라는 메시지와 함께 SQL_ERROR 반환 합니다.' *핸들* 매개 변수로 **SQLCancelHandle에** 대 한 호출 드라이버 관리자에 의해 **SQLCancel에** 대 한 호출에 매핑 되 고 드라이버 가 **SQLCancel SQL을**구현 하는 경우 처리할 수 있습니다. 응용 프로그램은 **SQLGetFunctions를** 사용하여 드라이버가 **SQLCancelHandle**을 지원하는지 확인할 수 있습니다.  
  
 **요약**  
 **SQLCancelHandle** 연결 또는 문에 대 한 처리를 취소 합니다. 드라이버 관리자는 *핸들 유형이* SQL_HANDLE_STMT 때 **SQLCancel핸들** 호출에 대한 호출을 **매핑합니다.**  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] 카셀 가공에 할 핸들의 유형입니다. 유효한 값은 SQL_HANDLE_DBC 또는 SQL_HANDLE_STMT.  
  
 *Handle*  
 [입력] 처리를 취소할 핸들입니다.  
  
 *핸들이* *HandleType에서*지정한 형식의 유효한 핸들이 아닌 경우 **SQLCancelHandle은** SQL_INVALID_HANDLE 반환합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLCancelHandle** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 SQL_HANDLE_STMT *핸들 의 핸들* 및 문 *핸들* 핸들 또는 SQL_HANDLE_DBC 핸들 *핸들* 및 연결 *핸들*핸들을 **호출** 하 여 가져올 수 있습니다.  
  
 다음 표에서는 **SQLCancelHandle에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. *인수 \*MessageText* 버퍼에서 [SQLGetDiagRec에서](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다.|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|*핸들과*연결된 문 핸들 중 하나에 대해 비동기적으로 실행되는 문 관련 함수가 호출되었으며 *HandleType은* SQL_HANDLE_DBC 설정되었습니다. **SQLCancelHandle이** 호출될 때 비동기 함수가 계속 실행중이었습니다.<br /><br /> (DM) *핸들 타이* 인수가 SQL_HANDLE_STMT; 연결된 연결 핸들에서 비동기적으로 실행되는 함수가 호출되었습니다. 이 함수가 호출될 때 함수가 계속 실행되고 있었습니다.<br /><br /> (DM) **SQLExecDirect**또는 **SQLMoreResults는** *핸들* 및 *핸들 유형과* 연결된 명령문 핸들 중 하나를 SQL_HANDLE_DBC 설정되어 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. **SQLExecute** 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> **SQLBrowseConnect는** *연결 핸들에*대 한 호출 및 SQL_NEED_DATA 반환 되었습니다. 이 함수는 검색 프로세스가 완료되기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY092|잘못된 특성/옵션 식별자|*핸들 유형이* SQL_HANDLE_ENV 또는 SQL_HANDLE_DESC 설정되었습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *핸들과* 연결된 드라이버가 기능을 지원하지 않습니다.|  
  
 SQL_HANDLE_STMT *위해 핸들 유형* 집합으로 **SQLCancelHandle을** 호출하는 경우 **SQLCancel**함수에서 반환할 수 있는 모든 SQLSTATE를 반환할 수 있습니다.  
  
## <a name="comments"></a>주석  
 이 함수는 **SQLCancel과** 유사하지만 연결 또는 문 핸들을 문 핸들이 아닌 매개 변수로 받아들일 수 있습니다. 드라이버 관리자는 *핸들 유형이* SQL_HANDLE_STMT 때 **SQLCancel핸들** 호출에 대한 호출을 **매핑합니다.** 이렇게 하면 응용 프로그램에서 **SQLCancelHandle을** 사용하여 드라이버가 **SQLCancelHandle**을 구현하지 않은 경우에도 명령문 작업을 취소할 수 있습니다.  
  
 문 작업 취소에 대한 자세한 내용은 [SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)를 참조하십시오.  
  
 진행 중인 작업이 없는 *Handle* 경우 **SQLCancelHandle에** 대 한 호출은 영향을 주지 않습니다.  
  
 연결 핸들의 **SQLCancelHandle은** 다음과 같은 처리 유형을 취소할 수 있습니다.  
  
-   연결에서 비동기적으로 실행되는 함수입니다.  
  
-   다른 스레드의 연결 핸들에서 실행되는 함수입니다.  
  
 **SQLCancelHandle** 연결에서 비동기적으로 실행 되는 함수를 취소 하도록 호출 하는 경우 **SQLCancelHandle에** 의해 게시 된 진단 레코드는 취소 되는 작업에 의해 반환 되는 것에 추가 됩니다. **그러나 다른** 스레드의 연결에서 실행 중인 함수를 취소할 때 는 진단 레코드를 반환 하지 않습니다.  
  
 **SQLCancelHandle을** 사용하여 **SQLEndTran을** 취소하면 연결이 일시 중단된 상태로 배치될 수 있습니다. 일시 중단된 상태에 대한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조하십시오.  
  
> [!NOTE]  
>  Windows 7보다 오래된 Windows 운영 체제에 배포될 응용 프로그램에서 **SQLCancelHandle을** 사용하는 방법에 대한 자세한 내용은 [호환성 매트릭스](../../../odbc/reference/develop-app/compatibility-matrix.md)를 참조하십시오.  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>연결 관련 비동기 처리 취소  
 함수가 SQL_STILL_EXECUTING 반환하는 경우 응용 프로그램은 **SQLCancelHandle을** 호출하여 작업을 취소할 수 있습니다. 취소 요청이 성공하면 **SQLCancelHandle이** SQL_SUCCESS 반환합니다. 원래 함수가 취소된 것은 아닙니다. 취소 요청이 처리되었지만 있음을 나타냅니다. 드라이버와 데이터 원본은 작업이 취소되는 시기 또는 여부를 결정합니다. 반환 코드가 SQL_STILL_EXECUTING 않을 때까지 응용 프로그램은 원래 함수를 계속 호출해야 합니다. 원래 함수가 취소된 경우 반환 코드가 SQL_ERROR SQLSTATE HY008(작업이 취소)됩니다. 원래 함수가 일반 처리를 완료한 경우(취소되지 않음) 반환 코드가 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO, 원래 함수가 실패한 경우 SQL_ERROR 및 HY008 이외의 SQLSTATE(작업 취소됨)입니다.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>다른 스레드에서 실행 하는 함수 취소  
 다중 스레드 응용 프로그램에서 응용 프로그램은 다른 스레드에서 실행 중인 작업을 취소할 수 있습니다. 작업을 취소하려면 응용 프로그램은 함수에서 사용하는 핸들을 사용하지만 다른 스레드에서 **SQLCancelHandle을** 호출합니다. 드라이버와 운영 체제는 작업이 취소되는 방법을 결정합니다. **SQLCancelHandle** 반환 코드는 드라이버가 요청을 처리했는지 여부를 나타내며 SQL_SUCCESS 또는 SQL_ERROR 반환합니다(진단 정보가 반환되지 않습니다). 원래 함수의 처리가 취소되면 원래 함수는 SQL_ERROR 및 SQLSTATE HY008(작업이 취소)으로 반환됩니다.  
  
 **SQLCancelHandle** 함수를 취소 하기 위해 다른 스레드에서 호출 될 때 함수가 실행 되 고 있는 경우 함수가 성공 하 고 취소가 적용 되기 전에 SQL_SUCCESS 반환 할 수 있습니다. **SQLCancelHandle 작업을** 취소할 수 있습니다 전에 작업이 완료 된 경우 **SQLCancelHandle에** 대 한 호출은 영향을 주지 않습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|문 핸들에서 비동기적으로 실행되는 함수를 취소하거나, 데이터가 필요한 명령문에서 함수를 취소하거나, 다른 스레드의 문에서 실행 중인 함수를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
