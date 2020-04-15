---
title: SQLSetStmt옵션(데스크톱 데이터베이스 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69b386aee3f95fd047f72510dce7658130ac7aa5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299413"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption(데스크톱 데이터베이스 드라이버)

|*f옵션*|주석|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|비동기 처리는 지원되지 않습니다. SQL_ASYNC_ENABLE fOption은 SQLSTATE S1C00 (드라이버를 할 수 없음)을 반환합니다.|  
|SQL_KEYSET_SIZE|혼합 커서와 동적 커서가 지원되지 않으므로 유효한 키 집합 크기는 0입니다. 이 값이 다른 숫자로 설정되면 0으로 변경되고 호출이 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01S02(옵션 값 변경)로 반환됩니다.|  
|SQL_MAX_ROWS|데스크톱 데이터베이스 드라이버는 반환되는 행 수를 제한하는 것을 지원하지 않으므로 유효한 행 집합 크기는 0입니다. 이 값이 다른 숫자로 설정되면 0으로 변경되고 호출이 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01S02(옵션 값 변경)로 반환됩니다.|  
|SQL_QUERY_TIMEOUT|지원되지 않습니다.|  
|SQL_ROW_NUMBER|지원되지 않습니다.|  
|SQL_SIMULATE_CURSOR|지원되지 않습니다.|
