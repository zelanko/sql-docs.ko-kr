---
title: "SQLAllocHandle 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLAllocHandle
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLAllocHandle
helpviewer_keywords: SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
caps.latest.revision: "43"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b8bf173bf0055dc06cf475aa72e137d9ca426222
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlallochandle-function"></a>SQLAllocHandle 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLAllocHandle** 환경, 연결, 문 또는 설명자 핸들을 할당 합니다.  
  
> [!NOTE]  
>  이 함수는 ODBC 2.0 함수를 대체 하는 핸들을 할당 하기 위한 제네릭 함수 **SQLAllocConnect**, **SQLAllocEnv**, 및 **SQLAllocStmt**합니다. 응용 프로그램이 호출할 수 있도록 **SQLAllocHandle** ODBC 2에서 실행 되도록 합니다. *x* 드라이버에 대 한 호출 **SQLAllocHandle** 드라이버 관리자를 매핑된 **SQLAllocConnect**, **SQLAllocEnv**, 또는  **SQLAllocStmt**를 적절 하 게 합니다. 자세한 내용은 "설명"을 참조 하십시오. 자세한 내용은 관리자에 대 한 어떤는 드라이버에 대 한 때 ODBC 3이이 함수를를 매핑합니다. *x* 응용 프로그램이 작동 ODBC 2. *x* 드라이버 참조 [이전 버전과 호환성의 응용 프로그램에 대 한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] 할당할 수에 대 한 핸들의 형식을 **SQLAllocHandle**합니다. 다음 값 중 하나 여야 합니다.  
  
-   SQL_HANDLE_DBC 라는  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   여  
  
 드라이버 관리자와 드라이버는 경우에 SQL_HANDLE_DBC_INFO_TOKEN 핸들이 사용 됩니다. 응용 프로그램에는이 핸들 형식은 사용 하지 않아야 합니다. SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 참조 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.  
  
 *InputHandle*  
 [입력] 해당 컨텍스트에서 새 핸들 할당은 입력된 하는 핸들입니다. 경우 *HandleType* SQL_HANDLE_ENV은 SQL_NULL_HANDLE입니다. 경우 *HandleType* sql_handle_dbc 라는 이며 이어야 합니다. 환경 핸들을 여 또는 SQL_HANDLE_DESC 인 경우 연결 핸들 이어야 합니다.  
  
 *OutputHandlePtr*  
 [출력] 새로 할당 된 데이터 구조에 핸들을 반환 하는 버퍼에 대 한 포인터입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE, 또는 SQL_ERROR 합니다.  
  
 환경 핸들을 이외의 핸들을 할당 하는 경우 때 **SQLAllocHandle** SQL_ERROR를 반환 합니다. 설정 *OutputHandlePtr* SQL_NULL_HDBC, SQL_NULL_HSTMT, 또는 따라 SQL_NULL_HDESC는 값 *HandleType*출력 인수는 null 포인터 하지 않는 한, 합니다. 응용 프로그램의 핸들과 연결 된 진단 데이터 구조에서 추가 정보 얻을 수 있습니다는 *InputHandle* 인수입니다.  
  
