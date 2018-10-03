---
title: '부록 b: ODBC 상태 전환 테이블 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 55fb40d6aa9b235837c761cf1362374d5c77d96d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47646221"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>부록 B: ODBC 상태 전환 테이블
이 부록의 표에서 ODBC 함수 환경, 연결, 문 및 설명자 상태 전환을 발생 하는 방법을 보여줍니다. 환경, 연결, 문 또는 설명자의 상태는 일반적으로 핸들 (환경, 연결, 문 또는 설명자)의 해당 형식을 사용 하는 함수를 호출할 수 있습니다 지정 합니다. 환경, 연결, 문 및 설명자 상태는 다음 그림과에서 같이 거의 겹칩니다. 예를 들어, C5 및 C6 정확한 중복 연결의 상태 및 문을 통해 S12 S1 데이터가 원본 종속 트랜잭션이 서로 다른 데이터 원본에 서로 다른 시간에 시작 후 D1i (암시적으로 할당 된 설명자) 설명자 상태에 따라 달라 집니다 상태 설명자와 관련 된 문의 상태를 상태 D1e (명시적으로 할당 된 설명자) 하는 동안에 문일의 상태와 무관 합니다. 각 상태에 대 한 참조 [환경 전환](../../../odbc/reference/appendixes/environment-transitions.md), [연결 전환](../../../odbc/reference/appendixes/connection-transitions.md)하십시오 [문 전환](../../../odbc/reference/appendixes/statement-transitions.md), 및 [설명자 전환 ](../../../odbc/reference/appendixes/descriptor-transitions.md)이 부록의 뒷부분에 나오는.  
  
 환경 및 연결 상태를 겹치는 다음과 같습니다.  
  
 ![환경 및 연결 상태 겹침](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 연결 및 구문 상태 겹침 같이:  
  
 ![연결 및 구문 상태 겹침](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 문 및 설명자 상태 겹침 다음과 같습니다.  
  
 ![문 및 설명자 상태 겹침](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 연결 및 설명자 상태 겹침 같이:  
  
 ![연결 및 설명자 상태 겹침](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 전환 테이블의 각 항목에는 다음 값 중 하나일 수 있습니다.  
  
-   **--** -상태 함수를 실행 한 후 변경 되지 않습니다.  
  
-   **E**  
     ***n*** , **C*n * * *, **S*n * **, 또는 **D * n***  -환경, 연결, 문 또는 설명자 상태로 이동 합니다 지정 된 상태입니다.  
  
-   **(구매자)**  -잘못 된 핸들을 함수에 전달 되었습니다. 핸들이 핸들을 null 이거나 잘못 된 형식의 유효한 핸들을 하는 경우-문 핸들을 필요한 경우 연결 핸들을 전달 된 예를 들어-함수에서 SQL_INVALID_HANDLE;을 반환 그렇지 않으면 동작이 정의 되지 않은 및 아마도 심각한있지 않습니다. 이 오류는 지정된 된 상태에서 함수를 호출 하는 유일한 결과 경우에 표시 됩니다. 이 오류 상태를 변경 하지 않습니다 하 고는 괄호로 표시 된 대로 드라이버 관리자에 의해 항상 검색 됩니다.  
  
-   **NS** -다음 상태입니다. 문 전환 문의 했습니다 비동기 상태 검사를 하지 처럼 동일 합니다. 예를 들어 결과 집합을 만드는 문을 상태가 S11 상태 S1에서에서 때문 **SQLExecDirect** SQL_STILL_EXECUTING을 반환 합니다. S11 상태의 NS 표기법 문에 대 한 전환으로 S1 상태일에서 문에 대 한 결과 집합을 만들고 동일한 지를 의미 합니다. 하는 경우 **SQLExecDirect** 오류를 반환할 문을 S1 상태로 유지 됩니다; 성공 하면 문이 S5 상태; 문을 이동 S8; 상태 데이터를 해야 하는 경우 이동한 S11 상태의 그대로 계속 실행 중인 경우.  
  
-   ***XXXXX*** 나 **(*XXXXX*)** -전환 테이블에 관련 된 SQLSTATE 드라이버 관리자에 의해 검색 되는 Sqlstate는 괄호로 구분 됩니다. 함수는 지정 된 SQLSTATE SQL_ERROR 반환 하지만 상태는 변경 되지 않습니다. 예를 들어 경우 **SQLExecute** 하기 전에 호출 됩니다 **SQLPrepare**, SQLSTATE HY010 반환 (함수 시퀀스 오류).  
  
> [!NOTE]  
>  테이블에서 상태를 변경 하지 않는 전환 테이블에 관련 되지 않은 오류를 표시 하지 않습니다. 예를 들어 **SQLAllocHandle** E1 환경 상태에서 호출 되 고 SQLSTATE HY001 반환 (메모리 할당 오류), 환경 E1 상태로 유지 됩니다;이 대 한 환경 전환 테이블에 표시 되지 않습니다  **SQLAllocHandle**합니다.  
  
 환경, 연결, 문 또는 설명자 둘 이상의 상태를 이동할 수, 하는 경우 가능한 각 상태 표시 되 고 하나 이상의 각주는 각 전환 수행 하는 조건에 설명 합니다. 각주를 다음 테이블에서 나타날 수 있습니다.  
  
|각주|의미|  
|--------------|-------------|  
|b|전후. 커서 결과 집합 또는 결과 집합의 끝을 시작 하기 전에 배치 되었습니다.|  
|c|현재 함수입니다. 현재 함수를 비동기적으로 실행 되었습니다.|  
|d|데이터가 필요 합니다. 함수는 SQL_NEED_DATA를 반환 합니다.|  
|e|오류입니다. 함수는 SQL_ERROR를 반환 합니다.|  
|i|잘못 된 행입니다. 커서가 있었기 결과의 행에 대해 집합과 행 삭제 또는 행에 대 한 작업에 오류가 발생 했습니다. 행 상태 배열이 존재 하는 경우 행에 대 한 행 상태 배열 값은 SQL_ROW_DELETED 이거나 SQL_ROW_ERROR 되었습니다. (행 상태 배열이 가리키는 SQL_ATTR_ROW_STATUS_PTR 문 특성입니다.)|  
|nf|찾을 수 없습니다. 함수에서 SQL_NO_DATA를 반환 합니다. 경우는 적용 되지 않습니다 **SQLExecDirect**를 **SQLExecute**, 또는 **SQLParamData** 검색을 실행 한 후 sql_no_data가 반환 update 또는 delete 문입니다.|  
|np|준비 되지 않았습니다. 문이 준비 되지 않았습니다.|  
|nr|결과가 없습니다. 문이 않습니다 또는 결과 집합을 만들지 않았습니다.|  
|o|다른 함수입니다. 다른 함수를 비동기적으로 실행 되었습니다.|  
|p|준비 합니다. 문이 준비 되어 있습니다.|  
|r|결과. 문은 대개 비어 있는 결과 집합을 만들지 않은 되거나 됩니다.|  
|s|성공했습니다. 함수는 SQL_SUCCESS_WITH_INFO 또는 관계 없이 SQL_SUCCESS를 반환 합니다.|  
|v|유효한 행입니다. 커서가 결과 집합의 행에 위치 되었습니다 및 행이 성공적으로 삽입, 업데이트 또는 행의 다른 작업을 성공적으로 완료 했습니다. 행 상태 배열이 존재 하는 경우 행을 행 상태 배열에 값 SQL_ROW_ADDED, SQL_ROW_SUCCESS, 또는 SQL_ROW_UPDATED 했습니다. (행 상태 배열이 가리키는 SQL_ATTR_ROW_STATUS_PTR 문 특성입니다.)|  
|x|실행 중입니다. 함수는 SQL_STILL_EXECUTING을 반환 합니다.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 이 예제에서 환경 상태 전환의 행에 대 한 테이블 **SQLFreeHandle** 때 *HandleType* SQL_HANDLE_ENV는 다음과 같습니다.  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(구매자)|E0|(HY010)|  
  
 하는 경우 **SQLFreeHandle** 사용 하 여 환경 상태 E0 라고 *HandleType* SQL_HANDLE_ENV로 드라이버 관리자에서 SQL_INVALID_HANDLE을 반환 합니다. 사용 하 여 E1 상태에서 호출 되 면 *HandleType* 함수는 성공 하 고 함수가 실패 하면 E1 상태를 유지 하는 경우 E0 상태 환경 이동 SQL_HANDLE_ENV로 설정 합니다. 사용 하 여 E2 상태에서 호출 되 면 *HandleType* SQL_HANDLE_ENV로 드라이버 관리자는 항상 반환 SQL_ERROR 및 SQLSTATE HY010 (함수 시퀀스 오류) 환경 상태 E2에에서 유지 됩니다.  
  
 상태 전환 테이블을 이해 하려면 참조 하는 항목 (환경, 연결, 문 또는 설명자)를 이해 하는 데 필요한 됩니다. X 형식의 항목의 핸들을 허용 하는 함수를 가정 합니다. 해당 함수에 대 한 X 상태 전환 표에서 어떻게 호출 X 형식의 항목의 핸들을 사용 하 여 함수에 영향을 해당 항목을 설명 합니다. 예를 들어 **SQLDisconnect** 연결 핸들을 허용 합니다. 에 대 한 연결 상태 전환 표에서 **SQLDisconnect** 에 대해 설명 하는 방법 **SQLDisconnect** 호출 하는 연결의 상태에 영향을 줍니다.  
  
 함수는 Y X와 같지 않은 Y, 형식 항목의 핸들을 가정 합니다. 해당 함수에 대 한 X 상태 전환 표에서 어떻게 호출 Y 형식의 항목과 연결 되는 X 형식에 대 한 핸들을 사용 하 여 함수에 영향을 줍니다 Y 형식의 항목을 설명 합니다. 예를 들어 문 상태 전환 테이블에 대 한 **SQLDisconnect** 에 대해 설명 하는 방법 **SQLDisconnect** 문이 있는 연결의 핸들을 사용 하 여 호출 하는 경우의 상태에 영향을 줍니다.는 문을 연결 됩니다.  
  
 이 부록에는 다음 항목에 있습니다.  
  
-   [환경 전환](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [연결 전환](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [문 전환](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [설명자 전환](../../../odbc/reference/appendixes/descriptor-transitions.md)
