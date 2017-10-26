---
title: "할당 하 고 버퍼를 해제 합니다. | Microsoft Docs"
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
- buffers [ODBC], allocating and freeing
- allocating buffers [ODBC]
- freeing buffers [ODBC]
ms.assetid: 886bc9ed-39d4-43d2-82ff-aebc35b14d39
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 73689fb95eb9b51e7f5f16b10c43256ef63f8dd2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="allocating-and-freeing-buffers"></a>할당 하 고 버퍼를 해제 합니다.
모든 버퍼가 할당 되 고 응용 프로그램에 의해 해제 됩니다. 버퍼를 연기 하지 되는 경우 함수에 대 한 호출 기간 동안 다만 필요 합니다. 예를 들어 **SQLGetInfo** 가리키는 버퍼에 특정 옵션과 관련 된 값을 반환 된 *InfoValuePtr* 인수입니다. 이 버퍼에 대 한 호출 직후 해제할 수 있도록 **SQLGetInfo**다음 코드 예제에 나온 것 처럼:  
  
```  
SQLSMALLINT   InfoValueLen;  
SQLCHAR *     InfoValuePtr = malloc(50);   // Allocate InfoValuePtr.  
  
SQLGetInfo(hdbc, SQL_DBMS_NAME, (SQLPOINTER)InfoValuePtr, 50,  
            &InfoValueLen);  
  
free(InfoValuePtr);                        // OK to free InfoValuePtr.  
```  
  
 지연 된 버퍼 하나의 함수에 지정 된 다른 사용 되는, 되므로 드라이버 여전히 기대에 존재 하는 동안 지연 된 버퍼를 해제할를 하면 응용 프로그램 프로그래밍 오류가 발생 합니다. 예를 들어의 주소는 \* *ValuePtr* 버퍼가 전달 될 **SQLBindCol** 에서 나중에 사용할 **SQLFetch**합니다. 열을 호출 하 여 같은 바인딩된 없을 때까지이 버퍼를 해제할 수 없습니다 **SQLBindCol** 또는 **SQLFreeStmt** 다음 코드 예제에 표시 된 대로:  
  
```  
SQLRETURN    rc;  
SQLINTEGER   ValueLenOrInd;  
SQLHSTMT     hstmt;  
  
// Allocate ValuePtr  
SQLCHAR * ValuePtr = malloc(50);  
  
// Bind ValuePtr to column 1. It is an error to free ValuePtr here.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, 50, &ValueLenOrInd);  
  
// Fetch each row of data and place the value for column 1 in *ValuePtr.  
// Code to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO   
// not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // It is an error to free ValuePtr here.  
}  
  
// Unbind ValuePtr from column 1.  It is now OK to free ValuePtr.  
SQLFreeStmt(hstmt, SQL_UNBIND);  
free(ValuePtr);  
```  
  
 함수에서 로컬로 버퍼를 선언 하 여 이러한 오류가 쉽게 발생 버퍼에는 응용 프로그램은 함수를 벗어날 때 해제 됩니다. 예를 들어 다음 코드는 드라이버에서 정의 되지 않은 및 아마도 심각한 동작을 발생합니다.  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
BindAColumn(hstmt);  
  
// Fetch each row of data and try to place the value for column 1 in  
// *ValuePtr. Because ValuePtr has been freed, the behavior is undefined  
// and probably fatal. Code to check if rc equals SQL_ERROR or   
// SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {}  
  
   .  
   .  
   .  
  
void BindAColumn(SQLHSTMT hstmt)  // WARNING! This function won't work!  
{  
   // Declare ValuePtr locally.  
   SQLCHAR      ValuePtr[50];  
   SQLINTEGER   ValueLenOrInd;  
  
   // Bind rgbValue to column.  
   SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr),  
               &ValueLenOrInd);  
  
   // ValuePtr is freed when BindAColumn exits.  
}  
```

