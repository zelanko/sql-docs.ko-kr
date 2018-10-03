---
title: SQLSetScrollOptions (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c2d78e26309d5ea7dc5e6eed5a04e84a1651b33
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622633"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: Partial  
  
 ODBC API 규칙: 수준 2  
  
 문 핸들을 사용 하 여 연결 된 커서의 동작을 제어 하는 옵션을 설정 합니다 *hstmt*합니다.  
  
 Visual FoxPro ODBC 드라이버에만 SQL_CONCUR_READ_ONLY; 지원 지원 되지 않습니다 합니다 *fConcurrency* SQL_CONCUR_ROWVER 값입니다. 드라이버 경고 ODBC_01S02 SQL_SCROLL_STATIC를 SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC, 및 SQL_CURSOR_KEYSET_DRIVEN를 변환합니다.  
  
 자세한 내용은 [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) 에 *ODBC 프로그래머 참조*합니다.
