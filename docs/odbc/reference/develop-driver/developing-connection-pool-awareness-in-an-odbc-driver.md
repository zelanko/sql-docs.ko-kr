---
title: "ODBC 드라이버에서 연결 풀 인식 개발 | Microsoft Docs"
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
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b96e4ef1e53fec8361bd96dee81206efdf138538
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>ODBC 드라이버에서 연결 풀 인식 개발
이 항목에서는 개발 방법 드라이버 연결 풀링 서비스를 제공 해야 하는 방법에 대 한 정보를 포함 하는 ODBC 드라이버의 세부 정보를 설명 합니다.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링을 사용 하도록 설정  
 드라이버는 다음과 같은 ODBC 서비스 공급자 인터페이스 (SPI) 기능을 구현 해야 합니다.  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 참조 [ODBC 서비스 공급자 인터페이스 (SPI) 참조](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) 자세한 정보에 대 한 합니다.  
  
 또한 드라이버는 드라이버 인식 풀링을 사용할 수 있도록 다음 기존 함수를 구현 해야 합니다.  
  
|함수|추가 된 기능|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|새 핸들 형식을 지원: SQL_HANDLE_DBC_INFO_TOKEN (아래 설명 참조).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|새 설정 전용 연결 특성을 지원: 연결을 다시 설정 하기 위해 SQL_ATTR_DBC_INFO_TOKEN (아래 설명 참조).|  
  
> [!NOTE]  
>  사용 되지 않는 같은 함수와 **SQLError** 및 **SQLSetConnectOption** 드라이버 인식 연결 풀링을 지원 되지 않습니다.  
  
## <a name="the-pool-id"></a>풀 ID  
 풀 ID가 서로 바꿔 사용할 수 있는 연결의 특정 그룹을 나타내는 데 포인터 길이 드라이버 관련 ID입니다. 연결 정보 집합이 제공 된, 드라이버 해야 신속 하 게 추론할 수는 해당 풀 id입니다.  
  
 예를 들어 풀 ID를 서버 이름 및 자격 증명 정보를 인코딩해야 합니다. 그러나, 드라이버는 연결을 다시 사용 하 고 새 연결을 만드는 것 보다 짧은 시간에 데이터베이스를 변경할 수 때문에 데이터베이스 이름이 필요 하지 않습니다.  
  
 드라이버는 풀 ID를 구성 하는 키 특성의 집합을 정의 해야 이러한 키 특성의 값은 연결 특성, 연결 문자열 및 DSN에서 가져올 수 있습니다. 이러한 원본에서 충돌이 있는 경우 이전 버전과 호환성을 위해 기존, 드라이버 관련 해결 정책을 사용 해야 합니다.  
  
 드라이버 관리자는 다른 풀 Id에 대 한 다른 풀을 사용 합니다. 동일한 풀의 모든 연결은 다시 사용할 수 있습니다. 드라이버 관리자에서 id가 다른 풀 ID와의 연결을 다시 사용 되지 않습니다.  
  
 따라서 드라이버는 해당 정의 된 키 특성에 값이 같은 연결의 모든 그룹에 대 한 고유한 풀 ID를 할당 해야 합니다. 경우 동일한 풀 ID를 사용 하 여 해당 키 특성에 값이 서로 다른 두 개의 연결에 대 한 드라이버를 드라이버 관리자는 여전히 넣습니다 (드라이버 관리자를 인식 하지 못하므로 드라이버 관련 키 특성에 대 한) 동일한 풀으로 합니다. 즉, 드라이버 관리자에 내부 다시 사용할 수 없는 키 특성의 다른 집합와의 연결을 보고 하기 위해 드라이버가 필요 함을 [SQLRateConnection 함수](../../../odbc/reference/syntax/sqlrateconnection-function.md)합니다. 성능이 저하 될 수이 하 고 권장 되지 않습니다.  
  
 드라이버 관리자 연결 정보를 모두 일치 하는 경우에 다른 드라이버 환경에서 할당 한 연결 다시 사용 하지 않습니다. 드라이버 관리자는 다른 풀을 사용 다른 환경에 대 한 연결 동일한 풀 ID가 지정 하는 경우에 따라서 풀 ID를 해당 드라이버 환경에 로컬입니다.  
  
 드라이버에서 풀 ID를 가져오기 위한 함수는 [SQLGetPoolID 함수](../../../odbc/reference/syntax/sqlgetpoolid-function.md)합니다.  
  
