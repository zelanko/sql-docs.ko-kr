---
title: 준비된 실행 ODBC | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 147ca85b21296575ff55afbe66ab286cc4824fae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282313"
---
# <a name="prepared-execution-odbc"></a>준비된 실행 ODBC
준비된 실행은 문을 두 번 이상 실행하는 효율적인 방법입니다. 명령문은 먼저 액세스 계획에 컴파일또는 *준비됩니다.* 그런 다음 액세스 계획이 나중에 하나 이상 실행됩니다. 액세스 계획에 대한 자세한 내용은 [SQL 문 처리를](../../../odbc/reference/processing-a-sql-statement.md)참조하십시오.  
  
 준비된 실행은 일반적으로 수직 및 사용자 지정 응용 프로그램에서 동일한 매개 변수화된 SQL 문을 반복적으로 실행하는 데 사용됩니다. 예를 들어 다음 코드는 서로 다른 부품의 가격을 업데이트하는 문을 준비합니다. 그런 다음 매번 다른 매개 변수 값으로 문을 여러 번 실행합니다.  
  
```  
SQLREAL       Price;  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0, PriceInd = 0;  
  
// Prepare a statement to update salaries in the Employees table.  
SQLPrepare(hstmt, "UPDATE Parts SET Price = ? WHERE PartID = ?", SQL_NTS);  
  
// Bind Price to the parameter for the Price column and PartID to  
// the parameter for the PartID column.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &PartID, 0, &PartIDInd);  
  
// Repeatedly execute the statement.  
while (GetPrice(&PartID, &Price)) {  
   SQLExecute(hstmt);  
}  
```  
  
 준비된 실행은 주로 문이 한 번만 컴파일되므로 두 번 이상 실행되는 명령문에 대해 직접 실행보다 빠릅니다. 직접 실행된 문은 실행될 때마다 컴파일됩니다. 준비된 실행은 또한 드라이버가 데이터 원본이 액세스 계획 식별자를 지원하는 경우 전체 SQL 문이 아닌 문이 실행될 때마다 데이터 원본에 액세스 계획 식별자를 보낼 수 있기 때문에 네트워크 트래픽감소를 제공할 수 있습니다.  
  
 응용 프로그램은 명령문이 준비된 후 실행되기 전에 결과 집합에 대한 메타데이터를 검색할 수 있습니다. 그러나 준비된 실행되지 않은 문에 대한 메타데이터를 반환하는 것은 일부 드라이버의 경우 비용이 많이 들며 가능하면 상호 운용 가능한 응용 프로그램에서 는 피해야 합니다. 자세한 내용은 [결과 집합 메타데이터](../../../odbc/reference/develop-app/result-set-metadata.md)를 참조하십시오.  
  
 한 번만 실행되는 문에는 준비된 실행을 사용하지 않아야 합니다. 이러한 명령문의 경우 추가 ODBC 함수 호출이 필요하기 때문에 직접 실행보다 약간 느립니다.  
  
> [!IMPORTANT]  
>  **SQLEndTran을** 명시적으로 호출하거나 자동 커밋 모드에서 작업하여 트랜잭션을 커밋하거나 롤백하면 일부 데이터 원본이 연결의 모든 문에 대한 액세스 계획을 삭제합니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명의 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 옵션을 참조하십시오.  
  
 문을 준비하고 실행하려면 응용 프로그램이 다음과 같은 것입니다.  
  
1.  **SQLPrepare를** 호출하고 SQL 문이 포함된 문자열을 전달합니다.  
  
2.  매개 변수의 값을 설정합니다. 매개 변수는 실제로 문을 준비하기 전이나 후에 설정할 수 있습니다. 자세한 내용은 이 섹션의 다음 부분의 [문 매개 변수를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오.  
  
3.  **SQLExecute를** 호출하고 데이터 가져오기와 같은 필요한 추가 처리를 수행합니다.  
  
4.  필요에 따라 2단계와 3단계를 반복합니다.  
  
5.  **SQLPrepare가** 호출될 때 드라이버:  
  
    -   SQL 문을 구문 분석 하지 않고 데이터 원본의 SQL 문법을 사용 하 여 수정 합니다. 여기에는 [ODBC의 이스케이프 시퀀스에서 설명하는 이스케이프 시퀀스 교체가 포함됩니다.](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 응용 프로그램은 **SQLNativeSql**을 호출하여 수정된 SQL 문의 형식을 검색할 수 있습니다. SQL_ATTR_NOSCAN 문 특성이 설정된 경우 이스케이프 시퀀스는 대체되지 않습니다.  
  
    -   준비를 위해 명령문을 데이터 원본으로 보냅니다.  
  
    -   나중에 실행을 위해 반환된 액세스 계획 식별자를 저장하거나(준비에 성공한 경우) 오류를 반환합니다(준비에 실패한 경우). 오류에는 SQLSTATE 42000(구문 오류 또는 액세스 위반)과 같은 구문 오류와 SQLSTATE 42S02(기본 테이블 또는 보기를 찾을 수 없습니다)와 같은 의미 체계 오류가 포함됩니다.  
  
        > [!NOTE]  
        >  일부 드라이버는 이 시점에서 오류를 반환하지 않고 문이 실행되거나 카탈로그 함수가 호출될 때 오류를 반환합니다. 따라서 **SQLPrepare실제로** 실패 했을 때 성공 한 것 같습니다.  
  
6.  **SQLExecute가** 호출될 때 드라이버는 다음과 같은 것입니다.  
  
    -   현재 매개 변수 값을 검색하고 필요에 따라 변환합니다. 자세한 내용은 이 섹션의 다음 부분의 [문 매개 변수를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오.  
  
    -   액세스 계획 식별자 및 변환된 매개 변수 값을 데이터 원본으로 보냅니다.  
  
    -   오류를 반환합니다. 일반적으로 SQLSTATE 24000(잘못된 커서 상태)과 같은 런타임 오류입니다. 그러나 일부 드라이버는 이 시점에서 구문 및 의미 체계 오류를 반환합니다.  
  
 데이터 원본이 명령문 준비를 지원하지 않는 경우 드라이버는 가능한 범위까지 에뮬레이트해야 합니다. 예를 들어 **SQLPrepare가** 호출될 때 드라이버는 아무 것도 수행하지 않으며 **SQLExecute가** 호출될 때 명령문을 직접 실행합니다.  
  
 데이터 원본이 실행 없이 구문 검사를 지원하는 경우 드라이버는 **SQLPrepare가** 호출될 때 검사하기 위한 문을 제출하고 **SQLExecute가** 호출될 때 실행을 위한 문을 제출할 수 있습니다.  
  
 드라이버가 문 준비를 에뮬레이트할 수 없는 경우 **SQLPrepare가** 호출될 때 문을 저장하고 **SQLExecute가** 호출될 때 실행을 위해 제출합니다.  
  
 에뮬레이트된 문 준비는 완벽하지 않기 때문에 **SQLExecute는** 일반적으로 **SQLPrepare**.
