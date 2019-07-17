---
title: SQLAllocHandle 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLAllocHandle
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLAllocHandle
helpviewer_keywords:
- SQLAllocHandle function [ODBC]
ms.assetid: 6e7fe420-8cf4-4e72-8dad-212affaff317
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f4f82a24e594a25b0b1ec9bbeab2256624ae6e9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036255"
---
# <a name="sqlallochandle-function"></a>SQLAllocHandle 함수
**규칙**  
 도입 된 버전: ODBC 3.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLAllocHandle** 환경, 연결, 문 또는 설명자 핸들을 할당 합니다.  
  
> [!NOTE]  
>  이 함수는 ODBC 2.0 함수를 대체 하는 제네릭 함수에 대 한 핸들을 할당 **SQLAllocConnect**하십시오 **SQLAllocEnv**, 및 **SQLAllocStmt**합니다. 호출 응용 프로그램을 허용 하도록 **SQLAllocHandle** ODBC 2를 사용 하 여 작동 합니다. *x* 드라이버에 대 한 호출 **SQLAllocHandle** 드라이버 관리자에 매핑된 **SQLAllocConnect**를 **SQLAllocEnv**, 또는  **SQLAllocStmt**를 적절 하 게 합니다. 자세한 내용은 "설명입니다."을 참조 하세요. 자세한 내용은 관리자에 대 한 어떤를 드라이버에 대 한 경우는 ODBC 3이이 함수를를 매핑합니다. *x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 합니다. *x* 드라이버를 참조 하세요 [이전 버전과 호환성의 응용 프로그램에 대 한 대체 함수 매핑](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] 할당할 핸들의 형식을 **SQLAllocHandle**합니다. 다음 값 중 하나 여야 합니다.  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 드라이버 관리자 및 드라이버에 의해서만 SQL_HANDLE_DBC_INFO_TOKEN 핸들을 사용 합니다. 응용 프로그램에는이 핸들 형식은 사용 하지 마십시오. SQL_HANDLE_DBC_INFO_TOKEN에 대 한 자세한 내용은 참조 하세요. [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)합니다.  
  
 *InputHandle*  
 [입력] 해당 컨텍스트에서 새 핸들이 할당할 입력된 핸들입니다. 하는 경우 *HandleType* SQL_HANDLE_ENV는 SQL_NULL_HANDLE입니다. 하는 경우 *HandleType* SQL_HANDLE_DBC은 환경 핸들을 이어야 합니다 하 고 호출 하 여 또는 SQL_HANDLE_DESC 인 경우 연결 핸들 이어야 합니다.  
  
 *OutputHandlePtr*  
 [출력] 새로 할당 된 데이터 구조에 핸들을 반환 하는 버퍼에 대 한 포인터입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE을 또는 SQL_ERROR를 선택 합니다.  
  
 경우에 환경 핸들이 아닌 핸들을 할당 하는 경우 **SQLAllocHandle** SQL_ERROR를 반환 합니다. 설정 *OutputHandlePtr* SQL_NULL_HDBC, SQL_NULL_HSTMT, 또는 SQL_NULL_HDESC을 따라는 값 *HandleType*출력 인수가 null 포인터가 아닌 경우. 응용 프로그램의 핸들과 연결 된 진단 데이터 구조에서 추가 정보를 얻으려면 다음 수를 *InputHandle* 인수입니다.  
  
