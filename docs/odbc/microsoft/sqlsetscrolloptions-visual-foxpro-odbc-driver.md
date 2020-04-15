---
title: SQLSet스크롤 옵션 (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
ms.openlocfilehash: 19051fc83466bc40d72c029089cfe6ec45c20a08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299423"
---
# <a name="sqlsetscrolloptions-visual-foxpro-odbc-driver"></a>SQLSetScrollOptions(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 부분  
  
 ODBC API 적합성: 수준 2  
  
 명령문 핸들 *hstmt와*연관된 커서의 동작을 제어하는 옵션을 설정합니다.  
  
 비주얼 FoxPro ODBC 드라이버는 SQL_CONCUR_READ_ONLY 지원됩니다. SQL_CONCUR_ROWVER *fConcurrency* 값을 지원하지 않습니다. 운전자는 SQL_KEYSET_SIZE, SQL_CURSOR_DYNAMIC 및 SQL_CURSOR_KEYSET_DRIVEN 경고 ODBC_01S02 SQL_SCROLL_STATIC 변환합니다.  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLSetScroll 옵션을](../../odbc/reference/syntax/sqlsetscrolloptions-function.md) 참조하십시오.
