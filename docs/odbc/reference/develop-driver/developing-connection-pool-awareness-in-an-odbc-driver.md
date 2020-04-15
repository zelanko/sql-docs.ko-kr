---
title: ODBC 드라이버에서 연결 풀 인식 개발 | 마이크로 소프트 문서
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
ms.openlocfilehash: f77fea1d8439ac9ce7374b7dd47db5665686cfbc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283433"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>ODBC 드라이버에서 연결 풀 인식 개발
이 항목에서는 드라이버가 연결 풀링 서비스를 제공하는 방법에 대한 정보가 포함된 ODBC 드라이버 개발에 대한 세부 정보를 설명합니다.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>드라이버 인식 연결 풀링 사용  
 드라이버는 다음과 같은 SPI(ODBC 서비스 공급자 인터페이스) 함수를 구현해야 합니다.  
  
-   SQLSet커넥트트트르포트bcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSet드라이버연결정보  
  
-   SQLGetPoolID  
  
-   SQLRate 연결  
  
-   SQL풀커넥트  
  
-   SQL클린업커넥션풀ID  
  
 자세한 내용은 [ODBC 서비스 공급자 인터페이스(SPI) 참조를](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) 참조하십시오.  
  
 또한 드라이버는 드라이버 인식 풀링을 사용하도록 설정할 수 있도록 다음과 같은 기존 함수를 구현해야 합니다.  
  