## <a name="environment-handle-allocation-errors"></a>환경 핸들 할당 오류  
 환경 할당 드라이버 관리자 내에서 그리고 각 드라이버 내에서 발생합니다. 반환 된 오류 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_ENV의 오류가 발생 한 수준에 따라 합니다.  
  
 드라이버 관리자에 대 한 메모리를 할당할 수 없습니다 하는 경우  *\*OutputHandlePtr* 면 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_ENV의 호출 또는 응용 프로그램에 대해 null 포인터를 제공 *OutputHandlePtr*하십시오 **SQLAllocHandle** SQL_ERROR를 반환 합니다. 드라이버 관리자를 설정 하는 **OutputHandlePtr* SQL_NULL_HENV를 (하지 않는 한 SQL_ERROR를 반환 하는 null 포인터를 제공 하는 응용 프로그램). 추가적인 진단 정보를 연결 하는 핸들이 있습니다.  
  
 드라이버 관리자 응용 프로그램이 호출 될 때까지 드라이버 수준 환경 핸들 할당 함수를 호출 하지 않습니다 **SQLConnect**하십시오 **SQLBrowseConnect**, 또는 **SQLDriverConnect**. 드라이버 수준에서 오류가 발생 하는 경우 **SQLAllocHandle** 함수를 다음 드라이버 관리자 수준 **SQLConnect**하십시오 **SQLBrowseConnect**, 또는  **SQLDriverConnect** SQL_ERROR를 반환 합니다. 진단 데이터 구조에는 SQLSTATE IM004 포함 (운전 **SQLAllocHandle** 실패). 연결 핸들에서 오류가 반환 됩니다.  
  
 드라이버 관리자와 드라이버 간의 함수 호출의 흐름에 대 한 자세한 내용은 참조 하세요. [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLAllocHandle** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 연관된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 적절 한 *HandleType* 하 고 *처리할* 의 값으로 설정 *InputHandle*합니다. SQL_SUCCESS_WITH_INFO (하지만 하지 SQL_ERROR)에 대해 반환 될 수는 *OutputHandle* 인수입니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLAllocHandle** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|오류|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08003|연결이 열려 있지 않습니다.|(DM)는 *HandleType* 인수 호출 되었거나 SQL_HANDLE_DESC, 하지만 지정 된 연결을 *InputHandle* 인수를 열 수 없습니다. 연결 프로세스가 성공적으로 완료 해야 합니다 (및 연결이 열려 있어야 합니다.) 문 또는 설명자를 할당 하도록 드라이버에 대 한 처리 합니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 **MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|(DM) The Driver Manager 지정된 된 핸들에 대 한 메모리를 할당할 수 없습니다.<br /><br /> 드라이버가 지정된 된 핸들에 대 한 메모리를 할당할 수 없습니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|(DM)는 *OutputHandlePtr* 인수가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)는 *HandleType* 인수가 SQL_HANDLE_DBC, 및 **SQLSetEnvAttr** SQL_ODBC_VERSION 환경 특성을 설정 하는 호출 되지 않았습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수에 대해 호출 된 합니다 **InputHandle** 때 계속 실행 하 고는 **SQLAllocHandle** 함수를 사용 하 여 호출한 **HandleType** 설정 호출 하거나 SQL_HANDLE_DESC 합니다.|  
|HY013|메모리 관리 오류|합니다 *HandleType* 인수가 SQL_HANDLE_DBC, 호출 하 여, 또는 SQL_HANDLE_DESC; 및 기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 했으므로 함수 호출을 처리할 수 없습니다 조건입니다.|  
|HY014|초과 하는 핸들의 수를 제한|핸들 형식의 할당 될 수 있는 핸들의 수에 대 한 드라이버에서 정의 된 제한에 나타난 합니다 *HandleType* 인수에 도달 했습니다.|  
|HY092|잘못 된 특성/옵션 식별자입니다.|(DM)는 *HandleType* 인수가 없습니다. SQL_HANDLE_ENV, SQL_HANDLE_DBC, 호출 하 여, 또는 SQL_HANDLE_DESC 합니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|합니다 *HandleType* 인수가 SQL_HANDLE_DESC 했는데 드라이버는 ODBC 2. *x* 드라이버입니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)는 *HandleType* 인수를 호출 하 여 되었으며 유효한 ODBC 드라이버가 없습니다.<br /><br /> (DM)는 *HandleType* 인수가 SQL_HANDLE_DESC, 및 드라이버 설명자 핸들 할당을 지원 하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLAllocHandle** 다음 섹션에 설명 된 대로 환경, 연결, 문 및 설명자에 대 한 핸들을 할당 하는 데 사용 됩니다. 핸들에 대 한 일반적인 정보를 참조 하세요 [핸들](../../../odbc/reference/develop-app/handles.md)합니다.  
  
 여러 할당 드라이버에서 지원 되는 경우 한 번에 응용 프로그램에서 둘 이상의 환경, 연결 또는 문 핸들을 할당할 수 있습니다. ODBC 환경, 연결, 문 또는 한 번에 할당 될 수 있는 설명자 핸들의 수에 제한이 정의 됩니다. 드라이버는 특정 유형의에서는 한 번에 할당 될 수 있는 핸들의 수에 제한을 적용 될 수 있습니다. 자세한 내용은 드라이버 설명서를 참조 하십시오.  
  
 응용 프로그램을 호출 하는 경우 **SQLAllocHandle** 사용 하 여  *\*OutputHandlePtr* 드라이버 덮어씁니다 환경, 연결, 문 또는 이미 존재 하는 설명자 핸들을로 설정 합니다 연관 된 정보는 *처리*응용 프로그램이 연결 풀링 (참조 "할당 된 환경 특성에 대 한 연결 풀링"이이 섹션의 뒷부분에 나오는)를 사용 하는 경우가 아니면 합니다. 드라이버 관리자를 확인 하지 않습니다 여부는 *처리* 에 입력 한  *\*OutputHandlePtr* 이미 사용 중인도 않습니다 핸들의 이전 내용을 덮어쓰기 전에 확인 .  
  
