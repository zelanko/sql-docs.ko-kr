---
description: SQLSetScrollOptions(Visual FoxPro ODBC 드라이버)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0e7cecfb0ce7640575cb69f1e84e805a884b57b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421637"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 부분  
  
 ODBC API 규칙: 수준 2  
  
 문 핸들 *hstmt*와 연결 된 커서의 동작을 제어 하는 옵션을 설정 합니다.  
  
 Visual FoxPro ODBC 드라이버는 SQL_CONCUR_READ_ONLY만 지원 합니다. SQL_CONCUR_ROWVER *Fconcurrency* 값을 지원 하지 않습니다. 드라이버는 SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC 및 SQL_CURSOR_KEYSET_DRIVEN를 경고 ODBC_01S02와 SQL_SCROLL_STATIC로 변환 합니다.  
  
 자세한 내용은 *ODBC 프로그래머 참조*에서 [SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) 를 참조 하세요.
