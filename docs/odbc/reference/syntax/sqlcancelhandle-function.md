---
title: SQLCancelHandle 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 629ff63f6fd06aaccc1f60209231f5c937f4a67d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036128"
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle 함수
**규칙**  
 소개 된 버전: ODBC 3.8  
  
 표준 준수: 없음  
  
 대부분의 ODBC 3.8 이상 드라이버가이 함수를 구현 하는 것으로 예상 됩니다. 드라이버가 그렇지 않으면 *핸들* *매개 SQL_ERROR* 변수에서 연결 핸들을 사용 하 여 **SQLCANCELHANDLE** 을 호출 하면 IM001 및 message ' 드라이버는 문 핸들을 사용 하 여 **Sqlcancelhandle** 을 호출 하 고, 드라이버 관리자에 의해 **sqlcancel** 호출에 매핑되고, 드라이버가 **sqlcancel**을 구현 하는 경우 처리 될 수 있으므로이 함수를 사용 하 여 문 핸들을 사용 하는 sqlcancelhandle을 호출 하면이 응용 프로그램은 **SQLGetFunctions** 를 사용 하 여 드라이버가 **sqlcancelhandle**을 지원 하는지 확인할 수 있습니다.  
  
 **요약**  
 **Sqlcancelhandle** 은 연결 또는 문에서 처리를 취소 합니다. *HandleType* 가 SQL_HANDLE_STMT 경우 드라이버 관리자는 **Sqlcancelhandle** 호출을 **sqlcancel** 호출에 매핑합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 입력 Cacel 처리를 처리할 핸들의 유형입니다. 유효한 값은 SQL_HANDLE_DBC 또는 SQL_HANDLE_STMT입니다.  
  
 *처리*  
 입력 처리를 취소할 핸들입니다.  
  
 *Handle* 이 *HandleType*에 의해 지정 된 형식의 유효한 핸들이 아닌 경우 **sqlcancelhandle** 은 SQL_INVALID_HANDLE를 반환 합니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlcancelhandle** 이 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 연결 된 SQLSTATE 값은 HandleType SQL_HANDLE_STMT의 ** 및 문 핸들 *핸들이* 나 SQL_HANDLE_DBC *HandleType* 및 연결 핸들 *핸들*을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 가져올 수 있습니다.  
  
 다음 표에서는 **Sqlcancelhandle** 에서 일반적으로 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류|비동기 방식으로 실행 되 고, *핸들과*연결 된 문 핸들 중 하나에 대해 문 관련 함수가 호출 되었으며, *HandleType* 가 SQL_HANDLE_DBC로 설정 되었습니다. **Sqlcancelhandle** 이 호출 될 때 비동기 함수가 실행 되 고 있습니다.<br /><br /> (DM) *HandleType* 인수가 SQL_HANDLE_STMT 되었습니다. 연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. 이 함수가 호출 될 때 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *핸들과* 연결 된 문 핸들 중 하나에 대해 호출 되 고 *HandleType* 가 SQL_HANDLE_DBC로 설정 되 고 SQL_PARAM_DATA_AVAILABLE 반환 됩니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> **SQLBrowseConnect** 가 *ConnectionHandle*에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 검색 프로세스가 완료 되기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY092|특성/옵션 식별자가 잘못 되었습니다.|*HandleType* 가 SQL_HANDLE_ENV 또는 SQL_HANDLE_DESC로 설정 되었습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *핸들과* 연결 된 드라이버에서 함수를 지원 하지 않습니다.|  
  
 *HandleType* 가 SQL_HANDLE_STMT로 설정 된 **sqlcancelhandle** 이 호출 되 면 **sqlcancel**함수에서 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다.  
  
## <a name="comments"></a>주석  
 이 함수는 **Sqlcancel** 과 비슷하지만 문 핸들 뿐 아니라 연결 또는 문 핸들을 매개 변수로 사용할 수 있습니다. *HandleType* 가 SQL_HANDLE_STMT 경우 드라이버 관리자는 **Sqlcancelhandle** 호출을 **sqlcancel** 호출에 매핑합니다. 이렇게 하면 응용 프로그램에서 **Sqlcancelhandle** 을 사용 하 여 **sqlcancelhandle**을 구현 하지 않는 경우에도 문 작업을 취소할 수 있습니다.  
  
 문 작업을 취소 하는 방법에 대 한 자세한 내용은 [Sqlcancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)를 참조 하세요.  
  
 *처리* 중인 작업이 없는 경우 **sqlcancelhandle** 에 대 한 호출이 영향을 미치지 않습니다.  
  
 연결 핸들의 **Sqlcancelhandle** 은 다음과 같은 유형의 처리를 취소할 수 있습니다.  
  
