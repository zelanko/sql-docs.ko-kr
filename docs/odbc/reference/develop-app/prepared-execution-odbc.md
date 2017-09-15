---
title: "준비 된 실행 ODBC | Microsoft Docs"
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
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d6b2437d1958e2583dabb75c0a4c26a2ed472975
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="prepared-execution-odbc"></a>준비 된 실행 ODBC
준비 된 실행은 문을 두 번 이상 실행 하는 효율적인 방법입니다. 문은 먼저 컴파일 또는 *준비* 액세스 계획으로 합니다. 액세스 계획이 하나를 실행 하거나 나중에 번 더입니다. 액세스 계획에 대 한 자세한 내용은 참조 [SQL 문 처리](../../../odbc/reference/processing-a-sql-statement.md)합니다.  
  
 준비 된 실행은 동일 하 고 매개 변수가 있는 SQL 문을 반복적으로 실행을 세로 및 사용자 지정 응용 프로그램에서 일반적으로 사용 됩니다. 예를 들어 다음 코드는 다양 한 부분 가격을 업데이트 하는 문을 준비 합니다. 그런 다음 다른 매개 변수 값으로 여러 번 문이 될 때마다 실행합니다.  
  
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
  
 준비 된 실행이 컴파일됩니다; 한 번만 때문에 두 번 이상 실행 되는 명령문에 대 한 직접 실행 보다 빠르게 직접 실행 되는 문은 실행 될 때마다가 컴파일됩니다. 준비 된 실행도 제공할 수 네트워크 트래픽이 감소 드라이버 수를 보내기 때문에 대 한 액세스 계획 식별자 데이터 원본에 될 때마다 문이 실행 되는 전체 SQL 문 대신 데이터 원본 지원 액세스 식별자를 계획 하는 경우.  
  
 응용 프로그램 설정 및 실행 하기 전에 문을 준비 된 후 결과 대 한 메타 데이터를 검색할 수 있습니다. 그러나 준비에 대 한 메타 데이터를 반환, 실행 되지 않은 일부 드라이버에 대 한 비용이 많이 듭니다 문과 상호 운용 가능한 응용 프로그램에서 가능한 경우 피해 야 합니다. 자세한 내용은 참조 [결과 집합 메타 데이터](../../../odbc/reference/develop-app/result-set-metadata.md)합니다.  
  
 한 번만 실행되는 문에는 준비된 실행을 사용하지 않아야 합니다. 이러한 문에서 추가 ODBC 함수 호출을 필요 하기 때문에 직접 실행 보다 약간 더 느려집니다.  
  
> [!IMPORTANT]  
>  명시적으로 호출 하 여 트랜잭션을 커밋하거나 **SQLEndTran** 자동 커밋 모드에서 작업으로 인해 일부 데이터 원본 연결에서 모든 문에 대 한 액세스 계획을 삭제 하 합니다. 자세한 내용은의 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 옵션을 참조 하십시오.는 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명 합니다.  
  
 준비한 문, 응용 프로그램을 실행 하려면:  
  
1.  호출 **SQLPrepare** SQL 문을 포함 하는 문자열을 전달 합니다.  
  
2.  매개 변수 값을 설정합니다. 매개 변수 앞 이나 뒤에서 문을 준비에 실제로 설정할 수 있습니다. 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)이 섹션의 뒷부분에 나오는 합니다.  
  
3.  호출 **SQLExecute** 필요한 데이터를 인출 하는 등 추가 처리를 수행 합니다.  
  
4.  필요에 따라 단계 2와 3 단계를 반복합니다.  
  
5.  때 **SQLPrepare** 호출 되는 드라이버:  
  
    -   문을 구문 분석 하지 않고도 데이터 소스의 SQL 문법을 사용 하도록 SQL 문을 수정 합니다. 여기에 이스케이프 시퀀스에 설명 된 바꿔 [odbc에서 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)합니다. 응용 프로그램 호출 하 여 수정 된 형식의 SQL 문 검색할 수 **SQLNativeSql**합니다. SQL_ATTR_NOSCAN 문 특성 설정 된 경우에 이스케이프 시퀀스 바뀌지 않습니다.  
  
    -   문을 준비에 대 한 데이터 원본에 보냅니다.  
  
    -   (준비 성공) 하는 경우 나중에 실행 반환 된 액세스 계획 식별자를 저장 하거나 (준비 실패) 하는 경우 모든 오류를 반환 합니다. (구문 오류 또는 액세스 위반) SQLSTATE 42000 같은 구문 오류를 SQLSTATE 42S02 같은 의미 체계 오류 등의 오류 (기본 테이블 또는 뷰를 찾을 수 없음).  
  
        > [!NOTE]  
        >  일부 드라이버는이 시점에서 오류를 반환 하지 않지만 대신 문이 실행 될 때 또는 카탈로그 함수가 호출 될 때 반환 합니다. 따라서 **SQLPrepare** 실제로 실패 했을 때 성공한 것으로 표시 될 수 있습니다.  
  
6.  때 **SQLExecute** 호출 되는 드라이버:  
  
    -   현재 매개 변수 값을 검색 하 고 필요에 따라 변환 합니다. 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)이 섹션의 뒷부분에 나오는 합니다.  
  
    -   데이터 원본에 대 한 액세스 계획 식별자 및 변환 된 매개 변수 값을 보냅니다.  
  
    -   모든 오류를 반환 합니다. 이들은 (잘못 된 커서 상태) SQLSTATE 24000 등 일반적으로 런타임 오류입니다. 그러나 일부 드라이버는이 시점에서 구문 및 의미 체계 오류가 반환 됩니다.  
  
 데이터 원본에서 문 준비를 지원 하지 않으면, 드라이버 가능한 범위까지 것 에뮬레이트해야 합니다. 예를 들어 드라이버 아무 작업도 수행할 수 때 **SQLPrepare** 호출 되 고 다음 문 직접 실행을 수행할 때 **SQLExecute** 호출 됩니다.  
  
 드라이버 때 검사에 대 한 문을 제출할 수도 데이터 소스 구문 실행 되지 않고 검사를 지 원하는 경우 **SQLPrepare** 호출 되 고 실행 하는 문을 제출할 때 **SQLExecute** 은 호출 됩니다.  
  
 드라이버는 문 준비를 에뮬레이션 수 없는 경우 문을 저장 때 **SQLPrepare** 라고 하며 실행을 위해 전송 때 **SQLExecute** 호출 됩니다.  
  
 에뮬레이트된 문 준비, 완벽 한 없기 때문에 **SQLExecute** 일반적으로에서 반환한 오류를 반환할 수 **SQLPrepare**합니다.
