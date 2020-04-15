---
title: 3.5 드라이버를 3.8 드라이버로 업그레이드 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dcd01d050e806b733d75c54058945d367a33d6a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294434"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>3.5 드라이버를 3.8 드라이버로 업그레이드
이 항목에서는 ODBC 3.5 드라이버를 ODBC 3.8 드라이버로 업그레이드하기 위한 지침및 고려 사항을 제공합니다.  
  
##### <a name="version-numbers"></a>버전 번호  
 다음 지침은 버전 번호와 관련이 있습니다.  
  
-   드라이버는 SQL_OV_ODBC2, SQL_OV_ODBC3 및 SQL_OV_ODBC3_80 이외의 값에 대해 SQL_ERROR 반환하는 SQL_ATTR_ODBC_VERSION 대한 SQL_OV_ODBC3_80 지원해야 합니다. 드라이버 관리자의 이후 버전은 드라이버가 [SQLSetEnvAttr 함수에서](../../../odbc/reference/syntax/sqlsetenvattr-function.md)SQL_SUCCESS 반환하는 경우 드라이버가 ODBC 준수 수준을 지원한다고 가정합니다.  
  
-   버전 3.8 드라이버는 SQL_DRIVER_ODBC_VER *InfoType*에 전달될 때 **SQLGetInfo에서** 03.80을 반환해야 합니다. 그러나 이전 버전의 Microsoft Windows에 포함 된 이전 드라이버 관리자는 드라이버를 버전 3.5 드라이버로 처리하고 경고를 발행합니다.  
  
     Windows 7에서 드라이버 관리자 버전은 03.80입니다. Windows 8에서 드라이버 관리자 버전은 SQLGetInfo SQL_DM_VER *(InfoType* 매개 변수)를 통해 03.81입니다. SQL_ODBC_VER 윈도우 7과 윈도우 8 모두에서 03.80로 버전을보고합니다.  
  
##### <a name="driver-specific-c-data-types"></a>드라이버별 C 데이터 유형  
 드라이버는 버전 3.8 ODBC 응용 프로그램과 함께 작동 할 때 C 데이터 형식을 사용자 정의 할 수 있습니다. (자세한 내용은 [ODBC의 C 데이터 형식을](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)참조하십시오.) 그러나 3.8 드라이버가 드라이버 별 C 형식을 구현할 필요는 없습니다. 그러나 드라이버는 여전히 C 유형의 범위 검사를 수행해야합니다. 드라이버 관리자는 3.8 드라이버에 대해 그렇게하지 않습니다. 드라이버 개발을 용이하게 하기 위해 드라이버 별 C 데이터 형식의 값을 다음 형식으로 정의할 수 있습니다.  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>드라이버 별 데이터 유형, 설명자 유형, 정보 유형, 진단 유형 및 특성  
 새 드라이버를 개발할 때는 데이터 유형, 설명자 유형, 정보 유형, 진단 유형 및 특성에 대해 드라이버 별 범위를 사용해야 합니다. 드라이버 별 범위 및 해당 기본 형식 값은 [드라이버 관련 데이터 유형, 설명자 유형, 정보 유형, 진단 유형 및 특성에서 설명합니다.](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)  
  
##### <a name="connection-pooling"></a>연결 풀링  
 연결 풀링을 보다 잘 관리하기 위해 ODBC 3.8은 **SQLSetConnectAttr에서**SQL_ATTR_RESET_CONNECTION 연결 특성을 도입합니다. SQL_RESET_CONNECTION_YES 이 특성에 대한 유일한 유효한 값입니다. SQL_ATTR_RESET_CONNECTION 드라이버 관리자가 연결 풀에 연결을 넣기 직전에 설정되므로 드라이버가 다른 연결 특성을 기본값으로 재설정할 수 있습니다.  
  
 서버와의 불필요한 통신을 방지하기 위해 드라이버는 풀에서 연결을 다시 사용한 후 원격 서버와의 다음 통신까지 연결 특성 재설정을 연기할 수 있습니다.  
  
 SQL_ATTR_RESET_CONNECTION 드라이버 관리자와 드라이버 간의 통신에만 사용됩니다. 응용 프로그램에서 이 특성을 직접 설정할 수 없습니다. 모든 버전 3.8 드라이버는 이 연결 특성을 구현해야 합니다.  
  
