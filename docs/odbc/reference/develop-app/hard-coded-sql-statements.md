---
title: 하드 코드 된 SQL 문 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7a092742e5f0151b7b08f434b453645cbd804a5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300203"
---
# <a name="hard-coded-sql-statements"></a>하드 코딩된 SQL 문
고정 태스크를 수행 하는 응용 프로그램은 일반적으로 하드 코드 된 SQL 문을 포함 합니다. 예를 들어 주문 입력 시스템은 다음 호출을 사용 하 여 오픈 판매 주문을 나열할 수 있습니다.  
  
```  
SQLExecDirect(hstmt, "SELECT OrderID FROM Orders WHERE Status = 'OPEN'", SQL_NTS);  
```  
  
 하드 코드 된 SQL 문에는 다음과 같은 몇 가지 이점이 있습니다. 응용 프로그램을 작성할 때 테스트할 수 있습니다. 런타임에 생성 된 문 보다 구현 하는 것이 더 간단 합니다. 그리고 응용 프로그램을 단순화 합니다.  
  
 문 매개 변수를 사용 하 고 문을 준비 하면 하드 코드 된 SQL 문을 사용 하는 것이 훨씬 더 나은 방법을 제공 합니다. 예를 들어 Parts 테이블에 PartID, 설명 및 가격 열이 포함 되어 있다고 가정 합니다. 이 테이블에 새 행을 삽입 하는 한 가지 방법은 **insert** 문을 생성 하 고 실행 하는 것입니다.  
  
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
  
 하드 코드 된 매개 변수가 있는 문을 사용 하는 것이 훨씬 더 좋은 방법입니다. 여기에는 하드 코드 된 데이터 값이 있는 문에 비해 두 가지 이점이 있습니다. 첫째, 데이터 값을 문자열로 변환 하는 대신 정수 및 부동 소수점 숫자와 같은 네이티브 형식으로 보낼 수 있으므로 매개 변수가 있는 문을 생성 하는 것이 더 쉽습니다. 둘째, 매개 변수 값을 변경 하 고 다시 실행 하는 것 만으로 이러한 문을 두 번 이상 사용할 수 있습니다. 다시 빌드할 필요가 없습니다.  
  
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
  
 이 문이 두 번 이상 실행 되는 것으로 가정 하면 훨씬 더 높은 효율성을 위해 준비할 수 있습니다.  
  
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
  
 문을 사용 하는 가장 효율적인 방법은 다음 코드 예제와 같이 문을 포함 하는 프로시저를 생성 하는 것입니다. 프로시저는 개발 시에 생성 되 고 데이터 소스에 저장 되므로 런타임에 준비할 필요가 없습니다. 이 방법의 단점은 프로시저를 만들기 위한 구문이 DBMS에 따라 달라 지 며, 응용 프로그램이 실행 되는 각 DBMS에 대해 프로시저를 별도로 생성 해야 한다는 것입니다.  
  
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
  
 매개 변수, 준비 된 문 및 프로시저에 대 한 자세한 내용은 [문 실행](../../../odbc/reference/develop-app/executing-a-statement.md)을 참조 하세요.