## <a name="environment-handle-allocation-errors"></a>환경 핸들 할당 오류  
 환경 할당이 드라이버 관리자 내에서 및 각 드라이버 내에서 발생합니다. 반환 된 오류 **SQLAllocHandle** 와 *HandleType* SQL_HANDLE_ENV의 오류가 발생 한 수준에 따라 다릅니다.  
  
 드라이버 관리자에 대 한 메모리를 할당할 수 없는 경우  *\*OutputHandlePtr* 때 **SQLAllocHandle** 와 *HandleType* SQL_HANDLE_ENV의 호출 또는 응용 프로그램에 대 한 null 포인터를 제공 *OutputHandlePtr*, **SQLAllocHandle** SQL_ERROR를 반환 합니다. 드라이버 관리자 설정 **OutputHandlePtr* SQL_NULL_HENV를 (제공 하지 않는 한 응용 프로그램 SQL_ERROR를 반환 하는 null 포인터). 추가 진단 정보를 연결 하는 핸들이 없습니다 있습니다.  
  
 드라이버 관리자가 응용 프로그램 호출할 때까지 드라이버 수준 환경 핸들 할당 함수를 호출 하지 않으면 **SQLConnect**, **SQLBrowseConnect**, 또는 **SQLDriverConnect**. 드라이버 수준에서 오류가 발생 하는 경우 **SQLAllocHandle** 함수, 다음 드라이버 관리자 – 수준 **SQLConnect**, **SQLBrowseConnect**, 또는  **SQLDriverConnect** 함수 SQL_ERROR를 반환 합니다. 진단 데이터 구조에 SQLSTATE IM004 (드라이버의 **SQLAllocHandle** 실패). 연결 핸들에는 오류가 반환 됩니다.  
  
 드라이버 관리자와 드라이버 사이의 함수 호출의 흐름에 대 한 자세한 내용은 참조 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLAllocHandle** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 는 적절 한 *HandleType* 및 *처리* 의 값으로 설정 *InputHandle*합니다. SQL_SUCCESS_WITH_INFO (않음 하지 SQL_ERROR)에 대해 반환 될 수는 *OutputHandle* 인수입니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLAllocHandle** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08003|연결이 열려 있지 않습니다|DM ()는 *HandleType* 인수 여 되었거나 SQL_HANDLE_DESC, 했지만 연결에 의해 지정 된 *InputHandle* 인수를 열 수 없습니다. 연결 프로세스가 성공적으로 완료 되어야 합니다 (및 연결이 열려 있어야 합니다.)를 할당할 문 또는 설명자 드라이버에 대 한 처리 합니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 **MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버 관리자에서 (DM) 지정된 된 핸들에 대 한 메모리를 할당할 수 없습니다.<br /><br /> 드라이버는 지정 된 핸들에 대 한 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|DM ()는 *OutputHandlePtr* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 *HandleType* 인수를 sql_handle_dbc 라는, 및 **SQLSetEnvAttr** SQL_ODBC_VERSION 환경 특성을 설정 하는 호출 되지 않았습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수에 대 한 호출한는 **InputHandle** 때 계속 실행 하 고는 **SQLAllocHandle** 함수를 호출 했습니다 **HandleType** 설정 여 또는 SQL_HANDLE_DESC 합니다.|  
|HY013|메모리 관리 오류입니다.|*HandleType* 인수 sql_handle_dbc 라는, 여, 또는 SQL_HANDLE_DESC; 였으며 기본 메모리 개체에 액세스할 수 없습니다, 수 있는 메모리가 부족 하기 때문에 함수 호출을 처리할 수 없습니다 조건입니다.|  
|HY014|한도 초과 하는 핸들의 수에|핸들 형식에 대 한 할당 될 수 있는 핸들의 수에 대 한 드라이버에 정의 된 제한으로 표시 된 *HandleType* 인수에 도달 했습니다.|  
|HY092|잘못 된 특성/옵션 식별자|DM ()는 *HandleType* 인수: SQL_HANDLE_ENV, sql_handle_dbc 라는, 여, 또는 SQL_HANDLE_DESC 합니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|*HandleType* 인수 SQL_HANDLE_DESC 이며 드라이버는 ODBC 2. *x* 드라이버입니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|DM ()는 *HandleType* 인수 여, 되었으며 유효한 ODBC 드라이버가 없습니다.<br /><br /> DM ()는 *HandleType* 인수 SQL_HANDLE_DESC, 였으며 드라이버 설명자 핸들 할당을 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLAllocHandle** 다음 섹션에 설명 된 대로 환경, 연결, 문 및 설명자에 대 한 핸들을 할당 하는 데 사용 됩니다. 핸들에 대 한 일반 정보를 참조 하십시오. [핸들](../../../odbc/reference/develop-app/handles.md)합니다.  
  
 여러 할당 드라이버에서 지원 되는 경우 한 번에 응용 프로그램에서 둘 이상의 환경, 연결 또는 문 핸들을 할당할 수 있습니다. ODBC, 환경, 연결, 문 또는 설명자 핸들과 한 번에 할당 될 수 있는 수에 제한이 없음을 정의 됩니다. 드라이버는 특정 유형의; 한 번에 할당 될 수 있는 핸들의 수에 제한을 설정할 수 있습니다. 자세한 내용은 드라이버 설명서를 참조 합니다.  
  
 응용 프로그램을 호출 하는 경우 **SQLAllocHandle** 와  *\*OutputHandlePtr* 드라이버 덮어씁니다 환경, 연결, 문 또는 이미 존재 하는 설명자 핸들을으로 설정 된 와 관련 된 정보는 *처리*응용 프로그램은 사용 하 여 연결 풀링 (참조 "할당 하는 환경 특성에 대 한 연결 풀링"이이 섹션의 뒷부분에 나오는) 하지 않는 한, 합니다. 드라이버 관리자를 확인 하지 않습니다 여부는 *처리* 에 입력 한  *\*OutputHandlePtr* 이미 사용 중 또는 시키는 핸들의 이전 내용의 덮어쓰기 전에 확인 .  
  
