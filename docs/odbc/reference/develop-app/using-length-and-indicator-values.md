---
title: 길이 및 표시기 값을 사용 하 여 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3a0b54617d55033addabc729adbd078680022fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902465"
---
# <a name="using-length-and-indicator-values"></a>길이 및 표시기 값 사용
길이/표시기 버퍼는 데이터 버퍼에 데이터가 NULL 인지 여부를 나타내는 SQL_NULL_DATA 등 특수 표시기 데이터의 바이트 길이 전달 하는 데 사용 됩니다. 사용 되는 함수에 따라 길이/표시기 버퍼는 SQLINTEGER 또는 SQLSMALLINT 되도록 정의 됩니다. 따라서 단일 인수 설명에 필요 합니다. 데이터 버퍼 nondeferred 입력된 버퍼 이면이 인수 자체 데이터의 바이트 길이 또는 표시기 값을 포함 합니다. 이름은 종종 *StrLen_or_Ind* 또는 비슷한 이름입니다. 예를 들어, 다음 코드 호출 **SQLPutData** 버퍼에 전달할 데이터의 전체; 바이트 길이 (*ValueLen*) 때문에 직접 전달 됩니다 데이터 버퍼 (*ValuePtr*)은 입력된 버퍼입니다.  
  
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
  
 데이터 버퍼 nondeferred 출력 버퍼를 지연 된 입력된 버퍼, 출력 버퍼 이면 인수 길이/표시기 버퍼의 주소를 포함 합니다. 이름은 종종 *StrLen_or_IndPtr* 또는 비슷한 이름입니다. 예를 들어, 다음 코드 호출 **SQLGetData** 데이터의 전체 버퍼를 검색 하려면 응용 프로그램에 길이/표시기 버퍼의 바이트 길이가 반환 됩니다 (*ValueLenOrInd*), 해당 주소는 전달할 **SQLGetData** 때문에 해당 데이터 버퍼 (*ValuePtr*) nondeferred 출력 버퍼입니다.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 길이/표시기 버퍼 인수가 0 일 수 있습니다는 특히 금지 하지 않는 한 (경우 nondeferred 입력) 또는 null 포인터 (하는 경우 지연 된 입력 또는 출력). 입력된 버퍼에 대 한 데이터의 바이트 길이 무시 하면이 합니다. 이 가변 길이 데이터를 전달 하는 경우 오류를 반환 하지만 일반적인 null이 아닌 고정 길이 데이터를 전달 하는 경우 길이가 아니고 지표 값 필요 하므로. 출력 버퍼에 대 한 드라이버는 데이터 또는 지표 값의 바이트 길이 반환 하지 그러면 합니다. 드라이버에서 반환한 데이터는 NULL 이지만 공용 고정 길이, null이 아닌 데이터를 검색할 때 길이가 아니고 지표 값 필요 하므로 하는 경우이 오류가 발생 합니다.  
  
 지연 된 데이터 버퍼의 주소를 드라이버에 전달 되 면 버퍼에 바인딩된 없을 때까지 지연된 길이/표시기 버퍼의 주소 유효한 남아 있어야 합니다.  
  
 다음 길이 길이/표시기 값으로 사용할 수 있습니다.  
  
-   *n*, 여기서 *n* > 0입니다.  
  
-   0.  
  
-   SQL_NTS. 드라이버는 해당 데이터 버퍼에 보낼 문자열은 null로 끝나는; 문자열을 전달 하는 바이트 길이 계산 하지 않고 C 프로그래머를 위한 편리한 방법입니다. 이 값에서 드라이버에 데이터를 보낼 때에 유효 합니다. 드라이버 응용 프로그램에 데이터를 반환 될 때 항상 데이터의 실제 바이트 길이 반환 합니다.  
  
 다음 값은 길이/표시기 값으로 잘못 되었습니다. SQL_NULL_DATA는 SQL_DESC_INDICATOR_PTR 설명자 필드;에 저장 됩니다. 다른 모든 값은 SQL_DESC_OCTET_LENGTH_PTR 설명자 필드에 저장 됩니다.  
  
-   SQL_NULL_DATA. 데이터는 NULL 데이터 값, 및 해당 데이터 버퍼의 값은 무시 됩니다. 이 값은 SQL 데이터를 전송 하거나 드라이버에서 검색할에 적합 합니다.  
  
-   SQL_DATA_AT_EXEC. 데이터 버퍼에 데이터가 없습니다. 사용 하 여 데이터를 전송 하는 대신 **SQLPutData** 때나 문이 실행 될 때 **SQLBulkOperations** 하거나 **SQLSetPos** 라고 합니다. 이 값은 드라이버에 전송 되는 SQL 데이터에만 적합 합니다. 자세한 내용은 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)를 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), 및 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)합니다.  
  
-   결과 SQL_LEN_DATA_AT_EXEC (*길이*) 매크로입니다. 이 값은 SQL_DATA_AT_EXEC 비슷합니다. 자세한 내용은 [긴 데이터를 보내는](../../../odbc/reference/develop-app/sending-long-data.md)합니다.  
  
-   SQL_NO_TOTAL. 드라이버는 출력 버퍼에서 반환할 수 있습니다. 긴 데이터의 바이트 수를 확인할 수 없습니다. 이 값은 드라이버에서 검색 된 SQL 데이터에만 적합 합니다.  
  
-   SQL_DEFAULT_PARAM. 프로시저를 해당 데이터 버퍼의 값이 아닌 프로시저에서 입력된 매개 변수의 기본값을 사용 하는 것입니다.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** 나 **SQLSetPos** 데이터 버퍼의 값을 무시 하는 것입니다. 호출 하 여 데이터 행을 업데이트 하는 경우 **SQLBulkOperations** 하거나 **SQLSetPos** 열 값이 변경 되지 않습니다. 호출 하 여 데이터의 새 행을 삽입할 때 **SQLBulkOperations**, 열 값을 기본값으로 설정 되어 또는 열에 기본값을 NULL로 없는 경우.
