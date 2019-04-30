---
title: SQLSetDescField 및 SQLSetDescRec (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDescField function [ODBC], Cursor Library
- SQLSetDescRec function [ODBC], Cursor Library
ms.assetid: 4ccff067-85cd-4bfa-a6cd-7f28051fb5b9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b390df48e676290696ae8080c8f671fd0e37bad8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298265"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField 및 SQLSetDescRec(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는의 사용을 설명 합니다 **SQLSetDescField** 및 **SQLSetDescRec** 커서 라이브러리의 함수입니다. 이러한 함수에 대 한 일반적인 정보를 참조 하세요 [SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 하 고 [SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)합니다.  
  
 커서 라이브러리를 실행 **SQLSetDescField** 책갈피 열에 대 한 설정 필드의 값을 반환 하도록 호출 되는 경우:  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_DATETIME_INTERVAL_CODE  
  
 SQL_DESC_SCALE  
  
 SQL_DESC_PRECISION  
  
 SQL_DESC_TYPE  
  
 SQL_DESC_NAME  
  
 SQL_DESC_UNNAMED  
  
 SQL_DESC_NULLABLE  
  
 커서 라이브러리에 대 한 호출을 실행 **SQLSetDescRec** 책갈피 열에 대 한 합니다.  
  
 ODBC 2 작업할 때. *x* 드라이버 커서 라이브러리에는 SQLSTATE HY090 반환 합니다 (잘못 된 문자열 또는 버퍼 길이) 때 **SQLSetDescField** 하거나 **SQLSetDescRec** SQL_DESC_OCTET_를 설정 하기 위해 호출 됩니다 같지 않음 4 값으로는 카드가의 책갈피 레코드의 필드 길이입니다. ODBC 3을 사용 하는 경우 *.x* 드라이버 커서 라이브러리를 통해 버퍼 크기입니다.  
  
 커서 라이브러리를 실행 **SQLSetDescField** SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE, 또는 SQL_DESC_ROW_STATUS_PTR 필드의 값을 반환 하도록 호출 되는 경우. 이러한 필드는 책갈피 행 뿐 아니라 모든 행에 대해 반환할 수 있습니다.  
  
 커서 라이브러리 실행 되지 않습니다 **SQLSetDescField** 앞에서 언급 한 필드 이외의 모든 설명자 필드를 변경 합니다. 응용 프로그램을 호출 하는 경우 **SQLSetDescField** 를 커서 라이브러리가 로드 되는 동안 다른 필드를 설정 하려면 호출 드라이버에 전달 됩니다.  
  
 커서 라이브러리는 응용 프로그램 설명자가 행의 모든 행의 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, 및 SQL_DESC_OCTET_LENGTH_PTR 필드를 동적으로 변경 지원 (호출 후 **SQLExtendedFetch**합니다 **SQLFetch**, 또는 **SQLFetchScroll**). 열에 대 한 길이 버퍼를 바인딩 해제에 null 포인터로 SQL_DESC_OCTET_LENGTH_PTR 필드를 변경할 수 있습니다.  
  
 커서 라이브러리는 커서가 열려 있을 때 APD 또는 카드가 SQL_DESC_BIND_TYPE 필드를 변경 하는 것을 지원 하지 않습니다. 커서를 닫은 후에 및 새 커서를 열기 전에 SQL_DESC_BIND_TYPE 필드를 변경할 수 있습니다. 커서 라이브러리는 커서가 열려 있을 때 변경 지만 설명자 필드는 SQL_DESC_ARRAY_STATUS_PTR, SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR을 및 SQL_DESC_ROWS_PROCESSED_ PTR입니다.  
  
 커서 라이브러리는 수정 후 카드가 SQL_DESC_COUNT 필드를 지원 하지 않습니다 **SQLExtendedFetch** 또는 **SQLFetchScroll** 호출한 전에 커서가 닫혔습니다.
