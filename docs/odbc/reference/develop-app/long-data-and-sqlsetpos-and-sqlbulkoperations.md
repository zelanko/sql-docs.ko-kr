---
title: 긴 데이터 및 SQLSetPos 및 SQLBulkOperations | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4bc6c5d2da2f796a7c312971635fc36bc2fae8af
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287867"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Long 데이터 및 SQLSetPos 및 SQLBulkOperations
SQL 문의 매개 변수와 마찬가지로 **SQLBulkOperations** 또는 **SQLSetPos로** 행을 업데이트하거나 **SQLBulkOperations**. 로 행을 삽입 할 때 긴 데이터를 보낼 수 있습니다. 데이터는 **SQLPutData**에 대한 여러 호출과 함께 부분적으로 전송됩니다. 실행 시 데이터가 전송되는 열을 실행 *시 데이터 열이라고 합니다.*  
  
> [!NOTE]  
>  응용 프로그램은 실제로 **SQLPutData를**사용하여 실행 시 모든 유형의 데이터를 보낼 수 있지만 문자 및 이진 데이터만 부분적으로 보낼 수 있습니다. 그러나 데이터가 단일 버퍼에 들어갈 만큼 작으면 일반적으로 **SQLPutData**를 사용할 이유가 없습니다. 버퍼를 바인딩하고 드라이버가 버퍼에서 데이터를 검색하도록 하는 것이 훨씬 쉽습니다.  
  
 긴 데이터 열은 일반적으로 바인딩되지 않으므로 응용 프로그램은 **SQLBulkOperations** 또는 **SQLSetPos를** 호출하기 전에 열을 바인딩하고 **SQLBulkOperations** 또는 **SQLSetPos**를 호출한 후 바인딩을 해제해야 합니다. **SQLBulkOperations** 또는 **SQLSetPos는** 바인딩된 열에서만 작동 하 고 **SQLGetData** 열에서 데이터를 검색 하는 데 사용할 수 있도록 바인딩되지 않은 해야 하기 때문에 열 바인딩되어야 합니다.  
  
 실행 시 데이터를 전송하기 위해 응용 프로그램은 다음을 수행합니다.  
  
1.  데이터 값 대신 행 집합 버퍼에 32비트 값을 배치합니다. 이 값은 나중에 응용 프로그램에 반환되므로 응용 프로그램은 열 수 또는 데이터가 포함된 파일의 핸들과 같은 의미 있는 값으로 설정해야 합니다.  
  
2.  길이/표시기 버퍼의 값을*SQL_LEN_DATA_AT_EXEC(길이)* 매크로의 결과로 설정합니다. 이 값은 드라이버에 매개 변수에 대한 데이터가 **SQLPutData**. *길이* 값은 긴 데이터를 데이터 원본으로 보낼 때 사용되며, 이 값은 공간을 할당할 수 있도록 전송되는 긴 데이터의 바이트 수를 알아야 합니다. 데이터 원본에 이 값이 필요한지 여부를 확인하려면 응용 프로그램에서 SQL_NEED_LONG_DATA_LEN 옵션을 사용하여 **SQLGetInfo를** 호출합니다. 모든 드라이버는 이 매크로를 지원해야 합니다. 데이터 원본에 바이트 길이가 필요하지 않은 경우 드라이버는 이를 무시할 수 있습니다.  
  
3.  **SQLBulkOperations** 또는 **SQLSetPos를**호출합니다. 드라이버는 길이/표시기 버퍼에*SQL_LEN_DATA_AT_EXEC(길이)* 매크로의 결과가 포함되어 있고 함수의 반환 값으로 SQL_NEED_DATA 반환한다는 것을 발견합니다.  
  
4.  SQL_NEED_DATA 반환 값에 대한 응답으로 **SQLParamData를** 호출합니다. 긴 데이터를 전송해야 하는 경우 **SQLParamData는** SQL_NEED_DATA 반환합니다. *ValuePtrPtr* 인수가 가리키는 버퍼에서 드라이버는 응용 프로그램이 행 집합 버퍼에 배치한 고유 값을 반환합니다. 실행 시 데이터 열이 두 개 이상 있는 경우 응용 프로그램은 이 값을 사용하여 데이터를 보낼 열을 결정합니다. 드라이버는 특정 순서로 실행 시 데이터 열에 대한 데이터를 요청할 필요가 없습니다.  
  
5.  **SQLPutData를** 호출하여 열 데이터를 드라이버로 보냅니다. 열 데이터가 단일 버퍼에 맞지 않는 경우, 긴 데이터의 경우와 마찬가지로 응용 프로그램은 **SQLPutData를** 반복적으로 호출하여 부분적으로 데이터를 보냅니다. 데이터를 다시 어셈블하는 것은 드라이버와 데이터 원본에 달려 있습니다. 응용 프로그램이 null 종료 문자열 데이터를 전달하는 경우 드라이버 또는 데이터 원본은 재구성 프로세스의 일부로 null 종료 문자를 제거해야 합니다.  
  
6.  **SQLParamData를** 호출하여 열에 대한 모든 데이터를 보냈음을 나타냅니다. 데이터가 전송되지 않은 데이터 실행 시 열이 있는 경우 드라이버는 SQL_NEED_DATA 반환하고 다음 실행 시 데이터 열에 대한 고유 값을 반환합니다. 응용 프로그램이 5단계로 돌아갑니다. 실행 시 모든 데이터에 대한 데이터가 전송된 경우 행의 데이터가 데이터 원본으로 전송됩니다. 그런 다음 **SQLParamData는** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 반환하고 **SQLBulkOperations** 또는 **SQLSetPos가** 반환할 수 있는 모든 SQLSTATE를 반환할 수 있습니다.  
  
 **SQLBulkOperations** 또는 **SQLSetPosSQL_NEED_DATA** 반환 하고 마지막 실행 시 데이터 열에 대 한 데이터를 완전히 전송 하기 전에 문은 필요 데이터 상태에 있습니다. 이 상태에서 응용 프로그램은 **SQLPutData,** **SQLParamData,** **SQLCancel**, **SQLGetDiagField**또는 **SQLGetDiagRec만**호출할 수 있습니다. 다른 모든 함수는 SQLSTATE HY010(함수 시퀀스 오류)을 반환합니다. **SQLCancel호출하면** 명령문의 실행이 취소되고 이전 상태로 반환됩니다. 자세한 내용은 [부록 B: ODBC 상태 전환 테이블을](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)참조하십시오.
