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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d29033460a7f89fc4a8b1c371a4d32bdf94a2a05
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288883"
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 함수
**규칙**  
 소개 된 버전: ODBC 3.81 표준 준수: ODBC  
  
 **요약**  
 **SQLRateConnection** 는 드라이버가 연결 풀에서 기존 연결을 다시 사용할 수 있는지 확인 합니다.  
  
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
 입력 새 응용 프로그램 연결 요청을 나타내는 토큰 핸들입니다.  
  
 *hCandidateConnection*  
 입력 연결 풀의 기존 연결입니다. 연결이 열린 상태 여야 합니다.  
  
 *fRequiredTransactionEnlistment*  
 입력 TRUE 인 경우 새 연결 요청 (*Hrequest*)에 기존 연결의 *hCandidateConnection* 를 다시 사용 하려면 추가 참여가 필요 합니다.  
  
 */Sid*  
 입력 *Frequiredtransactionenlistment* TRUE 이면 해당 요청에 등록 될 DTC *트랜잭션을 나타냅니다.* *Frequiredtransactionenlistment* FALSE 인 경우에 *는, 및가 무시 됩니다.*  
  
 *pRating*  
 출력 *Hrequest*에 대 한 *hCandidateConnection*의 재사용 등급입니다. 이 등급은 0에서 100 (포함) 사이에 있습니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 드라이버 관리자는이 함수에서 반환 된 진단 정보를 처리 하지 않습니다.  
  
## <a name="remarks"></a>설명  
 **SQLRateConnection** 는 0과 100 (포함) 사이의 점수를 생성 하 여 기존 연결이 요청과 얼마나 잘 일치 하는지를 나타냅니다.  
  
|점수 매기기|의미 (SQL_SUCCESS가 반환 되는 경우)|  
|-----------|-----------------------------------------------|  
|0|*Hrequest*에 *hCandidateConnection* 를 다시 사용 하지 않아야 합니다.|  
|1에서 98 사이의 값 (포함)|점수가 높을수록 *hCandidateConnection* 가 *hrequest*와 일치 하는 것 보다 더 가깝습니다.|  
|99|중요 하지 않은 특성에는 불일치가 있습니다.  드라이버 관리자는 등급 루프를 중지 해야 합니다.|  
|100|완벽 한 일치.  드라이버 관리자는 등급 루프를 중지 해야 합니다.|  
|100 보다 큰 다른 값|*hCandidateConnection* 는 배달 되지 않은 것으로 표시 되며 이후 연결 요청 에서도 다시 사용 되지 않습니다.|  
  
 반환 코드가 SQL_SUCCESS (SQL_SUCCESS_WITH_INFO 포함) 이외의 값 이거나 등급이 100 보다 큰 경우 드라이버 관리자는 연결을 비활성으로 표시 합니다. 이후 연결 요청 에서도 중단 된 연결이 다시 사용 되지 않으며, CPTimeout이 전달 된 후에 결국 시간이 초과 됩니다. 드라이버 관리자는 풀에서 요금으로의 다른 연결을 계속 찾습니다.  
  
 드라이버 관리자에서 점수가 100 (99 포함) 보다 엄격히 작은 연결을 다시 사용 하는 경우 드라이버 관리자는 SQLSetConnectAttr (SQL_ATTR_DBC_INFO_TOKEN)를 호출 하 여 연결을 응용 프로그램에서 요청한 상태로 다시 설정 합니다. 드라이버는이 함수 호출에서 연결을 다시 설정 하면 안 됩니다.  
  
 *Frequiredtransactionenlistment* TRUE 인 경우 *hCandidateConnection* 를 다시 사용 하려면 추가 인 리스트 먼 트 (*fsid* ! = null) 또는 unenlistment 필요 합니다 (*fsid* = = null). 이는 연결을 다시 사용 하는 비용과 드라이버가 연결을 다시 사용 하는 경우 연결을 등록/등록 취소 해야 하는지 여부를 나타냅니다. *Frequiretransactionenlistment* FALSE 인 경우 드라이버는 *fsid*의 값을 무시 해야 합니다.  
  
 드라이버 관리자는 *Hrequest* 와 *HCANDIDATECONNECTION* 의 부모 HENV 핸들이 동일 하도록 보장 합니다. 드라이버 관리자는 *Hrequest* 및 *hCandidateConnection* 와 연결 된 풀 ID가 동일 하다는 것을 보장 합니다.  
  
 응용 프로그램은이 함수를 직접 호출 하면 안 됩니다. 드라이버 인식 연결 풀링을 지 원하는 ODBC 드라이버는이 함수를 구현 해야 합니다.  
  
 ODBC 드라이버 개발용으로 sqlspi .h를 포함 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [드라이버 인식 연결 풀링](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
