---
title: SQLGetStmtOption (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984a8b1d-f12c-420c-8be4-f555114c764b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cb9e9178d7b90afaaa5cd324f79459a14a2dcc6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetstmtoption-visual-foxpro-odbc-driver"></a>SQLGetStmtOption (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 수준 1 ODBC API 적용 합니다.  
  
 문 옵션의 현재 설정을 반환합니다.  
  
|*fOption*|반환 값|  
|---------------|-------------|  
|SQL_GET_BOOKMARK|현재 레코드 번호에 대 한 책갈피는 32 비트 정수 값을|  
|SQL_ROW_NUMBER|결과에서 현재 행의 위치를 지정 하는 32 비트 정수 설정|  
|SQL_TRANSLATE_DLL|오류: "드라이버 사용할 수 없습니다.|  
  
 Visual FoxPro ODBC 드라이버 Dll 변환을 있습니다.  
  
 자세한 내용은 참조 [SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md) 에 *ODBC Programmer's Reference*합니다.
