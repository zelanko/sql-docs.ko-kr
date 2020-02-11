---
title: 준비 된 실행 ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2107ca1eeecc6fad24311c5bce629784ae4ceff0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68023286"
---
# <a name="prepared-execution-odbc"></a>준비된 실행 ODBC
준비 된 실행은 문을 두 번 이상 실행 하는 효율적인 방법입니다. 문은 먼저 액세스 계획으로 컴파일하거나 *준비* 됩니다. 액세스 계획은 나중에 한 번 이상 실행 됩니다. 액세스 계획에 대 한 자세한 내용은 [SQL 문 처리](../../../odbc/reference/processing-a-sql-statement.md)를 참조 하세요.  
  
 준비 된 실행은 일반적으로 수직 및 사용자 지정 응용 프로그램에서 동일한 매개 변수가 있는 SQL 문을 반복 해 서 실행 하는 데 사용 됩니다. 예를 들어 다음 코드는 여러 부분의 가격을 업데이트 하는 문을 준비 합니다. 그런 다음 매번 다른 매개 변수 값을 사용 하 여 문을 여러 번 실행 합니다.  
  
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
  
 실행 준비는 문이 한 번만 컴파일되기 때문에 두 번 이상 실행 되는 문의 직접 실행 보다 빠릅니다. 직접 실행 되는 문은 실행 될 때마다 컴파일됩니다. 또한 준비 된 실행은 데이터 원본에서 액세스 계획 식별자를 지 원하는 경우 전체 SQL 문이 아니라 문이 실행 될 때마다 데이터 원본에 액세스 계획 식별자를 보낼 수 있으므로 네트워크 트래픽 감소를 제공할 수 있습니다.  
  
 응용 프로그램은 문이 준비 된 후 실행 되기 전에 결과 집합에 대 한 메타 데이터를 검색할 수 있습니다. 그러나 준비 된 명령의 문에 대 한 메타 데이터를 반환 하는 것은 일부 드라이버의 경우 비용이 많이 들고 가능 하면 상호 운용 가능한 응용 프로그램에서 피해 야 합니다. 자세한 내용은 [결과 집합 메타 데이터](../../../odbc/reference/develop-app/result-set-metadata.md)를 참조 하세요.  
  
 한 번만 실행되는 문에는 준비된 실행을 사용하지 않아야 합니다. 이러한 문의 경우 추가 ODBC 함수 호출이 필요 하기 때문에 직접 실행 보다 약간 느립니다.  
  
> [!IMPORTANT]  
>  **Sqlendtran** 을 명시적으로 호출 하거나 자동 커밋 모드로 작업 하 여 트랜잭션을 커밋하거나 롤백하는 경우 일부 데이터 원본에서 연결의 모든 문에 대 한 액세스 계획을 삭제 합니다. 자세한 내용은 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 함수 설명의 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 옵션을 참조 하세요.  
  
 문을 준비 하 고 실행 하려면 응용 프로그램은 다음과 같습니다.  
  
1.  **Sqlprepare** 를 호출 하 고 SQL 문을 포함 하는 문자열을 전달 합니다.  
  
2.  매개 변수의 값을 설정 합니다. 매개 변수는 문을 준비 하기 전이나 후에 실제로 설정할 수 있습니다. 자세한 내용은이 섹션의 뒷부분에 나오는 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)를 참조 하세요.  
  
3.  는 **Sqlexecute** 를 호출 하 고 데이터 페치와 같이 필요한 추가 처리를 수행 합니다.  
  
4.  필요에 따라 2 단계와 3 단계를 반복 합니다.  
  
5.  **Sqlprepare** 가 호출 되 면 드라이버는 다음과 같습니다.  
  
    -   문을 구문 분석 하지 않고 데이터 원본의 SQL 문법을 사용 하도록 SQL 문을 수정 합니다. 여기에는 [ODBC의 이스케이프 시퀀스](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)에 설명 된 이스케이프 시퀀스 바꾸기가 포함 됩니다. 응용 프로그램은 **SQLNativeSql**를 호출 하 여 SQL 문의 수정 된 형태를 검색할 수 있습니다. SQL_ATTR_NOSCAN statement 특성이 설정 된 경우 이스케이프 시퀀스는 대체 되지 않습니다.  
  
    -   준비를 위해 문을 데이터 원본으로 보냅니다.  
  
    -   반환 된 액세스 계획 식별자를 나중에 실행 하기 위해 저장 하거나 (준비에 성공한 경우) 오류를 반환 합니다 (준비에 실패 한 경우). 오류에는 SQLSTATE 42000 (구문 오류 또는 액세스 위반) 및 의미 체계 오류 (예: SQLSTATE 42S02 (기본 테이블 또는 뷰 없음))와 같은 구문 오류가 포함 됩니다.  
  
        > [!NOTE]  
        >  일부 드라이버는이 시점에서 오류를 반환 하지 않지만 문이 실행 되거나 카탈로그 함수가 호출 될 때 해당 오류를 반환 합니다. 따라서 실제로 실패 한 경우 **Sqlprepare** 가 성공한 것 처럼 보일 수 있습니다.  
  
6.  **Sqlexecute** 가 호출 되 면 드라이버는 다음과 같습니다.  
  
    -   현재 매개 변수 값을 검색 하 고 필요에 따라 변환 합니다. 자세한 내용은이 섹션의 뒷부분에 나오는 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)를 참조 하세요.  
  
    -   액세스 계획 식별자와 변환 된 매개 변수 값을 데이터 원본으로 보냅니다.  
  
    -   모든 오류를 반환 합니다. 일반적으로 SQLSTATE 24000 (잘못 된 커서 상태)와 같은 런타임 오류가 발생 합니다. 그러나이 시점에서 일부 드라이버는 구문 및 의미 체계 오류를 반환 합니다.  
  
 데이터 원본에서 문 준비를 지원 하지 않는 경우 드라이버는 가능한 범위에 해당 데이터를 에뮬레이션 해야 합니다. 예를 들어 **Sqlprepare** 가 호출 될 때 드라이버에서 아무 작업도 수행 하지 않을 수 있으며 **sqlprepare** 가 호출 될 때 문을 직접 실행 합니다.  
  
 데이터 원본에서 실행 하지 않고 구문 검사를 지 원하는 경우에는 **Sqlprepare** 가 호출 될 때 드라이버에서 문을 제출 하 고 **sqlprepare** 가 호출 될 때 실행할 문을 제출할 수 있습니다.  
  
 드라이버가 문 준비를 에뮬레이트할 수 없는 경우 **Sqlprepare** 가 호출 될 때 문을 저장 하 고 **sqlprepare** 를 호출할 때 실행을 위해 전송 합니다.  
  
 에뮬레이트된 문 준비는 완벽 하지 않으므로 **Sqlexecute** 는 **sqlexecute**에서 반환 하는 모든 오류를 반환할 수 있습니다.
