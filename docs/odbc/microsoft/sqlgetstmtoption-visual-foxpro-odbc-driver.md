---
title: SQLGetStmt옵션 (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2624783f7bd55903f5741c62190626e455a9096d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295143"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 레벨 1  
  
 명령문 옵션의 현재 설정을 반환합니다.  
  
|*F옵션*|반환|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|현재 레코드 번호의 책갈피인 32비트 정수 값|  
|SQL_ROW_NUMBER|결과 집합 내에서 현재 행의 위치를 지정하는 32비트 정수|  
|SQL_TRANSLATE_DLL|오류: "드라이버를 수행할 수 없습니다."|  
  
 비주얼 폭스프로 ODBC 드라이버에는 번역 DLL이 없습니다.  
  
 자세한 내용은 *ODBC 프로그래머의 참조에서* [SQLGetStmt옵션을](../../odbc/reference/syntax/sqlgetstmtoption-function.md) 참조하십시오.
