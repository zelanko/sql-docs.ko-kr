---
title: (데스크톱 데이터베이스 드라이버) SQLSetStmtOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b797d3eddb7eae9232aee3c73ceae7c12ca163d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (데스크톱 데이터베이스 드라이버)
|*fOption*|설명|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|비동기 처리가 지원 되지 않습니다. SQL_ASYNC_ENABLE fOption SQLSTATE S1C00를 반환 합니다 (드라이버를 사용할 수 없습니다.).|  
|SQL_KEYSET_SIZE|유효한 키 집합 크기는 0, 혼합 있으므로 및 동적 커서는 지원 되지 않습니다. 이 값을 다른 모든 숫자를 설정 하는 경우 0으로 변경 됩니다 하 고는 호출은 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01 s 02를 반환 합니다 (옵션 값이 변경 됨).|  
|SQL_MAX_ROWS|유효한 행 집합 크기는 0, 데스크톱 데이터베이스 드라이버는 반환 되는 행 수를 제한를 지원 하지 않기 때문입니다. 이 값을 다른 모든 숫자를 설정 하는 경우 0으로 변경 됩니다 하 고는 호출은 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01 s 02를 반환 합니다 (옵션 값이 변경 됨).|  
|SQL_QUERY_TIMEOUT|지원되지 않습니다.|  
|SQL_ROW_NUMBER|지원되지 않습니다.|  
|SQL_SIMULATE_CURSOR|지원되지 않습니다.|
