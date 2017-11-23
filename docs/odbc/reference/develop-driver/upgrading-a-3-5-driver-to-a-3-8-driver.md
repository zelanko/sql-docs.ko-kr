---
title: "3.8 드라이버에 3.5 드라이버 업그레이드 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ffba36ac-d22e-40b9-911a-973fa9e10bd3
caps.latest.revision: "27"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5dc39bf1203a06d571bf188e17e7066e53167415
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="upgrading-a-35-driver-to-a-38-driver"></a>3.8 드라이버에 3.5 드라이버를 업그레이드합니다.
이 항목에서는 ODBC 3.8 드라이버에 ODBC 3.5 드라이버 업그레이드 시 고려 사항 및 지침을 제공 합니다.  
  
##### <a name="version-numbers"></a>버전 번호  
 다음 지침 버전 번호와 관련이 있습니다.  
  
-   드라이버를 sql_attr_odbc_version으로, SQL_OV_ODBC2, SQL_OV_ODBC3, 및 SQL_OV_ODBC3_80 외의 값에 대 한 SQL_ERROR를 반환에 대 한 SQL_OV_ODBC3_80를 지원 해야 합니다. 이후 버전의 드라이버 관리자는 드라이버에서 SQL_SUCCESS를 반환 하는 경우 드라이버는 ODBC 준수 수준을 지원 하는지 가정 [SQLSetEnvAttr 함수](../../../odbc/reference/syntax/sqlsetenvattr-function.md)합니다.  
  
-   버전 3.8 드라이버에서 03.80 반환할지 **SQLGetInfo** SQL_DRIVER_ODBC_VER에 전달 되 면 *정보 항목*합니다. 그러나 이전 버전의 Microsoft Windows에 포함 되었던 이전 드라이버 관리자 버전 3.5 드라이버를 드라이버를 처리 하 고 경고를 발생 합니다.  
  
     Windows 7, 드라이버 관리자 버전이 03.80 합니다. Windows 8에서는 드라이버 관리자 버전은 SQLGetInfo SQL_DM_VER 통해 03.81 (*정보 항목* 매개 변수). SQL_ODBC_VER는 03.80 둘 다 Windows 7 및 Windows 8로 버전을 보고합니다.  
  
##### <a name="driver-specific-c-data-types"></a>드라이버 관련 C 데이터 형식  
 드라이버 수 사용자 지정한 C 데이터 형식 버전 3.8 ODBC 응용 프로그램 작업을 수행할 때는 합니다. (자세한 내용은 참조 [odbc에서 C 데이터 형식을](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).) 그러나 모든 드라이버 관련 C 형식을 구현 하는 3.8 드라이버에 대 한 않아도가 됩니다. 드라이버 C 형식;의 범위 검사를 계속 실행 되어야 하지만 드라이버 관리자 3.8 드라이버는 수행 하지 않습니다. 드라이버 개발을 위해 다음과 같은 형식의 드라이버 관련 C 데이터 형식 값을 정의할 수 있습니다.  
  
```  
SQL_DRIVER_C_TYPE_BASE+0, SQL_DRIVER_C_TYPE_BASE+1  
```  
  
##### <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>드라이버 관련 데이터 형식, 형식 설명자, 정보 유형, 진단 형식 및 특성  
 새 드라이버를 개발할 때 데이터 형식, 형식 설명자, 정보 유형, 진단 형식 및 특성에 대 한 드라이버 관련 범위를 사용 해야 합니다. 드라이버 관련 범위 및 해당 기본 형식 값에 설명 되어 [드라이버 관련 데이터 형식, 형식 설명자, 정보 유형, 진단 형식 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)합니다.  
  
##### <a name="connection-pooling"></a>연결 풀링  
 연결 풀링을 보다 효율적으로 관리 ODBC 3.8 소개 SQL_ATTR_RESET_CONNECTION 연결 특성에 **SQLSetConnectAttr**합니다. SQL_RESET_CONNECTION_YES는이 특성에 대 한 유일한 유효 값입니다. 드라이버 관리자 배치 연결이 연결 풀에서 다른 연결 특성을 해당 기본값으로 다시 설정 하는 드라이버 수 있도록 하기 바로 전에 SQL_ATTR_RESET_CONNECTION 설정 됩니다.  
  
 서버와의 불필요 한 통신을 방지 하려면 드라이버는 연결 풀에서 다시 사용 되 면 원격 서버와의 다음 통신 될 때까지 다시 설정 연결 특성을 연기할 수 있습니다.  
  
 참고 SQL_ATTR_RESET_CONNECTION 드라이버 관리자와 드라이버 간의 통신에만 사용 됩니다. 응용 프로그램은이 특성을 직접 설정할 수 없습니다. 모든 버전 3.8 드라이버는이 연결 특성을 구현 해야 합니다.  
  
