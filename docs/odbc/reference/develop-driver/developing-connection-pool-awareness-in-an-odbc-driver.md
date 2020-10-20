---
description: ODBC 드라이버에서 연결 풀 인식 개발
title: ODBC 드라이버에서 Connection-Pool 인식 개발 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f22be001a7434c13158deae8677b8c7bcb2f0630
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192313"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>ODBC 드라이버에서 연결 풀 인식 개발
이 항목에서는 드라이버에서 연결 풀링 서비스를 제공 하는 방법에 대 한 정보가 포함 된 ODBC 드라이버 개발에 대 한 세부 정보를 설명 합니다.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>Driver-Aware 연결 풀링을 사용 하도록 설정  
 드라이버는 다음 ODBC SPI (서비스 공급자 인터페이스) 함수를 구현 해야 합니다.  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 자세한 내용은 [ODBC SPI (서비스 공급자 인터페이스) 참조](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) 를 참조 하세요.  
  
 드라이버 인식 풀링을 사용 하도록 설정할 수 있도록 드라이버는 다음과 같은 기존 함수도 구현 해야 합니다.  
  
|함수|추가 된 기능|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|새 핸들 형식 지원: SQL_HANDLE_DBC_INFO_TOKEN (아래 설명 참조).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|새 설정 전용 연결 특성을 지원 합니다. 연결을 다시 설정 하는 SQL_ATTR_DBC_INFO_TOKEN (아래 설명 참조).|  
  
> [!NOTE]  
>  **SQLError** 및 **SQLSetConnectOption** 와 같은 사용 되지 않는 함수는 드라이버 인식 연결 풀링을 지원 하지 않습니다.  
  
## <a name="the-pool-id"></a>풀 ID  
 풀 ID는 서로 교체 하 여 사용할 수 있는 특정 연결 그룹을 나타내는 포인터 길이 드라이버 관련 ID입니다. 연결 정보 집합이 지정 된 경우 드라이버는 해당 풀 ID를 신속 하 게 추론할 수 있습니다.  
  
 예를 들어 풀 ID는 서버 이름 및 자격 증명 정보를 인코딩해야 합니다. 그러나 드라이버가 연결을 다시 사용 하 고 새 연결을 만드는 것 보다 짧은 시간 내에 데이터베이스를 변경할 수 있기 때문에 데이터베이스 이름이 필요 하지 않습니다.  
  
 드라이버는 풀 ID를 구성 하는 키 특성 집합을 정의 해야 합니다. 이러한 키 특성의 값은 연결 특성, 연결 문자열 및 DSN에서 가져올 수 있습니다. 이러한 원본에 충돌이 발생 하는 경우 이전 버전과의 호환성을 위해 기존 드라이버 특정 해결 정책을 사용 해야 합니다.  
  
 드라이버 관리자는 다른 풀 Id에 다른 풀을 사용 합니다. 동일한 풀에 있는 모든 연결을 다시 사용할 수 있습니다. 드라이버 관리자는 다른 풀 ID의 연결을 다시 사용 하지 않습니다.  
  
 따라서 드라이버는 정의 된 키 특성에 동일한 값을 가진 모든 연결 그룹에 대해 고유한 풀 ID를 할당 해야 합니다. 드라이버에서 키 특성의 값이 서로 다른 두 연결에 동일한 풀 ID를 사용 하는 경우 드라이버 관리자는 동일한 풀에 해당 ID를 배치 합니다. 드라이버 관리자는 드라이버별 키 특성에 대 한 아무것도 인식 하지 못합니다. 즉, 드라이버는 다른 키 특성 집합을 사용 하는 연결을 [SQLRateConnection 함수](../../../odbc/reference/syntax/sqlrateconnection-function.md)내에서 다시 사용할 수 없다는 것을 드라이버 관리자에 게 보고 해야 합니다. 이렇게 하면 성능이 저하 될 수 있으며이는 권장 되지 않습니다.  
  
 드라이버 관리자는 모든 연결 정보가 일치 하는 경우에도 다른 드라이버 환경에서 할당 된 연결을 다시 사용 하지 않습니다. 연결 된 풀 ID를 사용 하는 경우에도 드라이버 관리자는 다른 환경에 다른 풀을 사용 합니다. 따라서 풀 ID는 해당 드라이버 환경에 대해 로컬입니다.  
  
 드라이버에서 풀 ID를 가져오는 함수는 [SQLGetPoolID 함수](../../../odbc/reference/syntax/sqlgetpoolid-function.md)입니다.  
  
