---
title: SQLAllocHandle 함수 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2fcf08a4a55a7c65dbc94219ac908da83ea15bad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68344276"
---
# <a name="sqlallochandle-function"></a>SQLAllocHandle 함수
**규칙**  
 소개 된 버전: ODBC 3.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLAllocHandle** 는 환경, 연결, 문 또는 설명자 핸들을 할당 합니다.  
  
> [!NOTE]  
>  이 함수는 ODBC 2.0 함수 **Sqlallocconnect**, **Sqlallocconnect**및 **sqlallocconnect**를 대체 하는 핸들을 할당 하는 일반 함수입니다. **SQLAllocHandle** 를 호출 하는 응용 프로그램에서 ODBC 2를 사용할 수 있도록 허용 합니다. *x* 드라이버는 **SQLAllocHandle** 에 대 한 호출이 드라이버 관리자에서 **sqlallocconnect**, **sqlallocconnect**또는 **sqlallocconnect**에 매핑됩니다. 자세한 내용은 "설명"을 참조 하십시오. ODBC 3의 경우 드라이버 관리자가이 기능을에 매핑하는 방법에 대 한 자세한 내용을 확인 하십시오. *x* 응용 프로그램에서 ODBC 2를 사용 하 고 있습니다. *x* 드라이버 [응용 프로그램의 이전 버전과의 호환성을 위해 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 입력 **SQLAllocHandle**에서 할당할 핸들의 형식입니다. 다음 값 중 하나여야 합니다.  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 핸들은 드라이버 관리자 및 드라이버 에서만 사용 됩니다. 응용 프로그램은이 핸들 형식을 사용 하면 안 됩니다. SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)을 참조 하세요.  
  
 *InputHandle*  
 입력 새 핸들이 할당 될 컨텍스트를 포함 하는의 입력 핸들입니다. *HandleType* 가 SQL_HANDLE_ENV 경우 SQL_NULL_HANDLE 됩니다. *HandleType* 이 SQL_HANDLE_DBC 경우이 핸들은 환경 핸들 이어야 하 고 SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC 경우 연결 핸들 이어야 합니다.  
  
 *OutputHandlePtr*  
 출력 새로 할당 된 데이터 구조에 대 한 핸들을 반환할 버퍼에 대 한 포인터입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE 또는 SQL_ERROR입니다.  
  
 환경 핸들 이외의 핸들을 할당할 때 **SQLAllocHandle** 가 SQL_ERROR 반환 하는 경우 출력 인수가 NULL 포인터가 아닌 경우 *HandleType*의 값에 따라 *OutputHandlePtr* 를 SQL_NULL_HDBC, SQL_NULL_HSTMT 또는 SQL_NULL_HDESC로 설정 합니다. 그러면 응용 프로그램은 *InputHandle* 인수의 핸들과 연결 된 진단 데이터 구조에서 추가 정보를 가져올 수 있습니다.  
  
## <a name="environment-handle-allocation-errors"></a>환경 핸들 할당 오류  
 환경 할당은 드라이버 관리자 및 각 드라이버 내에서 발생 합니다. **SQLAllocHandle** 에서 반환 하는 오류는 오류가 발생 한 수준에 따라 달라 집니다. *HandleType* 가 SQL_HANDLE_ENV.  
  
 *HandleType* 의 SQL_HANDLE_ENV **SQLAllocHandle** 가 호출 되거나 응용 프로그램이 *OutputHandlePtr*에 대해 null 포인터를 제공 하는 경우 드라이버 관리자가 * \*OutputHandlePtr* 에 대해 메모리를 할당할 수 없는 경우 **SQLAllocHandle** 는 SQL_ERROR를 반환 합니다. 응용 프로그램이 SQL_ERROR를 반환 하는 NULL 포인터를 제공 하지 않는 한 드라이버 관리자는 **OutputHandlePtr* 을 SQL_NULL_HENV로 설정 합니다. 추가 진단 정보를 연결 하는 데 사용할 핸들이 없습니다.  
  
 드라이버 관리자는 응용 프로그램에서 **SQLConnect**, **SQLBrowseConnect**또는 **SQLDriverConnect**를 호출할 때까지 드라이버 수준 환경 핸들 할당 함수를 호출 하지 않습니다. 드라이버 수준 **SQLAllocHandle** 함수에서 오류가 발생 하는 경우 드라이버 관리자 수준 **SQLConnect**, **SQLBrowseConnect**또는 **SQLDriverConnect** 함수는 SQL_ERROR를 반환 합니다. 진단 데이터 구조에 SQLSTATE IM004 (드라이버의 **SQLAllocHandle** 실패)가 포함 되어 있습니다. 이 오류는 연결 핸들에서 반환 됩니다.  
  
 드라이버 관리자와 드라이버 간의 함수 호출 흐름에 대 한 자세한 내용은 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조 하세요.  
  