|함수|추가된 기능|  
|--------------|-------------------------|  
|[SQLAlloc핸들](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|새 핸들 유형 지원: SQL_HANDLE_DBC_INFO_TOKEN(아래 설명 참조).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|새 설정 전용 연결 특성 지원: 연결을 재설정하기 위한 SQL_ATTR_DBC_INFO_TOKEN(아래 설명 참조).|  
  
> [!NOTE]  
>  **SQLError** 및 **SQLSetConnectOption과** 같은 더 이상 사용되지 않는 함수는 드라이버 인식 연결 풀링에 대해 지원되지 않습니다.  
  
## <a name="the-pool-id"></a>풀 ID  
 풀 ID는 상호 교환적으로 사용할 수 있는 특정 연결 그룹을 나타내는 포인터 길이 드라이버별 ID입니다. 연결 정보 집합이 주어지면 드라이버는 해당 풀 ID를 신속하게 추론할 수 있어야 합니다.  
  
 예를 들어 풀 ID는 서버 이름과 자격 증명 정보를 인코딩해야 합니다. 그러나 드라이버가 연결을 다시 사용한 다음 새 연결을 만드는 것보다 더 적은 시간에 데이터베이스를 변경할 수 있으므로 데이터베이스 이름이 필요하지 않습니다.  
  
 드라이버는 풀 ID를 구성하는 키 특성 집합을 정의해야 합니다. 이러한 키 특성의 값은 연결 특성, 연결 문자열 및 DSN에서 올 수 있습니다. 이러한 원본에 충돌이 있는 경우 이전 버전과의 호환성을 위해 기존 드라이버 별 해결 정책을 사용해야 합니다.  
  
 드라이버 관리자는 다른 풀 아이디에 대해 다른 풀을 사용합니다. 동일한 풀의 모든 연결을 다시 사용할 수 있습니다. 드라이버 관리자는 다른 풀 ID로 연결을 다시 사용하지 않습니다.  
  
 따라서 드라이버는 정의된 키 특성에 동일한 값을 가진 모든 연결 그룹에 대해 고유한 풀 ID를 할당해야 합니다. 드라이버가 키 속성에서 서로 다른 값을 가진 두 연결에 대해 동일한 풀 ID를 사용하는 경우에도 드라이버 관리자는 여전히 동일한 풀에 넣습니다(드라이버 관리자는 드라이버 관련 키 특성에 대해 전혀 알지 못합니다). 즉, 드라이버는 다른 키 특성 집합과의 연결이 [SQLRateConnection 기능](../../../odbc/reference/syntax/sqlrateconnection-function.md)내에서 재사용할 수 없다는 것을 드라이버 관리자에게 보고해야 합니다. 이렇게 하면 성능이 저하될 수 있으며 권장되지 않습니다.  
  
 드라이버 관리자는 모든 연결 정보가 일치하는 경우에도 다른 드라이버 환경에서 할당된 연결을 다시 사용하지 않습니다. 드라이버 관리자는 연결이 동일한 풀 ID를 사용하는 경우에도 서로 다른 환경에 대해 다른 풀을 사용합니다. 따라서 풀 ID는 드라이버 환경에 로컬입니다.  
  
 드라이버에서 풀 ID를 가져오는 함수는 [SQLGetPoolID 함수입니다.](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
## <a name="the-connection-rating"></a>연결 등급  
 새 연결을 설정하는 것과 비교하여 풀린 연결에서 데이터베이스와 같은 일부 연결 정보를 재설정하여 성능을 향상시킬 수 있습니다. 따라서 데이터베이스 이름이 키 특성 집합에 포함되지 않도록 할 수 있습니다. 그렇지 않으면 고객이 다양한 연결 문자열을 사용하는 중간 계층 응용 프로그램에서는 좋지 않을 수 있는 각 데이터베이스에 대해 별도의 풀을 가질 수 있습니다.  
  
 일부 특성 불일치가 있는 연결을 다시 사용할 때마다 반환된 연결이 응용 프로그램 요청과 동일하도록 새 응용 프로그램 요청에 따라 일치하지 않는 특성을 재설정해야 [합니다(SQLSetConnectAttr Function에서](https://go.microsoft.com/fwlink/?LinkId=59368)SQL_ATTR_DBC_INFO_TOKEN 특성에 대한 설명 참조). 그러나 이러한 특성을 재설정하면 성능이 저하될 수 있습니다. 예를 들어 데이터베이스를 재설정하려면 서버에 대한 네트워크 호출이 필요합니다. 따라서 사용 가능한 경우 완벽하게 일치하는 연결을 다시 사용합니다.  
  
 드라이버의 등급 함수는 새 연결 요청으로 기존 연결을 평가할 수 있습니다. 예를 들어 드라이버의 등급 함수는 다음을 결정할 수 있습니다.  
  
-   기존 연결이 요청과 완벽하게 일치하는 경우.  
  
-   재설정하기 위해 서버와의 통신이 필요하지 않은 연결 시간 지정과 같은 사소한 불일치만 있는 경우  
  
-   재설정하기 위해 서버와의 통신이 필요하지만 새 연결을 설정하는 것보다 성능이 향상되는 일부 불일치 특성이 있는 경우  
  
-   재설정하는 데 매우 많은 시간이 소요되는 특성에 대해 일치하지 않는 특성이 발생한 경우(드라이버 개발자는 풀 ID를 생성하는 데 사용되는 키 특성 집합에 이 특성을 추가하는 것을 고려할 수 있음).  
  
 0과 100 사이의 점수가 가능하며, 여기서 0은 재사용하지 않음을 의미하고 100은 완벽하게 일치하는 것을 의미합니다. [SQLRateConnection은](../../../odbc/reference/syntax/sqlrateconnection-function.md) 연결을 평가하는 기능입니다.  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>새로운 ODBC 핸들 - SQL_HANDLE_DBC_INFO_TOKEN  
 드라이버 인식 연결 풀링을 지원하려면 드라이버에 연결 정보가 필요하여 풀 ID를 계산합니다. 또한 드라이버는 새 연결 요청을 풀의 연결과 비교하기 위해 연결 정보가 필요합니다.  풀에서 연결을 다시 사용할 수 없을 때마다 드라이버는 새 연결을 설정해야 하므로 연결 정보가 필요합니다.  
  
 연결 정보는 여러 소스(연결 문자열, 연결 특성 및 DSN)에서 올 수 있기 때문에 드라이버는 연결 문자열을 구문 분석하고 위의 각 함수 호출에서 이러한 소스 간의 충돌을 해결해야 할 수 있습니다.  
  
 따라서 새로운 ODBC 핸들이 도입됩니다: SQL_HANDLE_DBC_INFO_TOKEN. SQL_HANDLE_DBC_INFO_TOKEN 경우 드라이버는 연결 문자열을 구문 분석하고 연결 정보의 충돌을 두 번 이상 해결할 필요가 없습니다. 드라이버 관련 데이터 구조이므로 드라이버는 연결 정보 또는 풀 ID와 같은 데이터를 저장할 수 있습니다.  
  
 이 핸들은 드라이버 관리자와 드라이버 간의 인터페이스로만 사용됩니다. 응용 프로그램에서 이 핸들을 직접 할당할 수 없습니다.  
  
 이 핸들의 상위 핸들은 SQL_HANDLE_ENV 유형이므로 드라이버가 연결 정보 확인 중에 HENV 핸들에서 환경 정보를 가져올 수 있습니다.  
  
 새 연결 요청을 받을 때마다 드라이버 관리자는 드라이버가 연결 풀 인식을 지원하는지 확인한 후 연결 정보를 저장하기 위한 SQL_HANDLE_DBC_INFO_TOKEN 형식 핸들을 할당합니다. 핸들 사용이 [끝나면(그러나 SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 또는 [SQLConnect에서](../../../odbc/reference/syntax/sqlconnect-function.md)SQL_STILL_EXECUTING 이외의 일부 반환 코드를 반환하기 전에) 드라이버 관리자는 핸들을 해제합니다. 따라서 핸들은 SQLAllocHandle 호출 후 만들어지고 SQLFreeHandle 호출 후에 소멸됩니다. 드라이버 관리자는 연결된 HENV를 해제하기 전에 핸들을 해제할 수 [있습니다(SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 또는 [SQLConnect에서](../../../odbc/reference/syntax/sqlconnect-function.md) 오류를 반환하는 경우).  
  
 드라이버는 다음 함수를 수정하여 새 핸들 유형 SQL_HANDLE_DBC_INFO_TOKEN 수락해야 합니다.  
  
1.  [SQLAlloc핸들](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 드라이버 관리자는 여러 스레드가 동일한 SQL_HANDLE_DBC_INFO_TOKEN 핸들을 동시에 사용하지 않도록 합니다. 따라서 이 핸들의 동기화 모델은 드라이버 내부에서 매우 간단할 수 있습니다. 드라이버 관리자는 SQL_HANDLE_DBC_INFO_TOKEN 할당하고 해제하기 전에 환경 잠금을 사용하지 않습니다.  
  
 드라이버 관리자의 **SQLAllocHandle** 및 **SQLFreeHandle이** 새 핸들 형식을 허용 하지 않습니다.  
  
 SQL_HANDLE_DBC_INFO_TOKEN 자격 증명과 같은 기밀 정보가 포함될 수 있습니다. 따라서 드라이버는 **SQLFreeHandle**을 사용하여 이 핸들을 릴리스하기 전에 중요한 정보가 포함된 [메모리 버퍼(SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)사용)를 안전하게 지워야 합니다. 응용 프로그램의 환경 핸들이 닫히면 연결된 모든 연결 풀이 닫힙집니다.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>드라이버 관리자 연결 풀 등급 알고리즘  
 이 섹션에서는 드라이버 관리자 연결 풀링에 대한 등급 알고리즘에 대해 설명합니다. 드라이버 개발자는 이전 버전과의 호환성을 위해 동일한 알고리즘을 구현할 수 있습니다. 이 알고리즘이 가장 좋은 알고리즘이 아닐 수 있습니다. 구현을 기반으로 이 알고리즘을 구체화해야 합니다(그렇지 않으면 이 기능을 구현할 이유가 없음).  
  
 드라이버 관리자는 풀에서 각 연결에 대해 0에서 100까지정격을 반환합니다. 0은 연결을 다시 사용할 수 없음을 의미하고 100은 일치하는 완벽을 나타냅니다. 연결 요청이 hRequest라고 명명되고 풀의 기존 연결이 hCandidate로 명명된다고 가정합니다. 다음 조건 중 하나라도 false이면 풀려진 연결 hCandidate를 hRequest에 다시 사용할 수 없습니다(드라이버 관리자는 0의 등급을 할당합니다).  
  
-   hCandidate 및 hRequest는 모두 유니코드 API(예: SQLDriverConnectW) 또는 ANSI API(예: SQLDriverConnectA)에서 가져옵니다. (유니코드 드라이버는 ANSI API 및 유니코드 API를 통해 다른 동작을 할 수 SQL_ATTR_ANSI_APP.)  
  
-   hCandidate 및 hRequest는 동일한 함수에 의해 생성됩니다. SQLDriverConnect 또는 SQLConnect 중 하나를 클릭합니다.  
  
-   hCandidate를 여는 데 사용되는 연결 문자열은 SQLDriverConnect를 사용할 때 hRequest와 같아야 합니다.  
  
-   서버 이름 (또는 DSN), 사용자 이름 및 hCandidate를 여는 데 사용 되는 암호는 SQLConnect를 사용 하는 경우 hRequest를 여는 데 사용 동일 해야 합니다.  
  
-   현재 스레드의 SID(보안 식별자)는 hCandidate를 여는 데 사용되는 SID와 같아야 합니다.  
  
-   등록 및 등록 취소 비용이 많이 드는 드라이버의 [경우(SQLConnect에서](../../../odbc/reference/syntax/sqlconnect-function.md)SQL_DTC_TRANSITION_COST 대한 설명 참조) *hRequest를* 다시 사용하면 추가 인리스트또는 인리스트먼트가 필요하지 않습니다.  
  
 다음 표에는 다양한 시나리오에 대한 점수 할당이 표시됩니다.  
  
|풀된 연결과 요청 간의 연결 특성 비교|입대 없음 / 입대 취소|추가 입대 필요 / 입대 취소|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|카탈로그(SQL_ATTR_CURRENT_CATALOG)가 다릅니다.|60|50|  
|일부 연결 특성은 다르지만 카탈로그는 동일합니다.|90|70|  
|모든 연결 속성이 완벽하게 일치|100|80|  
  
## <a name="sequence-diagram"></a>시퀀스 다이어그램  
 이 시퀀스 다이어그램은 이 항목에 설명된 기본 풀링 메커니즘을 보여 주며 있습니다. [SQLDriverConnect의](../../../odbc/reference/syntax/sqldriverconnect-function.md) 사용만 보여 주지만 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 케이스는 비슷합니다.  
  
 ![시퀀스 다이어그램](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>상태 다이어그램  
 이 상태 다이어그램은 이 항목에 설명된 연결 정보 토큰 개체를 보여 주며 있습니다. 다이어그램은 [SQLDriverConnect만](../../../odbc/reference/syntax/sqldriverconnect-function.md) 표시하지만 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 사례는 비슷합니다. 드라이버 관리자는 언제든지 오류를 처리해야 할 수 있기 때문에 드라이버 관리자는 모든 상태에 대해 [SQLFreeHandle을](../../../odbc/reference/syntax/sqlfreehandle-function.md) 호출할 수 있습니다.  
  
 ![상태 다이어그램](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>참고 항목  
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC SPI(서비스 공급자 인터페이스) 참조](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)
