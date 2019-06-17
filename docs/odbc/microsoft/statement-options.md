---
title: 문 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- custom statement options [ODBC]
- statement options [ODBC]
- ODBC driver for Oracle [ODBC], statement options
ms.assetid: cd73b769-c8b5-43e0-9f80-b3011b7a6162
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe57ffa0d7628601fcb6dd19218715b32a57322b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270019"
---
# <a name="statement-options"></a>명령문 옵션
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 이러한 옵션에는 사용자 지정 응용 프로그램 내에서 특정 실행 문의 수 있습니다.  
  
|문 옵션|참고|  
|----------------------|-----------|  
|SQL_BIND_TYPE|사용 가능한 메모리 또는 2,147,483,647 바이트를 초과할 수 없습니다.|  
|SQL_CONCURRENCY|허용 되는 값에 대 한 참조를 [커서 유형 및 동시성 조합](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)합니다.|  
|SQL_CURSOR_TYPE|드라이버는 SQL_CURSOR_DYNAMIC를 허용 하지 않습니다. 참조 [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) 자세한 내용은 합니다. 허용 되는 값에 대 한 참조를 [커서 유형 및 동시성 조합](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)합니다.|  
|SQL_GET_BOOKMARK|현재 레코드 수에 대 한 책갈피는 32 비트 정수 값을 반환 합니다. Get만 해당 합니다. 설정할 수 없습니다.|  
|SQL_KEYSET_SIZE|0에만 설정할 수 있습니다.|  
|SQL_MAX_ROWS|집합을 결과로 반환할 행의 최대 수입니다.|  
|SQL_ROW_NUMBER|결과 집합 내의 현재 행의 위치를 지정 하는 32 비트 정수를 반환 합니다. Get만 해당 합니다. 설정할 수 없습니다.|  
|SQL_ROWSET_SIZE|4294967296 행을 초과할 수 없습니다. 그러나 가상 메모리가 부족 하 여 요청을 처리할 컴퓨터에 있어야 합니다.|  
|SQL_USE_BOOKMARKS|SQL_UB_ON SQL_USE_BOOKMARKS 설정을 지원 하 고 고정 길이 책갈피를 노출 합니다.|
