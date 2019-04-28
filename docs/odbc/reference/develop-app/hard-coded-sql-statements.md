---
title: 하드 코드 된 SQL 문을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], hard-coded
- hard-coded SQL statements [ODBC]
- SQL statements [ODBC], constructing
ms.assetid: e355f5f1-4f1a-4933-8c74-ee73e90d2d19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 383a81aea121882b334bbfdab806408ac0513893
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724218"
---
# <a name="hard-coded-sql-statements"></a>하드 코딩된 SQL 문
일반적으로 고정 된 작업을 수행 하는 응용 프로그램에 하드 코딩 된 SQL 문을 포함 합니다. 예를 들어 주문 입력 시스템을 열고 판매 주문 목록 다음 호출을 사용할 수 있습니다.  
  
```  
SQLExecDirect(hstmt, "SELECT OrderID FROM Orders WHERE Status = 'OPEN'", SQL_NTS);  
```  
  
 하드 코드 된 SQL 문에 장점은 다음과 같습니다. 응용 프로그램; 쓰면 테스트할 수 있습니다. 간단 하 게; 런타임에 생성 하는 문을 보다 구현 및 응용 프로그램을 간소화할 수 있습니다.  
  
 문 준비와 문 매개 변수를 사용 하 여 하드 코드 된 SQL 문을 사용 하 여 더 나은 방법 제공 합니다. 예를 들어 부품 테이블 PartID, 설명 및 가격 열을 포함 합니다. 이 테이블에 새 행을 삽입 하는 한 가지 방법은 생성 하 고 실행 하는 것을 **삽입** 문:  
  
```  
#define DESC_LEN 51  
#define STATEMENT_LEN 51  
  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN], Statement[STATEMENT_LEN];  
SQLREAL       Price;  
  
// Set part ID, description, and price.  
GetNewValues(&PartID, Desc, &Price);  
  
// Build INSERT statement.  
sprintf_s(Statement, 100, "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (%d, '%s', %f)", PartID, Desc, Price);  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
```  
  
 더 좋은 방법은 하드 코드 된, 매개 변수가 있는 문을 사용 하는 경우 이 하드 코드 된 데이터 값을 사용 하 여 문 다음 두 가지 장점이 있습니다. 첫째, 데이터 값에 정수 및 부동 소수점 숫자 보다는 문자열로 변환 하기와 같은 원시 형식으로 보낼 수 있으므로 매개 변수가 있는 문을 생성 하기 쉽습니다. 둘째, 이러한 문을 사용할 수 한 번만 매개 변수 값을 변경 하 고, 종료할지 하면 다시 않아도가 됩니다.  
  
```  
#define DESC_LEN 51  
  
SQLCHAR * Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (?, ?, ?)";  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Set part ID, description, and price.  
GetNewValues(&PartID, Desc, &Price);  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
```  
  
 으로 가정 하 고이 문을 두 번 이상 실행할 효율성도 향상을 위해 준비 될 것:  
  
```  
#define DESC_LEN 51  
  
SQLCHAR *Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
         "VALUES (?, ?, ?)";  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Prepare the INSERT statement.  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Loop to continually get new values and insert them.  
while (GetNewValues(&PartID, Desc, &Price))  
   SQLExecute(hstmt);  
```  
  
 아마도 문을 사용 하는 가장 효율적인 방법은 다음 코드 예제와 같이 문을 포함 하는 프로시저를 만드는 것입니다. 절차는 개발 시에 생성 되 고 데이터 원본에 저장 된, 때문에 런타임에 준비가 필요 하지 않습니다. 이 메서드는 단점은 프로시저를 만드는 구문은 특정 DBMS를 실행 하는 응용 프로그램에는 각 DBMS에 대 한 절차를 별도로 생성 해야 합니다.  
  
```  
#define DESC_LEN 51  
  
SQLUINTEGER   PartID;  
SQLCHAR       Desc[DESC_LEN];  
SQLREAL       Price;  
SQLINTEGER    PartIDInd = 0, DescLenOrInd = SQL_NTS, PriceInd = 0;  
  
// Bind the parameters.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartID, 0, &PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  Desc, sizeof(Desc), &DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
  
// Loop to continually get new values and insert them.  
while (GetNewValues(&PartID, Desc, &Price))  
   SQLExecDirect(hstmt, "{call InsertPart(?, ?, ?)}", SQL_NTS);  
```  
  
 매개 변수, 준비 된 문 및 프로시저에 대 한 자세한 내용은 참조 하세요. [문을 실행](../../../odbc/reference/develop-app/executing-a-statement.md)합니다.