## <a name="the-connection-rating"></a>연결 등급  
 새 연결을 설정 하는 것과 비교 하 여 풀링된 연결에서 일부 연결 정보 (예: 데이터베이스)를 다시 설정 하 여 더 나은 성능을 얻을 수 있습니다. 따라서 키 특성 집합에 데이터베이스 이름을 지정할 수 없습니다. 그렇지 않으면 각 데이터베이스에 대해 별도의 풀을 사용할 수 있습니다 .이는 고객이 다양 한 연결 문자열을 사용 하는 중간 계층 응용 프로그램에는 적합 하지 않을 수 있습니다.  
  
 일부 특성이 일치 하지 않는 연결을 다시 사용할 때마다 새 응용 프로그램 요청에 따라 일치 하지 않는 특성을 다시 설정 해야 합니다. 그러면 반환 된 연결이 응용 프로그램 요청과 동일 하 게 됩니다 ( [SQLSetConnectAttr 함수](../syntax/sqlsetconnectattr-function.md)에서 특성 SQL_ATTR_DBC_INFO_TOKEN 설명 참조). 그러나 이러한 특성을 다시 설정 하면 성능이 저하 될 수 있습니다. 예를 들어 데이터베이스를 다시 설정 하려면 서버에 대 한 네트워크 호출이 필요 합니다. 따라서 사용 가능한 경우 완벽 하 게 일치 하는 연결을 다시 사용 합니다.  
  
 드라이버의 등급 함수는 새 연결 요청에 대 한 기존 연결을 평가할 수 있습니다. 예를 들어 드라이버의 등급 함수는 다음을 확인할 수 있습니다.  
  
-   기존 연결이 요청과 완전히 일치 하면입니다.  
  
-   서버와의 통신이 필요 하지 않은 연결 제한 시간 등의 몇 가지 중요 한 불일치가 있는 경우  
  
-   다시 설정 하기 위해 서버와의 통신이 필요한 일부 일치 하지 않는 특성이 있는 경우에도 새 연결을 설정 하는 것 보다 더 나은 성능을 얻을 수 있습니다.  
  
