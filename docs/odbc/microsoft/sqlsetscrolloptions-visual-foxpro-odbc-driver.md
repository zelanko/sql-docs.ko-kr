---
title: "SQLSetScrollOptions (Visual FoxPro ODBC 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 63efd04bc43855c08a6de02d5396bea45eabbc68
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 부분  
  
 ODBC API 규칙: 수준 2  
  
 문 핸들에 연결 된 커서의 동작을 제어 하는 옵션을 설정 *hstmt*합니다.  
  
 Visual FoxPro ODBC 드라이버는 SQL_CONCUR_READ_ONLY;만 지원합니다. 지원 하지 않습니다는 *fConcurrency* SQL_CONCUR_ROWVER 값입니다. 드라이버 경고 ODBC_01S02 SQL_SCROLL_STATIC 하 SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC, 및 SQL_CURSOR_KEYSET_DRIVEN를 변환합니다.  
  
 자세한 내용은 참조 [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) 에 *ODBC Programmer's Reference*합니다.

