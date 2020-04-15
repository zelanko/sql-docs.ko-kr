---
title: SQLSetDescField 및 SQLSetDescRec (커서 라이브러리) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b85eb84cdf48a1c2a441b8994076a9023d254f2d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300553"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField 및 SQLSetDescRec(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLSetDescField** 및 **SQLSetDescRec** 함수의 사용에 대해 설명합니다. 이러한 함수에 대한 일반적인 내용은 [SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 및 [SQLSetDescRec 함수를](../../../odbc/reference/syntax/sqlsetdescrec-function.md)참조하십시오.  
  
 커서 라이브러리는 책갈피 열에 대해 설정된 필드 값을 반환하기 위해 호출될 때 **SQLSetDescField를** 실행합니다.  
  
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
  
 커서 라이브러리는 책갈피 열에 대해 **SQLSetDescRec에** 대한 호출을 실행합니다.  
  
 ODBC *2.x* 드라이버로 작업할 때 커서 라이브러리는 **SQLSetDescField** 또는 **SQLSetDescRec이** ARD의 책갈피 레코드에 대한 SQL_DESC_OCTET_LENGTH 필드를 4와 같지 않은 값으로 설정하도록 호출될 때 SQLSTATE HY090(잘못된 문자열 또는 버퍼 길이)을 반환합니다. ODBC *3.x* 드라이버로 작업할 때 커서 라이브러리를 사용하면 버퍼의 크기가 다를 수 있습니다.  
  
 커서 라이브러리는 SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE 또는 SQL_DESC_ROW_STATUS_PTR 필드의 값을 반환하기 위해 호출될 때 **SQLSetDescField를** 실행합니다. 이러한 필드는 책갈피 행뿐만 아니라 모든 행에 대해 반환될 수 있습니다.  
  
 커서 라이브러리는 **SQLSetDescField를** 실행하지 않고 앞에서 언급한 필드 이외의 설명자 필드를 변경합니다. 응용 프로그램이 **SQLSetDescField를** 호출하여 커서 라이브러리가 로드되는 동안 다른 필드를 설정하면 호출이 드라이버로 전달됩니다.  
  
 커서 라이브러리는 **SQLExtendedFetch,** **SQLFetch**또는 **SQLFetch스크롤**호출 후 응용 프로그램 행 설명자의 모든 행의 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드를 동적으로 변경하는 데 지원됩니다. SQL_DESC_OCTET_LENGTH_PTR 필드는 열에 대한 길이 버퍼를 바인딩 해제하기 위해서만 null 포인터로 변경할 수 있습니다.  
  
 커서 라이브러리는 커서가 열려 있을 때 APD 또는 ARD에서 SQL_DESC_BIND_TYPE 필드를 변경하는 것을 지원하지 않습니다. SQL_DESC_BIND_TYPE 필드는 커서가 닫힌 후 새 커서를 열기 전에만 변경할 수 있습니다. 커서 라이브러리가 열려 있을 때 변경을 지원하는 유일한 설명자 필드는 SQL_DESC_ARRAY_STATUS_PTR, SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR 및 SQL_DESC_ROWS_PROCESSED_PTR.  
  
 커서 라이브러리는 **SQLExtendedFetch** 또는 **SQLFetchScroll가** 호출되고 커서가 닫히기 전에 ARD의 SQL_DESC_COUNT 필드 수정을 지원하지 않습니다.
