---
title: "SQLRateConnection 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e63a6312a6f4b637d13282e25311204ea3879fd5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 함수
**규칙**  
 도입 된 버전: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLRateConnection** 경우 드라이버를 다시 사용할 수는 연결 풀에서 기존 연결을 결정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>인수  
 *hRequest*  
 [입력] 새 응용 프로그램 연결 요청을 나타내는 토큰 핸들입니다.  
  
 *hCandidateConnection*  
 [입력] 연결 풀에서 기존 연결입니다. 연결이 열려 있는 상태에 있어야 합니다.  
  
 *fRequiredTransactionEnlistment*  
 [입력] True 인 경우, 기존 연결의 재사용 *hCandidateConnection* 새 연결 요청에 대 한 (*hRequest*) 추가 참여가 필요 합니다.  
  
 *transId*  
 [입력] 경우 *fRequiredTransactionEnlistment* 가 TRUE 이면 *transId* 요청 참여는 DTC 트랜잭션을 나타냅니다. 경우 *fRequiredTransactionEnlistment* 가 FALSE 이면 *transId* 무시 됩니다.  
  
 *pRating*  
 [출력] *hCandidateConnection*의 대 한 등급 재사용은 *hRequest*합니다. 이 등급은 0에서 100 (포함) 사이의 됩니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 드라이버 관리자는이 함수에서 반환 되는 진단 정보를 처리 하지 않습니다.  
  
## <a name="remarks"></a>주의  
 **SQLRateConnection** 0에서 기존 연결 요청과 일치 하는 정도 나타내는 100 (포함) 사이의 점수를 생성 합니다.  
  
|점수|의미 (SQL_SUCCESS가 반환) 하는 경우|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* 에 다시 사용 해야 합니다는 *hRequest*합니다.|  
|1과 98 (포함) 사이의 모든 값|점수가 높을수록는 좀 더 가까이 있는 *hCandidateConnection* 와 일치 *hRequest*합니다.|  
|99|유효 하지 않은 특성에만 불일치가 있습니다.  드라이버 관리자 등급 루프를 중지 해야 합니다.|  
|100|완벽 한 일치 항목입니다.  드라이버 관리자 등급 루프를 중지 해야 합니다.|  
|100 보다 큰 다른 값|*hCandidateConnection* 배달 되며는 다시 사용 하지 이후 연결 요청에도 표시 됩니다.|  
  
 드라이버 관리자는 반환 코드는 (SQL_SUCCESS_WITH_INFO) SQL_SUCCESS 이외의 또는 등급이 100 보다 큰 경우 배달으로 연결을 표시 합니다. 끊긴 연결 (이후 연결 요청 수)에 다시 사용 되지 않습니다을 결국 초과 되 CPTimeout 통과 합니다. 드라이버 관리자는 풀에서 다른 연결 속도을 찾으려고 계속 됩니다.  
  
 드라이버 관리자 점수가 (99 포함)는 100 보다 엄격 하 게 작으면 연결 다시 사용, 드라이버 관리자는 응용 프로그램에서 요청한 상태에 다시 연결을 다시 설정할 SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN)를 호출 합니다. 드라이버에서이 함수 호출에서 연결을 다시 설정 해야 합니다.  
  
 경우 *fRequiredTransactionEnlistment* TRUE이 고, 다시 사용은 *hCandidateConnection* 추가 참여가 필요 (*transId* ! = NULL) 또는 unenlistment (* transId* NULL = =) 합니다. 이 드라이버 참여 / 연결 다시 사용 하려는 경우 연결의 등록을 취소 해야 하는지 여부 및 연결을 다시 사용의 비용을 나타냅니다. 경우 *fRequireTransactionEnlistment* 가 FALSE 이면 드라이버의 값을 무시 해야 *transId*합니다.  
  
 드라이버 관리자의 처리 HENV 부모 보장 *hRequest* 및 *hCandidateConnection* 동일 합니다. 드라이버 관리자 연결 된 풀 ID를 보장 *hRequest* 및 *hCandidateConnection* 동일 합니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지원 되는 ODBC 드라이버가이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발에 대 한 sqlspi.h를 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 드라이버를 개발합니다.](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)