> [!NOTE]  
>  잘못 된 ODBC 응용 프로그램 프로그래밍 호출 하는 **SQLAllocHandle** 에 대해 정의 된 동일한 응용 프로그램 변수를 두고 두 번  *\*OutputHandlePtr* 호출 하지 않고  **SQLFreeHandle** 를 재할당 하기 전에 핸들을 해제 합니다. ODBC 덮어쓰기 일관 되지 않은 동작이 또는 ODBC 드라이버 안되며 오류 방식으로 처리 될 수 있습니다.  
  
 여러 스레드를 지 원하는 운영 체제에서 응용 프로그램 서로 다른 스레드에서 동일한 환경, 연결, 문 또는 설명자 핸들을 사용할 수 있습니다. 드라이버가이 정보에 대 한 안전 하 고 다중 스레드 액세스를 지원 하므로 해야 합니다. 이 작업을 수행할는 한 가지 방법은 임계 영역 또는 세마포를 사용 하 여은 예를 들어 있습니다. 스레딩에 대 한 자세한 내용은 참조 [다중 스레딩](../../../odbc/reference/develop-app/multithreading.md)합니다.  
  
 **SQLAllocHandle** SQL_ATTR_ODBC_VERSION 환경 특성을 설정 하지 않는 응용 프로그램 또는 SQLSTATE HY010가 환경 특성을 설정 해야; 환경 핸들을 할당을 호출 될 때 (함수 시퀀스 오류) 됩니다. 이 반환 **SQLAllocHandle** 연결 핸들을 할당 하기 위해 호출 됩니다.  
  
 표준 호환 응용 프로그램에 대 한 **SQLAllocHandle** 에 매핑된 **SQLAllocHandleStd** 컴파일 타임에 있습니다. 이 두 기능 간의 차이점은 **SQLAllocHandleStd** 으로 호출 될 경우 SQL_OV_ODBC3를 SQL_ATTR_ODBC_VERSION 환경 특성을 설정는 *HandleType* 인수는 SQL로 설정 _HANDLE_ENV 합니다. 표준 호환 응용 프로그램은 ODBC 3 항상 수행 됩니다. *x* 응용 프로그램입니다. 또한 표준을 등록 해야 응용 프로그램 버전은 필요 하지 않습니다. 이; 이들 두 함수 간의 유일한 차이점 그렇지 않으면 동일 합니다. **SQLAllocHandleStd** 에 매핑된 **SQLAllocHandle** 내 드라이버 관리자입니다. 따라서 타사 드라이버 필요가 없습니다 구현 **SQLAllocHandleStd**합니다.  
  
 ODBC 3.8 응용 프로그램을 사용 해야 합니다.  
  
-   **SQLAllocHandle 및 하지 SQLAllocHandleStd** 환경 핸들을 할당 합니다.  
  
-   **SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION 환경 특성 SQL_OV_ODBC3_80을로 설정 합니다.  
  