## <a name="diagnostics"></a>진단  
 **SQLAllocHandle** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 적절 한 *HandleType* 및 *핸들* 을 *InputHandle*값으로 설정 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. *OutputHandle* 인수에 대해서는 SQL_SUCCESS_WITH_INFO (SQL_ERROR는 아님)를 반환할 수 있습니다. 다음 표에서는 일반적으로 **SQLAllocHandle** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 값에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08003|연결이 열려 있지 않음|(DM) *HandleType* 인수가 SQL_HANDLE_STMT 되었거나 SQL_HANDLE_DESC 되었지만 *InputHandle* 인수로 지정 된 연결이 열려 있지 않습니다. 드라이버에서 문이나 설명자 핸들을 할당 하려면 연결 프로세스가 성공적으로 완료 되 고 연결이 열려 있어야 합니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. **MessageText* Buffer의 **SQLGetDiagRec** 에서 반환 된 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|(DM) 드라이버 관리자가 지정 된 핸들에 대해 메모리를 할당할 수 없습니다.<br /><br /> 드라이버가 지정 된 핸들에 대해 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|(DM) *OutputHandlePtr* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) *HandleType* 인수가 SQL_HANDLE_DBC 되었으며 SQL_ODBC_VERSION 환경 특성을 설정 하기 위해 **SQLSetEnvAttr** 가 호출 되지 않았습니다.<br /><br /> (DM) **InputHandle** 에 대해 비동기적으로 실행 되는 함수가 호출 되었으며 **HandleType** 가 SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC로 설정 된 상태에서 **SQLAllocHandle** 함수가 호출 될 때 계속 실행 중입니다.|  
|HY013|메모리 관리 오류|*HandleType* 인수는 SQL_HANDLE_DBC, SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC입니다. 메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY014|초과 된 핸들 수 제한|*HandleType* 인수가 나타내는 핸들의 형식에 할당할 수 있는 핸들 수에 대 한 드라이버 정의 제한에 도달 했습니다.|  
|HY092|특성/옵션 식별자가 잘못 되었습니다.|(DM) *HandleType* 인수는 SQL_HANDLE_ENV, SQL_HANDLE_DBC, SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC이 아닙니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|*HandleType* 인수가 SQL_HANDLE_DESC 되었으며 드라이버가 ODBC 2 였습니다. *x* 드라이버.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *HandleType* 인수가 SQL_HANDLE_STMT 되었으며 드라이버가 올바른 ODBC 드라이버가 아닙니다.<br /><br /> (DM) *HandleType* 인수가 SQL_HANDLE_DESC 되었지만 드라이버에서 설명자 핸들 할당을 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLAllocHandle** 는 다음 섹션에 설명 된 대로 환경, 연결, 문 및 설명자에 대 한 핸들을 할당 하는 데 사용 됩니다. 핸들에 대 한 일반적인 내용은 [핸들](../../../odbc/reference/develop-app/handles.md)을 참조 하십시오.  
  
 여러 할당이 드라이버에서 지원 되는 경우 한 번에 둘 이상의 환경, 연결 또는 문 핸들을 응용 프로그램에서 할당할 수 있습니다. ODBC에서 한 번에 할당할 수 있는 환경, 연결, 문 또는 설명자 핸들 수에는 제한이 정의 되어 있지 않습니다. 드라이버는 한 번에 할당할 수 있는 특정 핸들 형식의 수에 제한을 적용할 수 있습니다. 자세한 내용은 드라이버 설명서를 참조 하세요.  
  
 응용 프로그램에서 * \*OutputHandlePtr* 가 이미 존재 하는 환경, 연결, 문 또는 설명자 핸들로 설정 된 **SQLAllocHandle** 를 호출 하는 경우, 응용 프로그램에서 연결 풀링을 사용 하지 않는 한 드라이버는 *핸들과*연결 된 정보를 덮어씁니다 (이 섹션의 뒷부분에 나오는 "연결 풀링을 위한 환경 특성 할당" 참조). 드라이버 관리자는 * \*OutputHandlePtr* 에 입력 된 *핸들이* 이미 사용 중인지 여부를 확인 하지 않으며 핸들의 이전 콘텐츠를 덮어쓰기 전에 확인 하지 않습니다.  
  
