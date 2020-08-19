---
description: SQLBindCol 사용
title: SQLBindCol 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
- SQLBindCol function [ODBC], using
ms.assetid: 17277ab3-33ad-44d3-a81c-a26b5e338512
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f68aa647f600709dd1a4b989cdab8153775f0aaa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421447"
---
# <a name="using-sqlbindcol"></a>SQLBindCol 사용
응용 프로그램은 **SQLBindCol**를 호출 하 여 열을 바인딩합니다. 이 함수는 한 번에 하나의 열을 바인딩합니다. 응용 프로그램은 다음을 지정 합니다.  
  
-   열 번호입니다. 열 0은 책갈피 열입니다. 이 열은 일부 결과 집합에 포함 되지 않습니다. 다른 모든 열은 숫자 1부터 시작 하 여 번호가 매겨집니다. 결과 집합의 열 수보다 번호가 높은 열을 바인딩하는 것은 오류입니다. 결과 집합이 생성 될 때까지이 오류를 검색할 수 없으므로 **SQLBindCol**가 아니라 **sqlfetch**에 의해 반환 됩니다.  
  
-   열에 바인딩된 변수의 C 데이터 형식, 주소 및 바이트 길이입니다. 열의 SQL 데이터 형식을 변환할 수 없는 C 데이터 형식을 지정 하는 것은 오류입니다. 이 오류는 결과 집합이 생성 될 때까지 검색 되지 않을 수 있으므로 **SQLBindCol**가 아니라 **sqlfetch**에 의해 반환 됩니다. 지원 되는 변환 목록은 부록 D: 데이터 형식에서 [SQL에서 C 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 을 참조 하세요. 바이트 길이에 대 한 자세한 내용은 [데이터 버퍼 길이](../../../odbc/reference/develop-app/data-buffer-length.md)를 참조 하세요.  
  
-   길이/표시기 버퍼의 주소입니다. 길이/표시기 버퍼는 선택 사항입니다. 이진 또는 문자 데이터의 바이트 길이를 반환 하거나 데이터가 NULL 인 경우 SQL_NULL_DATA을 반환 하는 데 사용 됩니다. 자세한 내용은 [길이/표시기 값 사용](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)을 참조 하세요.  
  
 **SQLBindCol** 가 호출 되 면 드라이버는이 정보를 문과 연결 합니다. 데이터의 각 행이 인출 되 면 정보를 사용 하 여 바인딩된 응용 프로그램 변수의 각 열에 대 한 데이터를 저장 합니다.  
  
 예를 들어 다음 코드는 변수를 판매원 및 CustID 열에 바인딩합니다. 열에 대 한 데이터는 *판매 직원과* *CustID*에서 반환 됩니다. *판매원이* 문자 버퍼 이므로 응용 프로그램에서 바이트 길이 (11)를 지정 하 여 드라이버에서 데이터를 잘라낼 지 여부를 결정할 수 있도록 합니다. 반환 된 제목의 바이트 길이 또는 NULL 인지 여부는 *SalesPersonLenOrInd*에서 반환 됩니다.  
  
 *CustID* 는 정수 변수이 고 길이가 고정 되어 있기 때문에 해당 바이트 길이를 지정할 필요가 없습니다. 드라이버는 **sizeof (** SQLUINTEGER **)** 라고 가정 합니다. 반환 된 고객 ID 데이터의 바이트 길이 또는 NULL 인지 여부는 *CustIDInd*에서 반환 됩니다. 바이트 길이가 항상 **sizeof (** SQLUINTEGER **)** 이기 때문에 응용 프로그램은 급여의 NULL 여부에만 관심이 있습니다.  
  
```  
SQLCHAR       SalesPerson[11];  
SQLUINTEGER   CustID;  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLRETURN     rc;  
SQLHSTMT      hstmt;  
  
// Bind SalesPerson to the SalesPerson column and CustID to the   
// CustID column.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, SalesPerson, sizeof(SalesPerson),  
            &SalesPersonLenOrInd);  
SQLBindCol(hstmt, 2, SQL_C_ULONG, &CustID, 0, &CustIDInd);  
  
// Execute a statement to get the sales person/customer of all orders.  
SQLExecDirect(hstmt, "SELECT SalesPerson, CustID FROM Orders ORDER BY SalesPerson",  
               SQL_NTS);  
  
// Fetch and print the data. Print "NULL" if the data is NULL. Code to   
// check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (SalesPersonLenOrInd == SQL_NULL_DATA)   
            printf("NULL                     ");  
   else   
            printf("%10s   ", SalesPerson);  
   if (CustIDInd == SQL_NULL_DATA)   
         printf("NULL\n");  
   else   
            printf("%d\n", CustID);  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 다음 코드는 사용자가 입력 한 **select** 문을 실행 하 고 결과 집합에서 데이터의 각 행을 출력 합니다. 응용 프로그램은 **SELECT** 문에 의해 생성 된 결과 집합의 셰이프를 예측할 수 없으므로 앞의 예제와 같이 하드 코드 된 변수를 결과 집합에 바인딩할 수 없습니다. 대신, 응용 프로그램은 해당 행의 각 열에 대 한 데이터 및 길이/표시 버퍼를 포함 하는 버퍼를 할당 합니다. 각 열에 대해 해당 열에 대 한 메모리의 시작에 대 한 오프셋을 계산 하 고 해당 열에 대 한 데이터 및 길이/표시기 버퍼가 맞춤 경계에서 시작 되도록이 오프셋을 조정 합니다. 그런 다음 오프셋에서 시작 하 여 메모리를 열에 바인딩합니다. 드라이버의 관점에서이 메모리의 주소는 앞의 예제에서 바인딩된 변수의 주소와 구분할 수 없습니다. 맞춤에 대 한 자세한 내용은 [맞춤](../../../odbc/reference/develop-app/alignment.md)을 참조 하십시오.  
  
```  
// This application allocates a buffer at run time. For each column, this   
// buffer contains memory for the column's data and length/indicator.   
// For example:  
//      column 1         column 2      column 3      column 4  
// <------------><---------------><-----><------------>  
//      db1   li1   db2   li2   db3   li3   db4   li4  
//      |      |      |      |      |      |      |         |  
//      _____V_____V________V_______V___V___V______V_____V_  
// |__________|__|_____________|__|___|__|__________|__|  
//  
// dbn = data buffer for column n  
// lin = length/indicator buffer for column n  
  
// Define a macro to increase the size of a buffer so that it is a   
// multiple of the alignment size. Thus, if a buffer starts on an   
// alignment boundary, it will end just before the next alignment   
// boundary. In this example, an alignment size of 4 is used because   
// this is the size of the largest data type used in the application's   
// buffer--the size of an SDWORD and of the largest default C data type   
// are both 4. If a larger data type (such as _int64) was used, it would   
// be necessary to align for that size.  
#define ALIGNSIZE 4  
#define ALIGNBUF(Length) Length % ALIGNSIZE ? \  
                  Length + ALIGNSIZE - (Length % ALIGNSIZE) : Length  
  
SQLCHAR        SelectStmt[100];  
SQLSMALLINT    NumCols, *CTypeArray, i;  
SQLINTEGER *   ColLenArray, *OffsetArray, SQLType, *DataPtr;  
SQLRETURN      rc;   
SQLHSTMT       hstmt;  
  
// Get a SELECT statement from the user and execute it.  
GetSelectStmt(SelectStmt, 100);  
SQLExecDirect(hstmt, SelectStmt, SQL_NTS);  
  
// Determine the number of result set columns. Allocate arrays to hold   
// the C type, byte length, and buffer offset to the data.  
SQLNumResultCols(hstmt, &NumCols);  
CTypeArray = (SQLSMALLINT *) malloc(NumCols * sizeof(SQLSMALLINT));  
ColLenArray = (SQLINTEGER *) malloc(NumCols * sizeof(SQLINTEGER));  
OffsetArray = (SQLINTEGER *) malloc(NumCols * sizeof(SQLINTEGER));  
  
OffsetArray[0] = 0;  
for (i = 0; i < NumCols; i++) {  
   // Determine the column's SQL type. GetDefaultCType contains a switch   
   // statement that returns the default C type for each SQL type.  
   SQLColAttribute(hstmt, ((SQLUSMALLINT) i) + 1, SQL_DESC_TYPE, NULL, 0, NULL, (SQLPOINTER) &SQLType);  
   CTypeArray[i] = GetDefaultCType(SQLType);  
  
   // Determine the column's byte length. Calculate the offset in the   
   // buffer to the data as the offset to the previous column, plus the   
   // byte length of the previous column, plus the byte length of the   
   // previous column's length/indicator buffer. Note that the byte   
   // length of the column and the length/indicator buffer are increased   
   // so that, assuming they start on an alignment boundary, they will  
   // end on the byte before the next alignment boundary. Although this   
   // might leave some holes in the buffer, it is a relatively   
   // inexpensive way to guarantee alignment.  
   SQLColAttribute(hstmt, ((SQLUSMALLINT) i)+1, SQL_DESC_OCTET_LENGTH, NULL, 0, NULL, &ColLenArray[i]);  
   ColLenArray[i] = ALIGNBUF(ColLenArray[i]);  
   if (i)  
      OffsetArray[i] = OffsetArray[i-1]+ColLenArray[i-1]+ALIGNBUF(sizeof(SQLINTEGER));  
}  
  
// Allocate the data buffer. The size of the buffer is equal to the   
// offset to the data buffer for the final column, plus the byte length   
// of the data buffer and length/indicator buffer for the last column.  
void *DataPtr = malloc(OffsetArray[NumCols - 1] +  
               ColLenArray[NumCols - 1] + ALIGNBUF(sizeof(SQLINTEGER)));  
  
// For each column, bind the address in the buffer at the start of the   
// memory allocated for that column's data and the address at the start   
// of the memory allocated for that column's length/indicator buffer.  
for (i = 0; i < NumCols; i++)  
   SQLBindCol(hstmt,  
            ((SQLUSMALLINT) i) + 1,  
            CTypeArray[i],  
            (SQLPOINTER)((SQLCHAR *)DataPtr + OffsetArray[i]),  
            ColLenArray[i],  
            (SQLINTEGER *)((SQLCHAR *)DataPtr + OffsetArray[i] + ColLenArray[i]));  
  
// Retrieve and print each row. PrintData accepts a pointer to the data,   
// its C type, and its byte length/indicator. It contains a switch   
// statement that casts and prints the data according to its type. Code   
// to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   for (i = 0; i < NumCols; i++) {  
      PrintData((SQLCHAR *)DataPtr[OffsetArray[i]], CTypeArray[i],  
               (SQLINTEGER *)((SQLCHAR *)DataPtr[OffsetArray[i] + ColLenArray[i]]));  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