## <a name="allocating-an-environment-handle"></a>환경 핸들 할당  
 환경 핸들 유효한 연결 핸들 활성 연결 핸들 등과 같은 전역 정보에 대 한 액세스를 제공합니다. 환경 핸들에 대 한 일반 정보를 참조 하십시오. [환경 핸들](../../../odbc/reference/develop-app/environment-handles.md)합니다.  
  
 환경 핸들을 요청 하려면 응용 프로그램이 호출 **SQLAllocHandle** 와 *HandleType* SQL_HANDLE_ENV의 및 *InputHandle* SQL_NULL_HANDLE입니다. 환경 정보 및 연결된 핸들의 값을 다시 전달에 대 한 메모리를 할당 하는 드라이버는  *\*OutputHandlePtr* 인수입니다. 응용 프로그램 전달은  *\*OutputHandle* 환경 핸들 인수를 필요로 하는 모든 후속 호출에는 값입니다. 자세한 내용은 참조 [환경 처리할 할당](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)합니다.  
  
 드라이버 관리자의 환경 핸들을 이미 있을 경우 드라이버의 환경 핸들 다음 아래 **SQLAllocHandle** 와 *HandleType* SQL_HANDLE_ENV의 호출 되지 않습니다 드라이버의 경우는 연결 되 면만 **SQLAllocHandle** 와 *HandleType* sql_handle_dbc 라는의 합니다. 드라이버에서 SQL_HANDLE_ENV HandleType와 SQLAllocHandle와는 HandleType의 sql_handle_dbc 라는와 SQLAllocHandle 운전 환경 핸들 드라이버 관리자 환경 핸들에서 존재 하지 않습니다 있으면 호출 되는 경우 첫 번째 연결 환경 핸들은 드라이버에 연결 되어 있습니다.  
  
 드라이버 관리자가 처리 하는 경우는 **SQLAllocHandle** 작동는 *HandleType* SQL_HANDLE_ENV의 확인 된 **추적** 시스템의 [ODBC] 섹션에는 키워드 정보입니다. 1로 설정 하면 드라이버 관리자에서 현재 응용 프로그램에 대 한 추적이 있습니다. 추적 플래그를 설정 하는 경우 추적 시작 첫 번째 환경 핸들 할당 되 고 마지막 환경 핸들이 해제 될 때 종료 됩니다. 자세한 내용은 참조 [데이터 소스 구성](../../../odbc/reference/install/configuring-data-sources.md)합니다.  
  
 호출 하는 응용 프로그램 환경 핸들을 할당 한 후 **SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION 환경 특성을 설정 하 여 환경 핸들에 있습니다. 하기 전에이 특성이 설정 되지 않은 경우 **SQLAllocHandle** 연결 핸들을 할당 하기 위해 호출 됩니다는 환경에는 연결을 할당 호출은 SQLSTATE HY010을 반환 합니다 (함수 시퀀스 오류). 자세한 내용은 참조 [응용 프로그램의 ODBC 버전 선언](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)합니다.  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>연결 풀링을 위해 공유 환경 할당  
 환경은 단일 프로세스에서 여러 구성 요소 간에 공유할 수 있습니다. 공유 환경 동시에 둘 이상의 구성 요소에서 사용할 수 있습니다. 구성 요소는 공유 환경에서 사용할 경우 풀링된 연결을 할당 하 고 해당 연결을 다시 만들지 않고 기존 연결을 사용 하 게 사용할 수 있습니다.  
  
 응용 프로그램 호출 해야 하는 공유 환경 할당 연결 풀링을 위해 사용할 수 있습니다, **SQLSetEnvAttr** SQL_CP_ONE_PER_DRIVER 또는 SQL_CP_ONE_PER_ SQL_ATTR_CONNECTION_POOLING 환경 특성을 설정 하려면 HENV 합니다. **SQLSetEnvAttr** 이 예에서 사용 하 여 호출 *EnvironmentHandle* 프로세스 수준 특성 특성에는 null로 설정 합니다.  
  
 연결 풀링을 활성화 되어 있는 응용 프로그램 호출 **SQLAllocHandle** 와 *HandleType* 인수를 SQL_HANDLE_ENV로 설정 합니다. 이 호출에 의해 할당 되는 환경 연결 풀링을 설정 되어 있으므로 암시적 공유 환경이 됩니다.  
  
 사용 되는 환경까지 확인 되지 않으면 공유 환경 할당 되 면 **SQLAllocHandle** 와 *HandleType* sql_handle_dbc 라는의 호출 됩니다. 이 시점에서 드라이버 관리자는 응용 프로그램에서 요청한 환경 특성과 일치 하는 기존 환경의 찾을 하려고 시도 합니다. 이러한 환경이 있는 경우 공유 환경으로는 하나이 만들어집니다. 드라이버 관리자는 각 공유 환경;에 대 한 참조 횟수를 유지 관리 환경을 처음 만들어질 때 개수가 1로 설정 됩니다. 일치 하는 환경이 발견 되 면 해당 환경 핸들이 응용 프로그램에 반환 되 고 참조 횟수가 증가 합니다. 이런이 방식으로 할당 된 환경 핸들 입력 인수로 환경 핸들을 허용 하는 ODBC 함수에서 사용할 수 있습니다.  
  
