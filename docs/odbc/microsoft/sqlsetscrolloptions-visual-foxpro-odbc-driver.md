---
title: SQLSetScrollOptions (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
- SQLSetScrollOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 693e6e28-a845-41b1-9622-5058b0d87229
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81542e2e2187872725bd4db5f5922dbbefb2f944
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 부분  
  
 ODBC API 규칙: 수준 2  
  
 문 핸들에 연결 된 커서의 동작을 제어 하는 옵션을 설정 *hstmt*합니다.  
  
 Visual FoxPro ODBC 드라이버는 SQL_CONCUR_READ_ONLY;만 지원합니다. 지원 하지 않습니다는 *fConcurrency* SQL_CONCUR_ROWVER 값입니다. 드라이버 경고 ODBC_01S02 SQL_SCROLL_STATIC 하 SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC, 및 SQL_CURSOR_KEYSET_DRIVEN를 변환합니다.  
  
 자세한 내용은 참조 [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) 에 *ODBC Programmer's Reference*합니다.