> [!NOTE]  
>  잘못 된 ODBC 응용 프로그램 프로그래밍 호출 하는 것 **SQLAllocHandle** 에 대해 정의 된 동일한 응용 프로그램 변수의 두고 두 번  *\*OutputHandlePtr* 호출 하지 않고  **SQLFreeHandle** 를 재할당 하기 전에 핸들을 해제 합니다. ODBC를 덮어쓰지 일관 되지 않은 동작이 나 ODBC 드라이버 부분 오류를 이러한 방식으로 처리 될 수 있습니다.  
  
 여러 스레드를 지 원하는 운영 체제에서 응용 프로그램 다른 스레드에서 동일한 환경, 연결, 문 또는 설명자 핸들을 사용할 수 있습니다. 드라이버는이 정보에 대 한 안전 하 고 다중 스레드 액세스를 지원 하므로 해야 합니다. 이 위한 한 가지 방법은 예를 들어 경우 임계 또는 세마포를 사용 하 여 스레딩에 대 한 자세한 내용은 참조 하세요. [다중 스레딩](../../../odbc/reference/develop-app/multithreading.md)합니다.  
  
 **SQLAllocHandle** SQL_ATTR_ODBC_VERSION 환경 특성을 설정 하지 않습니다는 응용 프로그램, 또는 SQLSTATE HY010 환경 특성을 설정 해야 합니다; 환경 핸들을 할당 하 여 호출 될 때 (함수 시퀀스 오류) 됩니다. 경우에 반환 **SQLAllocHandle** 연결 핸들을 할당 하기 위해 호출 됩니다.  
  
 표준 호환 응용 프로그램에 대 한 **SQLAllocHandle** 매핑됩니다 **SQLAllocHandleStd** 컴파일 타임에 있습니다. 이 두 함수 간의 차이점은 **SQLAllocHandleStd** SQL_ATTR_ODBC_VERSION 환경 특성을 설정 합니다 SQL_OV_ODBC3으로 호출 될 때 합니다 *HandleType* 인수 SQL로 설정 _HANDLE_ENV 합니다. 표준 호환 응용 프로그램은 항상 ODBC 3 때문에 수행 됩니다. *x* 응용 프로그램입니다. 또한 표준 등록할 응용 프로그램 버전이 필요 하지 않습니다. 이이 두 함수; 간의 유일한 차이점 그렇지 않으면 동일 합니다. **SQLAllocHandleStd** 매핑됩니다 **SQLAllocHandle** 드라이버 관리자 내에서. 따라서 타사 드라이버 않아도 구현 **SQLAllocHandleStd**합니다.  
  
 ODBC 3.8 응용 프로그램을 사용 해야 합니다.  
  
-   **SQLAllocHandle 및 없습니다 SQLAllocHandleStd** 환경 핸들을 할당 합니다.  
  
-   **SQLSetEnvAttr** SQL_OV_ODBC3_80를 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 합니다.  
  