> [!NOTE]  
>  **Sqlfreehandle** 을 호출 하지 않고 * \*OutputHandlePtr* 에 대해 정의 된 동일한 응용 프로그램 변수를 사용 하 여 **SQLAllocHandle** 를 두 번 호출 하 여 다시 할당 하기 전에 핸들을 해제 하는 것이 잘못 된 ODBC 응용 프로그램 프로그래밍 이러한 방식으로 ODBC 핸들을 덮어쓰면 ODBC 드라이버의 일부에서 일관 되지 않은 동작이 나 오류가 발생할 수 있습니다.  
  
 여러 스레드를 지 원하는 운영 체제에서 응용 프로그램은 다른 스레드에서 동일한 환경, 연결, 문 또는 설명자 핸들을 사용할 수 있습니다. 따라서 드라이버는이 정보에 대 한 안전한 다중 스레드 액세스를 지원 해야 합니다. 예를 들어이를 구현 하는 한 가지 방법은 임계 영역 또는 세마포를 사용 하는 것입니다. 스레딩에 대 한 자세한 내용은 [다중 스레딩](../../../odbc/reference/develop-app/multithreading.md)을 참조 하세요.  
  
 **SQLAllocHandle** 는 환경 핸들을 할당 하기 위해 호출 될 때 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 하지 않습니다. 환경 특성은 응용 프로그램에서 설정 해야 합니다. 그렇지 않으면 **SQLAllocHandle** 를 호출 하 여 연결 핸들을 할당할 때 SQLSTATE HY010 (함수 시퀀스 오류)가 반환 됩니다.  
  
 표준 규격 응용 프로그램의 경우 **SQLAllocHandle** 는 컴파일 시간에 **SQLAllocHandleStd** 에 매핑됩니다. 이러한 두 함수 간의 차이점은 **SQLAllocHandleStd** 는 SQL_HANDLE_ENV로 설정 된 *HandleType* 인수를 사용 하 여 호출 될 때 SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC3로 설정 한다는 것입니다. 표준 규격 응용 프로그램은 항상 ODBC 3 이므로이 작업을 수행 합니다. *x* 응용 프로그램. 또한 표준에는 응용 프로그램 버전을 등록 하지 않아도 됩니다. 이는이 두 함수 간의 유일한 차이점입니다. 그렇지 않으면 동일 합니다. **SQLAllocHandleStd** 는 드라이버 관리자 내의 **SQLAllocHandle** 에 매핑됩니다. 따라서 타사 드라이버는 **SQLAllocHandleStd**를 구현할 필요가 없습니다.  
  
 ODBC 3.8 응용 프로그램은 다음을 사용 해야 합니다.  
  
-   환경 핸들을 할당 하는 **SQLAllocHandle 및 Not SQLAllocHandleStd** .  
  
-   **SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION 환경 특성을 SQL_OV_ODBC3_80로 설정 합니다.  
  
