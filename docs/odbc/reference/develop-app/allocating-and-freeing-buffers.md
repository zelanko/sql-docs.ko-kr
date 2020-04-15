---
title: 버퍼 할당 및 해제 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], allocating and freeing
- allocating buffers [ODBC]
- freeing buffers [ODBC]
ms.assetid: 886bc9ed-39d4-43d2-82ff-aebc35b14d39
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6aab888d24fcbc987b3db921436f14812618519
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288403"
---
# <a name="allocating-and-freeing-buffers"></a>버퍼 할당 및 해제
모든 버퍼는 응용 프로그램에서 할당되고 해제됩니다. 버퍼가 지연되지 않으면 함수에 대한 호출 기간 동안만 존재합니다. 예를 **들어, SQLGetInfo** *InfoValuePtr* 인수에 의해 가리키는 버퍼에서 특정 옵션과 관련 된 값을 반환 합니다. 다음 코드 예제와 같이 **SQLGetInfo를**호출한 직후이 버퍼를 해제할 수 있습니다.  
  
```  
SQLSMALLINT   InfoValueLen;  
SQLCHAR *     InfoValuePtr = malloc(50);   // Allocate InfoValuePtr.  
  
SQLGetInfo(hdbc, SQL_DBMS_NAME, (SQLPOINTER)InfoValuePtr, 50,  
            &InfoValueLen);  
  
free(InfoValuePtr);                        // OK to free InfoValuePtr.  
```  
  
 지연 된 버퍼는 한 함수에 지정 하 고 다른 함수에서 사용 하기 때문에 드라이버가 여전히 존재 를 기대 하는 동안 지연 된 버퍼를 해제 하는 응용 프로그램 프로그래밍 오류입니다. 예를 들어 \* *ValuePtr* 버퍼의 주소는 **SQLBindCol에서** 나중에 사용할 수 있도록 **SQLBindCol에**전달됩니다. 다음 코드 예제와 같이 **SQLBindCol** 또는 **SQLFreeStmt에** 대한 호출과 같이 열이 언바운드될 때까지 이 버퍼를 해제할 수 없습니다.  
  
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
  
 이러한 오류는 함수에서 로컬로 버퍼를 선언하여 쉽게 이루어집니다. 버퍼는 응용 프로그램이 함수를 떠날 때 해제됩니다. 예를 들어 다음 코드로 인해 드라이버에서 정의되지 않고 치명적인 동작이 발생합니다.  
  
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
