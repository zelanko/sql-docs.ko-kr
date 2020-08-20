---
description: 3.5 드라이버를 3.8 드라이버로 업그레이드
title: 3.5 드라이버를 3.8 드라이버로 업그레이드 | Microsoft Docs
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
ms.openlocfilehash: ac140c92b4042df1b4754d3a56237a6aa4b3afaf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461335"
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>3.5 드라이버를 3.8 드라이버로 업그레이드
이 항목에서는 odbc 3.5 드라이버를 ODBC 3.8 드라이버로 업그레이드 하는 방법에 대 한 지침과 고려 사항을 제공 합니다.  
  
##### <a name="version-numbers"></a>버전 번호  
 버전 번호와 관련 된 지침은 다음과 같습니다.  
  
-   드라이버는 SQL_ATTR_ODBC_VERSION에 대 한 SQL_OV_ODBC3_80를 지원 하 여 SQL_OV_ODBC2, SQL_OV_ODBC3 및 SQL_OV_ODBC3_80 이외의 값에 대 한 SQL_ERROR 반환 해야 합니다. 이후 버전의 드라이버 관리자는 드라이버가 [SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)에서 SQL_SUCCESS를 반환 하는 경우 드라이버에서 ODBC 준수 수준을 지원 한다고 가정 합니다.  
  
-   SQL_DRIVER_ODBC_VER이 *InfoType*에 전달 되 면 버전 3.8 드라이버가 **SQLGetInfo** 에서 03.80을 반환 해야 합니다. 그러나 이전 버전의 Microsoft Windows에 포함 된 이전 드라이버 관리자는 드라이버를 버전 3.5 드라이버로 처리 하 고 경고를 실행 합니다.  
  
     Windows 7에서 드라이버 관리자 버전은 03.80입니다. Windows 8에서 드라이버 관리자 버전은 SQLGetInfo SQL_DM_VER (*InfoType* 매개 변수)를 통해 03.81입니다. SQL_ODBC_VER Windows 7 및 Windows 8에서 버전을 03.80로 보고 합니다.  
  
##### <a name="driver-specific-c-data-types"></a>드라이버 관련 C 데이터 형식  
 드라이버는 버전 3.8 ODBC 응용 프로그램에서 작동 하는 경우 사용자 지정 된 C 데이터 형식을 가질 수 있습니다. 자세한 내용은 [ODBC의 C 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)을 참조 하세요. 그러나 드라이버 관련 C 유형을 구현 하기 위해 3.8 드라이버를 요구 하지 않습니다. 하지만 드라이버는 여전히 C 형식의 범위 검사를 수행 해야 합니다. 드라이버 관리자는 3.8 드라이버에 대해이 작업을 수행 하지 않습니다. 드라이버 개발을 용이 하 게 하기 위해 드라이버 특정 C 데이터 형식의 값을 다음 형식으로 정의할 수 있습니다.  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>드라이버 특정 데이터 형식, 설명자 유형, 정보 유형, 진단 유형 및 특성  
 새 드라이버를 개발 하는 경우 데이터 형식, 설명자 유형, 정보 유형, 진단 유형 및 특성에 대 한 드라이버별 범위를 사용 해야 합니다. 드라이버별 범위 및 해당 기본 형식 값은 [드라이버별 데이터 형식, 설명자 형식, 정보 형식, 진단 유형 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)에서 설명 합니다.  
  
##### <a name="connection-pooling"></a>연결 풀링  
 연결 풀링을 보다 효율적으로 관리 하기 위해 ODBC 3.8에서는 **SQLSetConnectAttr**의 SQL_ATTR_RESET_CONNECTION 연결 특성을 소개 합니다. 이 특성의 유일한 유효 값은 SQL_RESET_CONNECTION_YES입니다. 드라이버 관리자가 연결 풀에서 연결을 설정 하 여 다른 연결 특성을 기본값으로 다시 설정할 수 있도록 SQL_ATTR_RESET_CONNECTION 설정 됩니다.  
  
 서버와의 불필요 한 통신을 방지 하기 위해 드라이버는 연결이 풀에서 다시 사용 된 후 원격 서버와의 다음 통신을 수행할 때까지 연결 특성이 다시 설정 되는 것을 연기할 수 있습니다.  
  
 SQL_ATTR_RESET_CONNECTION는 드라이버 관리자와 드라이버 간 통신에만 사용 됩니다. 응용 프로그램은이 특성을 직접 설정할 수 없습니다. 모든 버전 3.8 드라이버는이 연결 특성을 구현 해야 합니다.  
  