## <a name="allocating-an-environment-handle"></a>환경 핸들 할당  
 환경 핸들을 잘못 연결 핸들에서 활성 연결 핸들 등의 전역 정보에 대 한 액세스를 제공합니다. 환경 핸들에 대 한 일반적인 정보를 참조 하세요 [환경 핸들](../../../odbc/reference/develop-app/environment-handles.md)합니다.  
  
 환경 핸들을 요청 하려면 응용 프로그램 호출 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_ENV의 및 *InputHandle* SQL_NULL_HANDLE입니다. 드라이버는 환경 정보 및 연결된 핸들의 값에 다시 전달에 대 한 메모리를 할당 합니다  *\*OutputHandlePtr* 인수입니다. 응용 프로그램 전달 된  *\*OutputHandle* 환경 핸들 인수를 필요로 하는 모든 후속 호출에서 값입니다. 자세한 내용은 [환경 핸들 할당](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)합니다.  
  
 드라이버 관리자의 환경 핸들이 이미 존재 하면 운전 환경 핸들을 다음 아래 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_ENV의 호출 되지 않습니다 해당 드라이버의 경우는 만 연결이 설정 되 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DBC입니다. SQL_HANDLE_ENV HandleType를 사용 하 여 SQLAllocHandle와 SQLAllocHandle SQL_HANDLE_DBC HandleType를 사용 하 여 드라이버에서 라고 드라이버 관리자 환경 핸들에서 드라이버의 환경 핸들이 없으면 때 첫 번째 연결 환경 핸들은 드라이버에 연결 됩니다.  
  
 드라이버 관리자를 처리 하는 경우는 **SQLAllocHandle** 함수를 *HandleType* SQL_HANDLE_ENV의 확인을 **추적** 시스템의 [ODBC] 섹션에는 키워드 정보입니다. 1로 설정 되 고, 경우 드라이버 관리자는 현재 응용 프로그램에 대 한 추적을 활성화 합니다. 추적 플래그를 설정 하는 경우 첫 번째 환경 핸들 할당 되 고 마지막 환경 핸들이 해제 될 때 종료 하는 경우 추적 시작 합니다. 자세한 내용은 [데이터 원본 구성](../../../odbc/reference/install/configuring-data-sources.md)합니다.  
  
 환경 핸들을 할당 한 후 응용 프로그램에서 호출 해야 합니다 **SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION 환경 특성을 설정 하 여 환경 핸들에 있습니다. 하기 전에이 특성이 설정 되지 않은 경우 **SQLAllocHandle** 연결 핸들을 할당 하기 위해 호출 환경에서 연결 할당에 대 한 호출에는 SQLSTATE HY010 반환 됩니다 (함수 시퀀스 오류). 자세한 내용은 [응용 프로그램의 ODBC 버전 선언](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)합니다.  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>연결 풀링을 위해 환경 공유할 할당  
 단일 프로세스에서 여러 구성 요소 간에 환경 공유할 수 있습니다. 공유 환경 동시에 둘 이상의 구성 요소에서 사용할 수 있습니다. 구성 요소에서는 공유 환경 때 할당 하 고 해당 연결을 다시 만들지 않고 기존 연결을 사용 하 게 하는 풀링된 연결을 사용할 수 있습니다.  
  
 응용 프로그램에서 호출 해야 하는 공유 환경 할당 연결 풀링을 사용할 수 있습니다, **SQLSetEnvAttr** SQL_CP_ONE_PER_DRIVER 또는 SQL_CP_ONE_PER_ SQL_ATTR_CONNECTION_POOLING 환경 특성을 설정 하려면 HENV 합니다. **SQLSetEnvAttr** 사용 하 여이 경우 라고 *EnvironmentHandle* 특성 프로세스 수준 특성을 사용 하면 null로 설정 합니다.  
  
 연결 풀링에서 사용할 수 있는 응용 프로그램 호출 **SQLAllocHandle** 사용 하 여 합니다 *HandleType* 인수를 SQL_HANDLE_ENV로 설정 합니다. 이 호출에 의해 할당 되는 환경 연결 풀링을 설정 되어 있기 때문에 암시적 공유 environment이 됩니다.  
  
 사용 되는 환경에서는 공유 환경 할당 될 때까지 결정 되지 않습니다 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DBC의 호출 됩니다. 이 시점에서 드라이버 관리자는 응용 프로그램이 요청한 환경 특성과 일치 하는 기존 환경을 찾으려고 합니다. 이러한 환경이 없고 있으면 공유 환경으로는 하나이 만들어집니다. 드라이버 관리자는 각 공유 환경에 대 한 참조 횟수를 유지 관리 환경을 처음 만들어질 때 수를 1로 설정 됩니다. 일치 하는 환경이 있으면 해당 환경의 핸들이 응용 프로그램에 반환 된 및 참조 개수가 증가 합니다. 이 방식으로 할당 된 환경 핸들을 입력 인수로 환경 핸들을 허용 하는 ODBC 함수에서 사용할 수 있습니다.  
  
