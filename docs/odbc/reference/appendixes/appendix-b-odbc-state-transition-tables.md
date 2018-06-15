---
title: '부록 b: ODBC 상태 전환 테이블 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0d114dd574faf2909fa200f7c24ab0ccaa07804
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913898"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>부록 b: ODBC 상태 전환 테이블
이 부록의 표에서 ODBC 함수 환경, 연결, 문 및 설명자 상태 전환을 발생 하는 방법을 보여줍니다. 환경, 연결, 문 또는 설명자의 상태는 일반적으로 해당 형식의 핸들 (환경, 연결, 문 또는 설명자)를 사용 하는 함수를 호출할 수 있습니다 결정 합니다. 환경, 연결, 문 및 설명자 상태는 다음 그림에 나와 있는 것 처럼 대략 겹칩니다. 예를 들어 연결의 정확한 겹치는 C5 내용과 C6 하 문 S12 통해 S1을 데이터 원본 – 종속 트랜잭션이 서로 다른 데이터 원본에 대해 서로 다른 시간에 시작 하 고 D1i (암시적으로 할당 된 설명자) 설명자 상태에 따라 달라 집니다. 설명자와 관련 된 문의 상태 state D1e (명시적으로 할당 된 설명자)는 모든 문은의 상태와 무관입니다. 각 상태에 대 한 참조 [환경이 전환](../../../odbc/reference/appendixes/environment-transitions.md), [연결 전환](../../../odbc/reference/appendixes/connection-transitions.md), [문을 전환](../../../odbc/reference/appendixes/statement-transitions.md), 및 [설명자 전환 ](../../../odbc/reference/appendixes/descriptor-transitions.md)이 부록의 뒷부분에 나오는 합니다.  
  
 환경 및 연결 상태는 다음과 같이 겹칩니다.  
  
 ![환경 및 연결 상태 겹침](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 연결 및 문 상태는 다음과 같이 겹칩니다.  
  
 ![연결 및 구문 상태 겹침](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 구문 및 설명자 상태 겹침 다음과 같습니다.  
  
 ![구문 및 설명자 상태 겹침](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 연결 및 설명자 상태 겹침 다음과 같습니다.  
  
 ![연결 및 설명자 상태 겹침](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 전환 테이블의 각 항목은 다음 값 중 하나일 수 있습니다.  
  
-   **--** -함수를 실행 한 후 상태 변경 되지 않습니다.  
  
-   **E**  
     ***n*** , **C*n * * *, **S*n * **, 또는 **D * n***  -이동 환경, 연결, 문 또는 설명자 상태는 지정 된 상태입니다.  
  
-   **(면)**  -잘못 된 핸들이 함수에 전달 되었습니다. 핸들이 핸들을 null 이거나 잘못 된 형식의 유효한 핸들 경우-문 핸들을 필요한 경우에 연결 핸들 전달 된 예를 들어-함수에서 SQL_INVALID_HANDLE;을 반환 그렇지 않으면 동작이 정의 되지 않은 및 아마도 치명적있지 않습니다. 이 오류는 지정된 된 상태에는 함수 호출의 가능한 결과 경우에 표시 됩니다. 이 오류 상태를 변경 하지 않으며는 괄호로 표시 된 대로 드라이버 관리자에 의해 항상 검색 됩니다.  
  
-   **NS** -다음 상태입니다. 문 전환 명령문에는 비동기 상태 검사를 하지 마치 같습니다. 예를 들어 결과 집합을 만드는 문을 상태가 S11 S1 상태에서 때문에 **SQLExecDirect** SQL_STILL_EXECUTING을 반환 합니다. S11 상태의 NS 표기법 도구 문에 대 한 전환 동일 S1 상태일에서 문에 대 한 결과 집합을 만드는 있습니다. 경우 **SQLExecDirect** 은 오류를 반환할 문이 S1 상태로 유지 됩니다; 성공 하면 문이 S5 상태; 문을 이동 S8; 상태 데이터를 해야 하는 경우 이동한 S11 상태로 남아 아직 실행 되는 경우.  
  
-   ***XXXXX*** 또는 **(*XXXXX*)** —; 전환 테이블에 관련 된 SQLSTATE 드라이버 관리자에서 검색 하는 Sqlstate는 괄호로 구분 됩니다. SQL_ERROR와 지정 된 SQLSTATE 함수 반환 하지만 상태 변경 되지 않습니다. 예를 들어 경우 **SQLExecute** 하기 전에 호출 **SQLPrepare**, SQLSTATE HY010 반환 (함수 시퀀스 오류).  
  
> [!NOTE]  
>  테이블에서 상태를 변경 하지 않는 전환 테이블에 관련 되지 않은 오류를 표시 하지 않습니다. 예를 들어 **SQLAllocHandle** E1 환경 상태에서 호출 되 고 SQLSTATE HY001 반환 (메모리 할당 오류) 환경 E1 상태로 유지 됩니다;이 대 한 환경 전환 테이블에 표시 되지 않습니다  **SQLAllocHandle**합니다.  
  
 환경, 연결, 문 또는 설명자는 하나 이상의 상태를 이동할 수, 하는 경우에 가능한 각 상태 표시 되 고 하나 이상의 각주는 각 전환에 발생 하는 조건을 설명 합니다. 모든 테이블에 다음 각주 나타날 수 있습니다.  
  
|각주|의미|  
|--------------|-------------|  
|b|앞 이나 뒤 합니다. 커서 시작 이후 또는 결과 집합의 끝 이후에 결과 집합의 앞에 배치 되었습니다.|  
|c|현재 함수입니다. 현재 함수가 비동기적으로 실행 되 고.|  
|d|데이터가 필요 합니다. 함수는 SQL_NEED_DATA를 반환 합니다.|  
|e|오류입니다. 함수는 SQL_ERROR를 반환 합니다.|  
|i|행이 잘못 되었습니다. 커서가 있었기 결과의 행에 대해 집합과 행 삭제 또는 행에 대 한 작업에 오류가 발생 했습니다. 행 상태 배열이 존재 하는 경우 행에 대 한 행 상태 배열이의 값은 SQL_ROW_DELETED 또는 SQL_ROW_ERROR 했습니다. (행 상태 배열이 가리키는 SQL_ATTR_ROW_STATUS_PTR 문 특성입니다.)|  
|nf|찾을 수 없습니다. 함수가 SQL_NO_DATA를 반환 했습니다. 시기는 적용 되지 않습니다 **SQLExecDirect**, **SQLExecute**, 또는 **SQLParamData** sql_no_data가 반환 검색을 실행 한 후 업데이트 또는 삭제 문의 합니다.|  
|np|준비 되지 않았습니다. 문이 준비 되지 않았습니다.|  
|nr|결과가 없습니다. 문을 하지 또는 결과 집합을 생성 하지 못했습니다.|  
|o|다른 함수입니다. 다른 함수는 비동기적으로 실행 되었습니다.|  
|p|준비합니다. 문이 준비 되어 있습니다.|  
|r|결과. 문을 또는 (비어 있을 수 있음) 결과 집합을 만들려면 않았습니다.|  
|s|성공했습니다. 함수가는 SQL_SUCCESS_WITH_INFO 또는 관계 없이 SQL_SUCCESS를 반환 했습니다.|  
|v|유효한 행입니다. 커서가 결과 집합의 행에 위치 되었습니다 및 행에 성공적으로 삽입, 업데이트 또는 행에 다른 작업이 이었으므로 성공적으로 완료 합니다. 행 상태 배열이 존재 하는 경우에 행에 대 한 행 상태 배열이 값 SQL_ROW_ADDED, SQL_ROW_SUCCESS, 또는 SQL_ROW_UPDATED 했습니다. (행 상태 배열이 가리키는 SQL_ATTR_ROW_STATUS_PTR 문 특성입니다.)|  
|x|실행 중입니다. 함수는 SQL_STILL_EXECUTING을 반환 합니다.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 이 예제에서는 환경 상태 전환의 행에 대 한 테이블 **SQLFreeHandle** 때 *HandleType* SQL_HANDLE_ENV는 다음과 같습니다.  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> 할당 된|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(면)|E0|(HY010)|  
  
 경우 **SQLFreeHandle** 환경 상태가 E0 라고 *HandleType* SQL_HANDLE_ENV로 설정 하면 드라이버 관리자에서 SQL_INVALID_HANDLE을 반환 합니다. 상태가 E1 호출 되 면 *HandleType* E0 함수는 성공 하 고 함수가 실패 하면 E1 상태를 유지 하도록 환경 이동 SQL_HANDLE_ENV로 설정 합니다. 상태가 E2 호출 되 면 *HandleType* SQL_HANDLE_ENV로 설정 하면 드라이버 관리자 항상 반환 SQL_ERROR 및 SQLSTATE HY010 (함수 시퀀스 오류입니다.) 환경 상태 E2에에서 유지 됩니다.  
  
 상태 전환 테이블을 이해 하려면를 참조 (환경, 연결, 문 또는 설명자) 항목을 이해 해야 합니다. 함수 수락 X 유형의 항목의 핸들을 가정 합니다. 해당 함수에 대 한 X 상태 전환 표에서 호출 방법을 X, 유형의 항목의 핸들을 사용 하 여 함수, 영향을 주는 설명 해당 항목입니다. 예를 들어 **SQLDisconnect** 연결 핸들을 허용 합니다. 에 대 한 연결 상태 전환 표에서 **SQLDisconnect** 설명 방법을 **SQLDisconnect** 호출 하는 연결의 상태에 영향을 줍니다.  
  
 Y X과 같지 않은 Y 형식의 항목의 핸들을 수락 하는 함수를 가정 합니다. 해당 함수에 대 한 X 상태 전환 표에서 호출 방법을 Y 형식의 항목에 연관 된 X 형식의 핸들을 사용 하 여 함수, 영향을 주는 설명 Y 형식의 항목입니다. 예를 들어 문 상태 전환 테이블에 대 한 **SQLDisconnect** 설명 방법을 **SQLDisconnect** 상태는 연결의 핸들을 사용 하 여 호출 하는 경우 문의 영향을 줍니다.는 문을 연결 됩니다.  
  
 이 부록의 내용에는 다음 항목이 포함 되어 있습니다.  
  
-   [환경 전환](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [연결 전환](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [문 전환](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [설명자 전환](../../../odbc/reference/appendixes/descriptor-transitions.md)
