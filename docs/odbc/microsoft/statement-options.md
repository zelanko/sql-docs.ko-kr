---
title: "문 옵션 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac14e06bc71aac307fdba1d87110610ac5bae4b3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="statement-options"></a>문 옵션
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 이러한 옵션에는 사용자 지정 응용 프로그램 내에서 특정 실행 문의을 허용 합니다.  
  
|문 옵션|참고|  
|----------------------|-----------|  
|SQL_BIND_TYPE|사용 가능한 메모리 또는 2147483647 바이트를 초과할 수 없습니다.|  
|SQL_CONCURRENCY|허용 되는 값에 대 한 참조는 [커서 유형 및 동시성 조합](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)합니다.|  
|에서는 SQL_CURSOR_TYPE|드라이버는 SQL_CURSOR_DYNAMIC를 허용 하지 않습니다. 참조 [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) 자세한 정보에 대 한 합니다. 허용 되는 값에 대 한 참조는 [커서 유형 및 동시성 조합](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)합니다.|  
|SQL_GET_BOOKMARK|현재 레코드 번호에 대 한 책갈피가 하는 32 비트 정수 값을 반환 합니다. Get만 사용 합니다. 설정할 수 없습니다.|  
|SQL_KEYSET_SIZE|0에만 설정할 수 있습니다.|  
|SQL_MAX_ROWS|결과에서 반환할 행의 최대 수를 설정 합니다.|  
|SQL_ROW_NUMBER|결과 집합 내에서 현재 행의 위치를 지정 하는 32 비트 정수를 반환 합니다. Get만 사용 합니다. 설정할 수 없습니다.|  
|SQL_ROWSET_SIZE|4294967296 행을 초과할 수 없습니다. 그러나 요청을 처리할 컴퓨터에 가상 메모리가 충분 한 있어야 합니다.|  
|SQL_USE_BOOKMARKS|에서는 SQL_USE_BOOKMARKS SQL_UB_ON를 설정 하 고 고정 길이의 책갈피를 노출 합니다.|
