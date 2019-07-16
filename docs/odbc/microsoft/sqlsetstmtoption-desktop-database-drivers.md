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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 20043c96771bf888defa2c8fbeb028aaa18f5abc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905340"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption(데스크톱 데이터베이스 드라이버)

|*fOption*|주석|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|비동기 처리가 지원 되지 않습니다. SQL_ASYNC_ENABLE fOption SQLSTATE S1C00 반환 됩니다 (드라이버를 사용할 수 없습니다.).|  
|SQL_KEYSET_SIZE|혼합 하기 때문에 유효한 키 크기는 0, 및 동적 커서는 지원 되지 않습니다. 이 값을 다른 숫자를 설정 하는 경우 0으로 변경 됩니다 및 호출 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01S02를 반환 합니다 (옵션 값이 변경 됨).|  
|SQL_MAX_ROWS|유효한 행 집합 크기는 0, 데스크톱 데이터베이스 드라이버에 반환 되는 행 수를 제한 지원 하지 않기 때문입니다. 이 값을 다른 숫자를 설정 하는 경우 0으로 변경 됩니다 및 호출 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01S02를 반환 합니다 (옵션 값이 변경 됨).|  
|SQL_QUERY_TIMEOUT|지원되지 않습니다.|  
|SQL_ROW_NUMBER|지원되지 않습니다.|  
|SQL_SIMULATE_CURSOR|지원되지 않습니다.|
