---
description: 매개 변수 배열 바인딩
title: 매개 변수 배열 바인딩 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameter arrays [ODBC]
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 037afe23-052d-4f3a-8aa7-45302b199ad0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 529ea49d2697ffcf7b89217746420ab5cb298890
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429485"
---
# <a name="binding-arrays-of-parameters"></a>매개 변수 배열 바인딩
매개 변수 배열을 사용 하는 응용 프로그램은 배열을 SQL 문의 매개 변수에 바인딩합니다. 다음과 같은 두 가지 바인딩 스타일이 있습니다.  
  
-   각 매개 변수에 배열을 바인딩합니다. 각 데이터 구조 (배열)에는 단일 매개 변수에 대 한 모든 데이터가 포함 됩니다. 이는 단일 매개 변수에 대 한 값 열을 바인딩되기 때문에 *열 단위 바인딩* 이라고 합니다.  
  
-   전체 매개 변수 집합에 대 한 매개 변수 데이터를 포함 하는 구조체를 정의 하 고 이러한 구조체의 배열을 바인딩합니다. 각 데이터 구조에는 단일 SQL 문에 대 한 데이터가 포함 됩니다. 이는 매개 변수 행을 바인딩하기 때문에 *행 단위 바인딩* 이라고 합니다.  
  
 응용 프로그램이 단일 변수를 매개 변수에 바인딩하는 것 처럼 **SQLBindParameter** 를 호출 하 여 배열을 매개 변수에 바인딩합니다. 유일한 차이점은 전달 된 주소가 단일 변수 주소가 아니라 배열 주소 이기 때문입니다. 응용 프로그램은 SQL_ATTR_PARAM_BIND_TYPE statement 특성을 설정 하 여 열 단위 (기본값) 또는 행 단위 바인딩을 사용할지 여부를 지정 합니다. 열 단위 또는 행 단위 바인딩을 사용할지 여부는 주로 응용 프로그램 기본 설정에 따라 결정 됩니다. 프로세서가 메모리에 액세스 하는 방법에 따라 행 단위 바인딩이 더 빠를 수 있습니다. 그러나 매우 많은 수의 매개 변수 행을 제외 하 고 차이점은 무시할 수 있습니다.  
  
## <a name="column-wise-binding"></a>열 단위 바인딩  
 열 단위 바인딩을 사용 하는 경우 응용 프로그램은 데이터를 제공할 각 매개 변수에 하나 또는 두 개의 배열을 바인딩합니다. 첫 번째 배열에는 데이터 값이 포함 되 고 두 번째 배열에는 길이/표시기 버퍼가 포함 됩니다. 각 배열에는 매개 변수에 대 한 값 만큼의 요소가 포함 되어 있습니다.  
  
 열 단위 바인딩은 기본값입니다. 응용 프로그램은 SQL_ATTR_PARAM_BIND_TYPE statement 특성을 설정 하 여 행 단위 바인딩에서 열 단위 바인딩으로 변경할 수도 있습니다. 다음 그림에서는 열 단위 바인딩의 작동 방식을 보여 줍니다.  
  
 ![열&#45;의 바인딩 작동 방식을 보여 줍니다.](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 예를 들어 다음 코드는 10 개의 요소 배열을 PartID, Description 및 Price 열의 매개 변수에 바인딩하고 문을 실행 하 여 10 개의 행을 삽입 합니다. 열 단위 바인딩을 사용 합니다.  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
                                                "VALUES (?, ?, ?)";  
SQLUINTEGER    PartIDArray[ARRAY_SIZE];  
SQLCHAR        DescArray[ARRAY_SIZE][DESC_LEN];  
SQLREAL        PriceArray[ARRAY_SIZE];  
SQLINTEGER     PartIDIndArray[ARRAY_SIZE], DescLenOrIndArray[ARRAY_SIZE],  
               PriceIndArray[ARRAY_SIZE];  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
memset(DescLenOrIndArray, 0, sizeof(DescLenOrIndArray));  
memset(PartIDIndArray, 0, sizeof(PartIDIndArray));  
memset(PriceIndArray, 0, sizeof(PriceIndArray));  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, SQL_PARAM_BIND_BY_COLUMN, 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in column-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  PartIDArray, 0, PartIDIndArray);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  DescArray, DESC_LEN, DescLenOrIndArray);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  PriceArray, 0, PriceIndArray);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartIDArray[i], DescArray[i], &PriceArray[i]);  
   PartIDIndArray[i] = 0;  
   DescLenOrIndArray[i] = SQL_NTS;  
   PriceIndArray[i] = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
}  
```  
  
## <a name="row-wise-binding"></a>행 단위 바인딩  
 행 단위 바인딩을 사용 하는 경우 응용 프로그램은 각 매개 변수 집합에 대 한 구조를 정의 합니다. 구조체에는 각 매개 변수에 대해 하나 또는 두 개의 요소가 포함 되어 있습니다. 첫 번째 요소는 매개 변수 값을 보유 하 고, 두 번째 요소는 길이/지표 버퍼를 보유 합니다. 그런 다음 응용 프로그램은 각 매개 변수에 대 한 값 만큼의 요소를 포함 하는 이러한 구조체의 배열을 할당 합니다.  
  
 응용 프로그램은 SQL_ATTR_PARAM_BIND_TYPE statement 특성을 사용 하 여 구조 크기를 드라이버에 선언 합니다. 응용 프로그램은 배열의 첫 번째 구조에 있는 매개 변수의 주소를 바인딩합니다. 따라서 드라이버는 특정 행 및 열에 대 한 데이터 주소를  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 행 번호는 1에서 매개 변수 집합의 크기 사이입니다. 오프셋 (정의 된 경우)은 SQL_ATTR_PARAM_BIND_OFFSET_PTR statement 특성이 가리키는 값입니다. 다음 그림에서는 행 단위 바인딩의 작동 방식을 보여 줍니다. 매개 변수는 임의의 순서로 구조에 배치 될 수 있지만 명확 하 게 나타내기 위해 순서 대로 표시 됩니다.  
  
 ![행&#45;의 바인딩 작동 방식을 보여 줍니다.](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 다음 코드는 PartID, 설명 및 가격 열에 저장할 값의 요소가 포함 된 구조체를 만듭니다. 그런 다음 이러한 구조체의 10 개 요소 배열을 할당 하 고 행 단위 바인딩을 사용 하 여 PartID, 설명 및 가격 열의 매개 변수에 바인딩합니다. 그런 다음 문을 실행 하 여 10 개의 행을 삽입 합니다.  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
typedef tagPartStruct {  
   SQLREAL       Price;  
   SQLUINTEGER   PartID;  
   SQLCHAR       Desc[DESC_LEN];  
   SQLINTEGER    PriceInd;  
   SQLINTEGER    PartIDInd;  
   SQLINTEGER    DescLenOrInd;  
} PartStruct;  
  
PartStruct PartArray[ARRAY_SIZE];  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  
                Price) "  
               "VALUES (?, ?, ?)";  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, sizeof(PartStruct), 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in row-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartArray[0].PartID, 0, &PartArray[0].PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  PartArray[0].Desc, DESC_LEN, &PartArray[0].DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &PartArray[0].Price, 0, &PartArray[0].PriceInd);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartArray[i].PartID, PartArray[i].Desc, &PartArray[i].Price);  
   PartArray[0].PartIDInd = 0;  
   PartArray[0].DescLenOrInd = SQL_NTS;  
   PartArray[0].PriceInd = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
```