## <a name="the-connection-rating"></a>연결 등급  
 새 연결을 설정에 비해, 풀링된 연결의 일부 연결 정보 (예: 데이터베이스)를 다시 설정 하 여 더 나은 성능을 얻을 수 있습니다. 따라서 키 특성의 집합에 포함 되도록 데이터베이스 이름을 원하지 않을 수 있습니다. 그렇지 않으면 고객이 다양 한 다른 연결 문자열을 사용 하는 위치 하지 않을 수 있는 중간 계층 응용 프로그램의 좋은, 각 데이터베이스에 대 한 별도 풀을 사용할 수 있습니다.  
  
 반환 된 연결은 응용 프로그램 요청에 동일 하 고 새 응용 프로그램 요청에 따라 일치 하지 않는 특성을 다시 설정 해야 일부 속성 불일치로 없는 연결을 다시 사용할 때마다 (SQL_ATTR 특성 설명을 참조 하십시오. _DBC_INFO_TOKEN [SQLSetConnectAttr 함수](http://go.microsoft.com/fwlink/?LinkId=59368)). 이러한 특성을 다시 설정 하면 성능이 저하 될 수 있습니다. 예를 들어 데이터베이스를 다시 설정 하려면 서버에 네트워크 호출이 필요 합니다. 따라서 사용 가능한 경우 완벽 하 게 일치 하는 연결을 다시 사용 합니다.  
  
 드라이버에서 등급 함수는 새 연결 요청을 사용 하는 기존 연결이 평가할 수 있습니다. 예를 들어 드라이버의 등급 함수 확인할 수 있습니다.  
  
-   경우 기존 연결 요청과 함께 일치 완벽 하 게 됩니다.  
  
-   불일치가 있을 경우 에서만 일부 무효, 연결 시간 제한 등 다시 설정 하는 서버와의 통신을 필요로 하지 않는 합니다.  
  
-   다시 설정 하기 위해 서버와 통신을 요구 하지만 새 연결을 설정 하는 보다 더 나은 성능을 초래 여전히 일부 일치 하지 않는 특성이 없으면 합니다.  
  
-   일치 하지 않는 발생 다시 설정 하는 데 많은 시간이 소요 되는 특성 (드라이버의 개발자 고려할 수 풀 ID를 생성 하는 데 사용 되는 키 특성의 집합으로이 특성을 추가).  
  
 0과 100 사이의 점수는 0으로 다시 사용 하지 않는 가능한 한 완벽 하 게 일치 100으로 설정 합니다. [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) 연결 등급에 대 한 함수입니다.  
  
## <a name="new-odbc-handle---sqlhandledbcinfotoken"></a>새 ODBC 핸들 SQL_HANDLE_DBC_INFO_TOKEN  
 드라이버의 id입니다. 풀 계산 하는 데 필요한 연결 정보 필요를 지원 하기 위해 드라이버 인식 연결 풀링 드라이버는 연결 풀에서 새 연결 요청을 비교 하는 데 필요한 연결 정보도 필요 합니다.  때마다 풀에서 연결을 다시 사용할 수 드라이버는 연결 정보가 필요 하 여 새 연결을 설정 합니다.  
  
 연결 정보 (연결 문자열, 연결 특성 및 DSN) 여러 원본에서 가져올 수 있습니다, 때문 드라이버 연결 문자열을 구문 분석 하 고 이러한 소스는 위의 함수 호출의 각 간의 충돌을 해결 해야 할 수 있습니다.  
  
 새 ODBC 핸들을 도입 따라서: SQL_HANDLE_DBC_INFO_TOKEN 합니다. SQL_HANDLE_DBC_INFO_TOKEN, 연결 문자열을 구문 분석 하 고 두 번 이상 연결 정보에서 충돌을 해결 하는 드라이버 필요 하지 않습니다. 드라이버는 드라이버별 데이터 구조 이므로, 연결 정보 같은 데이터를 저장 하거나 풀 id입니다. 수 있습니다.  
  
 이 핸들 드라이버 관리자와 드라이버 간의 인터페이스로로 사용 됩니다. 응용 프로그램은이 핸들을 직접 할당할 수 없습니다.  
  
 이 핸들의 부모 핸들 형식 의미 하는 드라이버 정보를 얻을 수 환경 HENV 핸들에서 연결 정보를 확인 하는 동안 SQL_HANDLE_ENV입니다.  
  
 새 연결 요청을 받을 때마다 드라이버 관리자 드라이버 인식 연결 풀을 지원 하는지 확인 한 후에 연결 정보를 저장 하기 위한 SQL_HANDLE_DBC_INFO_TOKEN 형식의 핸들을 할당 합니다. 핸들을 사용 하 여 완료 되 면 (하지만 일부 반환에서 SQL_STILL_EXECUTING 이외의 코드가 반환 하기 전에 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 또는 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), 드라이버 관리자 핸들을 해제 합니다. 따라서 핸들 SQLAllocHandle 호출 후 생성 되어 SQLFreeHandle 호출 후에 인스턴스가 삭제 됩니다. 드라이버 관리자 핸들을 해제 하는 연결 된 HENV를 해제 하기 전에 것입니다 보장 (때 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 또는 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 오류가 반환).  
  
 드라이버는 SQL_HANDLE_DBC_INFO_TOKEN 새 핸들 형식을 수락 하는 다음 기능을 수정 해야 합니다.  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 드라이버 관리자는 여러 스레드가 사용 하지 않습니다 동일한 SQL_HANDLE_DBC_INFO_TOKEN 핸들 동시에 보장 합니다. 따라서이 핸들의 동기화 모델 드라이버 내의 매우 간단한 수 있습니다. 드라이버 관리자를 할당 및 SQL_HANDLE_DBC_INFO_TOKEN 해제 하기 전에 환경 잠금을 미치지 않습니다.  
  
 드라이버 관리자 **SQLAllocHandle** 및 **SQLFreeHandle** 이 새 핸들 형식을 허용 하지 것입니다.  
  
 SQL_HANDLE_DBC_INFO_TOKEN 자격 증명과 같은 기밀 정보를 포함할 수 있습니다. 따라서 드라이버를 안전 하 게 지워야 메모리 버퍼 (사용 하 여 [SecureZeroMemory](http://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx))이이 핸들을 해제 하기 전에 중요 한 정보가 들어 있는 **SQLFreeHandle**합니다. 응용 프로그램의 환경 핸들이 닫힐 때마다 모든 관련된 연결 풀을 닫습니다.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>드라이버 관리자 연결 풀 알고리즘 등급  
 이 섹션에서는 드라이버 관리자 연결 풀링에 대해 등급 알고리즘에 설명 합니다. 드라이버 개발자는 이전 버전과 호환성을 위해 동일한 알고리즘을 구현할 수 있습니다. 이 알고리즘에 가장 적합 한 아닐 수 있습니다. 이 구체화 해야 알고리즘 기반 구현 (그렇지 않은 경우이 기능을 구현할 필요가 없습니다).  
  
 드라이버 관리자는 풀에서 각 연결에 대해 100를 0에서 정수 계열 등급을 반환 합니다. 0 연결을 다시 사용할 수 없는 문서를 나타내고 100 완벽 한 일치를 의미 합니다. 연결 요청은 hRequest, 기존 연결 풀에서이 이름 hCandidate로 가정 합니다. 다음 조건 중 하나가 false 이면 풀링된 연결 hCandidate hRequest (드라이버 관리자 0 등급을 할당 합니다)에 대 한 다시 사용할 수 없습니다.  
  
-   hCandidate 및 hRequest 유니코드 API (예:: SQLDriverConnectW) 또는 ANSI API (예:: SQLDriverConnectA)에서 제공 됩니다. (유니코드 드라이버 수는 다른 동작 (SQL_ATTR_ANSI_APP 연결 특성 참조) ANSI API 및 유니코드 API를 제공 합니다.)  
  
-   hCandidate 및 hRequest; 동일한 함수에 의해 생성 됩니다. SQLDriverConnect 또는 SQLConnect 합니다.  
  
-   SQLDriverConnect를 사용할 때 hCandidate를 여는 데 사용 하는 연결 문자열, hRequest 동일 해야 합니다.  
  
-   서버 이름 (또는 DSN), 사용자 이름 및 hCandidate를 여는 데 사용 되는 암호 동일 SQLConnect를 사용할 때 hRequest를 여는 데 사용 해야 합니다.  
  
-   SID hCandidate를 여는 데 사용 하는 대로 현재 스레드의 보안 식별자 (SID) 동일 해야 합니다.  
  
-   등록 및 등록을 취소 하는 비용이 많이 듭니다 드라이버에 대 한 (에서 SQL_DTC_TRANSITION_COST의 설명을 참조 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)) 재사용 하는 방식, *hRequest* 추가 인 리스트 먼 트 또는 unenlistment 요구 하지 않아야 합니다.  
  
 다음 표에서 다양 한 시나리오에 대 한 점수 할당을 보여 줍니다.  
  
|풀링된 연결 및 요청 간에 연결 특성에 대해 비교|참여가 / unenlistment|추가 참여할 필요 / Unenlistment|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|카탈로그 (SQL_ATTR_CURRENT_CATALOG) 차이가 있습니다.|60|50|  
|일부 연결 특성 서로 다르지만 카탈로그는 동일|90|70|  
|완벽 하 게 일치 하는 모든 연결 특성|100|80|  
  
## <a name="sequence-diagram"></a>시퀀스 다이어그램  
 이 시퀀스 다이어그램에서는이 항목에서 설명 하는 기본 풀링 메커니즘을 보여 줍니다. 만의 사용법을 보여줍니다 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 있지만 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 사례 것과 비슷합니다.  
  
 ![시퀀스 다이어그램](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>상태 다이어그램  
 이 상태 다이어그램에는 연결 정보 토큰 개체를이 항목에 설명 된 보여 줍니다. 다이어그램 표시 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 있지만 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 사례 것과 비슷합니다. 드라이버 관리자를 호출할 수 있으므로 드라이버 관리자는 언제 든 지 오류를 처리 해야 할 수, [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) 상태입니다.  
  
 ![상태 다이어그램](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>관련 항목:  
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC SPI(Service Provider Interface) 참조](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
