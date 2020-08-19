---
description: SQLSetDescField 및 SQLSetDescRec(커서 라이브러리)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cef4967a81a78e08dee733072359459c864b9627
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476945"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField 및 SQLSetDescRec(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLSetDescField** 및 **SQLSetDescRec** 함수를 사용 하는 방법에 대해 설명 합니다. 이러한 함수에 대 한 일반적인 정보는 [SQLSetDescField 함수](../../../odbc/reference/syntax/sqlsetdescfield-function.md) 및 [SQLSetDescRec 함수](../../../odbc/reference/syntax/sqlsetdescrec-function.md)를 참조 하세요.  
  
 커서 라이브러리는 책갈피 열에 대해 설정 된 필드의 값을 반환 하기 위해 호출 될 때 **SQLSetDescField** 를 실행 합니다.  
  
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
  
 커서 라이브러리는 책갈피 열에 대해 **SQLSetDescRec** 호출을 실행 합니다.  
  
 ODBC 2.x 드라이버를 사용 하는 경우 **SQLSetDescField** 또는 **SQLSetDescRec** 를 호출 하 여 값의 책갈피 레코드에 대 한 SQL_DESC_OCTET_LENGTH 필드를 4가 아닌 값으로 설정 하는 경우 커서 라이브러리는 SQLSTATE HY090 (잘못 된 문자열 또는 버퍼 길이)를 반환 *합니다.* ODBC 3.x 드라이버를 사용 하는 경우 커서 라이브러리를 사용 하 여 버퍼 크기를 지정할 수 *있습니다.*  
  
 커서 라이브러리는 SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE 또는 SQL_DESC_ROW_STATUS_PTR 필드의 값을 반환 하기 위해 호출 될 때 **SQLSetDescField** 를 실행 합니다. 이러한 필드는 책갈피 행 뿐만 아니라 모든 행에 대해 반환 될 수 있습니다.  
  
 커서 라이브러리는 **SQLSetDescField** 를 실행 하 여 앞에서 언급 한 필드가 아닌 설명자 필드를 변경 하지 않습니다. 커서 라이브러리가 로드 되는 동안 응용 프로그램에서 **SQLSetDescField** 를 호출 하 여 다른 필드를 설정 하는 경우 호출이 드라이버에 전달 됩니다.  
  
 커서 라이브러리는 **Sqlextendedfetch**, **Sqlfetch**또는 **sqlextendedfetch**을 호출한 후에 응용 프로그램 행 설명자의 모든 행에 대 한 SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR 및 SQL_DESC_OCTET_LENGTH_PTR 필드를 동적으로 변경할 수 있도록 지원 합니다. SQL_DESC_OCTET_LENGTH_PTR 필드는 열에 대 한 길이 버퍼의 바인딩을 해제 하기 위한 null 포인터로만 변경할 수 있습니다.  
  
 커서 라이브러리는 커서가 열려 있을 때 APD의 SQL_DESC_BIND_TYPE 필드를 변경 하는 기능을 지원 하지 않습니다. SQL_DESC_BIND_TYPE 필드는 커서를 닫은 후 새 커서가 열리기 전에만 변경할 수 있습니다. 커서를 열 때 커서 라이브러리가 변경을 지 원하는 설명자 필드는 SQL_DESC_ARRAY_STATUS_PTR, SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR, SQL_DESC_ROWS_PROCESSED_PTR입니다.  
  
 커서 라이브러리는 **Sqlextendedfetch** 또는 **sqlextendedfetch** 을 호출한 후 커서를 닫기 전에는의 SQL_DESC_COUNT 필드를 수정 하는 기능을 지원 하지 않습니다.