-   연결에서 비동기적으로 실행 되는 함수입니다.  
  
-   다른 스레드의 연결 핸들에서 실행 되는 함수입니다.  
  
 연결에서 비동기적으로 실행 되는 함수를 취소 하기 위해 **sqlcancelhandle** 이 호출 되 면 **sqlcancelhandle** 에서 게시 된 진단 레코드는 취소 중인 작업에서 반환 된 레코드에 추가 됩니다. 그러나 **Sqlcancelhandle** 은 다른 스레드의 연결에서 실행 되는 함수를 취소 하는 경우 진단 레코드를 반환 하지 않습니다.  
  
 **Sqlcancelhandle** 을 사용 하 여 **sqlcancelhandle** 을 취소 하면 연결이 suspended 상태로 전환 될 수 있습니다. 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.  
  
> [!NOTE]  
>  Windows 7 이전의 Windows 운영 체제에 배포 되는 응용 프로그램에서 **Sqlcancelhandle** 을 사용 하는 방법에 대 한 자세한 내용은 [호환성 매트릭스](../../../odbc/reference/develop-app/compatibility-matrix.md)를 참조 하세요.  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>연결 관련 비동기 처리 취소  
 함수가 SQL_STILL_EXECUTING 반환 하는 경우 응용 프로그램은 **Sqlcancelhandle** 을 호출 하 여 작업을 취소할 수 있습니다. 취소 요청이 성공 하면 **Sqlcancelhandle** 은 SQL_SUCCESS 반환 합니다. 이는 원래 함수가 취소 된 것을 의미 하지는 않습니다. 이는 취소 요청이 처리 되었음을 나타냅니다. 드라이버 및 데이터 원본은 작업이 취소 되는 시기 또는 시기를 결정 합니다. 응용 프로그램은 반환 코드를 SQL_STILL_EXECUTING 하지 않을 때까지 계속 원래 함수를 호출 해야 합니다. 원래 함수가 취소 된 경우 반환 코드는 SQL_ERROR 및 SQLSTATE HY008 (작업이 취소 됨)입니다. 원래 함수가 취소 되지 않은 정상적인 처리를 완료 한 경우 반환 코드는 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO SQL_ERROR 되거나 원래 함수가 실패 한 경우에는 HY008 (작업 취소 됨)가 아닌 SQLSTATE를 반환 합니다.  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>다른 스레드에서 실행 중인 함수 취소  
 다중 스레드 응용 프로그램에서 응용 프로그램은 다른 스레드에서 실행 중인 작업을 취소할 수 있습니다. 작업을 취소 하기 위해 응용 프로그램은 함수에서 사용 되는 핸들을 사용 하 여 **Sqlcancelhandle** 을 호출 하지만 다른 스레드에서 호출 합니다. 드라이버 및 운영 체제에서 작업을 취소 하는 방법을 결정 합니다. **Sqlcancelhandle** 반환 코드는 드라이버에서 요청을 처리 하 고 SQL_SUCCESS 또는 SQL_ERROR (진단 정보는 반환 되지 않음)를 반환 하는지 여부를 나타냅니다. 원래 함수의 처리가 취소 되 면 원래 함수는 SQL_ERROR 및 SQLSTATE HY008 (작업이 취소 됨)를 반환 합니다.  
  
 함수를 취소 하기 위해 다른 스레드에서 **Sqlcancelhandle** 이 호출 될 때 함수가 실행 되는 경우에는 함수가 성공 하 고 취소를 적용 하기 전에 SQL_SUCCESS를 반환할 수 있습니다. Sqlcancelhandle **에 대 한** 호출은 **sqlcancelhandle** 이 작업을 취소할 수 있도록 하기 전에 작업이 완료 된 경우에는 영향을 주지 않습니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|문 핸들에서 비동기적으로 실행 되는 함수를 취소 하거나, 데이터를 필요로 하는 문에서 함수를 취소 하거나, 다른 스레드의 문에서 실행 되는 함수를 취소 합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [비동기 실행(폴링 메서드)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
