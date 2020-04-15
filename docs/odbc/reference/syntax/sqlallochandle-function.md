---
title: SQLAllocHandle 함수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 178e3fad1ec062dd7f812125da66b7e21a7a4f4b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290214"
---
# <a name="sqlallochandle-function"></a>SQLAllocHandle 함수
**규칙**  
 버전 출시: ODBC 3.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLAllocHandle** 환경, 연결, 문 또는 설명자 핸들을 할당합니다.  
  
> [!NOTE]  
>  이 함수는 ODBC 2.0 함수 **SQLAllocConnect,** **SQLAllocEnv**및 **SQLAllocStmt를**대체하는 핸들을 할당하기 위한 일반 함수입니다. **SQLAllocHandle을** 호출하는 응용 프로그램이 ODBC 2로 작동하도록 허용합니다. *x* 드라이버, **SQLAllocHandle에** 대 한 호출은 **SQLAllocConnect,** **SQLAllocEnv**또는 **SQLAllocStmt에**드라이버 관리자에 적절 하 게 매핑 됩니다. 자세한 내용은 '댓글'을 참조하세요. 드라이버 관리자가 이 함수를 ODBC 3에 매핑하는 기능에 대한 자세한 내용을 참조하십시오. *x* 응용 프로그램이 ODBC 2로 작동합니다. *x* 드라이버, [응용 프로그램의 이전 버전과의 호환성에 대한 매핑 교체 함수를](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLAllocHandle(  
      SQLSMALLINT   HandleType,  
      SQLHANDLE     InputHandle,  
      SQLHANDLE *   OutputHandlePtr);  
```  
  
## <a name="arguments"></a>인수  
 *HandleType*  
 [입력] **SQLAllocHandle에서**할당할 핸들 유형입니다. 다음 값 중 하나여야 합니다.  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 핸들은 드라이버 관리자와 드라이버에서만 사용됩니다. 응용 프로그램에서는 이 핸들 형식을 사용해서는 안 됩니다. SQL_HANDLE_DBC_INFO_TOKEN 대한 자세한 내용은 [ODBC 드라이버에서 연결-풀 인식 개발을](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)참조하십시오.  
  
 *입력 핸들*  
 [입력] 컨텍스트에서 새 핸들을 할당할 입력 핸들입니다. *핸들 유형이* SQL_HANDLE_ENV 경우 SQL_NULL_HANDLE. *핸들유형이* SQL_HANDLE_DBC 경우 환경 핸들이어야 하며 SQL_HANDLE_STMT SQL_HANDLE_DESC 경우 연결 핸들이어야 합니다.  
  
 *출력핸들프트르*  
 [출력] 새로 할당된 데이터 구조에 핸들을 반환할 버퍼에 대한 포인터입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_INVALID_HANDLE 또는 SQL_ERROR.  
  
 환경 핸들 이외의 핸들을 할당할 때 **SQLAllocHandle** SQL_ERROR 반환 하는 경우 output 인수null 포인터 가 아닌 경우 *HandleType의*값에 따라 SQL_NULL_HDBC, SQL_NULL_HSTMT 또는 SQL_NULL_HDESC *OutputHandlePtr을* 설정 합니다. 그런 다음 응용 프로그램은 *InputHandle* 인수의 핸들과 연결된 진단 데이터 구조에서 추가 정보를 얻을 수 있습니다.  
  
## <a name="environment-handle-allocation-errors"></a>환경 처리 할당 오류  
 환경 할당은 드라이버 관리자 와 각 드라이버 내에서 모두 발생합니다. *SQL_HANDLE_ENV 핸들 타입을* 사용 하 여 **SQLAllocHandle에** 의해 반환 된 오류는 오류가 발생 하는 수준에 따라 달라 집니다.  
  
 *핸들 타입의 핸들 타입을* 사용하여 **SQLAllocHandle** SQL_HANDLE_ENV이 호출될 때 드라이버 관리자가 * \*OutputHandlePtr에* 대한 메모리를 할당할 수 없거나 응용 프로그램이 *OutputHandlePtr에*대한 null 포인터를 제공하는 경우 **SQLAllocHandle은** SQL_ERROR 반환합니다. 드라이버 관리자는 **OutputHandlePtr을* SQL_NULL_HENV 설정합니다(응용 프로그램이 SQL_ERROR 반환하는 null 포인터를 제공하지 않는 한). 추가 진단 정보를 연결할 핸들이 없습니다.  
  
 드라이버 관리자는 응용 프로그램이 **SQLConnect,** **SQLBrowseConnect**또는 **SQLDriverConnect**를 호출할 때까지 드라이버 수준 환경 핸들 할당 함수를 호출하지 않습니다. 드라이버 수준 **SQLAllocHandle** 함수에서 오류가 발생하면 드라이버 관리자 수준 **SQLConnect,** **SQLBrowseConnect**또는 **SQLDriverConnect** 함수가 SQL_ERROR 반환합니다. 진단 데이터 구조에는 SQLSTATE IM004(드라이버의 **SQLAllocHandle** 실패)가 포함되어 있습니다. 연결 핸들에서 오류가 반환됩니다.  
  
 드라이버 관리자와 드라이버 간의 함수 호출 흐름에 대한 자세한 내용은 [SQLConnect 함수를](../../../odbc/reference/syntax/sqlconnect-function.md)참조하십시오.  
  
## <a name="diagnostics"></a>진단  
 **SQLAllocHandle** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값을 적절 한 *핸들 유형* 및 *핸들* *입력 핸들의*값으로 설정 된 **SQLGetDiagRec를** 호출 하 여 가져올 수 있습니다. SQL_SUCCESS_WITH_INFO(SQL_ERROR 아님)는 *OutputHandle* 인수에 대해 반환될 수 있습니다. 다음 표에서는 **SQLAllocHandle에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|08003|연결이 열려 있지 않음|(DM) *HandleType* 인수가 SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC *입력핸들* 인수에 의해 지정된 연결이 열려 있지 않았습니다. 드라이버가 명령문 또는 설명자 핸들을 할당하려면 연결 프로세스가 성공적으로 완료되어야 하며 연결이 열려 있어야 합니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. **MessageText* 버퍼에서 **SQLGetDiagRec에서** 반환된 오류 메시지는 오류와 그 원인을 설명합니다.|  
|HY01|메모리 할당 오류|(DM) 드라이버 관리자가 지정된 핸들에 대한 메모리를 할당할 수 없습니다.<br /><br /> 드라이버가 지정된 핸들에 메모리를 할당할 수 없습니다.|  
|HY09|null 포인터의 잘못된 사용|(DM) *OutputHandlePtr* 인수는 null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) *핸들타이* 인수가 SQL_HANDLE_DBC **SQLSetEnvAttr이** SQL_ODBC_VERSION 환경 특성을 설정하기 위해 호출되지 않았습니다.<br /><br /> (DM) **InputHandle에** 대해 비동기적으로 실행되는 함수가 호출되었으며, 핸들 유형이 SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC 설정된 **HandleType으로** **SQLAllocHandle** 함수가 호출될 때 여전히 실행 중이었습니다.|  
|HY013|메모리 관리 오류|*핸들타이* 인수가 SQL_HANDLE_DBC, SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC. 메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY014|초과된 핸들 수 제한|*HandleType* 인수에 의해 표시된 핸들 유형에 대해 할당할 수 있는 핸들 수에 대한 드라이버 정의 제한에 도달했습니다.|  
|HY092|잘못된 특성/옵션 식별자|(DM) *핸들타이* 인수는 SQL_HANDLE_ENV, SQL_HANDLE_DBC, SQL_HANDLE_STMT 또는 SQL_HANDLE_DESC.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|*핸들 타입* 인수는 SQL_HANDLE_DESC 드라이버가 ODBC 2였습니다. *x* 드라이버.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *핸들타이* 인수가 SQL_HANDLE_STMT 드라이버가 유효한 ODBC 드라이버가 아닙니다.<br /><br /> (DM) *핸들 타입* 인수가 SQL_HANDLE_DESC 드라이버가 설명자 핸들 할당을 지원하지 않습니다.|  
  
## <a name="comments"></a>주석  
 **SQLAllocHandle은** 다음 섹션에 설명된 대로 환경, 연결, 명령문 및 설명자에 대한 핸들을 할당하는 데 사용됩니다. 핸들에 대한 일반적인 정보는 [핸들 을](../../../odbc/reference/develop-app/handles.md)참조하십시오.  
  
 드라이버에서 여러 할당을 지원하는 경우 응용 프로그램에서 한 번에 둘 이상의 환경, 연결 또는 명령문 핸들을 할당할 수 있습니다. ODBC에서 한 번에 할당할 수 있는 환경, 연결, 명령문 또는 설명자 핸들 의 수에는 제한이 정의되지 않습니다. 드라이버는 한 번에 할당할 수 있는 특정 유형의 핸들 수에 제한을 부과할 수 있습니다. 자세한 내용은 드라이버 설명서를 참조하십시오.  
  
 응용 프로그램이 * \*이미* 존재하는 환경, 연결, 문 또는 설명자 핸들로 SET을 사용하는 **SQLAllocHandle을** 호출하는 경우, 드라이버는 응용 프로그램이 연결 풀링을 사용하고 있는 경우가 아니면 *핸들과*관련된 정보를 덮어씁니다(이 섹션의 후반부 "연결 풀링에 대한 환경 특성 할당" 참조). 드라이버 관리자는 * \*OutputHandlePtr에* 입력된 *핸들이* 이미 사용 중인지 확인하지 않으며 덮어쓰기 전에 핸들의 이전 내용을 확인하지도 않습니다.  
  
> [!NOTE]  
>  SQLFreeHandle을 호출하지 않고 * \*OutputHandlePtr에* 대해 정의된 동일한 응용 프로그램 변수로 **SQLFreeHandle** **SQLAllocHandle을** 두 번 호출하는 것은 잘못된 ODBC 응용 프로그램 프로그래밍입니다. 이러한 방식으로 ODBC 핸들을 덮어쓰면 ODBC 드라이버부분에서 일관되지 않은 동작이나 오류가 발생할 수 있습니다.  
  
 여러 스레드를 지원하는 운영 체제에서 응용 프로그램은 서로 다른 스레드에서 동일한 환경, 연결, 명령문 또는 설명자 핸들을 사용할 수 있습니다. 따라서 드라이버는 이 정보에 대한 안전한 다중 스레드 액세스를 지원해야 합니다. 예를 들어 이를 달성하는 한 가지 방법은 임계 섹션 또는 세마포를 사용하는 것입니다. 스레딩에 대한 자세한 내용은 [다중 스레딩](../../../odbc/reference/develop-app/multithreading.md)을 참조하십시오.  
  
 **SQLAllocHandle** 환경 핸들을 할당 하기 위해 호출 될 때 SQL_ATTR_ODBC_VERSION 환경 특성을 설정 하지 않습니다. 환경 특성은 응용 프로그램에서 설정해야 하거나 SQLSTATE HY010(함수 시퀀스 오류)은 **SQLAllocHandle이** 호출되어 연결 핸들을 할당할 때 반환됩니다.  
  
 표준을 준수하는 응용 프로그램의 경우 **SQLAllocHandle은** 컴파일 타임에 **SQLAllocHandleStd에** 매핑됩니다. 이 두 함수의 차이점은 **SQLAllocHandleStd가** SQL_HANDLE_ENV 설정된 *HandleType* 인수를 사용하여 호출될 때 SQL_OV_ODBC3 SQL_ATTR_ODBC_VERSION 환경 특성을 설정한다는 점입니다. 이는 표준을 준수하는 응용 프로그램이 항상 ODBC 3이기 때문에 수행됩니다. *x* 응용 프로그램. 또한 표준은 응용 프로그램 버전을 등록할 필요가 없습니다. 이 두 함수 간의 유일한 차이점은 다음과 같은 것입니다. 그렇지 않으면 동일합니다. **SQLAllocHandleStd는** 드라이버 관리자 내부의 **SQLAllocHandle에** 매핑됩니다. 따라서 타사 드라이버는 **SQLAllocHandleStd를**구현할 필요가 없습니다.  
  
 ODBC 3.8 응용 프로그램은 다음을 사용해야 합니다.  
  
-   **SQLAllocHandle 이 아닌 SQLAllocHandleStd** 환경 핸들을 할당합니다.  
  
-   **SQLSetEnvAttrSQL_ATTR_ODBC_VERSION** 환경 특성을 SQL_OV_ODBC3_80 설정합니다.  
  
## <a name="allocating-an-environment-handle"></a>환경 핸들 할당  
 환경 핸들은 유효한 연결 핸들 및 활성 연결 핸들과 같은 전역 정보에 대한 액세스를 제공합니다. 환경 핸들에 대한 일반 정보는 [환경 핸들 을](../../../odbc/reference/develop-app/environment-handles.md)참조하십시오.  
  
 환경 핸들을 요청하려면 응용 프로그램은 *SQL_HANDLE_ENV 핸들 유형과* SQL_NULL_HANDLE *입력 핸들을* 사용하여 **SQLAllocHandle을** 호출합니다. 드라이버는 환경 정보에 대한 메모리를 할당하고 * \*OutputHandlePtr* 인수에서 연결된 핸들의 값을 다시 전달합니다. 응용 프로그램은 환경 핸들 인수를 필요로 하는 모든 후속 호출에서 * \*OutputHandle* 값을 전달합니다. 자세한 내용은 [환경 핸들 할당을](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)참조하십시오.  
  
 드라이버 관리자의 환경 핸들에서 드라이버의 환경 핸들이 이미 있는 경우 *핸들 유형이* 있는 **SQL_HANDLE_ENV SQLAllocHandle은** 연결이 이루어질 때 해당 드라이버에서 호출되지 않으며 핸들 *유형이* 있는 **SQLAllocHandle만** SQL_HANDLE_DBC. 드라이버 관리자의 환경 핸들 아래에 드라이버의 환경 핸들이 없는 경우 환경의 첫 번째 연결 핸들이 드라이버에 연결될 때 핸들 유형 SQL_HANDLE_ENV 및 핸들 유형SQL_HANDLE_DBC 있는 SQLAllocHandle이 모두 드라이버에서 호출됩니다.  
  
 드라이버 관리자가 *SQL_HANDLE_ENV 핸들 유형으로* **SQLAllocHandle** 함수를 처리하면 시스템 정보의 [ODBC] 섹션에서 **추적** 키워드를 확인합니다. 1로 설정된 경우 드라이버 관리자는 현재 응용 프로그램에 대한 추적을 활성화합니다. 추적 플래그가 설정된 경우 첫 번째 환경 핸들이 할당될 때 추적이 시작되고 마지막 환경 핸들이 해제될 때 종료됩니다. 자세한 내용은 [데이터 원본 구성](../../../odbc/reference/install/configuring-data-sources.md)을 참조하십시오.  
  
 환경 핸들을 할당한 후 응용 프로그램은 환경 핸들에서 **SQLSetEnvAttr을** 호출하여 SQL_ATTR_ODBC_VERSION 환경 특성을 설정해야 합니다. **SQLAllocHandle이** 환경에 연결 핸들을 할당하기 전에 이 특성을 설정하지 않으면 연결을 할당하는 호출이 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다. 자세한 내용은 [응용 프로그램의 ODBC 버전 선언을](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md)참조하십시오.  
  
## <a name="allocating-shared-environments-for-connection-pooling"></a>연결 풀링을 위한 공유 환경 할당  
 환경은 단일 프로세스의 여러 구성 요소 간에 공유할 수 있습니다. 공유 환경은 동시에 두 개 이상의 구성 요소에서 사용할 수 있습니다. 구성 요소가 공유 환경을 사용하는 경우 풀로 된 연결을 사용할 수 있으므로 해당 연결을 다시 만들지 않고도 기존 연결을 할당하고 사용할 수 있습니다.  
  
 연결 풀링에 사용할 수 있는 공유 환경을 할당하기 전에 응용 프로그램은 **SQLSetEnvAttr을** 호출하여 SQL_ATTR_CONNECTION_POOLING 환경 특성을 SQL_CP_ONE_PER_DRIVER 또는 SQL_CP_ONE_PER_HENV 설정해야 합니다. 이 경우 **SQLSetEnvAttr은** *환경 핸들을* null로 설정하여 호출되어 특성을 프로세스 수준 특성으로 만듭니다.  
  
 연결 풀링을 사용하도록 설정한 후 응용 프로그램은 *handleType* 인수가 SQL_HANDLE_ENV 설정된 **SQLAllocHandle을** 호출합니다. 연결 풀링이 활성화되었기 때문에 이 호출에서 할당된 환경은 암시적 공유 환경이 됩니다.  
  
 공유 환경이 할당되면 *핸들 유형* SQL_HANDLE_DBC 호출할 때까지 사용할 **환경이** 결정되지 않습니다. 이 때 드라이버 관리자는 응용 프로그램에서 요청한 환경 특성과 일치하는 기존 환경을 찾으려고 합니다. 이러한 환경이 없으면 공유 환경으로 만들어집니다. 드라이버 관리자는 각 공유 환경에 대한 참조 수를 유지 관리합니다. 개수는 환경을 처음 만들 때 1로 설정됩니다. 일치하는 환경이 발견되면 해당 환경의 핸들이 응용 프로그램에 반환되고 참조 수가 증가합니다. 이러한 방식으로 할당된 환경 핸들은 환경 핸들을 입력 인수로 허용하는 모든 ODBC 함수에서 사용할 수 있습니다.  
  
## <a name="allocating-a-connection-handle"></a>연결 핸들 할당  
 연결 핸들은 연결의 유효한 명령문 및 설명자 핸들및 트랜잭션이 현재 열려 있는지 여부와 같은 정보에 대한 액세스를 제공합니다. 연결 핸들에 대한 일반적인 내용은 [연결 핸들 을](../../../odbc/reference/develop-app/connection-handles.md)참조하십시오.  
  
 연결 핸들을 요청하려면 응용 프로그램이 *핸들 유형* SQL_HANDLE_DBC **SQLAllocHandle을** 호출합니다. *InputHandle* 인수는 해당 핸들을 할당한 **SQLAllocHandle** 호출에서 반환된 환경 핸들로 설정됩니다. 드라이버는 연결 정보에 대한 메모리를 할당하고 * \*OutputHandlePtr에서*연결된 핸들의 값을 다시 전달합니다. 응용 프로그램은 연결 * \*핸들이* 필요한 모든 후속 호출에서 OutputHandlePtr 값을 전달합니다. 자세한 내용은 [연결 핸들 할당을](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md)참조하십시오.  
  
 드라이버 관리자는 **SQLAllocHandle** 함수를 처리하고 응용 프로그램이 **SQLConnect,** **SQLBrowseConnect**또는 **SQLDriverConnect를**호출할 때 드라이버의 **SQLAllocHandle** 함수를 호출합니다. (자세한 내용은 [SQLConnect 함수를](../../../odbc/reference/syntax/sqlconnect-function.md)참조하십시오.)  
  
 SQL_ATTR_ODBC_VERSION 환경 특성이 **SQLAllocHandle이 호출되어** 환경에서 연결 핸들을 할당하기 전에 설정되지 않은 경우 연결을 할당하는 호출은 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다.  
  
 응용 프로그램이 SQL_HANDLE_DBC 설정된 *InputHandle* 인수를 사용하여 **SQLAllocHandle을** 호출하고 공유 환경 핸들로 설정하면 드라이버 관리자는 응용 프로그램에서 설정한 환경 특성과 일치하는 기존 공유 환경을 찾으려고 합니다. 이러한 환경이 없으면 1의 참조 개수(드라이버 관리자가 유지 관리)를 통해 환경이 만들어집니다. 일치하는 공유 환경이 발견되면 해당 핸들이 응용 프로그램에 반환되고 참조 수가 증가합니다.  
  
 사용할 실제 연결은 **SQLConnect** 또는 **SQLDriverConnect가** 호출될 때까지 드라이버 관리자에 의해 결정되지 않습니다. 드라이버 관리자는 **SQLConnect** 호출의 연결 옵션(또는 **SQLDriverConnect**호출의 연결 키워드)과 연결 할당 후 설정된 연결 특성을 사용하여 풀에서 사용할 연결을 결정합니다. 자세한 내용은 [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)를 참조하십시오.  
  
## <a name="allocating-a-statement-handle"></a>문 핸들 할당  
 문 핸들은 SQL 문 처리를 위한 오류 메시지, 커서 이름 및 상태 정보와 같은 명령문 정보에 대한 액세스를 제공합니다. 명령문 핸들에 대한 일반 정보는 [명령문 핸들 을](../../../odbc/reference/develop-app/statement-handles.md)참조하십시오.  
  
 명령문 핸들을 요청하려면 응용 프로그램이 데이터 원본에 연결한 다음 SQL 문을 제출하기 전에 **SQLAllocHandle을** 호출합니다. 이 호출에서 *핸들 을* SQL_HANDLE_STMT 설정 해야 하 고 *InputHandle* 해당 핸들을 할당 하는 **SQLAllocHandle에** 대 한 호출에 의해 반환 된 연결 핸들에 설정 해야 합니다. 드라이버는 명령문 정보에 대한 메모리를 할당하고 문 핸들을 지정된 연결과 연결하고 * \*OutputHandlePtr에서*연결된 핸들의 값을 다시 전달합니다. 응용 프로그램은 * \** 문 핸들이 필요한 모든 후속 호출에서 OutputHandlePtr 값을 전달합니다. 자세한 내용은 [명령문 핸들 할당을](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md)참조하십시오.  
  
 명령문 핸들이 할당되면 드라이버는 자동으로 네 개의 설명자 집합을 할당하고 이러한 설명자에 대한 핸들을 SQL_ATTR_APP_ROW_DESC, SQL_ATTR_APP_PARAM_DESC, SQL_ATTR_IMP_ROW_DESC 및 SQL_ATTR_IMP_PARAM_DESC 문 특성에 할당합니다. 이를 *암시적으로* 할당된 설명자라고 합니다. 응용 프로그램 설명기를 명시적으로 할당하려면 다음 섹션 "설명자 핸들 할당"을 참조하십시오.  
  
## <a name="allocating-a-descriptor-handle"></a>설명자 핸들 할당  
 응용 프로그램이 *핸들 유형* SQL_HANDLE_DESC **사용하여 SQLAllocHandle을** 호출하면 드라이버는 응용 프로그램 설명자가 할당됩니다. 이를 *명시적으로* 할당된 설명자라고 합니다. 응용 프로그램은 **SQLSetStmtAttr** 함수를 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 특성을 호출하여 지정된 문 핸들에 대해 자동으로 할당된 응용 프로그램 설명자 대신 명시적으로 할당된 응용 프로그램 설명기를 사용하도록 드라이버를 지시합니다. 구현 설명자는 명시적으로 할당할 수 없으며 **SQLSetStmtAttr** 함수 호출에 구현 설명기도 지정할 수 없습니다.  
  
 명시적으로 할당된 설명자는 자동으로 할당된 설명자가 있는 것처럼 문 핸들 대신 연결 핸들과 연결됩니다. 설명자는 응용 프로그램이 실제로 데이터베이스에 연결되어 있는 경우에만 할당된 상태로 유지됩니다. 명시적으로 할당된 설명자는 연결 핸들과 연결되므로 응용 프로그램은 명시적으로 할당된 설명자와 연결 내의 둘 이상의 문을 연결할 수 있습니다. 반면에 암시적으로 할당된 응용 프로그램 설명자는 두 개 이상의 문 핸들과 연결할 수 없습니다. (할당된 문 이 아닌 다른 문 핸들과 연결할 수 없습니다.) 명시적으로 할당된 설명자 핸들은 응용 프로그램에서 명시적으로 해제하거나 *핸들유형* SQL_HANDLE_DESC **SQLFreeHandle을** 호출하거나 연결이 닫혀 있을 때 암시적으로 해제할 수 있습니다.  
  
 명시적으로 할당된 설명자가 해제되면 암시적으로 할당된 설명자가 다시 문과 연결됩니다. 해당 명령문에 대한 SQL_ATTR_APP_ROW_DESC 또는 SQL_ATTR_APP_PARAM_DESC 특성은 암시적으로 할당된 설명자 핸들로 다시 설정됩니다. 이는 연결에 명시적으로 할당된 설명자와 연결된 모든 문에 해당됩니다.  
  
 설명자에 대한 자세한 내용은 [설명자](../../../odbc/reference/develop-app/descriptors.md)를 참조하십시오.  
  
## <a name="code-example"></a>코드 예  
 [샘플 ODBC 프로그램,](../../../odbc/reference/sample-odbc-program.md) [SQLBrowseConnect 함수,](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) [SQLConnect 함수](../../../odbc/reference/syntax/sqlconnect-function.md)및 [SQLSetCursorName 함수를](../../../odbc/reference/syntax/sqlsetcursorname-function.md)참조하십시오.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQL실행 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|환경, 연결, 명령문 또는 설명자 핸들 해제|[SQLFreeHandle 함수](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|실행을 위한 명령문 준비|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|연결 특성 설정|[SQLSetConnectAttr 함수](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|설명자 필드 설정|[SQLSetDesc필드 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|환경 특성 설정|[SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|문 특성 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