##### <a name="streamed-output-parameters"></a>스트리밍된 출력 매개변수  
 ODBC 버전 3.8은 스트리밍 된 출력 매개 변수를 도입하여 출력 매개 변수를 검색하는 보다 확장 가능한 방법을 도입합니다. 자세한 내용은 [SQLGetData를 사용하여 출력 매개 변수 검색을](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)참조하십시오. 이 기능을 지원하려면 **SQL_GETDATA_EXTENSIONS SQLGetInfo** 호출의 *InfoType인* 경우 드라이버는 반환 값으로 SQL_GD_OUTPUT_PARAMS 설정해야 합니다. 스트리밍된 출력 매개 변수가 있는 SQL 형식에 대한 지원은 드라이버에서 구현해야 합니다. 드라이버 관리자는 잘못된 SQL 형식에 대한 오류를 생성하지 않습니다. 스트리밍된 출력 매개 변수를 지원하는 SQL 형식은 드라이버에 정의되어 있습니다.  
  
 응용 프로그램에서 **SQLGetData를 사용하여 SQLParamData에서** 반환되는 매개 변수와 같지 **SQLParamData**않은 매개 변수를 검색하는 경우 드라이버는 SQL_ERROR 반환해야 합니다.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>연결 작업에 대한 비동기 실행(폴링 방법)  
 드라이버는 다양한 연결 작업에 대한 비동기 지원을 활성화할 수 있습니다.  
  
 Windows 7에서 시작하여 ODBC는 폴링 메서드를 지원합니다(자세한 내용은 [비동기 실행(폴링 메서드 참조)을](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)참조하십시오. 버전 3.8 ODBC 드라이버가 연결 핸들에서 비동기 작업을 구현할 필요는 없습니다. 드라이버가 연결 핸들에서 비동기 작업을 구현하지 않더라도 드라이버는 SQL_ASYNC_DBC_FUNCTIONS *InfoType을* 구현하고 **SQL_ASYNC_DBC_NOT_CAPABLE**반환해야 합니다.  
  
 비동기 연결 작업을 사용하도록 설정하면 연결 작업의 실행 시간은 모든 반복 호출의 총 시간입니다. 총 시간이 SQL_ATTR_CONNECTION_TIMEOUT 연결 특성에 의해 설정된 값을 초과하고 작업이 완료되지 않은 후 마지막으로 반복되는 호출이 발생하면 드라이버는 SQL_ERROR 반환하고 SQLState HYT01을 사용 하 여 진단 레코드를 기록 하 고 메시지 "연결 시간 초과 만료". 작업이 완료되면 시간 시간이 지정되지 않습니다.  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 함수  
 ODBC 3.8은 연결 및 문 작업을 모두 취소하는 데 사용되는 [SQLCancelHandle 함수를](../../../odbc/reference/syntax/sqlcancelhandle-function.md)지원합니다. **SQLCancelHandle을** 지원하는 드라이버는 함수를 내보내야 합니다. 드라이버는 응용 프로그램이 문 핸들에서 **SQLCancel** 또는 **SQLCancelHandle을** 호출하는 경우 진행 중인 동기 또는 비동기 연결 함수를 취소해서는 안 됩니다. 마찬가지로 드라이버는 응용 프로그램이 연결 핸들에서 **SQLCancelHandle을** 호출하는 경우 진행 중인 동기 또는 비동기 문 함수를 취소해서는 안 됩니다. 또한 드라이버는 응용 프로그램이 연결 핸들에서 **SQLCancelHandle을** 호출하는 경우 검색**작업(SQLBrowseConnectSQL_NEED_DATA** 반환)을 취소해서는 안 됩니다. 이러한 경우 드라이버는 HY010, "함수 시퀀스 오류"를 반환해야 합니다.  
  
 **SQLCancelHandle** 및 비동기 연결 작업을 동시에 지원할 필요는 없습니다. 드라이버는 비동기 연결 작업을 지원할 수 있지만 **SQLCancelHandle은**지원하지 않으며 그 반대의 경우도 마찬가지입니다.  
  
##### <a name="suspended-connections"></a>일시 중단된 연결  
 ODBC 3.8 드라이버 관리자는 연결을 일시 중단된 상태로 만들 수 있습니다. 응용 프로그램은 **SQLDisconnect를** 호출하여 연결과 관련된 리소스를 해제합니다. 이 경우 드라이버는 연결 상태를 확인하지 않고 가능한 한 많은 리소스를 릴리스하려고 시도해야 합니다. 일시 중단된 상태에 대한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조하십시오.  
  
##### <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링  
 Windows 8의 ODBC를 사용하면 드라이버가 연결 풀 동작을 사용자 지정할 수 있습니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 참조하십시오.  
  
##### <a name="asynchronous-execution-notification-method"></a>비동기 실행(알림 방법)  
 ODBC 3.8은 Windows 8에서 시작하여 사용할 수 있는 비동기 작업에 대한 알림 방법을 지원합니다. 자세한 내용은 [비동기 실행(알림 메서드)을](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [마이크로소프트 제공 ODBC 드라이버](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
