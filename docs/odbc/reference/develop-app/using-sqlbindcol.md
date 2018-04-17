---
title: SQLBindCol를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
- SQLBindCol function [ODBC], using
ms.assetid: 17277ab3-33ad-44d3-a81c-a26b5e338512
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2e3329d1f5990edae9805538d6e9c5e4c563b028
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="using-sqlbindcol"></a>SQLBindCol를 사용 하 여
응용 프로그램 호출 하 여 열을 바인딩하는 **SQLBindCol**합니다. 이 함수는 한 번에 하나의 열을 바인딩합니다. 응용 프로그램이 다음을 지정합니다.  
  
-   열 번호입니다. 책갈피 열; 열 0입니다. 이 열은 일부 결과 집합에 포함 되지 않습니다. 다른 모든 열을 숫자 1부터 매겨집니다. 결과 집합의 열 수보다 번호가 높은 열을 바인딩할 오류가 발생 이 오류 감지할 수 없는 결과 집합이 만들어질 때까지 반환한 하므로 **SQLFetch**이 아니라 **SQLBindCol**합니다.  
  
-   변수의 C 데이터 형식, 주소 및 바이트 길이 열에 바인딩됩니다. SQL 데이터 형식의 열을 변환할 수 없습니다; C 데이터 형식을 지정 하면 오류가 발생 이 오류가 수 검색 되지 결과 집합이 만들어질 때까지 반환한 하므로 **SQLFetch**이 아니라 **SQLBindCol**합니다. 목록이 지원 되는 변환에 대 한 참조 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 부록 d: 데이터 형식에서입니다. 바이트 길이 대 한 정보를 참조 하십시오. [데이터 버퍼 길이](../../../odbc/reference/develop-app/data-buffer-length.md)합니다.  
  
-   길이/표시기 버퍼의 주소입니다. 길이/표시기 버퍼 선택 사항입니다. 데이터는 NULL 바이트 길이의 이진 또는 문자 데이터 또는 반환 SQL_NULL_DATA를 반환할 수 사용 됩니다. 자세한 내용은 참조 [길이/표시기 값을 사용 하 여](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)합니다.  
  
 때 **SQLBindCol** 은 호출 드라이버 연결이 정보는 문을 사용 하 여 합니다. 데이터의 각 행을 인출할 때 바인딩된 응용 프로그램 변수에서 각 열에 대 한 데이터를 배치 하는 정보를 사용 합니다.  
  
 예를 들어 다음 코드는 영업 사원 및 CustID 열에 변수를 바인딩합니다. 에 열에 대 한 데이터를 반환할 *판매원* 및 *CustID*합니다. 때문에 *판매원* 문자 버퍼는 드라이버를 데이터를 자를지 여부를 결정할 수 있도록 응용 프로그램 (11)의 바이트 길이 지정 합니다. 반환 된 바이트 길이 제목, 또는 NULL 인지에서 반환할 *SalesPersonLenOrInd*합니다.  
  
 때문에 *CustID* 정수 변수 이며 고정 길이 바이트 길이 지정할 필요가 없습니다; 드라이버가 것으로 간주 **sizeof (**SQLUINTEGER**)**합니다. 반환 된 고객의 바이트 길이 데이터, ID 또는 NULL 인지 여부에 반환 됩니다 *CustIDInd*합니다. 바이트 길이 항상 때문에 응용 프로그램의 급여가 NULL 인지 여부에 interested가 참고 **sizeof (**SQLUINTEGER**)**합니다.  
  
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
  
 다음 코드를 실행 하는 **선택** 문은 사용자가 입력 하 고 결과 집합의 데이터의 각 행을 출력 합니다. 응용 프로그램에서 결과의 셰이프를 예측할 수 없는 있기 때문에 설정 하 여 만든는 **선택** 문, 결과 집합 앞의 예제에서와 같이 하드 코드 된 변수에 바인딩할 수 없습니다. 대신, 응용 프로그램 같은 행의 각 열에 대 한 데이터를 보유 하는 버퍼 및 길이/표시기 버퍼를 할당 합니다. 각 열에 대 한 열에 대 한 메모리의 시작 부분에 오프셋을 계산이 오프셋을 조정 하는 열에 대 한 데이터 및 길이/표시기 버퍼 맞춤 경계에서 시작 합니다. 다음 열 오프셋에서 시작 하는 메모리를 바인딩합니다. 드라이버의 관점에서이 메모리의 주소 앞의 예제에서 바인딩된 변수의 주소를 구분 되지 않습니다. 정렬에 대 한 자세한 내용은 참조 [맞춤](../../../odbc/reference/develop-app/alignment.md)합니다.  
  
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
