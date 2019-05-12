---
title: SQLRateConnection 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9614ea6bb3de3475f651fe900589b6fa5a9c0f4b
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537320"
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 함수
**규칙**  
 도입 된 버전: ODBC 3.81 표준 준수 합니다. ODBC  
  
 **요약**  
 **SQLRateConnection** 드라이버 연결 풀에서 기존 연결을 다시 사용할 수 하는 경우를 결정 합니다.  
  
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
 *hRequest*  
 [입력] 새 응용 프로그램 연결 요청을 나타내는 토큰 핸들입니다.  
  
 *hCandidateConnection*  
 [입력] 연결 풀에서 기존 연결입니다. 연결을 열린된 상태 여야 합니다.  
  
 *fRequiredTransactionEnlistment*  
 [입력] TRUE 이면 기존 연결의 재사용 *hCandidateConnection* 새 연결 요청에 대 한 (*hRequest*)는 추가 인 리스트 먼 트 해야 합니다.  
  
 *transId*  
 [입력] 하는 경우 *fRequiredTransactionEnlistment* 가 TRUE 인 *transId* 요청은 등록 된 DTC 트랜잭션을 나타냅니다. 하는 경우 *fRequiredTransactionEnlistment* 은 FALSE *transId* 무시 됩니다.  
  
 *pRating*  
 [출력] *hCandidateConnection*에 대 한 등급의 재사용을 *hRequest*합니다. 이 등급은 0에서 100 (포함) 사이 여야 합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 드라이버 관리자는이 함수에서 반환 된 진단 정보를 처리 하지 않습니다.  
  
## <a name="remarks"></a>Remarks  
 **SQLRateConnection** 0부터 100 사이 (포함)는 기존 연결 요청과 일치 하는 정도 나타내는 점수를 생성 합니다.  
  
|점수|의미 (SQL_SUCCESS가 반환 됨) 하는 경우|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* 에 다시 사용 해야 합니다 *hRequest*합니다.|  
|1 ~ 98 (포함) 사이의 모든 값|점수가 높을수록, 가까울수록 서로입니다 *hCandidateConnection* 일치 *hRequest*합니다.|  
|99|불필요 한 특성에만 불일치가 있습니다.  드라이버 관리자 등급 루프를 중지 해야 합니다.|  
|100|완벽 한 일치 항목입니다.  드라이버 관리자 등급 루프를 중지 해야 합니다.|  
|100 보다 큰 다른 값|*hCandidateConnection* 배달 못 한 편지 하며는 재사용 되지 이후 연결 요청에도 하는 것으로 표시 됩니다.|  
  
 드라이버 관리자는 반환 코드는 SQL_SUCCESS_WITH_INFO 등 SQL_SUCCESS 이외의 등급이 100 보다 큰 경우 배달 못 한 편지로 연결을 표시 합니다. 비활성 연결 (향후 연결 요청 수)에 다시 사용 되지 않습니다 및 결국 초과 되 CPTimeout 지난 후 합니다. 드라이버 관리자는 속도를 풀에서 다른 연결을 찾을 계속 합니다.  
  
 드라이버 관리자는 해당 점수는 엄격 하 게 99 등 100 미만의 연결을 다시 사용 하는 경우 드라이버 관리자는 응용 프로그램이 요청한 상태로 다시 연결을 다시 설정 SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN)를 호출 합니다. 드라이버에서이 함수 호출에서 연결을 다시 설정 해야 합니다.  
  
 하는 경우 *fRequiredTransactionEnlistment* 는 TRUE이 고, 재사용 *hCandidateConnection* 는 추가 인 리스트 먼 트 해야 (*transId* ! = NULL) 또는 unenlistment ( *transId* = = NULL). 이 드라이버를 등록 / 연결을 다시 사용 하려는 경우 연결을 등록 취소 해야 하는지 여부 및 연결을 다시 사용 비용을 나타냅니다. 하는 경우 *fRequireTransactionEnlistment* 은 FALSE 드라이버의 값을 무시 해야 *transId*합니다.  
  
 드라이버 관리자 부모 HENV 처리 보장 *hRequest* 하 고 *hCandidateConnection* 동일 합니다. 드라이버 관리자 연결 된 풀 ID를 보장 *hRequest* 하 고 *hCandidateConnection* 동일 합니다.  
  
 응용 프로그램에서이 함수를 직접 호출 하지 않습니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발을 위한 sqlspi.h 포함 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
