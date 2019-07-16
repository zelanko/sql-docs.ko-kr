---
title: ODBC 드라이버에서 연결 풀 인식 개발 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02577370218a799faf86a7f8986859c415962f5a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897740"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>ODBC 드라이버에서 연결 풀 인식 개발
이 항목에서는 드라이버 연결 풀링 서비스를 제공 해야 하는 방법에 대 한 정보를 포함 하는 ODBC 드라이버를 개발 하는 세부 정보를 설명 합니다.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링을 사용 하도록 설정  
 드라이버가 다음 ODBC 서비스 공급자 인터페이스 SPI () 함수를 구현 해야 합니다.  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 참조 [ODBC 서비스 공급자 인터페이스 (SPI) 참조](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) 자세한 내용은 합니다.  
  
 또한 드라이버는 드라이버 인식 풀링을 사용할 수 있도록 다음 기존 함수를 구현 해야 합니다.  
  
|함수|추가 기능|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|새 핸들 형식을 지원 합니다. SQL_HANDLE_DBC_INFO_TOKEN (아래 설명 참조).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|새로운 집합 전용 연결 특성을 지원 합니다. 연결 다시 설정 하기 위해 SQL_ATTR_DBC_INFO_TOKEN (아래 설명 참조).|  
  
> [!NOTE]  
>  와 같은 함수를 사용 되지 않음 **SQLError** 하 고 **SQLSetConnectOption** 드라이버 인식 연결 풀링을 지원 되지 않습니다.  
  
## <a name="the-pool-id"></a>풀 ID  
 풀 ID가 서로 교환해 서 사용할 수 있는 연결의 특정 그룹을 나타내는 포인터 길이의 드라이버별 ID입니다. 지정 된 연결 정보 집합을 드라이버 해야 해당 풀 ID를 신속 하 게 추론할 수  
  
 예를 들어, 풀 ID를 서버 이름 및 자격 증명 정보를 인코딩해야 합니다. 그러나 드라이버 연결을 다시 사용 하 고 새 연결을 만드는 것 보다 더 짧은 시간에 데이터베이스를 변경 하는 일을 할 수 있기 때문에 데이터베이스 이름이 필요 하지 않습니다.  
  
 드라이버는 풀 ID를 구성 하는 키 특성의 집합을 정의 해야 이러한 키 특성의 값은 연결 특성, 연결 문자열 및 DSN에서 가져올 수 있습니다. 이러한 원본에서 충돌이 있는 경우 이전 버전과 호환성을 위해 기존에 드라이버별 확인 정책을 사용 해야 합니다.  
  
 드라이버 관리자는 다른 풀 Id에 대 한 다른 풀을 사용 합니다. 동일한 풀의 모든 연결은 다시 사용할 수 있습니다. 드라이버 관리자는 다른 풀 ID 사용 하 여 연결을 다시 사용 되지 않습니다.  
  
 따라서 드라이버는 정의 된 키 특성에 동일한 값을 사용 하 여 연결의 모든 그룹에 대 한 고유 풀 ID를 할당 해야 합니다. 해당 키 특성의 값이 서로 다른 두 개의 연결에 대 한 동일한 풀 ID를 사용 하는 드라이버를 드라이버 관리자는 여전히 넣습니다 (드라이버 관리자 드라이버별 키 특성에 대 한 아무런) 동일한 풀에. 즉, 드라이버를 드라이버 관리자 내에서 다시 사용할 수 없는 다양 한 키 특성을 사용 하 여 연결을 보고 해야 합니다 [SQLRateConnection 함수](../../../odbc/reference/syntax/sqlrateconnection-function.md)합니다. 성능 저하 될 수 및이 권장 되지 않습니다.  
  
 드라이버 관리자 모든 연결 정보가 일치 하는 경우에 다른 드라이버 환경에서 할당 한 연결 다시 사용 하지 않습니다. 드라이버 관리자를 사용 하 여 다른 풀 다른 환경에 대 한 연결 풀 ID가 같을 경우에 따라서 풀 ID는 해당 드라이버 환경에 로컬입니다.  
  
 드라이버에서 풀 ID를 가져오기 위한 함수가 [SQLGetPoolID 함수](../../../odbc/reference/syntax/sqlgetpoolid-function.md)합니다.  
  
