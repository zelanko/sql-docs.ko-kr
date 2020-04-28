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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca40765dff98e9102fbe36e88c7e79535f311d97
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299213"
---
# <a name="statement-options"></a>명령문 옵션
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 이러한 옵션을 사용 하면 응용 프로그램 내에서 특정 실행 문을 사용자 지정할 수 있습니다.  
  
|문 옵션|참고|  
|----------------------|-----------|  
|SQL_BIND_TYPE|2147483647 바이트 또는 사용 가능한 메모리를 초과할 수 없습니다.|  
|SQL_CONCURRENCY|허용 되는 값은 [커서 유형 및 동시성 조합](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)을 참조 하세요.|  
|SQL_CURSOR_TYPE|드라이버가 SQL_CURSOR_DYNAMIC을 허용 하지 않습니다. 자세한 내용은 [SQLSetScrollOptions](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) 를 참조 하세요. 허용 되는 값은 [커서 유형 및 동시성 조합](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)을 참조 하세요.|  
|SQL_GET_BOOKMARK|현재 레코드 번호의 책갈피 인 32 비트 정수 값을 반환 합니다. 가져오기 전용; 를 설정할 수 없습니다.|  
|SQL_KEYSET_SIZE|0 으로만 설정할 수 있습니다.|  
|SQL_MAX_ROWS|결과 집합에서 반환할 최대 행 수입니다.|  
|SQL_ROW_NUMBER|결과 집합 내에서 현재 행의 위치를 지정 하는 32 비트 정수를 반환 합니다. 가져오기 전용; 를 설정할 수 없습니다.|  
|SQL_ROWSET_SIZE|4294967296 행을 초과할 수 없습니다. 그러나 사용자의 요청을 처리할 수 있도록 컴퓨터에 충분 한 가상 메모리가 있어야 합니다.|  
|SQL_USE_BOOKMARKS|SQL_UB_ON SQL_USE_BOOKMARKS를 설정 하 고 고정 길이 책갈피를 노출 하도록 지원 합니다.|
