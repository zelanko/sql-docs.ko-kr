---
title: 길이 및 표시기 값 사용 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0c878c9038b26aa996ed206c6b8adfe8d6c21e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306764"
---
# <a name="using-length-and-indicator-values"></a>길이 및 표시기 값 사용
길이/표시기 버퍼는 데이터 버퍼의 바이트 길이 또는 데이터가 NULL임을 나타내는 SQL_NULL_DATA 같은 특수 표시기를 전달하는 데 사용됩니다. 사용되는 함수에 따라 길이/표시기 버퍼는 SQLINTEGER 또는 SQLSMALLINT로 정의됩니다. 따라서 이를 설명하려면 단일 인수가 필요합니다. 데이터 버퍼가 지연되지 않은 입력 버퍼인 경우 이 인수에는 데이터 자체의 바이트 길이 또는 표시기 값이 포함됩니다. 그것은 종종 *StrLen_or_Ind* 또는 유사한 이름입니다. 예를 들어 다음 코드는 **SQLPutData를** 호출하여 데이터로 가득 찬 버퍼를 전달합니다. 바이트 길이 *(ValueLen)는*데이터 버퍼 *(ValuePtr)가*입력 버퍼이기 때문에 직접 전달됩니다.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLen;  
  
// Call local function to place data in ValuePtr. In ValueLen, return the  
// number of bytes of data placed in ValuePtr. If there is not enough  
// data, this will be less than 50.  
FillBuffer(ValuePtr, sizeof(ValuePtr), &ValueLen);  
  
// Call SQLPutData to send the data to the driver.  
SQLPutData(hstmt, ValuePtr, ValueLen);  
```  
  
 데이터 버퍼가 지연된 입력 버퍼, 지연되지 않은 출력 버퍼 또는 출력 버퍼인 경우 인수에는 길이/표시기 버퍼의 주소가 포함됩니다. 그것은 종종 *StrLen_or_IndPtr* 또는 유사한 이름입니다. 예를 들어 다음 코드는 **SQLGetData를** 호출하여 데이터로 가득 찬 버퍼를 검색합니다. 바이트 길이는 길이/표시기*버퍼(ValueLenOrInd)에서*응용 프로그램에 반환되며, 해당 데이터*버퍼(ValuePtr)는*비연 출력 버퍼이기 때문에 해당 주소가 **SQLGetData에** 전달됩니다.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 특별히 금지되지 않는 한 길이/표시기 버퍼 인수는 0(지연되지 않은 입력인 경우) 또는 null 포인터(출력 또는 지연된 입력인 경우)일 수 있습니다. 입력 버퍼의 경우 드라이버가 데이터의 바이트 길이를 무시하게 됩니다. 이렇게 하면 가변 길이 데이터를 전달할 때 오류가 반환되지만 길이나 표시기 값이 필요하지 않으므로 null이 아닌 고정 길이 데이터를 전달할 때 일반적입니다. 출력 버퍼의 경우 드라이버가 데이터의 바이트 길이 또는 표시기 값을 반환하지 않습니다. 드라이버에서 반환되는 데이터가 NULL이지만 길이나 표시기 값이 필요하지 않으므로 고정 길이, null이 아닌 데이터를 검색할 때 일반적인 경우 오류입니다.  
  
 지연된 데이터 버퍼의 주소가 드라이버에 전달될 때와 마찬가지로 지연된 길이/표시기 버퍼의 주소는 버퍼가 언바운드될 때까지 유효해야 합니다.  
  
 다음 길이는 길이/표시기 값으로 유효합니다.  
  
-   *n*, *여기서 n* > 0입니다.  
  
-   0.  
  
-   SQL_NTS. 해당 데이터 버퍼의 드라이버에 전송된 문자열은 null-종료됩니다. 이는 C 프로그래머가 바이트 길이를 계산하지 않고도 문자열을 통과할 수 있는 편리한 방법입니다. 이 값은 응용 프로그램이 드라이버에 데이터를 보내는 경우에만 합법적입니다. 드라이버가 응용 프로그램에 데이터를 반환하면 항상 데이터의 실제 바이트 길이를 반환합니다.  
  
 다음 값은 길이/표시기 값으로 유효합니다. SQL_NULL_DATA SQL_DESC_INDICATOR_PTR 설명자 필드에 저장됩니다. 다른 모든 값은 SQL_DESC_OCTET_LENGTH_PTR 설명자 필드에 저장됩니다.  
  
-   SQL_NULL_DATA. 데이터는 NULL 데이터 값이며 해당 데이터 버퍼의 값은 무시됩니다. 이 값은 드라이버에서 보내거나 검색된 SQL 데이터에 대해서만 합법적입니다.  
  
-   SQL_DATA_AT_EXEC. 데이터 버퍼에는 데이터가 포함되어 있지 않습니다. 대신 문이 실행되거나 **SQLBulkOperations** 또는 **SQLSetPos가** 호출될 때 데이터가 **SQLPutData와** 함께 전송됩니다. 이 값은 드라이버에 전송된 SQL 데이터에 대해서만 합법적입니다. 자세한 내용은 [SQLBind매개 변수,](../../../odbc/reference/syntax/sqlbindparameter-function.md) [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)및 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)를 참조하십시오.  
  
-   SQL_LEN_DATA_AT_EXEC *(길이)* 매크로의 결과입니다. 이 값은 SQL_DATA_AT_EXEC 비슷합니다. 자세한 내용은 [긴 데이터 전송](../../../odbc/reference/develop-app/sending-long-data.md)을 참조하십시오.  
  
-   SQL_NO_TOTAL. 드라이버는 출력 버퍼에서 반환할 수 있는 긴 데이터의 바이트 수를 확인할 수 없습니다. 이 값은 드라이버에서 검색된 SQL 데이터에 대해서만 합법적입니다.  
  
-   SQL_DEFAULT_PARAM. 프로시저는 해당 데이터 버퍼의 값 대신 프로시저에서 입력 매개 변수의 기본값을 사용하는 것입니다.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** 또는 **SQLSetPos는** 데이터 버퍼의 값을 무시하는 것입니다. **SQLBulkOperations** 또는 **SQLSetPos를** 호출하여 데이터 행을 업데이트할 때 열 값은 변경되지 않습니다. **SQLBulkOperations를**호출하여 새 데이터 행을 삽입할 때 열 값이 기본값으로 설정되거나 열에 기본값이 없는 경우 NULL로 설정됩니다.
