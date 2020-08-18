---
description: '부록 B: ODBC 상태 전환 테이블'
title: '부록 B: ODBC 상태 전환 테이블 | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b81b43d40d3552959ade377cb7b967eb7331b7f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411619"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>부록 B: ODBC 상태 전환 테이블
이 부록의 표는 ODBC 함수가 환경, 연결, 문 및 설명자 상태를 전환 하는 방법을 보여 줍니다. 환경, 연결, 문 또는 설명자의 상태는 일반적으로 해당 유형의 핸들 (환경, 연결, 문 또는 설명자)을 사용 하는 함수를 호출할 수 있는 시기를 결정 합니다. 환경, 연결, 문 및 설명자 상태는 다음 그림과 같이 대략적으로 겹칩니다. 예를 들어 트랜잭션은 서로 다른 데이터 원본에서 서로 다른 시간에 시작 되 고 설명자 상태 D1i (암시적으로 할당 된 설명자)는 설명자가 연결 된 문의 상태에 따라 달라 지는 반면, 상태 D1e (명시적으로 할당 된 설명자)는 모든 문의 상태에 독립적 이기 때문에 데이터 원본에 따라 달라 집니다. 각 상태에 대 한 설명은이 부록의 뒷부분에 나오는 [환경 전환](../../../odbc/reference/appendixes/environment-transitions.md), [연결 전환](../../../odbc/reference/appendixes/connection-transitions.md), [문 전환](../../../odbc/reference/appendixes/statement-transitions.md)및 [설명자 전환](../../../odbc/reference/appendixes/descriptor-transitions.md)을 참조 하세요.  
  
 환경 및 연결 상태는 다음과 같이 겹칩니다.  
  
 ![환경 및 연결 상태 겹침](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 연결 및 문 상태는 다음과 같이 겹칩니다.  
  
 ![연결 및 구문 상태 겹침](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 문과 설명자 상태는 다음과 같이 겹칩니다.  
  
 ![구문 및 설명자 상태 겹침](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 연결 및 설명자 상태는 다음과 같이 겹칩니다.  
  
 ![연결 및 설명자 상태 겹침](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 전환 테이블의 각 항목은 다음 값 중 하나일 수 있습니다.  
  
-   **--** -함수를 실행 한 후에는 상태가 변경 되지 않습니다.  
  
-   **우표**  

     **_n_** , **C_n_**, **S_n_** 또는 **D_n_** -환경, 연결, 문 또는 설명자 상태가 지정 된 상태로 이동 합니다.  
 
-   **(Ih)** -잘못 된 핸들이 함수에 전달 되었습니다. 핸들이 null 핸들 이거나 잘못 된 형식의 올바른 핸들 일 경우 (예: 문 핸들이 필요한 경우 연결 핸들이 전달 됨) 함수는 SQL_INVALID_HANDLE을 반환 합니다. 그렇지 않으면 동작이 정의 되지 않으며 심각한 것일 수 있습니다. 이 오류는 지정 된 상태에서 함수를 호출 하는 경우에만 가능한 결과가 있는 경우에만 표시 됩니다. 이 오류는 상태를 변경 하지 않으며 괄호로 표시 된 드라이버 관리자에 의해 항상 검색 됩니다.  
  
-   **NS** -다음 상태입니다. 문 전환은 문이 비동기 상태를 거치지 않은 경우와 동일 합니다. 예를 들어 **Sqlexecdirect** 가 SQL_STILL_EXECUTING 반환 되었기 때문에 결과 집합을 만드는 문이 S1 상태에서 S11 상태를 반환 한다고 가정 합니다. 상태 S11의 NS 표기법은 문에 대 한 전환이 결과 집합을 만드는 상태 S1의 문과 동일한 지를 의미 합니다. **Sqlexecdirect** 에서 오류를 반환 하는 경우 문은 S1 상태로 유지 됩니다. 성공 하면 문이 상태 S5로 이동 합니다. 데이터를 필요로 하는 경우 문이 상태 S8로 이동 합니다. 여전히 실행 되 고 있는 경우에는 S11 상태로 유지 됩니다.  

-   **_XXXXX_**  또는 **(*XXXXX*)** -전환 테이블과 관련 된 SQLSTATE입니다. 드라이버 관리자에서 감지한 SQLSTATEs는 괄호로 묶여 있습니다. 함수는 SQL_ERROR 및 지정 된 SQLSTATE를 반환 하지만 상태는 변경 되지 않습니다. 예를 들어 **Sqlexecute**전에 **sqlexecute** 를 호출 하면 sqlstate HY010 (함수 시퀀스 오류)가 반환 됩니다.  

> [!NOTE]  
>  테이블에는 상태를 변경 하지 않는 전환 테이블과 관련이 없는 오류가 표시 되지 않습니다. 예를 들어 **SQLAllocHandle** 이 환경 상태 E1에서 호출 되 고 SQLSTATE HY001 (메모리 할당 오류)를 반환 하는 경우 환경은 E1 상태를 유지 합니다. **SQLAllocHandle**에 대 한 환경 전환 테이블에는 표시 되지 않습니다.  
  
 환경, 연결, 문 또는 설명자가 둘 이상의 상태로 이동할 수 있는 경우 각각의 가능한 상태가 표시 되 고 하나 이상의 각주가 각 전환이 수행 되는 조건을 설명 합니다. 다음 각주가 표에 표시 될 수 있습니다.  
  
|각주|의미|  
|--------------|-------------|  
|b|이전 또는 이후. 커서는 결과 집합의 시작 위치 앞 이나 결과 집합의 끝 뒤에 배치 되었습니다.|  
|c|현재 함수입니다. 현재 함수가 비동기적으로 실행 되 고 있습니다.|  
|d|데이터가 필요 합니다. SQL_NEED_DATA 반환 되는 함수입니다.|  
|e|오류. SQL_ERROR 반환 되는 함수입니다.|  
|i|행이 잘못 되었습니다. 커서가 결과 집합의 행에 배치 되었고 행이 삭제 되었거나 행의 작업에서 오류가 발생 했습니다. 행 상태 배열이 있는 경우 행에 대 한 행 상태 배열의 값이 SQL_ROW_DELETED 되었거나 SQL_ROW_ERROR. 행 상태 배열은 SQL_ATTR_ROW_STATUS_PTR statement 특성에 의해 가리키고 있습니다.|  
|nf|찾을 수 없음 SQL_NO_DATA 반환 되는 함수입니다. 이는 검색 된 update 또는 delete 문을 실행 한 후 **Sqlexecdirect**, **Sqlexecute**또는 **sqlexecdirect** 가 SQL_NO_DATA를 반환 하는 경우에는 적용 되지 않습니다.|  
|np|준비 되지 않았습니다. 문을 준비 하지 않았습니다.|  
|nr|결과가 없습니다. 문은 결과 집합을 만들지 않거나 생성 하지 않습니다.|  
|o|기타 함수입니다. 다른 함수가 비동기적으로 실행 되 고 있습니다.|  
|p|잘. 문을 준비 했습니다.|  
|r|결과. 문은 (비어 있을 수 있음) 결과 집합을 만듭니다.|  
|s|성공 함수는 SQL_SUCCESS_WITH_INFO 또는 SQL_SUCCESS을 반환 합니다.|  
|v|올바른 행입니다. 커서가 결과 집합의 행에 배치 되었고 행이 성공적으로 삽입 되었거나 성공적으로 업데이트 되었거나 행의 다른 작업이 성공적으로 완료 되었습니다. 행 상태 배열이 있는 경우 행에 대 한 행 상태 배열의 값은 SQL_ROW_ADDED, SQL_ROW_SUCCESS 또는 SQL_ROW_UPDATED입니다. 행 상태 배열은 SQL_ATTR_ROW_STATUS_PTR statement 특성에 의해 가리키고 있습니다.|  
|x|실행 중입니다. SQL_STILL_EXECUTING 반환 되는 함수입니다.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 이 예제에서 *HandleType* 가 SQL_HANDLE_ENV 경우 **sqlfreehandle** 에 대 한 환경 상태 전환 테이블의 행은 다음과 같습니다.  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|항목|E0|HY010|  
  
 *HandleType* 가 SQL_HANDLE_ENV로 설정 된 환경 상태 E0에서 **sqlfreehandle** 을 호출 하면 드라이버 관리자는 SQL_INVALID_HANDLE를 반환 합니다. *HandleType* 가 SQL_HANDLE_ENV로 설정 된 상태 e1에서 호출 되는 경우 함수가 성공 하 고 함수에 오류가 발생 하는 경우 상태를 e1으로 유지 하면 환경이 E0로 이동 합니다. *HandleType* 가 SQL_HANDLE_ENV로 설정 된 E2 상태에서 호출 되는 경우 드라이버 관리자는 항상 SQL_ERROR 및 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 하며 환경은 E2 상태로 유지 됩니다.  
  
 상태 전환 테이블을 이해 하려면 참조 하는 항목 (환경, 연결, 문 또는 설명자)을 이해 해야 합니다. 함수에서 X 형식의 항목에 대 한 핸들을 수락 한다고 가정 합니다. 해당 함수의 X 상태 전환 테이블은 X 형식의 항목 핸들을 사용 하 여 함수를 호출 하는 방법을 설명 하 고 해당 항목에 영향을 줍니다. 예를 들어 **Sqldisconnect** 는 연결 핸들을 허용 합니다. **Sqldisconnect** 의 연결 상태 전환 테이블은 **sqldisconnect** 가 호출 된 연결의 상태에 미치는 영향을 설명 합니다.  
  
 함수에서 Y 형식의 항목에 대 한 핸들을 수락 한다고 가정 합니다. 여기서 Y는 X와 같지 않습니다. 이 함수에 대 한 X 상태 전환 테이블은 y 형식의 항목에 연결 된 X 형식의 핸들을 사용 하 여 함수를 호출 하는 방법을 설명 합니다 .이 함수는 y 형식의 항목에 영향을 줍니다. 예를 들어 **sqldisconnect** 의 문 상태 전환 테이블은 문이 연결 된 연결의 핸들을 사용 하 여 호출 될 때 **sqldisconnect** 가 문의 상태에 미치는 영향을 설명 합니다.  
  
 이 부록에는 다음 항목이 포함 되어 있습니다.  
  
-   [환경 전환](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [연결 전환](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [문 전환](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [설명자 전환](../../../odbc/reference/appendixes/descriptor-transitions.md)
