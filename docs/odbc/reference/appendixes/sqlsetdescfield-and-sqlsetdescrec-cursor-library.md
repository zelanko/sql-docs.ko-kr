---
title: "SQLSetDescField 및 SQLSetDescRec (커서 라이브러리) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetDescField function [ODBC], Cursor Library
- SQLSetDescRec function [ODBC], Cursor Library
ms.assetid: 4ccff067-85cd-4bfa-a6cd-7f28051fb5b9
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba3d5db821bbbfa287efb811db0ca616b01df244
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField 및 SQLSetDescRec (커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 마십시오 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하세요. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목의 사용을 설명는 **SQLSetDescField** 및 **SQLSetDescRec** 커서 라이브러리의 함수입니다. 이러한 함수에 대 한 일반 정보를 참조 하십시오. [SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 및 [SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)합니다.  
  
 커서 라이브러리 실행 **SQLSetDescField** 책갈피 열에 대해 설정 된 필드의 값을 반환 하도록 호출 될 때:  
  
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
  
 커서 라이브러리에 대 한 호출 실행 **SQLSetDescRec** 책갈피 열에 대 한 합니다.  
  
 ODBC 2 작업할 때는. *x* 드라이버 커서 라이브러리 반환 SQLSTATE HY090 (잘못 된 문자열 또는 버퍼 길이) 때 **SQLSetDescField** 또는 **SQLSetDescRec** 는 SQL_DESC_OCTET_ 설정 하기 위해 호출 4 같지 않은 값으로 카드가의 책갈피 레코드의 필드 길이입니다. ODBC 3 작업할 때*.x* 드라이버 커서 라이브러리의 규모에 버퍼를 허용 합니다.  
  
 커서 라이브러리 실행 **SQLSetDescField** SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE, 또는 SQL_DESC_ROW_STATUS_PTR 필드의 값을 반환 하도록 호출 됩니다. 이러한 필드는 책갈피 행 뿐 아니라 행에 대해 반환할 수 있습니다.  
  
 커서 라이브러리를 실행 하지 않고 **SQLSetDescField** 앞에서 언급 한 필드가 아닌 설명자 필드를 변경할 수 있습니다. 응용 프로그램을 호출 하는 경우 **SQLSetDescField** 을 커서 라이브러리를 로드 하는 동안 다른 모든 필드를 설정 하려면 호출 드라이버 통해 전달 됩니다.  
  
 커서 라이브러리가 지원 응용 프로그램 행 설명자의 모든 행의 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드를 동적으로 변경 (호출한 후 **SQLExtendedFetch**, **SQLFetch**, 또는 **SQLFetchScroll**). 열에 대 한 길이 버퍼의 바인딩을 해제 하려면만 null 포인터 SQL_DESC_OCTET_LENGTH_PTR 필드를 변경할 수 있습니다.  
  
 커서 라이브러리는 커서가 열려 있을 때 APD 또는 카드가 SQL_DESC_BIND_TYPE 필드를 변경 하는 것을 지원 하지 않습니다. 커서를 닫은 후에 하 고 새 커서를 열기 전에 SQL_DESC_BIND_TYPE 필드를 변경할 수 있습니다. 커서 라이브러리는 커서가 열려 있을 때 변경을 지 원하는 유일한 설명자 필드는 SQL_DESC_ARRAY_STATUS_PTR, SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR, 및 SQL_DESC_ROWS_PROCESSED_ PTR입니다.  
  
 커서 라이브러리는 수정 후 카드가의 SQL_DESC_COUNT 필드를 지원 하지 않습니다 **SQLExtendedFetch** 또는 **SQLFetchScroll** 호출한 전에 커서가 닫혔습니다.
