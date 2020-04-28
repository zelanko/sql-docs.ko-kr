---
title: SQLSetStmtOption (데스크톱 데이터베이스 드라이버) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299413"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption(데스크톱 데이터베이스 드라이버)

|*fOption*|주석|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|비동기 처리가 지원 되지 않습니다. SQL_ASYNC_ENABLE fOption은 SQLSTATE S1C00 (드라이버를 사용할 수 없음)를 반환 합니다.|  
|SQL_KEYSET_SIZE|혼합 및 동적 커서는 지원 되지 않으므로 올바른 키 집합 크기는 0입니다. 이 값을 다른 숫자로 설정 하면 0으로 변경 되 고 호출은 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 합니다.|  
|SQL_MAX_ROWS|데스크톱 데이터베이스 드라이버는 반환 되는 행 수를 제한 하는 것을 지원 하지 않으므로 올바른 행 집합 크기는 0입니다. 이 값을 다른 숫자로 설정 하면 0으로 변경 되 고 호출은 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01 S 02 (옵션 값이 변경 됨)를 반환 합니다.|  
|SQL_QUERY_TIMEOUT|지원되지 않습니다.|  
|SQL_ROW_NUMBER|지원되지 않습니다.|  
|SQL_SIMULATE_CURSOR|지원되지 않습니다.|
