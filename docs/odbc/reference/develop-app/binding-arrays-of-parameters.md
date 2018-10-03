---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76f756b96a62a174e329614f9ab1baf634937522
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636872"
---
# <a name="binding-arrays-of-parameters"></a>매개 변수 배열 바인딩
매개 변수 배열을 사용 하는 응용 프로그램 SQL 문의 매개 변수는 배열을 바인딩합니다. 바인딩 스타일 두 가지가 있습니다.  
  
-   각 매개 변수에 배열을 바인딩하십시오. 각 데이터 구조 (배열)의 모든 데이터는 단일 매개 변수를 포함합니다. 이 이라고 *열 단위 바인딩을* 단일 매개 변수 값의 열에 바인딩되어 있기 때문에 있습니다.  
  
-   이러한 구조의 배열을 바인딩하고 매개 변수는 전체 집합에 대 한 매개 변수 데이터가 구조를 정의 합니다. 각 데이터 구조는 단일 SQL 문에 대 한 데이터를 포함합니다. 이 이라고 *행 단위 바인딩은* 매개 변수의 행 바인딩되기 때문에 있습니다.  
  
 호출 응용 프로그램 매개 변수를 단일 변수를 바인딩할 때 **SQLBindParameter** 배열 매개 변수를 바인딩할 합니다. 유일한 차이 전달 주소 배열 주소, 없습니다 단일 변수 주소. 응용 프로그램 사용 (기본값) 열 단위 또는 행 단위 바인딩은 인지 여부를 지정 하는 SQL_ATTR_PARAM_BIND_TYPE 문 특성을 설정 합니다. 응용 프로그램 기본 설정 하기에 열 단위 또는 행 단위 바인딩을 사용 여부입니다. 프로세서가 메모리에 액세스 하는 방법에 따라 행 단위 바인딩은 가속화할 수 있습니다. 그러나 차이점은 매우 많은 수의 매개 변수 행 제외 하 고 무시할 수 있습니다.  
  
## <a name="column-wise-binding"></a>열 단위 바인딩  
 열 단위 바인딩을 사용 하는 경우 응용 프로그램 하나 또는 두 개의 배열 데이터를 제공 하는 각 매개 변수에 바인딩합니다. 첫 번째 배열을 데이터 값을 보유 하 고 두 번째 배열 길이/표시기 버퍼 저장 키를 누릅니다. 각 배열 매개 변수에 대해 값이 있는 만큼의 요소가 포함 됩니다.  
  
 열 단위 바인딩은 기본값입니다. 응용 프로그램 수에서 변경할 수도 행 단위 바인딩은 열 단위 바인딩 SQL_ATTR_PARAM_BIND_TYPE 문 특성을 설정 하 여. 다음 그림에서는 어떻게 열 단위 바인딩의 작동 보여 줍니다.  
  
 ![표시 방법 열&#45;바인딩 작동 하는 것이 좋습니다](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 예를 들어, 다음 코드는 요소가 10 개인 배열을 PartID, 설명 및 가격 열에 대 한 매개 변수를 바인딩하고 10 개의 행을 삽입 하는 문을 실행 합니다. 열 단위 바인딩을 사용합니다.  
  
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
 행 단위 바인딩을 사용 하는 경우 응용 프로그램 각 매개 변수 집합에 대 한 구조를 정의 합니다. 구조는 각 매개 변수에 대 한 하나 또는 두 개의 요소가 있습니다. 첫 번째 요소에는 매개 변수 값을 보유 하 고 길이/표시기 버퍼를 보유 하는 두 번째 요소 키를 누릅니다. 그러면 응용 프로그램이 각 매개 변수에 대해 값이 있는 만큼의 요소가 포함 된 이러한 구조의 배열을 할당 합니다.  
  
 응용 프로그램 SQL_ATTR_PARAM_BIND_TYPE 문 특성을 사용 하 여 구조의 크기를 선언합니다. 응용 프로그램 배열의 첫 번째 구조의 주소 매개 변수를 바인딩합니다. 따라서 드라이버의 특정 행과 열 데이터 주소를 계산할 수 있습니다.  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 여기서 행은 매개 변수 집합의 크기에 1부터 매겨집니다. 오프셋을 정의 하는 경우에 SQL_ATTR_PARAM_BIND_OFFSET_PTR 문 특성에서 가리키는 값입니다. 다음 그림에서는 바인딩의 작동 하는 행 단위 하는 방법을 보여 줍니다. 매개 변수 순서에 관계 없이 구조에 적용할 수 있지만 쉽게 구별할 수 있도록 순서 대로 표시 됩니다.  
  
 ![표시 방법을 행&#45;바인딩 작동 하는 것이 좋습니다](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 다음 코드는 PartID, 설명 및 가격 열에 저장 하는 값에 대 한 요소를 사용 하 여 구조를 만듭니다. 그런 다음 이러한 구조는 요소가 10 개인 배열을 할당 하 고 행 단위 바인딩을 사용 하 여 PartID, 설명 및 가격 열에 대 한 매개 변수를 바인딩합니다. 그런 다음 10 개의 행을 삽입 하는 문을 실행 합니다.  
  
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
