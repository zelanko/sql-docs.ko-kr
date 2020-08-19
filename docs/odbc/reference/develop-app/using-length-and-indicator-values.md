---
description: 길이 및 표시기 값 사용
title: 길이 및 표시기 값 사용 | Microsoft Docs
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
ms.openlocfilehash: 7e9c7feb463b2a92d716be24c76d00b64c69a860
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424405"
---
# <a name="using-length-and-indicator-values"></a>길이 및 표시기 값 사용
길이/표시기 버퍼는 데이터 버퍼의 데이터 바이트 길이 또는 데이터가 NULL 임을 나타내는 SQL_NULL_DATA와 같은 특수 표시기를 전달 하는 데 사용 됩니다. 사용 되는 함수에 따라 길이/표시기 버퍼가 SQLINTEGER 또는 SQLINTEGER로 정의 됩니다. 따라서이를 설명 하려면 단일 인수가 필요 합니다. 데이터 버퍼가 지연 되지 않은 입력 버퍼 이면이 인수는 데이터 자체의 바이트 길이 또는 표시기 값을 포함 합니다. 종종 이름이 *StrLen_or_Ind* 또는 유사한 이름입니다. 예를 들어 다음 코드는 **Sqlputdata** 를 호출 하 여 버퍼 전체에 데이터를 전달 합니다. 데이터 버퍼 (*Valueptr*)는 입력 버퍼 이므로 바이트*길이 (#*)가 직접 전달 됩니다.  
  
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
  
 데이터 버퍼가 지연 된 입력 버퍼, 지연 되지 않은 출력 버퍼 또는 출력 버퍼 인 경우 인수에는 길이/표시기 버퍼의 주소가 포함 됩니다. 종종 이름이 *StrLen_or_IndPtr* 또는 유사한 이름입니다. 예를 들어 다음 코드는 **SQLGetData** 를 호출 하 여 데이터의 전체 버퍼를 검색 합니다. 바이트 길이는 해당 하는 데이터 버퍼 (*Valueptr*)가 지연 되지 않은 출력 버퍼 이기 때문에 주소가 **SQLGetData** 에 전달 되는 길이/표시기 버퍼 (*valuelenorind*)의 응용 프로그램에 반환 됩니다.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 특별히 금지 된 경우를 제외 하 고는 길이/표시기 버퍼 인수가 0 (지연 된 입력 인 경우) 이거나 null 포인터 (출력 또는 지연 된 입력 인 경우)가 될 수 있습니다. 입력 버퍼의 경우 드라이버에서 데이터의 바이트 길이를 무시 합니다. 이는 가변 길이 데이터를 전달 하는 경우 오류를 반환 하지만 null이 아닌 고정 길이 데이터를 전달할 때 일반적으로 길이와 표시기 값이 필요 하지 않기 때문에 발생 합니다. 출력 버퍼의 경우 드라이버에서 데이터의 바이트 길이 또는 표시기 값을 반환 하지 않습니다. 이 오류는 드라이버에서 반환 된 데이터가 NULL 인 경우에는 오류이 고, 길이가 나 표시기 값은 필요 하지 않으므로 고정 길이의 null을 허용 하지 않는 데이터를 검색할 때 일반적으로 발생 합니다.  
  
 지연 된 데이터 버퍼의 주소가 드라이버로 전달 되는 경우에는 버퍼가 바인딩 해제 될 때까지 지연 된 길이/표시기 버퍼의 주소가 유효한 상태로 유지 되어야 합니다.  
  
 길이/지표 값으로 유효한 길이는 다음과 같습니다.  
  
-   *n*, 여기서 *n* > 0입니다.  
  
-   0.  
  
-   SQL_NTS. 해당 데이터 버퍼의 드라이버로 전송 된 문자열이 null로 종료 되었습니다. 이 방법은 C 프로그래머가 바이트 길이를 계산 하지 않고도 문자열을 전달할 수 있는 편리한 방법입니다. 이 값은 응용 프로그램이 데이터를 드라이버로 보낼 때만 유효 합니다. 드라이버가 응용 프로그램에 데이터를 반환 하는 경우 항상 데이터의 실제 바이트 길이를 반환 합니다.  
  
 다음 값은 길이/지표 값으로 유효 합니다. SQL_NULL_DATA은 SQL_DESC_INDICATOR_PTR 설명자 필드에 저장 됩니다. 다른 모든 값은 SQL_DESC_OCTET_LENGTH_PTR 설명자 필드에 저장 됩니다.  
  
-   SQL_NULL_DATA. 데이터는 NULL 데이터 값 이며 해당 데이터 버퍼의 값은 무시 됩니다. 이 값은 드라이버에 전송 되거나 드라이버에서 검색 된 SQL 데이터에 대해서만 유효 합니다.  
  
-   SQL_DATA_AT_EXEC. 데이터 버퍼에 데이터가 포함 되어 있지 않습니다. 대신 문이 실행 되거나 **SQLBulkOperations** 또는 **SQLSetPos** 가 호출 될 때 **sqlputdata** 를 사용 하 여 데이터가 전송 됩니다. 이 값은 드라이버에 전송 된 SQL 데이터에 대해서만 유효 합니다. 자세한 내용은 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)및 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)를 참조 하세요.  
  
-   SQL_LEN_DATA_AT_EXEC (*길이*) 매크로의 결과입니다. 이 값은 SQL_DATA_AT_EXEC와 비슷합니다. 자세한 내용은 [긴 데이터 전송](../../../odbc/reference/develop-app/sending-long-data.md)을 참조 하세요.  
  
-   SQL_NO_TOTAL. 드라이버는 출력 버퍼에서 반환할 수 있는 긴 데이터의 바이트 수를 확인할 수 없습니다. 이 값은 드라이버에서 검색 된 SQL 데이터에 대해서만 유효 합니다.  
  
-   SQL_DEFAULT_PARAM. 프로시저는 해당 데이터 버퍼의 값 대신 프로시저에서 입력 매개 변수의 기본값을 사용 하는 것입니다.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** 또는 **SQLSetPos** 는 데이터 버퍼의 값을 무시 하는 것입니다. **SQLBulkOperations** 또는 **SQLSetPos** 를 호출 하 여 데이터 행을 업데이트 하는 경우 열 값은 변경 되지 않습니다. **SQLBulkOperations**에 대 한 호출을 통해 데이터의 새 행을 삽입 하는 경우 열 값은 기본값으로 설정 되거나 열에 기본값이 없으면 NULL로 설정 됩니다.
