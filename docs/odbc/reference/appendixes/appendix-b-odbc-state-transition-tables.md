---
title: '부록 B: ODBC 상태 전환 표 | 마이크로 소프트 문서'
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
ms.openlocfilehash: db20c492ababbe6bf8f065fce88067c643f2694d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302887"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>부록 B: ODBC 상태 전환 테이블
이 부록의 표는 ODBC 함수가 환경, 연결, 명령문 및 설명자 상태의 전환을 일으키는 방법을 보여 준다. 환경, 연결, 문 또는 설명자의 상태는 일반적으로 해당 유형의 핸들(환경, 연결, 명령문 또는 설명자)을 사용하는 함수를 호출할 수 있는 시기를 지정합니다. 환경, 연결, 명령문 및 설명자 상태는 다음 그림과 같이 대략 겹칩니다. 예를 들어 C5 및 C6 및 문 상태의 정확한 겹치는 S1-s1-S12는 트랜잭션이 서로 다른 데이터 원본에서 서로 다른 시간에 시작되고 설명자 상태 D1i(암시적으로 할당된 설명자)는 설명자가 연결된 명령문의 상태에 따라 달라지며 상태 D1e(명시적으로 할당된 설명자)는 모든 명령문과 독립적입니다. 각 상태에 대한 설명은 이 부록의 다음 부분에서 [환경 전환,](../../../odbc/reference/appendixes/environment-transitions.md) [연결 전환,](../../../odbc/reference/appendixes/connection-transitions.md) [명령문 전환](../../../odbc/reference/appendixes/statement-transitions.md)및 [설명자 전환을](../../../odbc/reference/appendixes/descriptor-transitions.md)참조하십시오.  
  
 환경 및 연결 상태는 다음과 같이 겹칩니다.  
  
 ![환경 및 연결 상태 겹침](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 연결 및 명령문 상태는 다음과 같이 겹칩니다.  
  
 ![연결 및 구문 상태 겹침](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 명령문 및 설명자 상태는 다음과 같이 겹칩니다.  
  
 ![구문 및 설명자 상태 겹침](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 연결 및 설명자 상태는 다음과 같이 겹칩니다.  
  
 ![연결 및 설명자 상태 겹침](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 전환 테이블의 각 항목은 다음 값 중 하나일 수 있습니다.  
  
-   **--**-기능을 실행한 후에는 상태가 변경되지 않습니다.  
  
-   **전자**  

     **_n_** , **C_n_**, **S_n_** 또는 **D_n_** - 환경, 연결, 명령문 또는 설명자 상태가 지정된 상태로 이동합니다.  
 
-   **(IH)** - 잘못된 핸들이 함수에 전달되었습니다. 핸들이 null 핸들이거나 잘못된 형식의 올바른 핸들인 경우(예: 명령문 핸들이 필요할 때 연결 핸들이 전달됨) 함수는 SQL_INVALID_HANDLE 반환합니다. 그렇지 않으면 동작이 정의되지 않았으며 치명적일 수 있습니다. 이 오류는 지정된 상태에서 함수를 호출할 수 있는 유일한 결과인 경우에만 표시됩니다. 이 오류는 상태를 변경하지 않으며 괄호에 표시된 대로 항상 드라이버 관리자에 의해 검색됩니다.  
  
-   **NS** - 다음 상태입니다. 명령문 전환은 문이 비동기 상태를 통과하지 않은 경우와 동일합니다. 예를 들어 **SQLExecDirect가** SQL_STILL_EXECUTING 반환했기 때문에 결과 집합을 만드는 문이 상태 S1에서 S11 상태S1로 진입한다고 가정합니다. 상태 S11의 NS 표기는 명령문에 대한 전환이 결과 집합을 만드는 상태 S1의 명령문과 동일하다는 것을 의미합니다. **SQLExecDirect가** 오류를 반환하는 경우 문은 상태 S1에 남아 있습니다. 성공하면 문은 상태 S5로 이동합니다. 데이터가 필요한 경우 명령문은 S8 상태로 이동합니다. 여전히 실행 중인 경우 S11 상태입니다.  

-   **_XXXXX_** 또는 ***(XXXXX)*** - 전환 테이블과 관련된 SQLSTATE; 드라이버 관리자에서 검색한 SQLSTAT은 괄호로 둘러싸여 있습니다. 함수가 SQL_ERROR 지정된 SQLSTATE를 반환했지만 상태는 변경되지 않습니다. 예를 들어 SQLPrepare **전에** **SQLExecute가** 호출되면 SQLSTATE HY010(함수 시퀀스 오류)이 반환됩니다.  

> [!NOTE]  
>  테이블은 상태를 변경하지 않는 전환 테이블과 관련이 없는 오류를 표시하지 않습니다. 예를 **들어, SQLAllocHandle** 환경 상태 E1에서 호출 되 고 SQLSTATE HY001 (메모리 할당 오류)를 반환 하는 경우 환경 상태 E1에 남아 있습니다. **이는 SQLAllocHandle**에 대한 환경 전환 테이블에 표시되지 않습니다.  
  
 환경, 연결, 명령문 또는 설명자가 두 개 이상의 상태로 이동할 수 있는 경우 가능한 각 상태가 표시되고 하나 이상의 각주가 각 전환이 발생하는 조건을 설명합니다. 다음 각주가 모든 테이블에 나타날 수 있습니다.  
  
|각주|의미|  
|--------------|-------------|  
|b|전이나 후에. 커서는 결과 집합이 시작되기 전이나 결과 집합이 끝난 후에 배치되었습니다.|  
|c|현재 함수입니다. 현재 함수가 비동기적으로 실행되었습니다.|  
|d|데이터가 필요합니다. 함수가 SQL_NEED_DATA 반환되었습니다.|  
|e|오류가 표시됩니다. 함수가 SQL_ERROR 반환되었습니다.|  
|i|잘못된 행입니다. 커서가 결과 집합의 행에 배치되었으며 행이 삭제되었거나 행의 작업에서 오류가 발생했습니다. 행 상태 배열이 있는 경우 행 상태 배열의 값이 SQL_ROW_DELETED 또는 SQL_ROW_ERROR. 행 상태 배열은 SQL_ATTR_ROW_STATUS_PTR 문 특성으로 가리개됩니다.)|  
|nf|찾을 수 없음 함수가 SQL_NO_DATA 반환되었습니다. **이는 SQLExecDirect**, **SQLExecute**또는 **SQLParamData가** 검색된 업데이트를 실행하거나 문을 삭제한 후 SQL_NO_DATA 반환하는 경우에는 적용되지 않습니다.|  
|np|준비되지 않았습니다. 성명서가 준비되지 않았습니다.|  
|nr|결과가 없습니다. 명령문은 결과 집합을 만들지 않거나 만들지 않습니다.|  
|o|다른 기능. 또 다른 함수는 비동기적으로 실행되었습니다.|  
|p|준비. 성명서가 준비되었습니다.|  
|r|결과. 문은 (비어 있을 수 있는) 결과 집합을 만들거나 만들지 않습니다.|  
|s|성공했습니다. 함수가 SQL_SUCCESS_WITH_INFO 반환되거나 SQL_SUCCESS.|  
|v|유효한 행입니다. 커서가 결과 집합의 행에 배치되었으며 행이 성공적으로 삽입되었거나 성공적으로 업데이트되었거나 행의 다른 작업이 성공적으로 완료되었습니다. 행 상태 배열이 있는 경우 행 상태 배열의 값이 SQL_ROW_ADDED, SQL_ROW_SUCCESS 또는 SQL_ROW_UPDATED. 행 상태 배열은 SQL_ATTR_ROW_STATUS_PTR 문 특성으로 가리개됩니다.)|  
|x|실행 중입니다. 함수가 SQL_STILL_EXECUTING 반환되었습니다.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 이 예제에서는 *핸들 유형이* SQL_HANDLE_ENV **때 SQLFreeHandle에** 대한 환경 상태 전환 테이블의 행은 다음과 같습니다.  
  
|E0<br /><br /> 할당되지 않음|E1<br /><br /> Allocated|E2<br /><br /> 연결|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|(HY010)|  
  
 *핸들 유형이* SQL_HANDLE_ENV 설정된 환경 상태 E0에서 **SQLFreeHandle이** 호출되면 드라이버 관리자가 SQL_INVALID_HANDLE 반환합니다. *핸들타이가* SQL_HANDLE_ENV 설정된 상태 E1에서 호출되는 경우 함수가 성공하고 함수가 실패할 경우 환경이 상태 E1로 이동합니다. *핸들타이가* SQL_HANDLE_ENV 설정된 상태 E2에서 호출되는 경우 드라이버 관리자는 항상 SQL_ERROR 및 SQLSTATE HY010(함수 시퀀스 오류)을 반환하고 환경은 상태 E2에 남아 있습니다.  
  
 상태 전환 테이블을 이해하려면 참조하는 항목(환경, 연결, 문 또는 설명자)을 이해해야 합니다. 함수가 X형식 항목의 핸들을 수락한다고 가정합니다. 해당 함수의 X 상태 전환 테이블은 X 형식의 항목의 핸들을 통해 함수를 호출하는 것이 해당 항목에 미치는 영향을 설명합니다. 예를 들어 **SQLDisconnect는** 연결 핸들을 허용합니다. **SQLDisconnect에** 대한 연결 상태 전환 테이블은 **SQLDisconnect가** 호출되는 연결의 상태에 미치는 영향을 설명합니다.  
  
 함수가 Y가 X와 같지 않은 Y 형식의 항목의 핸들을 수락한다고 가정합니다. 해당 함수의 X 상태 전환 테이블은 Y 형식의 항목과 연결된 X 형식의 핸들을 통해 함수를 호출하는 것이 Y 형식의 항목에 영향을 주는 방법을 설명합니다. 예를 들어 **SQLDisconnect에** 대한 명령문 상태 전환 테이블은 문이 연결된 연결의 핸들을 호출할 때 **SQLDisconnect가** 명령문의 상태에 미치는 영향을 설명합니다.  
  
 이 부록에는 다음 항목이 포함되어 있습니다.  
  
-   [환경 전환](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [연결 전환](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [문 전환](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [설명자 전환](../../../odbc/reference/appendixes/descriptor-transitions.md)