## <a name="allocating-an-environment-handle"></a>환경 핸들 할당  
 환경 핸들은 유효한 연결 핸들 및 활성 연결 핸들과 같은 전역 정보에 대 한 액세스를 제공 합니다. 환경 핸들에 대 한 일반 정보는 [환경 핸들](../../../odbc/reference/develop-app/environment-handles.md)을 참조 하세요.  
  
 환경 핸들을 요청 하기 위해 응용 프로그램은 SQL_HANDLE_ENV *HandleType* 및 SQL_NULL_HANDLE *InputHandle* 를 사용 하 여 **SQLAllocHandle** 를 호출 합니다. 드라이버는 환경 정보에 대 한 메모리를 할당 하 고 * \*OutputHandlePtr* 인수에 연결 된 핸들의 값을 다시 전달 합니다. 응용 프로그램은 환경 핸들 인수가 필요한 모든 후속 호출에서 * \*OutputHandle* 값을 전달 합니다. 자세한 내용은 [환경 핸들 할당](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)을 참조 하세요.  
  
 드라이버 관리자의 환경 핸들에서, 드라이버의 환경 핸들이 이미 있는 경우 SQLAllocHandle SQL_HANDLE_ENV *HandleType* 를 사용 하는 **** 는 연결이 설정 될 때 해당 드라이버에서 호출 되지 않습니다. SQLAllocHandle는 SQL_HANDLE_DBC *HandleType* 를 사용 하 여 **** 합니다. 드라이버의 환경 핸들이 드라이버 관리자의 환경 핸들 아래에 없는 경우 SQLAllocHandle SQL_HANDLE_ENV HandleType를 사용 하는 두와 SQLAllocHandle SQL_HANDLE_DBC의 HandleType를 사용 하 여 첫 번째 연결 시 드라이버에서 호출 됩니다. 환경의 핸들이 드라이버에 연결 되어 있습니다.  
  
 드라이버 관리자는 SQL_HANDLE_ENV *HandleType* 로 **SQLAllocHandle** 함수를 처리 하는 경우 시스템 정보의 [ODBC] 섹션에서 **Trace** 키워드를 확인 합니다. 1로 설정 된 경우 드라이버 관리자는 현재 응용 프로그램에 대 한 추적을 사용 하도록 설정 합니다. 추적 플래그를 설정 하면 첫 번째 환경 핸들이 할당 될 때 추적이 시작 되 고 마지막 환경 핸들이 해제 될 때 종료 됩니다. 자세한 내용은 [데이터 원본 구성](../../../odbc/reference/install/configuring-data-sources.md)을 참조 하세요.  
  
 환경 핸들을 할당 한 후 응용 프로그램은 환경 핸들에서 **SQLSetEnvAttr** 을 호출 하 여 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 해야 합니다. 환경에서 연결 핸들을 할당 하기 위해 **SQLAllocHandle** 가 호출 되기 전에이 특성이 설정 되지 않은 경우 연결을 할당 하는 호출은 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다. 자세한 내용은 [응용 프로그램의 ODBC 버전 선언](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)을 참조 하세요.  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>연결 풀링을 위한 공유 환경 할당  
 단일 프로세스에서 여러 구성 요소 간에 환경을 공유할 수 있습니다. 한 번에 둘 이상의 구성 요소에서 공유 환경을 사용할 수 있습니다. 구성 요소가 공유 환경을 사용 하는 경우 풀링된 연결을 사용 하 여 해당 연결을 다시 만들지 않고 기존 연결을 할당 및 사용할 수 있습니다.  
  
 연결 풀링을 사용할 수 있는 공유 환경을 할당 하기 전에 응용 프로그램은 **SQLSetEnvAttr** 를 호출 하 여 SQL_ATTR_CONNECTION_POOLING 환경 특성을 SQL_CP_ONE_PER_DRIVER 또는 SQL_CP_ONE_PER_HENV으로 설정 해야 합니다. 이 경우 **SQLSetEnvAttr** 는 *EnvironmentHandle* 를 null로 설정 하 여 호출 됩니다. 그러면이 특성이 프로세스 수준 특성으로 설정 됩니다.  
  
 연결 풀링을 사용 하도록 설정 하면 응용 프로그램에서 *HandleType* 인수가 SQL_HANDLE_ENV로 설정 된 **SQLAllocHandle** 를 호출 합니다. 연결 풀링이 사용 하도록 설정 되었기 때문에이 호출에서 할당 한 환경은 암시적 공유 환경이 됩니다.  
  
 공유 환경을 할당 하는 경우 **SQLAllocHandle** SQL_HANDLE_DBC *HandleType* 가 호출 될 때까지 사용 되는 환경이 결정 되지 않습니다. 이 시점에서 드라이버 관리자는 응용 프로그램에서 요청 하는 환경 특성과 일치 하는 기존 환경을 찾으려고 시도 합니다. 이러한 환경이 없으면 공유 환경으로 만듭니다. 드라이버 관리자는 각 공유 환경의 참조 횟수를 유지 관리 합니다. 환경을 처음 만들 때 카운트를 1로 설정 합니다. 일치 하는 환경을 찾으면 해당 환경의 핸들이 응용 프로그램에 반환 되 고 참조 횟수가 증가 합니다. 이러한 방식으로 할당 된 환경 핸들은 입력 인수로 환경 핸들을 허용 하는 모든 ODBC 함수에서 사용할 수 있습니다.  
  