##### <a name="streamed-output-parameters"></a>스트리밍된 출력 매개 변수  
 ODBC 버전 3.8에는 출력 매개 변수를 검색 하는 보다 확장성 있는 방법인 스트리밍된 출력 매개 변수가 도입 되었습니다. 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)을 참조 하세요. 이 기능을 지원 하기 위해 SQL_GETDATA_EXTENSIONS가 **SQLGetInfo** 호출에서 *InfoType* 때 드라이버는 반환 값에 SQL_GD_OUTPUT_PARAMS를 설정 해야 합니다. 스트리밍된 출력 매개 변수가 포함 된 SQL 형식에 대 한 지원은 드라이버에서 구현 되어야 합니다. 드라이버 관리자는 잘못 된 SQL 형식에 대해 오류를 생성 하지 않습니다. 스트리밍된 출력 매개 변수를 지 원하는 SQL 형식은 드라이버에 정의 되어 있습니다.  
  
 응용 프로그램에서 **SQLGetData** 를 사용 하 여 **sqlparamdata**에서 반환 된 매개 변수와 동일한 매개 변수를 검색 하는 경우 드라이버는 SQL_ERROR을 반환 해야 합니다.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>연결 작업에 대 한 비동기 실행 (폴링 방법)  
 드라이버는 다양 한 연결 작업에 대 한 비동기 지원을 사용할 수 있습니다.  
  
 Windows 7부터 ODBC는 폴링 방법을 지원 합니다. 자세한 내용은 [비동기 실행 (폴링 방법)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)을 참조 하세요. 연결 핸들에 대해 비동기 작업을 구현 하기 위해 버전 3.8 ODBC 드라이버에 대 한 요구 사항은 없습니다. 드라이버가 연결 핸들에 대해 비동기 작업을 구현 하지 않는 경우에도 드라이버는 SQL_ASYNC_DBC_FUNCTIONS *InfoType* 을 구현 하 고 **SQL_ASYNC_DBC_NOT_CAPABLE**를 반환 해야 합니다.  
  
 비동기 연결 작업을 사용 하는 경우 연결 작업의 실행 시간은 반복 되는 모든 호출의 총 시간입니다. 총 시간이 SQL_ATTR_CONNECTION_TIMEOUT 연결 특성에 설정 된 값을 초과 하 여 마지막으로 반복 되는 호출이 발생 하 고 작업이 완료 되지 않은 경우 드라이버는 SQL_ERROR를 반환 하 고 SQLState HYT01와 "연결 제한 시간이 만료 되었습니다." 라는 메시지가 포함 된 진단 레코드를 로깅합니다. 작업이 완료 되 면 시간 제한이 없습니다.  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 함수  
 ODBC 3.8은 연결 및 문 작업을 모두 취소 하는 데 사용 되는 [Sqlcancelhandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md)를 지원 합니다. **Sqlcancelhandle** 을 지 원하는 드라이버는 함수를 내보내야 합니다. 응용 프로그램이 문 핸들에 대해 **Sqlcancel** 또는 **sqlcancelhandle** 을 호출 하는 경우 드라이버는 진행 중인 모든 동기 또는 비동기 연결 함수를 취소 하면 안 됩니다. 마찬가지로, 응용 프로그램이 연결 핸들에서 **Sqlcancelhandle** 을 호출 하는 경우 드라이버는 진행 중인 동기 또는 비동기 문 함수를 취소 하면 안 됩니다. 또한 응용 프로그램이 연결 핸들에서 **Sqlcancelhandle** 을 호출 하는 경우 드라이버는 검색 작업을 취소 하지 않아야 합니다 (**SQLBrowseConnect** 반환 SQL_NEED_DATA). 이러한 경우 드라이버는 "함수 시퀀스 오류" HY010를 반환 해야 합니다.  
  
 **Sqlcancelhandle** 과 비동기 연결 작업을 동시에 지원할 필요는 없습니다. 드라이버는 비동기 연결 작업을 지원할 수 있지만 **Sqlcancelhandle**은 지원할 수 없으며 그 반대의 경우도 마찬가지입니다.  
  
##### <a name="suspended-connections"></a>일시 중단 된 연결  
 ODBC 3.8 드라이버 관리자는 일시 중단 상태에 대 한 연결을 설정할 수 있습니다. 응용 프로그램은 **Sqldisconnect** 를 호출 하 여 연결과 관련 된 리소스를 해제 합니다. 이 경우 드라이버는 연결 상태를 확인 하지 않고 최대한 많은 리소스를 해제 하려고 합니다. 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.  
  
##### <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링  
 Windows 8의 ODBC에서는 드라이버가 연결 풀 동작을 사용자 지정할 수 있습니다. 자세한 내용은 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)을 참조 하세요.  
  
##### <a name="asynchronous-execution-notification-method"></a>비동기 실행(알림 방법)  
 ODBC 3.8은 Windows 8부터 사용 가능한 비동기 작업에 대 한 알림 방법을 지원 합니다. 자세한 내용은 [비동기 실행 (알림 방법)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)을 참조 하세요.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft에서 제공 하는 ODBC 드라이버](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
