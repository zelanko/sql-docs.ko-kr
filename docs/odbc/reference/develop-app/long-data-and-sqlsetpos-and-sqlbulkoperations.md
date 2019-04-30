---
title: Long 데이터 및 SQLSetPos 및 SQLBulkOperations | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1d1a55d3b417ff7a0a673bda8d289a72d7c1cb1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312858"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Long 데이터 및 SQLSetPos 및 SQLBulkOperations
사용 하 여 행을 업데이트 하는 경우 긴 데이터를 보낼 수 SQL 문에서 매개 변수를 사용 하 여 대/소문자 그대로 **SQLBulkOperations** 하거나 **SQLSetPos** 사용 하 여 행을 삽입할 때 또는 **SQLBulkOperations**. 데이터에 대 한 여러 호출을 사용 하 여 부분으로 보내지는 **SQLPutData**합니다. 실행 시 데이터는 전송 하는 열 이라고 *실행 시 데이터 열*합니다.  
  
> [!NOTE]  
>  응용 프로그램 실제로 유형을 보낼 수 있는 모든 데이터 실행 시 **SQLPutData**이지만 부분에서 문자 및 이진 데이터를 보낼 수 있습니다. 그러나 데이터를 단일 버퍼로 수 있을 정도로 작고 경우 일반적으로 사용 하는 이유 **SQLPutData**합니다. 버퍼를 바인딩 및 드라이버 버퍼에서 데이터를 검색할 수 있도록 하려면 훨씬 쉽습니다.  
  
 응용 프로그램 호출 하기 전에 열을 바인딩해야 long 데이터가 열 일반적으로 바인딩되지 않은, 때문 **SQLBulkOperations** 하거나 **SQLSetPos** 호출한 후 언바인딩해야 및 **SQLBulkOperations**  나 **SQLSetPos**합니다. 때문에 열을 바인딩해야 **SQLBulkOperations** 하거나 **SQLSetPos** 바인딩된 열에 대해서만 작동 하며 바인딩 해제 해야 되도록 **SQLGetData** 데이터를 검색할 수 열입니다.  
  
 응용 프로그램 실행 시 데이터를 보내려면 다음을 수행 합니다.  
  
1.  데이터 값 대신 행 집합 버퍼에는 32 비트 값을 배치합니다. 응용 프로그램 데이터를 포함 하는 파일의 핸들을 열 수 등 의미 있는 값을로 설정 해야 하므로 응용 프로그램을 나중에이 값이 반환 됩니다.  
  
2.  결과 SQL_LEN_DATA_AT_EXEC에 길이/표시기 버퍼의 값을 설정 (*길이*) 매크로입니다. 이 값의 데이터 매개 변수를 사용 하 여 전송 되는 드라이버 나타냅니다 **SQLPutData**합니다. 합니다 *길이* 공간 사전 할당 수 있도록 긴 데이터의 바이트 수를 보낼지 알아야 하는 데이터 원본에 긴 데이터를 보낼 때 값이 사용 됩니다. 이 값을 호출 하 여 응용 프로그램 데이터 원본에 필요한 지 여부를 결정할 **SQLGetInfo** SQL_NEED_LONG_DATA_LEN 옵션을 사용 합니다. 모든 드라이버에서이 매크로 지원 해야 합니다. 데이터 원본 바이트 길이가 필요 하지 않으면 드라이버 무시 해도 됩니다.  
  
3.  호출 **SQLBulkOperations** 하거나 **SQLSetPos**합니다. 드라이버는 길이/표시기 버퍼를 SQL_LEN_DATA_AT_EXEC의 결과 포함 하는 검색 (*길이*) 매크로 및 함수의 반환 값으로는 SQL_NEED_DATA 반환 합니다.  
  
4.  호출 **SQLParamData** 는 SQL_NEED_DATA에 대 한 응답에서 값을 반환 합니다. Long 데이터를 전송 해야 하는 경우 **SQLParamData** SQL_NEED_DATA를 반환 합니다. 가리키는 버퍼에는 *ValuePtrPtr* 인수를 드라이버에는 응용 프로그램 행 집합 버퍼에 배치 하는 고유 값을 반환 합니다. 이 값을 사용 하 여;에 대 한 데이터를 전송 하는 열을 확인 하려면 응용 프로그램 실행 시 데이터 열이 하나 이상 있으면 드라이버를 특정 순서로 실행 시 데이터 열에 대 한 데이터를 요청할 필요 하지 않습니다.  
  
5.  호출 **SQLPutData** 드라이버에 열 데이터를 보냅니다. 열 데이터는 긴 데이터의 경우 대개 단일 버퍼에 맞지 않으면, 응용 프로그램 호출 **SQLPutData** 반복적으로 데이터를에서 보내도록 파트; 드라이버 및 데이터 원본 데이터를 어셈블해야 하기 때문에 달려 있습니다. Null로 끝나는 문자열 데이터를 전달 하는 응용 프로그램, 드라이버 또는 데이터 원본 리어셈블리 프로세스의 일부로 null 종료 문자를 제거 해야 합니다.  
  
6.  호출 **SQLParamData** 다시 가리키는 모든 열에 대 한 데이터 전송에 해당 합니다. 데이터 전송 되지 않은, 드라이버 SQL_NEED_DATA 및 다음 실행 시 데이터 열;에 대 한 고유한 값을 반환 합니다. 모든 실행 시 데이터 열이 있는 경우 응용 프로그램 5 단계를 반환합니다. 모든 실행 시 데이터 열에 대해 전송 된 데이터 행에 대 한 데이터는 데이터 원본에 전송 됩니다. **SQLParamData** SQL_SUCCESS, SQL_SUCCESS_WITH_INFO 및 수를 반환 하면 모든 SQLSTATE는 다음 **SQLBulkOperations** 하거나 **SQLSetPos** 반환할 수 있습니다.  
  
 이후에 **SQLBulkOperations** 또는 **SQLSetPos** SQL_NEED_DATA를 반환 합니다 이며 데이터의 마지막 실행 시 데이터 열에 대 한 완전히 전송 되기 전에 문에 필요한 데이터 상태에서입니다. 이 상태에서는 응용 프로그램 에서만 호출할 수 **SQLPutData**, **SQLParamData**, **SQLCancel**하십시오 **SQLGetDiagField**, 또는 **SQLGetDiagRec**; 다른 모든 함수와 반환 SQLSTATE HY010 (함수 시퀀스 오류). 호출 **SQLCancel** 문의 실행을 취소 하 고 이전 상태로 돌아갑니다. 자세한 내용은 참조 하세요. [부록 b: ODBC 상태 전환 테이블](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)합니다.