## <a name="allocating-a-connection-handle"></a>연결 핸들 할당  
 연결 핸들은 연결에 대 한 유효한 문과 설명자 핸들 및 트랜잭션이 현재 열려 있는지 여부와 같은 정보에 대 한 액세스를 제공 합니다. 연결 핸들에 대 한 일반적인 내용은 [연결 핸들](../../../odbc/reference/develop-app/connection-handles.md)을 참조 하십시오.  
  
 연결 핸들을 요청 하기 위해 응용 프로그램은 SQL_HANDLE_DBC *HandleType* 를 사용 하 여 **SQLAllocHandle** 를 호출 합니다. *InputHandle* 인수는 해당 핸들을 할당 한 **SQLAllocHandle** 에 대 한 호출에서 반환 된 환경 핸들로 설정 됩니다. 드라이버는 연결 정보에 대 한 메모리를 할당 하 고 * \*OutputHandlePtr*에 연결 된 핸들의 값을 다시 전달 합니다. 응용 프로그램은 연결 핸들이 필요한 모든 후속 호출에서 * \*OutputHandlePtr* 값을 전달 합니다. 자세한 내용은 [연결 핸들 할당](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)을 참조 하세요.  
  
 드라이버 관리자는 **SQLAllocHandle** 함수를 처리 하 고 응용 프로그램이 **SQLConnect**, **SQLBrowseConnect**또는 **SQLDriverConnect**를 호출할 때 드라이버의 **SQLAllocHandle** 함수를 호출 합니다. 자세한 내용은 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조 하세요.  
  
 환경에서 연결 핸들을 할당 하기 위해 **SQLAllocHandle** 가 호출 되기 전에 SQL_ATTR_ODBC_VERSION 환경 특성이 설정 되지 않은 경우 연결을 할당 하는 호출은 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다.  
  
 응용 프로그램에서 *InputHandle* 인수가 SQL_HANDLE_DBC로 설정 되 고 공유 환경 핸들로 설정 된 **SQLAllocHandle** 를 호출 하는 경우 드라이버 관리자는 응용 프로그램에서 설정한 환경 특성과 일치 하는 기존 공유 환경을 찾으려고 시도 합니다. 이러한 환경이 없으면 1의 참조 횟수 (드라이버 관리자에서 유지 관리)를 사용 하 여 하나를 만듭니다. 일치 하는 공유 환경이 발견 되 면 해당 핸들이 응용 프로그램에 반환 되 고 참조 횟수가 증가 합니다.  
  
 **SQLConnect** 또는 **SQLDriverConnect** 가 호출 될 때까지 사용 되는 실제 연결은 드라이버 관리자에 의해 결정 되지 않습니다. 드라이버 관리자는 **SQLConnect** 에 대 한 호출 (또는 **SQLDriverConnect**에 대 한 호출의 연결 키워드)의 연결 옵션을 사용 하 고 연결 할당 후에 설정 된 연결 특성을 사용 하 여 풀에서 사용할 연결을 결정 합니다. 자세한 내용은 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조 하세요.  
  
