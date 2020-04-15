---
title: 하드 코딩된 SQL 문 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300203"
---
# <a name="hard-coded-sql-statements"></a>하드 코딩된 SQL 문
고정 된 작업을 수행 하는 응용 프로그램에 대 한 하드 코딩 된 SQL 문을 포함 합니다. 예를 들어 주문 입력 시스템은 다음 호출을 사용하여 열린 판매 주문을 나열할 수 있습니다.  
  
```  
SQLExecDirect(hstmt, "SELECT OrderID FROM Orders WHERE Status = 'OPEN'", SQL_NTS);  
```  
  
 하드 코딩된 SQL 문에는 몇 가지 장점이 있습니다. 런타임에 생성된 문보다 구현하기가 더 간단합니다. 응용 프로그램을 단순화합니다.  
  
 문 매개 변수를 사용하고 문 준비 문을 사용하면 하드 코딩된 SQL 문을 사용하는 더 나은 방법을 사용할 수 있습니다. 예를 들어 부품 테이블에 PartID, 설명 및 가격 열이 포함되어 있다고 가정합니다. 이 테이블에 새 행을 삽입하는 한 가지 방법은 **INSERT** 문을 생성하고 실행하는 것입니다.  
  
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
  
 더 좋은 방법은 하드 코딩된 매개 변수화된 문을 사용하는 것입니다. 이 경우 하드 코딩된 데이터 값이 있는 문보다 두 가지 장점이 있습니다. 첫째, 데이터 값을 문자열로 변환하는 대신 정수 및 부동 점 번호와 같은 네이티브 형식에서 보낼 수 있으므로 매개 변수로 된 문을 생성하는 것이 더 쉽습니다. 둘째, 이러한 문은 매개 변수 값을 변경하고 다시 실행하여 두 번 이상 사용할 수 있습니다. 다시 빌드할 필요가 없습니다.  
  
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
  
 이 명령문이 두 번 이상 실행될 것이라고 가정하면 효율성을 훨씬 높일 수 있습니다.  
  
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
  
 다음 코드 예제와 같이 문을 포함하는 프로시저를 구성하는 것이 문을 사용하는 가장 효율적인 방법일 수 있습니다. 프로시저는 개발 시점에 생성되고 데이터 원본에 저장되므로 런타임에 준비할 필요가 없습니다. 이 메서드의 단점은 프로시저 만들기구문이 DBMS에 따라 다르며 응용 프로그램이 실행되는 각 DBMS에 대해 프로시저를 별도로 구성해야 한다는 것입니다.  
  
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
  
 매개 변수, 준비된 명령문 및 절차에 대한 자세한 내용은 [명령문 실행 을](../../../odbc/reference/develop-app/executing-a-statement.md)참조하십시오.