## <a name="allocating-a-connection-handle"></a>연결 핸들 할당  
 설명자 핸들에 연결 및 트랜잭션이 현재 인지 열 및 연결 핸들 유효한 문 등의 정보에 대 한 액세스를 제공 합니다. 연결 핸들에 대 한 일반 정보를 참조 하십시오. [연결 핸들](../../../odbc/reference/develop-app/connection-handles.md)합니다.  
  
 연결 핸들을 요청 하려면 응용 프로그램이 호출 **SQLAllocHandle** 와 *HandleType* sql_handle_dbc 라는입니다. *InputHandle* 인수에 대 한 호출에서 반환 된 환경 핸들으로 설정 되어 **SQLAllocHandle** 를 해당 핸들을 할당 합니다. 드라이버는 연결 정보 및 연결된 핸들의 값을 다시 전달에 대 한 메모리를 할당  *\*OutputHandlePtr*합니다. 응용 프로그램 전달은  *\*OutputHandlePtr* 연결 핸들을 필요로 하는 모든 후속 호출에는 값입니다. 자세한 내용은 참조 [연결 핸들 할당](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)합니다.  
  
 드라이버 관리자가 처리는 **SQLAllocHandle** 함수를 호출 하는 드라이버의 **SQLAllocHandle** 응용 프로그램 호출 될 때 작동 **SQLConnect**, **SQLBrowseConnect**, 또는 **SQLDriverConnect**합니다. (자세한 내용은 참조 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md).)  
  
 하기 전에 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 하지 않으면 **SQLAllocHandle** 연결 핸들을 할당 하기 위해 호출 됩니다는 환경에는 연결을 할당 호출은 SQLSTATE HY010을 반환 합니다 (시퀀스 함수 오류)입니다.  
  
 응용 프로그램 호출 하는 경우 **SQLAllocHandle** 와 *InputHandle* 인수 SQL_HANDLE_DBC로 설정 하 고 공유 환경 핸들을 설정, 드라이버 관리자를 기존 공유를 확인 하려고 합니다. 응용 프로그램에서 설정한 환경 특성을 일치 하는 환경입니다. 이러한 환경이 있는 경우 하나 만들어집니다 1 참조 카운트 (드라이버 관리자에서 유지). 일치 하는 공유 환경 발견 되, 해당 핸들이 응용 프로그램에 반환 된 및 참조 개수가 증가 합니다.  
  
 사용 되는 실제 연결 될 때까지 드라이버 관리자에서 확인 되지 않으면 **SQLConnect** 또는 **SQLDriverConnect** 호출 됩니다. 드라이버 관리자 연결 옵션에 대 한 호출에서 사용 하 여 **SQLConnect** (또는 연결 키워드에 대 한 호출에서 **SQLDriverConnect**) 연결 특성에 대 한 연결 할당 한 후 설정 사용 해야 하는 풀에서 연결을 확인 합니다. 자세한 내용은 참조 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