-   다시 설정 하는 데 시간이 많이 걸리는 특성에 대해 일치 하지 않는 오류가 발생 한 경우 (드라이버의 개발자는 풀 ID를 생성 하는 데 사용 되는 키 특성 집합에이 특성을 추가 하는 것을 고려할 수 있습니다.)  
  
 0에서 100 사이의 점수를 사용할 수 있습니다. 여기서 0은 다시 사용 되지 않으며 100은 정확히 일치 하는 것을 의미 합니다. [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) 는 연결 등급을 매기는 함수입니다.  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>새 ODBC 핸들-SQL_HANDLE_DBC_INFO_TOKEN  
 드라이버 인식 연결 풀링을 지원 하려면 풀 ID를 계산 하기 위해 드라이버에 연결 정보가 필요 합니다. 또한 드라이버에는 새 연결 요청을 풀의 연결과 비교 하는 연결 정보가 필요 합니다.  풀에서 다시 사용할 수 있는 연결이 없는 경우 드라이버는 새 연결을 설정 해야 하므로 연결 정보가 필요 합니다.  
  
 연결 정보는 여러 원본 (연결 문자열, 연결 특성 및 DSN)에서 가져올 수 있으므로 드라이버가 연결 문자열을 구문 분석 하 고 위의 각 함수 호출에서 이러한 소스 간의 충돌을 해결 해야 할 수 있습니다.  
  
 따라서 SQL_HANDLE_DBC_INFO_TOKEN 새 ODBC 핸들이 도입 되었습니다. SQL_HANDLE_DBC_INFO_TOKEN를 사용 하는 경우 드라이버는 연결 문자열을 구문 분석 하 고 연결 정보에서 충돌을 두 번 이상 해결할 필요가 없습니다. 드라이버 관련 데이터 구조 이므로 드라이버에서 연결 정보 또는 풀 ID와 같은 데이터를 저장할 수 있습니다.  
  
 이 핸들은 드라이버 관리자와 드라이버 간의 인터페이스로만 사용 됩니다. 응용 프로그램은이 핸들을 직접 할당할 수 없습니다.  
  
 이 핸들의 부모 핸들은 SQL_HANDLE_ENV 형식입니다. 즉, 드라이버는 연결 정보를 확인 하는 동안 HENV 핸들에서 환경 정보를 가져올 수 있습니다.  
  
 새 연결 요청을 받을 때마다 드라이버 관리자는 연결 정보를 저장 하기 위해 SQL_HANDLE_DBC_INFO_TOKEN 유형의 핸들을 할당 합니다. 그러면 드라이버가 연결 풀 인식 기능을 지원 하는지 확인 합니다. 핸들 사용을 완료 했지만 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 또는 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)에서 SQL_STILL_EXECUTING 이외의 반환 코드를 반환 하기 전에 드라이버 관리자가 핸들을 해제 합니다. 따라서 핸들은 SQLAllocHandle 호출 후에 만들어지고 SQLFreeHandle 호출 후에 삭제 됩니다. 드라이버 관리자는 연결 된 HENV을 해제 하기 전에 핸들을 해제 하도록 보장 합니다 ( [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 또는 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 에서 오류를 반환 하는 경우).  
  
 드라이버는 새 핸들 형식 SQL_HANDLE_DBC_INFO_TOKEN를 허용 하도록 다음 함수를 수정 해야 합니다.  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 드라이버 관리자는 여러 스레드가 동일한 SQL_HANDLE_DBC_INFO_TOKEN 핸들을 동시에 사용 하지 않도록 보장 합니다. 따라서이 핸들의 동기화 모델은 드라이버 내부에서 매우 간단할 수 있습니다. SQL_HANDLE_DBC_INFO_TOKEN 할당 하 고 해제 하기 전에는 드라이버 관리자가 환경 잠금을 수행 하지 않습니다.  
  
 드라이버 관리자의 **SQLAllocHandle** 및 **sqlfreehandle** 은이 새 핸들 유형을 허용 하지 않습니다.  
  
 SQL_HANDLE_DBC_INFO_TOKEN는 자격 증명과 같은 기밀 정보를 포함할 수 있습니다. 따라서 드라이버는 **Sqlfreehandle**을 사용 하 여이 핸들을 해제 하기 전에 중요 한 정보를 포함 하는 메모리 버퍼 ( [SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)사용)를 안전 하 게 지워야 합니다. 응용 프로그램의 환경 핸들이 닫힐 때마다 연결 된 모든 연결 풀이 닫힙니다.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>드라이버 관리자 연결 풀 등급 알고리즘  
 이 섹션에서는 드라이버 관리자 연결 풀링을 위한 등급 알고리즘에 대해 설명 합니다. 드라이버 개발자는 이전 버전과의 호환성을 위해 동일한 알고리즘을 구현할 수 있습니다. 이 알고리즘은 가장 적합 한 알고리즘이 아닐 수 있습니다. 구현을 기반으로이 알고리즘을 구체화 해야 합니다. 그렇지 않으면이 기능을 구현할 이유가 없습니다.  
  
 드라이버 관리자는 풀에서 각 연결에 대해 0에서 100 까지의 정수 등급을 반환 합니다. 0은 연결을 다시 사용할 수 없고 100는 완벽 하 게 일치 하는 것을 나타냅니다. 연결 요청 이름이 hRequest이 고 풀의 기존 연결 이름이 Hrequest로 지정 되어 있다고 가정 합니다. 다음 조건 중 하나에 해당 하는 경우에는 풀링된 연결 hCandidate를 Hcandidate에 다시 사용할 수 없습니다. 드라이버 관리자는 등급 0을 할당 합니다.  
  
-   hCandidate와 Hcandidate는 모두: Sqldriverconnectw 등의 UNICODE API 또는 ANSI API (예:: Sqldriverconnecta)에서 제공 됩니다. 유니코드 드라이버는 지정 된 ANSI API 및 UNICODE API의 동작을 다르게 할 수 있습니다 (연결 특성 SQL_ATTR_ANSI_APP 참조).  
  
-   hCandidate와 Hcandidate는 동일한 함수에 의해 생성 됩니다. SQLDriverConnect 또는 SQLConnect 중 하나입니다.  
  
-   SQLDriverConnect를 사용 하는 경우 hCandidate를 여는 데 사용 되는 연결 문자열은 Hcandidate와 동일 해야 합니다.  
  
-   SQLConnect를 사용 하는 경우 hCandidate를 여는 데 사용 된 ServerName (또는 DSN), 사용자 이름 및 암호는 Hcandidate를 열 때와 동일 해야 합니다.  
  
-   현재 스레드의 SID (보안 식별자)는 hCandidate를 여는 데 사용 된 SID와 동일 해야 합니다.  
  
-   등록 하 고 등록을 취소 하는 데 비용이 많이 드는 드라이버의 경우 ( [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)의 SQL_DTC_TRANSITION_COST 설명 참조) *hrequest* 를 다시 사용 하려면 추가 참여 또는 등록 취소를 요구 하지 않아야 합니다.  
  
 다음 표에서는 다양 한 시나리오에 대 한 점수 할당을 보여 줍니다.  
  
|풀링된 연결과 요청 간 연결 특성 비교|인 리스트 먼 트 없음/참여 안 함|추가 참여/인 리스트 먼 트 필요|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|카탈로그 (SQL_ATTR_CURRENT_CATALOG)가 다릅니다.|60|50|  
|일부 연결 특성이 다르지만 카탈로그는 동일 합니다.|90|70|  
|완벽 하 게 일치 하는 모든 연결 특성|100|80|  
  
## <a name="sequence-diagram"></a>시퀀스 다이어그램  
 이 시퀀스 다이어그램은이 항목에 설명 된 기본 풀링 메커니즘을 보여 줍니다. [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 사용만 표시 하지만 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 사례는 비슷합니다.  
  
 ![시퀀스 다이어그램](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>상태 다이어그램  
 이 상태 다이어그램은이 항목에 설명 된 연결 정보 토큰 개체를 표시 합니다. 다이어그램에는 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 표시 되지만 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 사례는 비슷합니다. 드라이버 관리자는 언제 든 지 오류를 처리 해야 할 수 있으므로 모든 상태에 대해 [Sqlfreehandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) 을 호출할 수 있습니다.  
  
 ![상태 다이어그램](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>참고 항목  
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC SPI(서비스 공급자 인터페이스) 참조](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)