## <a name="allocating-a-statement-handle"></a>문 핸들 할당  
 문 핸들은 오류 메시지, 커서 이름 및 SQL 문 처리에 대 한 상태 정보와 같은 문 정보에 대 한 액세스를 제공 합니다. 문 핸들에 대 한 일반 정보는 [문 핸들](../../../odbc/reference/develop-app/statement-handles.md)을 참조 하세요.  
  
 문 핸들을 요청 하기 위해 응용 프로그램은 데이터 원본에 연결한 다음 SQL 문을 전송 하기 전에 **SQLAllocHandle** 를 호출 합니다. 이 호출에서 *HandleType* 는 SQL_HANDLE_STMT로 설정 해야 하며 *InputHandle* 는 해당 핸들을 할당 한 **SQLAllocHandle** 호출에서 반환 된 연결 핸들로 설정 해야 합니다. 드라이버는 문 정보에 대 한 메모리를 할당 하 고, 문 핸들을 지정 된 연결과 연결 하 고, 연결 된 핸들의 값을 다시 * \*OutputHandlePtr*로 전달 합니다. 응용 프로그램은 문 핸들이 필요한 모든 후속 호출에서 * \*OutputHandlePtr* 값을 전달 합니다. 자세한 내용은 [문 핸들 할당](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)을 참조 하세요.  
  
 문 핸들이 할당 되 면 드라이버는 자동으로 4 개의 설명자 집합을 할당 하 고 이러한 설명자에 대 한 핸들을 SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC, SQL_ATTR_IMP_ROW_DESC 및에 할당 SQL_ATTR_IMP_PARAM_DESC 문 특성. 이러한 설명자를 *암시적* 으로 할당 된 설명자 라고 합니다. 응용 프로그램 설명자를 명시적으로 할당 하려면 다음 섹션인 "설명자 핸들 할당" 섹션을 참조 하세요.  
  
## <a name="allocating-a-descriptor-handle"></a>설명자 핸들 할당  
 응용 프로그램에서 *HandleType* 가 SQL_HANDLE_DESC 인 **SQLAllocHandle** 를 호출 하는 경우 드라이버는 응용 프로그램 설명자를 할당 합니다. 이를 *명시적* 으로 할당 된 설명자 라고 합니다. 응용 프로그램은 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 특성으로 **SQLSetStmtAttr** 함수를 호출 하 여 지정 된 문 핸들에 대해 자동으로 할당 되는 대신 명시적으로 할당 된 응용 프로그램 설명자를 사용 하도록 드라이버에 지시 합니다. 구현 설명자는 명시적으로 할당 될 수 없으며 **SQLSetStmtAttr** 함수 호출에서 구현 설명자를 지정할 수도 없습니다.  
  
 명시적으로 할당 된 설명자는 문 핸들 대신 연결 핸들과 연결 됩니다 (자동으로 할당 된 설명자는). 응용 프로그램이 실제로 데이터베이스에 연결 된 경우에만 설명자가 할당 된 상태로 유지 됩니다. 명시적으로 할당 된 설명자는 연결 핸들과 연결 되기 때문에 응용 프로그램은 명시적으로 할당 된 설명자를 연결 내에서 둘 이상의 문과 연결할 수 있습니다. 반면에 암시적으로 할당 된 응용 프로그램 설명자는 둘 이상의 문 핸들에 연결할 수 없습니다. (할당 된 문 이외의 다른 문 핸들에는 연결할 수 없습니다.) 명시적으로 할당 된 설명자 핸들은 응용 프로그램에서 명시적으로 해제 하거나, HandleType SQL_HANDLE_DESC의 ** 를 사용 하 여 **sqlfreehandle** 을 호출 하거나, 연결이 닫히면 암시적으로 해제할 수 있습니다.  
  
 명시적으로 할당 된 설명자가 해제 되 면 암시적으로 할당 된 설명자가 문과 다시 연결 됩니다. (해당 문의 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 특성은 암시적으로 할당 된 설명자 핸들로 다시 설정 됩니다.) 이는 연결에서 명시적으로 할당 된 설명자와 연결 된 모든 문에 적용 됩니다.  
  
 설명자에 대 한 자세한 내용은 [설명자](../../../odbc/reference/develop-app/descriptors.md)를 참조 하십시오.  
  
## <a name="code-example"></a>코드 예  
 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md), [SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md), [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)및 [SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)를 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|환경, 연결, 문 또는 설명자 핸들 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|실행을 위한 문 준비|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|설명자 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|환경 특성 설정|[SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
