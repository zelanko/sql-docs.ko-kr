---
title: SQLGetStmtOption (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 373f5e13712ef7b0864401ea3d2c204cb03ebb09
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240260"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 1  
  
 문 옵션의 현재 설정을 반환합니다.  
  
|*FOption*|반환 값|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|현재 레코드 수에 대 한 책갈피는 32 비트 정수 값을|  
|SQL_ROW_NUMBER|결과 내에서 현재 행의 위치를 지정 하는 32 비트 정수 설정|  
|SQL_TRANSLATE_DLL|오류: "드라이버를 사용할 수 없습니다."|  
  
 Visual FoxPro ODBC 드라이버에 Dll 변환 되지 않습니다.  
  
 자세한 내용은 [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) 에 *ODBC 프로그래머 참조*합니다.