## <a name="allocating-a-connection-handle"></a>연결 핸들 할당  
 연결 핸들을 유효한 문 등의 정보에 대 한 액세스를 제공 하 고 연결 및 트랜잭션이 현재 인지 설명자 핸들 엽니다. 연결 핸들에 대 한 일반적인 정보를 참조 하세요 [연결 핸들](../../../odbc/reference/develop-app/connection-handles.md)합니다.  
  
 연결 핸들을 요청 하려면 응용 프로그램 호출 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DBC입니다. 합니다 *InputHandle* 인수에 대 한 호출에서 반환 된 환경 핸들을으로 설정 됩니다 **SQLAllocHandle** 해당 핸들을 할당 하는 합니다. 드라이버는 연결 정보 및 연결된 핸들의 값에 다시 전달에 대 한 메모리를 할당  *\*OutputHandlePtr*합니다. 응용 프로그램 전달 된  *\*OutputHandlePtr* 연결 핸들을 필요로 하는 모든 후속 호출에서 값입니다. 자세한 내용은 [연결 핸들 할당](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)합니다.  
  
 드라이버 관리자를 처리 합니다 **SQLAllocHandle** 함수를 호출 하는 드라이버의 **SQLAllocHandle** 응용 프로그램을 호출 하는 경우에 작동 **SQLConnect**를 **SQLBrowseConnect**, 또는 **SQLDriverConnect**합니다. (자세한 내용은 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md).)  
  
 전에 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 하지 않으면 **SQLAllocHandle** 연결 핸들을 할당 하기 위해 호출 환경에서 연결 할당에 대 한 호출에는 SQLSTATE HY010 반환 됩니다 (시퀀스 함수 오류)입니다.  
  
 응용 프로그램을 호출할 때 **SQLAllocHandle** 사용 하 여 합니다 *InputHandle* 인수를 SQL_HANDLE_DBC로 설정 하 고 공유 환경 핸들을 설정, 드라이버 관리자가 기존 공유를 찾으려고 시도 응용 프로그램에 의해 설정 된 환경 특성을 일치 하는 환경입니다. 이러한 환경이 있는 경우 하나 만들어집니다 1 참조 카운트 (드라이버 관리자에 의해 유지 관리 됨). 일치 하는 공유 environment가 발견 되었습니다, 그리고 응용 프로그램에 해당 핸들이 반환 되 고 해당 참조 개수가 증가 합니다.  
  
 사용 되는 실제 연결 될 때까지 드라이버 관리자에 의해 결정 되지 않습니다 **SQLConnect** 하거나 **SQLDriverConnect** 라고 합니다. 드라이버 관리자 연결 옵션을 사용 하 여 호출에서 **SQLConnect** (또는 연결 키워드에 대 한 호출에 **SQLDriverConnect**) 연결 특성에 연결을 할당 한 후 설정 풀에서 연결을 사용할지를 결정 합니다. 자세한 내용은 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)합니다.  
  