## <a name="the-connection-rating"></a>연결 평가  
 새 연결에 비해, 풀링된 연결의 일부 연결 정보 (예: 데이터베이스)를 다시 설정 하 여 더 나은 성능을 얻을 수 있습니다. 따라서 하지 못하게 하려는 데이터베이스 이름 키 특성 집합의 수입니다. 그렇지 않은 경우 고객은 다양 한 다른 연결 문자열을 사용 하는 위치 하지 않을 수 있는 중간 계층 응용 프로그램에 적합 한, 각 데이터베이스에 대해 별도 풀을 할 수 있습니다.  
  
 반환 된 연결이 동일한 응용 프로그램 요청에 있도록 새 응용 프로그램 요청에 따라 일치 하지 않는 특성을 다시 설정 해야의 일부 특성이 일치 하지 않습니다 하는 연결을 다시 사용할 때마다 (SQL_ATTR 특성의 설명을 참조 하세요. _DBC_INFO_TOKEN [SQLSetConnectAttr 함수](https://go.microsoft.com/fwlink/?LinkId=59368)). 그러나 이러한 특성을 다시 설정 하면 성능이 떨어질 수 있습니다. 예를 들어, 데이터베이스를 다시 설정 하면 서버는 네트워크 호출을 해야 합니다. 따라서 가능한 경우 완벽 하 게 일치 하는 연결을 다시 사용 합니다.  
  
 드라이버의 등급 함수는 새 연결 요청을 사용 하 여 기존 연결을 평가할 수 있습니다. 예를 들어 드라이버의 등급 함수 확인할 수 있습니다.  
  
-   경우 기존 연결 요청과 일치 완벽 하 게 됩니다.  
  
-   불일치가 있을 경우만 일부 불필요 한, 같은 연결 시간 제한 다시 설정 하려면 서버와의 통신을 요구 하지 않는 합니다.  
  
-   다시 설정 하려면 서버와 통신을 필요로 하지만 여전히 인해 새 연결을 설정 하는 보다 더 나은 성능을 일부 일치 하지 않는 특성이 없으면입니다.  
  
-   경우는 일치 하지 않는 발생 했습니다. 다시 설정 하는 데 많은 시간이 소요 되는 특성 (드라이버의 개발자에 게 좋습니다 풀 ID를 생성 하는 데 사용 되는 키 특성의 집합에이 특성을 추가).  
  
 0과 100 사이의 점수는 0으로 다시 사용 하지 마십시오 가능한 한 완벽 하 게 일치 하는 100 의미 합니다. [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) 는 연결을 평가 하기 위한 함수입니다.  
  
## <a name="new-odbc-handle---sqlhandledbcinfotoken"></a>새 ODBC 핸들-SQL_HANDLE_DBC_INFO_TOKEN  
 드라이버를 지원 하기 위해 드라이버 인식 연결 풀링 연결 정보를 id입니다. 풀 계산에 필요 드라이버는 연결 정보는 풀에서에서 연결을 사용 하 여 새 연결 요청을 비교할 수 있도록 해야 합니다.  풀에서 연결을 다시 사용할 수 있습니다, 때마다 드라이버는 연결 정보를 필요로 하므로 새 연결을 설정 해야 합니다.  
  
 연결 정보 (연결 문자열, 연결 특성 및 DSN)에 여러 원본에서 가져올 수 있습니다, 되므로 드라이버 연결 문자열을 구문 분석 하 고 이러한 위의 함수 호출의 각이 원본 간의 충돌을 해결 해야 합니다.  
  
 따라서 새 ODBC 핸들을 도입 되었습니다. SQL_HANDLE_DBC_INFO_TOKEN. SQL_HANDLE_DBC_INFO_TOKEN를 사용 하 여 드라이버 않아도 연결 문자열을 구문 분석 하 고 두 번 이상 연결 정보에서 충돌을 해결 합니다. 드라이버가 연결 정보와 같은 데이터를 저장할 수 있습니다 또는 풀 id입니다. 드라이버별 데이터 구조 이므로  
  
 이 핸들은 드라이버 관리자와 드라이버 인터페이스로만 사용 됩니다. 응용 프로그램은이 핸들을 직접 할당할 수 없습니다.  
  
 이 핸들의 상위 핸들 형식 SQL_HANDLE_ENV, 드라이버를 가져올 수 있도록 환경 정보 HENV 핸들에서 연결 정보를 확인 하는 동안 의미입니다.  
  
 새 연결 요청을 받을 때마다 드라이버 관리자 드라이버 지원 연결 풀 인식 하는지 확인 한 후 연결 정보를 저장 하기 위한 SQL_HANDLE_DBC_INFO_TOKEN 형식의 핸들을 할당 됩니다. 핸들을 사용 하 여 완료 되 면 (반환 하기 전에 일부에서 SQL_STILL_EXECUTING 이외의 코드가 반환 되지만 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 하거나 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), 드라이버 관리자는 핸들을 해제 합니다. 따라서 핸들 SQLAllocHandle 호출 후 생성 되어 SQLFreeHandle 호출 후에 삭제 됩니다. 드라이버 관리자 연결 된 해당 HENV를 해제 하기 전에 핸들 해제지 것입니다 보장 (때 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 하거나 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 오류를 반환 합니다).  
  
 드라이버는 새 핸들 형식은 SQL_HANDLE_DBC_INFO_TOKEN를 허용 하도록 다음 함수를 수정 해야 합니다.  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 드라이버 관리자는 여러 스레드를 사용 하지 않도록 동일한 SQL_HANDLE_DBC_INFO_TOKEN 핸들을 동시에 보장 합니다. 따라서이 핸들의 동기화 모델은 매우 간단한 드라이버 내의 수 있습니다. 드라이버 관리자를 할당 하 고 SQL_HANDLE_DBC_INFO_TOKEN 해제 하기 전에 환경 잠금이 적용 되지 않습니다.  
  
 드라이버 관리자의 **SQLAllocHandle** 하 고 **SQLFreeHandle** 이 새 핸들 형식은 허용 하지 것입니다.  
  
 SQL_HANDLE_DBC_INFO_TOKEN 자격 증명과 같은 비밀 정보를 포함할 수 있습니다. 따라서 드라이버를 안전 하 게 지워야 메모리 버퍼 (사용 하 여 [SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)) 사용 하 여이 핸들을 해제 하기 전에 중요 한 정보가 포함 된 **SQLFreeHandle**합니다. 응용 프로그램의 환경 핸들이 닫힐 때마다 모든 연결 풀을 닫습니다.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>드라이버 관리자 연결 풀 알고리즘 등급  
 이 섹션에서는 드라이버 관리자 연결 풀링 등급 알고리즘을 설명 합니다. 드라이버 개발자는 이전 버전과 호환성을 위해 동일한 알고리즘을 구현할 수 있습니다. 이 알고리즘에 가장 적합 한을 사용할 수 없습니다. 이 구체화 해야 알고리즘 기반 구현 (그렇지 않은 경우에이 기능을 구현할 필요가 없습니다).  
  
 드라이버 관리자는 풀에서 각 연결에 대 한 100에 0에서 정수는 등급을 반환 합니다. 0 연결을 다시 사용할 수 없는 문서를 나타내고 100을 완벽 하 게 일치를 의미 합니다. 연결 요청 hRequest 라는 hCandidate로 풀에서 기존 연결 라고 가정 합니다. 다음 조건 중 하나라도 false 인 경우 풀링된 연결이 hCandidate hRequest (드라이버 관리자는 0 등급이 할당 됩니다)에 대 한 다시 사용할 수 없습니다.  
  
-   hCandidate 및 hRequest 유니코드 API (예:: SQLDriverConnectW) 또는 ANSI API (예:: SQLDriverConnectA)에서 제공 됩니다. (유니코드 드라이버 수는 다른 동작 (SQL_ATTR_ANSI_APP 연결 특성을 참조 하세요.) ANSI API 및 유니코드 API를 제공 합니다.)  
  
-   hCandidate 및 hRequest; 동일한 함수 별로 생성 됩니다. SQLDriverConnect 또는 SQLConnect 합니다.  
  
-   SQLDriverConnect를 사용할 때 hCandidate을 여는데 사용 되는 연결 문자열 hRequest,으로 동일 해야 합니다.  
  
-   서버 이름 (또는 DSN), 사용자 이름 및 hCandidate를 여는 데 사용 되는 암호 동일 hRequest SQLConnect를 사용할 때 여는 데 사용 해야 합니다.  
  
-   SID hCandidate를 여는 데 사용 하는 대로 현재 스레드의 보안 식별자 (SID) 동일 해야 합니다.  
  
-   등록 및 등록을 취소 하는 데 비용이 많이 드는 드라이버에 대 한 (SQL_DTC_TRANSITION_COST의 설명을 참조 하십시오 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), 재사용 *hRequest* 추가 인 리스트 먼 트 또는 unenlistment를 요구 하지 않아야 합니다.  
  
 다음 표에서 다양 한 시나리오에 대 한 점수가 할당을 보여 줍니다.  
  
|연결 특성 풀링된 연결 및 요청 사이 비교|없는 인 리스트 먼 트 / unenlistment|추가 인 리스트 먼 트 해야 / Unenlistment|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|카탈로그 (SQL_ATTR_CURRENT_CATALOG) 다릅니다.|60|50|  
|일부 연결 특성은 다른 카탈로그는 동일 하지만|90|70|  
|완벽 하 게 일치 하는 모든 연결 특성|100|80|  
  
## <a name="sequence-diagram"></a>시퀀스 다이어그램  
 이 시퀀스 다이어그램에는이 항목에서 설명한 기본 풀링 메커니즘을 보여 줍니다. 사용 표시 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 되지만 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 사례 비슷합니다.  
  
 ![시퀀스 다이어그램](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>상태 다이어그램  
 이 상태 다이어그램 개체를 보여 줍니다 연결 정보 토큰을이 항목에서 설명 합니다. 다이어그램만 보여 줍니다 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 되지만 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 사례 비슷합니다. 드라이버 관리자는 언제 든 지 오류를 처리 해야 할 수 있으므로, 드라이버 관리자를 호출할 수 있습니다 [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) 상태입니다.  
  
 ![상태 다이어그램](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>관련 항목  
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC SPI(Service Provider Interface) 참조](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