##### <a name="streamed-output-parameters"></a>스트리밍된 출력 매개 변수  
 ODBC 3.8 버전 출력 매개 변수를 검색 하는 확장성이 뛰어난 방법이 스트리밍된 출력 매개 변수를 소개 합니다. (자세한 내용은 참조 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).) 이 기능을 지원 하려면 드라이버 설정할지 SQL_GD_OUTPUT_PARAMS 반환 값에 SQL_GETDATA_EXTENSIONS 경우는 *정보 항목* 에 **SQLGetInfo** 호출 합니다. 스트리밍된 출력 매개 변수를 포함 하는 SQL 형식에 대 한 지원 드라이버에 구현 되어야 합니다. 드라이버 관리자에서 잘못 된 SQL 형식에 대 한 오류를 생성 하지 않습니다. 스트리밍된 출력 매개 변수를 지 원하는 SQL 유형의 드라이버에서 정의 됩니다.  
  
 응용 프로그램이 사용 하는 경우 드라이버에서 SQL_ERROR를 반환 해야 **SQLGetData** 에서 반환 되는 매개 변수와 동일 하지 않은 매개 변수를 검색 하려면 **SQLParamData**합니다.  
  
##### <a name="asynchronous-execution-for-connection-operations-polling-method"></a>연결 작업 (폴링 방법)에 대 한 비동기 실행  
 드라이버는 다양 한 연결 작업에 대 한 비동기 지원을 사용 하도록 설정할 수 있습니다.  
  
 Windows 7부터, ODBC에서 폴링 메서드를 지원 (자세한 내용은 참조 [비동기 실행 (폴링 방법)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)합니다. 연결 핸들에 대 한 비동기 작업을 구현 하는 버전 3.8 ODBC 드라이버에 대 한 않아도가 됩니다. 드라이버는 SQL_ASYNC_DBC_FUNCTIONS 구현 해야 하는 드라이버는 연결 핸들에 대 한 비동기 작업을 구현 하지 않으면 경우에 *정보 항목* 다음 다시 돌아와 **SQL_ASYNC_DBC_NOT_CAPABLE**합니다.  
  
 비동기 연결 작업을 사용 하는 경우 연결 작업의 실행 시간 반복된 하 여 모든 호출의 총 시간이입니다. 마지막 반복 호출 롤백되 총 시간이 SQL_ATTR_CONNECTION_TIMEOUT 연결 특성으로 설정 된 값을 초과 했으므로 되 고 작업을 완료 하지 드라이버가 SQL_ERROR를 반환 하 고 SQLState HYT01 된 진단 레코드가 기록 및 "연결 제한 시간이 만료 되었습니다." 메시지입니다. 작업을 완료 하는 경우 제한 시간은 없습니다.  
  
##### <a name="sqlcancelhandle-function"></a>SQLCancelHandle 함수  
 ODBC 3.8 지원 [SQLCancelHandle 함수](../../../odbc/reference/syntax/sqlcancelhandle-function.md), 연결 및 문 작업을 모두 취소 하는 데 사용 되는 합니다. 지 원하는 드라이버 **SQLCancelHandle** 함수 내보내기를 수행 해야 합니다. 드라이버는 응용 프로그램을 호출 하는 경우 진행 중인 모든 동기 또는 비동기 연결 함수 취소 해서는 안됩니다 **SQLCancel** 또는 **SQLCancelHandle** 문 핸들에서 합니다. 마찬가지로, 드라이버 취소 해서는 안됩니다 응용 프로그램을 호출 하는 경우 진행 중인 모든 동기 또는 비동기 문 함수 **SQLCancelHandle** 연결 핸들에 있습니다. 또한 드라이버 해야 작업을 취소할 검색 (**SQLBrowseConnect** sql_need_data가 반환) 응용 프로그램을 호출 하는 경우 **SQLCancelHandle** 연결 핸들에 있습니다. 이러한 경우에는 드라이버 HY010, "함수 시퀀스 오류"를 반환 해야 합니다.  
  
 둘 다 지 원하는 데 필요 없는 **SQLCancelHandle** 및 동시에 비동기 연결 작업입니다. 드라이버는 비동기 연결 작업을 지원할 수 있지만 **SQLCancelHandle**, 또는 그 반대로 합니다.  
  
##### <a name="suspended-connections"></a>일시 중단 된 연결  
 ODBC 3.8 드라이버 관리자 일시 중단된 상태에 대 한 연결을 넣을 수 있습니다. 응용 프로그램에서 호출할 **SQLDisconnect** 연결과 관련 된 리소스를 해제 합니다. 이 경우 드라이버는 연결의 상태를 확인 하지 않고 최대한 많은 리소스를 해제 하기 위해 시도해 보십시오. 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.  
  
##### <a name="driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링  
 Windows 8에서 ODBC 드라이버가 연결 풀의 동작을 사용자 지정할 수 있습니다. 자세한 내용은 참조 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)합니다.  
  
##### <a name="asynchronous-execution-notification-method"></a>비동기 실행(알림 방법)  
 ODBC 3.8 Windows 8에서 시작 하 고 사용 가능한 비동기 작업에 대 한 알림 방법을 지원 합니다. 자세한 내용은 참조 [비동기 실행 (알림 방법)](../../../odbc/reference/develop-app/asynchronous-execution-notification-method.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 드라이버를 개발합니다.](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Microsoft에서 제공 하는 ODBC 드라이버](../../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)   
 [ODBC 3.8의 새로운 기능](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