## <a name="allocating-a-statement-handle"></a>문 핸들 할당  
 문 핸들 SQL 문 처리에 대 한 오류 메시지, 커서 이름 및 상태 정보 등 문 정보에 대 한 액세스를 제공합니다. 문 핸들에 대 한 일반적인 정보를 참조 하세요 [문 핸들](../../../odbc/reference/develop-app/statement-handles.md)합니다.  
  
 문 핸들을 요청 하려면 응용 프로그램 데이터 원본에 연결 하 고 호출 **SQLAllocHandle** SQL 문을 제출 하기 전에 합니다. 이 호출 *HandleType* 호출으로 설정 해야 하 고 *InputHandle* 에 대 한 호출에서 반환 된 연결 핸들을 설정 해야 **SQLAllocHandle** 해당 핸들을 할당합니다. 드라이버는 문 정보에 대 한 메모리를 할당, 지정 된 연결 및 연결된 핸들의 값에 다시 전달 사용 하 여 문 핸들에 연결  *\*OutputHandlePtr*합니다. 응용 프로그램 전달 된  *\*OutputHandlePtr* 문 핸들을 필요로 하는 모든 후속 호출에서 값입니다. 자세한 내용은 [문 핸들 할당](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)합니다.  
  
 문 핸들 할당 될 때 드라이버 자동으로 4 설명자 집합을 할당 하 고 SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC, SQL_ATTR_IMP_ROW_DESC, 및 SQL_ATTR_IMP_PARAM_DESC 이러한 설명자에 대 한 핸들을 할당 합니다. 문 특성 이러한 이라고 *암시적으로* 설명자를 할당 합니다. 응용 프로그램 설명자를를 명시적으로 할당 하려면 다음 섹션에서는 "설명자 핸들을 할당 합니다."를 참조 하세요.  
  
## <a name="allocating-a-descriptor-handle"></a>설명자 핸들 할당  
 응용 프로그램을 호출할 때 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DESC의 드라이버는 응용 프로그램 설명자를 할당 합니다. 이러한 이라고 *명시적으로* 설명자를 할당 합니다. 응용 프로그램 호출 하 여 지정 된 문 핸들에 대 한 항목을 자동으로 할당된 하는 대신 명시적으로 할당 된 응용 프로그램 설명자를 사용 하기 위해 드라이버를 지시 합니다 **SQLSetStmtAttr** 는 SQL_ATTR_APP_ROW_DESC 사용 하 여 함수 또는 SQL_ATTR_APP_PARAM_DESC 특성을 추가 합니다. 구현 설명자를 명시적으로 할당할 수 없습니다 나 구현 설명자를 지정할 수는 **SQLSetStmtAttr** 함수 호출 합니다.  
  
 (으로 자동으로 할당 된 설명자) 명시적으로 할당 된 설명자를 문 핸들 대신 연결 핸들에 연결 됩니다. 설명자는 응용 프로그램 데이터베이스에 실제로 연결 되어 있는 경우에 할당 된 상태로 유지 합니다. 명시적으로 할당 된 설명자 연결 핸들을 사용 하 여 연결 이기 때문에 응용 프로그램 연결 내에서 둘 이상의 문을 사용 하 여 명시적으로 할당 된 설명자를 연결할 수 있습니다. 암시적으로 할당 된 응용 프로그램 설명자를 다른 한편으로 연결할 수 없습니다 둘 이상의 문 핸들을 사용 하 여. (없습니다 것에 대 한 할당 된 것과 다른 모든 문 핸들을 사용 하 여 연결 합니다.) 명시적으로 할당 된 설명자 핸들을 명시적으로 해제할 수 응용 프로그램에서 또는 전화 800-659-3579 **SQLFreeHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DESC, 또는 암시적으로 연결 되 면 닫힙니다.  
  
 명시적으로 할당 된 설명자 해제 될 때 암시적으로 할당 된 설명자가 문과 사용 하 여 연결 다시 합니다. (해당 문에 대해 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 특성을 암시적으로 할당 된 설명자 핸들을 다시 설정 됩니다.) 연결에 명시적으로 할당 된 설명자와 연결 된 모든 문에 대해 마찬가지입니다.  
  
 설명자에 대 한 자세한 내용은 참조 하세요. [설명자](../../../odbc/reference/develop-app/descriptors.md)합니다.  
  
## <a name="code-example"></a>코드 예  
 참조 [샘플 ODBC 프로그램](../../../odbc/reference/sample-odbc-program.md)를 [SQLBrowseConnect 함수](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)합니다 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md), 및 [SQLSetCursorName 함수](../../../odbc/reference/syntax/sqlsetcursorname-function.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|SQL 문을 실행합니다.|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|환경, 연결, 문 또는 설명자 핸들을 해제합니다.|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|실행할 문을 준비합니다.|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|연결 특성을 설정합니다.|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|설명자 필드 설정|[SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|환경 특성 설정|[SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
