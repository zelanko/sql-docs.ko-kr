---
title: Long Data 및 SQLSetPos and SQLBulkOperations | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287867"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Long 데이터 및 SQLSetPos 및 SQLBulkOperations
SQL 문의 매개 변수를 사용 하는 경우 **SQLBulkOperations** 또는 **SQLSetPos** 를 사용 하 여 행을 업데이트 하거나 **SQLBulkOperations**를 사용 하 여 행을 삽입할 때 긴 데이터를 보낼 수 있습니다. 데이터는 **Sqlputdata**를 여러 번 호출 하 여 파트로 전송 됩니다. 실행 시 데이터를 전송 하는 열을 *실행 시 데이터 열*이라고 합니다.  
  
> [!NOTE]  
>  응용 프로그램은 실제로 **Sqlputdata**를 사용 하 여 실행 시 모든 형식의 데이터를 보낼 수 있지만, 문자 및 이진 데이터만 파트로 전송 될 수 있습니다. 그러나 데이터가 단일 버퍼에 맞게 충분히 작은 경우 일반적으로 **Sqlputdata**를 사용할 이유가 없습니다. 버퍼를 바인딩하는 것이 훨씬 쉬우며 드라이버에서 버퍼의 데이터를 검색할 수 있습니다.  
  
 Long 데이터 열은 일반적으로 바인딩되지 않으므로 응용 프로그램은 **SQLBulkOperations** 또는 **sqlsetpos** 를 호출 하기 전에 열을 바인딩하고 **SQLBulkOperations** 또는 **sqlsetpos**를 호출한 후에 바인딩 해제 해야 합니다. **SQLBulkOperations** 또는 **SQLSetPos** 는 바인딩된 열 에서만 작동 하 고 열에서 데이터를 검색 하는 데 **SQLGetData** 를 사용할 수 있도록 바인딩되지 않아야 하므로 열은 바인딩되어야 합니다.  
  
 실행 시 데이터를 전송 하기 위해 응용 프로그램은 다음을 수행 합니다.  
  
1.  데이터 값 대신 행 집합 버퍼에 32 비트 값을 배치 합니다. 이 값은 나중에 응용 프로그램에 반환 되므로 응용 프로그램은 열 번호 또는 데이터를 포함 하는 파일의 핸들과 같은 의미 있는 값으로 설정 해야 합니다.  
  
2.  길이/표시기 버퍼의 값을 SQL_LEN_DATA_AT_EXEC (*length*) 매크로의 결과로 설정 합니다. 이 값은 매개 변수의 데이터가 **Sqlputdata**를 사용 하 여 전송 됨을 드라이버에 나타냅니다. *길이* 값은 공간을 미리 할당할 수 있도록 전송할 long 데이터의 바이트 수를 알아야 하는 긴 데이터를 데이터 원본으로 보낼 때 사용 됩니다. 데이터 원본에이 값이 필요한 지 여부를 확인 하기 위해 응용 프로그램은 SQL_NEED_LONG_DATA_LEN 옵션으로 **SQLGetInfo** 를 호출 합니다. 모든 드라이버는이 매크로를 지원 해야 합니다. 데이터 원본에 바이트 길이가 필요 하지 않은 경우 드라이버는이를 무시할 수 있습니다.  
  
3.  **SQLBulkOperations** 또는 **SQLSetPos**를 호출 합니다. 이 드라이버는 길이/지표 버퍼에 SQL_LEN_DATA_AT_EXEC (*length*) 매크로의 결과가 포함 되어 있음을 검색 하 고 SQL_NEED_DATA를 함수의 반환 값으로 반환 합니다.  
  
4.  SQL_NEED_DATA 반환 값에 대 한 응답으로 **Sqlparamdata** 를 호출 합니다. Long 데이터를 전송 해야 하는 경우 **Sqlparamdata** 는 SQL_NEED_DATA을 반환 합니다. *Valueptrptr* 인수가 가리키는 버퍼에서 드라이버는 응용 프로그램이 행 집합 버퍼에 배치 하는 고유한 값을 반환 합니다. 실행 시 데이터 열이 두 개 이상 있는 경우 응용 프로그램은이 값을 사용 하 여 데이터를 보낼 열을 결정 합니다. 드라이버는 특정 순서로 실행 시 데이터 열에 대 한 데이터를 요청 하는 데 필요 하지 않습니다.  
  
5.  **Sqlputdata** 를 호출 하 여 열 데이터를 드라이버로 보냅니다. 열 데이터가 단일 버퍼에 맞지 않는 경우 (긴 데이터의 경우) 응용 프로그램은 **Sqlputdata** 를 반복적으로 호출 하 여 데이터를 파트로 보냅니다. 데이터를 다시 어셈블할 수 있는 드라이버 및 데이터 원본이 있습니다. 응용 프로그램이 null로 끝나는 문자열 데이터를 전달 하는 경우에는 드라이버 또는 데이터 원본이 리어셈블리 프로세스의 일부로 null 종료 문자를 제거 해야 합니다.  
  
6.  **Sqlparamdata** 를 다시 호출 하 여 열에 대 한 모든 데이터를 보냈는지 여부를 표시 합니다. 데이터가 전송 되지 않은 실행 시 데이터 열이 있는 경우 드라이버는 SQL_NEED_DATA을 반환 하 고 다음 실행 시 데이터 열에 대 한 고유 값을 반환 합니다. 응용 프로그램이 5 단계로 돌아옵니다. 모든 실행 시 데이터 열에 대해 데이터가 전송 되 면 해당 행의 데이터가 데이터 원본으로 전송 됩니다. 그러면 **Sqlparamdata** 가 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO을 반환 하 고 **SQLBulkOperations** 또는 **SQLSetPos** 에서 반환할 수 있는 모든 SQLSTATE를 반환할 수 있습니다.  
  
 **SQLBulkOperations** 또는 **SQLSetPos** 는 SQL_NEED_DATA을 반환 하 고 마지막으로 실행 시 데이터 열에 대해 데이터를 완전히 보내기 전에 데이터를 필요로 하는 경우에는 데이터 상태가 필요 합니다. 이 상태에서 응용 프로그램은 **Sqlputdata**, **sqlputdata**, **Sqlcancel**, **SQLGetDiagField**또는 **SQLGetDiagRec**만 호출할 수 있습니다. 다른 모든 함수는 SQLSTATE HY010 (함수 시퀀스 오류)를 반환 합니다. **Sqlcancel** 을 호출 하면 문의 실행이 취소 되 고 이전 상태로 돌아갑니다. 자세한 내용은 [부록 B: ODBC 상태 전환 표](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)를 참조 하세요.