## <a name="allocating-a-statement-handle"></a>문 핸들 할당  
 문 핸들 SQL 문 처리에 대 한 오류 메시지, 커서 이름, 상태 정보 등 문 정보에 대 한 액세스를 제공합니다. 문 핸들에 대 한 일반 정보를 참조 하십시오. [문 핸들](../../../odbc/reference/develop-app/statement-handles.md)합니다.  
  
 문 핸들을 요청 하려면 응용 프로그램 데이터 원본에 연결 하 고 다음 호출 **SQLAllocHandle** SQL 문을 전송 하기 전에. 이 호출에서 *HandleType* 여로 설정 해야 하 고 *InputHandle* 연결 핸들에 대 한 호출에서 반환 된로 설정 해야 **SQLAllocHandle** 해당 핸들을 할당 합니다. 드라이버는 문 정보에 대 한 메모리를 할당, 지정 된 연결 및 연결된 핸들의 값을 다시 전달 문 핸들 연결  *\*OutputHandlePtr*합니다. 응용 프로그램 전달은  *\*OutputHandlePtr* 문 핸들을 필요로 하는 모든 후속 호출에는 값입니다. 자세한 내용은 참조 [문 핸들 할당](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)합니다.  
  
 문 핸들 할당 되 면 드라이버 자동으로 4 개의 설명자의 집합을 할당 하 고 SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC, SQL_ATTR_IMP_ROW_DESC, 및 SQL_ATTR_IMP_PARAM_DESC에 이러한 설명자에 대 한 핸들을 할당 합니다. 문 특성입니다. 이 라고 *암시적으로* 설명자를 할당 합니다. 응용 프로그램 설명자를 명시적으로 할당 하려면 다음 섹션인 "설명자 핸들을 할당 합니다."를 참조 하십시오.  
  
## <a name="allocating-a-descriptor-handle"></a>설명자 핸들 할당  
 응용 프로그램 호출 하는 경우 **SQLAllocHandle** 와 *HandleType* SQL_HANDLE_DESC의 드라이버는 응용 프로그램 설명자를 할당 합니다. 이 라고 *명시적으로* 설명자를 할당 합니다. 응용 프로그램 지시를 호출 하 여 지정 된 문 핸들에는 자동으로 할당 된 항목 대신 명시적으로 할당 된 응용 프로그램 설명자를 사용 하는 드라이버는 **SQLSetStmtAttr** 는 SQL_ATTR_APP_ROW_DESC 함수 또는 SQL_ATTR_APP_PARAM_DESC 특성입니다. 구현 설명자를 명시적으로 할당할 수 없습니다 및 구현 설명자에 지정할 수는 **SQLSetStmtAttr** 함수 호출 합니다.  
  
 (으로 자동으로 할당 된 설명자) 설명자를 명시적으로 할당 된 문 핸들 대신 연결 핸들에 연결 됩니다. 설명자는 응용 프로그램이 데이터베이스에 실제로 연결 되는 경우에 할당 된 상태로 유지 합니다. 명시적으로 할당 된 설명자 연결 핸들에 연결 되어 있으므로, 응용 프로그램 연결 내에서 둘 이상의 문을 사용 하 여 명시적으로 할당 된 설명자를 연결할 수 있습니다. 암시적으로 할당 된 응용 프로그램 설명자 반면에 연결할 수 없습니다 둘 이상의 문 핸들을 포함 합니다. (이에 연결할 수 없습니다 것에 대 한 할당 된 다른 모든 문 핸들입니다.) 명시적으로 할당 된 설명자 핸들을 명시적으로 해제할 수 있습니다. 응용 프로그램이 나 호출 하 여 **SQLFreeHandle** 와 *HandleType* SQL_HANDLE_DESC, 또는 암시적으로 연결 된 경우 닫힙니다.  
  
 명시적으로 할당 된 설명자 해제 될 때 암시적으로 할당 된 설명자 다시와 관련이 문이 있습니다. (해당 문에 대해 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 특성 암시적으로 할당 된 설명자 핸들을 다시 설정 됩니다.) 연결에 명시적으로 할당 된 설명자와 연결 된 모든 문이 적용 됩니다.  
  
 설명자에 대 한 자세한 내용은 참조 [설명자](../../../odbc/reference/develop-app/descriptors.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [ODBC 프로그램 샘플](../../../odbc/reference/sample-odbc-program.md), [SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md), 및 [SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|환경, 연결, 문 또는 설명자 핸들 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|실행할 문을 준비합니다.|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|설명자 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|환경 특성 설정|[SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
