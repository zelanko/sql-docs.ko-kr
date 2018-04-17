---
title: 긴 데이터와 SQLSetPos SQLBulkOperations | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82a51c05c5f40c2f4b2fb24f8b3e43e09d6d4514
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>긴 데이터와 SQLSetPos SQLBulkOperations
행을 업데이트 하는 경우 긴 데이터를 보낼 수 SQL 문에서 매개 변수가 있는 경우 처럼 **SQLBulkOperations** 또는 **SQLSetPos** 와 행을 삽입할 때 또는 **SQLBulkOperations**. 데이터를 여러 번 호출 된 부분으로 보내집니다 **SQLPutData**합니다. 열을 데이터 전송에 실행 시 라고 *실행 시 데이터 열*합니다.  
  
> [!NOTE]  
>  응용 프로그램 실제로 수를 보낼 모든 종류의 데이터와 실행 시간에 **SQLPutData**문자 및 이진 데이터 부분에 보낼 수 있지만, 합니다. 그러나 데이터를 단일 버퍼로 수 있을 정도로 작고 경우 없기 일반적으로 사용할 이유가 없습니다 **SQLPutData**합니다. 훨씬 버퍼를 바인딩하고 버퍼에서 데이터를 검색 하는 드라이버를 사용 하는 것이 쉽습니다.  
  
 응용 프로그램 호출 하기 전에 열을 바인딩해야 long 데이터가 열 일반적으로 바인딩되지, **SQLBulkOperations** 또는 **SQLSetPos** 호출한 후 바인딩 해제 **SQLBulkOperations**  또는 **SQLSetPos**합니다. 때문에 열을 바인딩해야 **SQLBulkOperations** 또는 **SQLSetPos** 바인딩된 열에 대해서만 작동 하며 바인딩 해제 해야 있도록 **SQLGetData** 는 데이터를 검색 하는 데 사용할 수 열입니다.  
  
 응용 프로그램 실행 시 데이터를 보내려면 다음을 수행 합니다.  
  
1.  데이터 값 대신 행 집합 버퍼에는 32 비트 값을 배치합니다. 이 값은 응용 프로그램 열의 번호 또는 데이터를 포함 하는 파일 핸들 등의 의미 있는 값으로 설정 해야 하므로 응용 프로그램을 나중에 반환 됩니다.  
  
2.  결과 SQL_LEN_DATA_AT_EXEC에 길이/표시기 버퍼의 값을 설정 (*길이*) 매크로입니다. 이 값 매개 변수 데이터가 전송 되는 드라이버에 알립니다 **SQLPutData**합니다. *길이* 값 공간을 미리 할당할 수 있도록 긴 데이터의 바이트 수를 보내집니다 알아야 하는 데이터 원본에 대 한 long 데이터를 보낼 때 사용 됩니다. 이 값을 호출 하 여 응용 프로그램 데이터 원본에 필요한 지 여부를 확인 하려면 **SQLGetInfo** SQL_NEED_LONG_DATA_LEN 옵션을 사용 합니다. 모든 드라이버;이 매크로 지원 해야 합니다. 데이터 원본 바이트 길이 필요 하지 않으면 드라이버 무시 해도 됩니다.  
  
3.  호출 **SQLBulkOperations** 또는 **SQLSetPos**합니다. 드라이버는 길이/표시기 버퍼는 SQL_LEN_DATA_AT_EXEC의 결과 포함 하는 검색 (*길이*) 매크로 및 함수의 반환 값으로는 SQL_NEED_DATA 반환 합니다.  
  
4.  호출 **SQLParamData** 는 SQL_NEED_DATA에 대 한 응답에서 값을 반환 합니다. Long 데이터를 전송 해야 할 경우 **SQLParamData** SQL_NEED_DATA를 반환 합니다. 가 가리키는 버퍼에는 *ValuePtrPtr* 인수, 드라이버는 응용 프로그램이 행 집합 버퍼에 배치 하는 고유 값을 반환 합니다. 응용 프로그램 실행 시 데이터 열이 여러 개 있으면;에 대 한 데이터를 전송 하는 열을 확인 하려면이 값을 사용 드라이버가 특정 순서로 실행 시 데이터 열에 대 한 데이터를 요청 하는 필요 하지 않습니다.  
  
5.  호출 **SQLPutData** 드라이버에 열 데이터를 보냅니다. 응용 프로그램이 호출할 수 있으므로 긴 데이터의 경우 열 데이터를 단일 버퍼에 맞지 않으면, **SQLPutData** 반복 해 서 부분;의 데이터를 전송 하는 데이터를 다시 드라이버와 데이터 소스는 합니다. Null로 끝나는 문자열 데이터를 전달 하는 응용 프로그램, 드라이버 또는 데이터 원본 리어셈블리 프로세스의 일부로 null 종결 문자를 제거 해야 합니다.  
  
6.  호출 **SQLParamData** 다시 나타내려면 모든 데이터 열에 대 한 전송 않은 것입니다. 드라이버는 SQL_NEED_DATA 및 다음 실행 시 데이터 열에 대 한 고유 값을 반환을 전송 되지 않은 데이터는 실행 시 데이터 열이 있는 경우 응용 프로그램 5 단계를 반환합니다. 모든 실행 시 데이터 열에 대 한 데이터를 전송한 경우 행에 대 한 데이터는 데이터 원본에 전송 됩니다. **SQLParamData** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO 및 수를 반환 하면 모든 SQLSTATE는 다음 **SQLBulkOperations** 또는 **SQLSetPos** 반환할 수 있습니다.  
  
 후 **SQLBulkOperations** 또는 **SQLSetPos** sql_need_data가 반환 되며 데이터가 마지막 실행 시 데이터 열에 대 한 완전히 플러시된 전에 문이에서 필요한 데이터 상태입니다. 이 상태에서는 응용 프로그램이 호출할 수만 **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**, 또는 **SQLGetDiagRec**; 다른 모든 함수가 반환 SQLSTATE HY010 (함수 시퀀스 오류). 호출 **SQLCancel** 문 실행을 취소 하 고 이전 상태로 돌아갑니다. 자세한 내용은 참조 [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.
