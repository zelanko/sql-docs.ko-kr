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
ms.openlocfilehash: 5521fb11cad064cf487d38562f4146fd32587993
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898791"
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 1  
  
 문 옵션의 현재 설정을 반환 합니다.  
  
|*FOption*|반환|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|현재 레코드 번호의 책갈피 인 32 비트 정수 값입니다.|  
|SQL_ROW_NUMBER|결과 집합 내에서 현재 행의 위치를 지정 하는 32 비트 정수입니다.|  
|SQL_TRANSLATE_DLL|오류: "드라이버를 사용할 수 없음"|  
  
 Visual FoxPro ODBC 드라이버에는 변환 Dll이 없습니다.  
  
 자세한 내용은 *ODBC 프로그래머 참조*에서 [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) 를 참조 하세요.
