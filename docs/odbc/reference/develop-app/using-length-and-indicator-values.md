---
title: 길이 표시기 값을 사용 하 여 | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aa4cb7310d579fb787a3e08da8e309d4e5c6e4d1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-length-and-indicator-values"></a>길이 표시기 값을 사용 하 여
길이/표시기 버퍼 데이터 버퍼 또는 데이터가 NULL 인지 여부를 나타내는 SQL_NULL_DATA 등 특별 한 표시기에 있는 데이터의 바이트 길이 전달 하는 데 사용 됩니다. 사용 되는 함수에 따라 길이/표시기 버퍼는 SQLINTEGER 또는 SQLSMALLINT 되도록 정의 됩니다. 따라서을 설명 하는 하나의 인수가 필요 합니다. 데이터 버퍼가 nondeferred 입력된 버퍼 경우이 인수 자체 데이터의 바이트 길이 또는 표시기 값을 포함 합니다. 종종 라는 *StrLen_or_Ind* 또는 비슷한 이름입니다. 예를 들어 다음 코드 호출 **SQLPutData** 버퍼를 전달할 데이터의 전체; 바이트 길이 (*ValueLen*) 때문에 직접 전달 데이터 버퍼 (*ValuePtr*)은 입력된 버퍼입니다.  
  
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
  
 데이터 버퍼가 지연 된 입력된 버퍼, nondeferred 출력 버퍼를 또는 출력 버퍼로 인수 길이/표시기 버퍼의 주소를 포함 합니다. 종종 라는 *StrLen_or_IndPtr* 또는 비슷한 이름입니다. 예를 들어 다음 코드 호출 **SQLGetData** 검색 데이터의 전체 버퍼를 바이트 길이 길이/표시기 버퍼에서 응용 프로그램에 반환 됩니다 (*ValueLenOrInd*), 해당 주소는 에 전달 된 **SQLGetData** 때문에 일치 하는 데이터 버퍼 (*ValuePtr*) nondeferred 출력 버퍼입니다.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 길이/표시기 버퍼 인수는 0 일 수 있습니다는 구체적으로 금지 하지 않는 한 (경우 nondeferred 입력) 또는 null 포인터 (하는 경우 출력 또는 지연 된 입력). 입력된 버퍼에 대 한이 인해는 드라이버는 데이터의 바이트 길이 무시 하도록 합니다. 가변 길이 데이터를 전달 하는 경우 오류가 반환 이지만이 일반적인 null이 아닌 고정 길이 데이터를 전달할 때 길이 아니고 표시기 값이 필요 하기 때문에 있습니다. 출력 버퍼에 대 한 드라이버를 표시기 값 또는 데이터의 바이트 길이 반환 하지 그러면 합니다. 드라이버에서 반환 되는 데이터는 NULL 이지만 일반적인 고정 길이, null이 아닌 데이터를 검색할 때 길이 아니고 표시기 값 필요 하므로 하는 경우는 오류입니다.  
  
 대로 드라이버에는 지연 된 데이터 버퍼의 주소에 대 한 전달, 버퍼가 바인딩된 때까지 지연된 길이/표시기 버퍼의 주소 유효한 상태로 유지 되어야 합니다.  
  
 다음과 같은 길이 길이/표시기 값으로 사용할 수 있습니다.  
  
-   *n*여기서 *n* > 0입니다.  
  
-   0.  
  
-   SQL_NTS 합니다. 해당 하는 데이터 버퍼의 드라이버에 전송 하는 문자열은 null로 끝나는; 이것이 문자열을 전달 하 고 바이트 길이 계산 하지 않고 C 프로그래머를 위한 편리한 방법입니다. 이 값은 드라이버에 데이터를 보낼 때에 유효 합니다. 드라이버 데이터 응용 프로그램에 반환 될 때 항상 데이터의 실제 바이트 길이 반환 합니다.  
  
 다음 값은 길이/표시기 값으로 유효 합니다. SQL_NULL_DATA는 SQL_DESC_INDICATOR_PTR 설명자 필드;에 저장 다른 모든 값은 SQL_DESC_OCTET_LENGTH_PTR 설명자 필드에 저장 됩니다.  
  
-   SQL_NULL_DATA 합니다. 데이터는 NULL 데이터 값 및 해당 하는 데이터 버퍼의 값은 무시 됩니다. 이 값은 전송 하거나 드라이버에서 검색 된 SQL 데이터에 대해서만 유효 합니다.  
  
-   SQL_DATA_AT_EXEC입니다. 데이터 버퍼에 데이터가 없습니다. 대신, 데이터 전송 **SQLPutData** 때나 문이 실행 될 때 **SQLBulkOperations** 또는 **SQLSetPos** 호출 됩니다. 이 값은 드라이버에 전송 된 SQL 데이터에 대해서만 유효 합니다. 자세한 내용은 참조 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), 및 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)합니다.  
  
-   결과 SQL_LEN_DATA_AT_EXEC (*길이*) 매크로입니다. 이 값은 SQL_DATA_AT_EXEC 비슷합니다. 자세한 내용은 참조 [긴 데이터를 보내는](../../../odbc/reference/develop-app/sending-long-data.md)합니다.  
  
-   SQL_NO_TOTAL 합니다. 드라이버는 출력 버퍼에서 반환할 수 있습니다. 긴 데이터의 바이트 수를 확인할 수 없습니다. 이 값은 드라이버에서 검색 된 SQL 데이터에 대해서만 유효 합니다.  
  
-   SQL_DEFAULT_PARAM 합니다. 프로시저 일치 하는 데이터 버퍼에 있는 값 대신 프로시저의 입력된 매개 변수의 기본값을 사용 하는 것입니다.  
  
-   SQL_COLUMN_IGNORE 합니다. **SQLBulkOperations** 또는 **SQLSetPos** 데이터 버퍼에 값을 무시 하는 것입니다. 호출 하 여 데이터의 행을 업데이트할 때 **SQLBulkOperations** 또는 **SQLSetPos** 열 값이 변경 되지 않습니다. 호출 하 여 데이터의 새 행을 삽입할 때 **SQLBulkOperations**, 열 값은 기본 설정으로 또는 열에 NULL로 기본이 없는 경우.
