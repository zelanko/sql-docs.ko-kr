---
title: SQLRate연결 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d29033460a7f89fc4a8b1c371a4d32bdf94a2a05
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288883"
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 함수
**규칙**  
 버전 출시: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLRateConnection** 드라이버 연결 풀에서 기존 연결을 다시 사용할 수 있는지 여부를 결정 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp
  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>인수  
 *h요청*  
 [입력] 새 응용 프로그램 연결 요청을 나타내는 토큰 핸들입니다.  
  
 *h후보 연결*  
 [입력] 연결 풀의 기존 연결입니다. 연결이 열린 상태여야 합니다.  
  
 *fRequired트랜잭션인서리스트먼트*  
 [입력] TRUE인 경우 새 연결*요청(hRequest)에*대해 기존 연결의 *hCandidateConnection를* 다시 사용하려면 추가 인리스트먼트가 필요합니다.  
  
 *트랜스 Id*  
 [입력] *fRequiredTransaction 인리스트먼트가* TRUE인 경우 *transId는* 요청이 참여하게 될 DTC 트랜잭션을 나타냅니다. *fRequiredTransaction 인리스트먼트가* FALSE이면 *transId는* 무시됩니다.  
  
 *pRating*  
 [출력] *hCandidateConnection* *'의 재사용 등급에*대한 요청 . 이 등급은 0에서 100(포함) 사이입니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 드라이버 관리자는 이 기능에서 반환된 진단 정보를 처리하지 않습니다.  
  
## <a name="remarks"></a>설명  
 **SQLRateConnection은** 기존 연결이 요청과 얼마나 잘 일치하는지를 나타내는 0에서 100(포함) 사이의 점수를 생성합니다.  
  
|점수|의미(SQL_SUCCESS 반환되는 경우)|  
|-----------|-----------------------------------------------|  
|0|*hCandidate연결은* *hRequest에*재사용해서는 안 됩니다.|  
|1에서 98 사이의 모든 값(포함)|점수가 높을수록 *hCandidateConnection가* *hRequest와*일치합니다.|  
|99|중요하지 않은 특성에는 불일치만 있습니다.  드라이버 관리자는 등급 루프를 중지해야 합니다.|  
|100|완벽한 일치.  드라이버 관리자는 등급 루프를 중지해야 합니다.|  
|100보다 큰 기타 값|*hCandidateConnection는* 죽은 것으로 표시되며 향후 연결 요청에서도 다시 사용되지 않습니다.|  
  
 반환 코드가 SQL_SUCCESS(SQL_SUCCESS_WITH_INFO 포함) 또는 등급이 100보다 큰 경우 드라이버 관리자는 연결을 죽은 것으로 표시합니다. 해당 연결은 나중에 연결 요청에서도 다시 사용되지 않으며 CPTimeout이 지나가면 결국 시간 만료됩니다. 드라이버 관리자는 풀에서 요금에 대한 다른 연결을 계속 찾습니다.  
  
 드라이버 관리자가 점수가 100(99 포함)보다 엄격하게 작은 연결을 재사용한 경우 드라이버 관리자는 SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN)를 호출하여 응용 프로그램에서 요청한 상태로 연결을 다시 설정합니다. 드라이버가 이 함수 호출에서 연결을 재설정해서는 안 됩니다.  
  
 *fRequiredTransaction 인리스트먼트가* TRUE인 경우 *hCandidateConnection를* 다시 사용하려면 추가 인리스트먼트(transId != NULL) 또는 인리스트먼트(transId == NULL)가 필요합니다.*transId* *transId* 이는 연결을 다시 사용하는 비용과 연결을 다시 사용할 경우 드라이버가 연결을 등록/등록 해제해야 하는지 여부를 나타냅니다. *fRequireTransaction인가* FALSE인 경우 드라이버는 *transId*의 값을 무시해야 합니다.  
  
 드라이버 관리자는 *hRequest* 및 *hCandidateConnection의* 상위 HENV 핸들이 동일하다는 것을 보장합니다. 드라이버 관리자는 *hRequest* 및 *hCandidateConnection와* 연결된 풀 ID가 동일하다는 것을 보장합니다.  
  
 응용 프로그램은 이 함수를 직접 호출해서는 안 됩니다. 드라이버 인식 연결 풀링을 지원하는 ODBC 드라이버는 이 기능을 구현해야 합니다.  
  
 ODBC 드라이버 개발을 위해 sqlspi.h를 포함합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
