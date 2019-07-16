---
title: SQLExecDirect (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e701340217a885fbf1e3372c33ed1a8cfdb21457
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053855"
---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 코어 수준  
  
 새 실행 [preparable SQL 문을](../../odbc/microsoft/visual-foxpro-terminology.md)합니다. Visual FoxPro ODBC 드라이버 문에 매개 변수가 존재 하는 경우 매개 변수 표식 변수의 현재 값을 사용 합니다.  
  
 한 번에 둘 이상의 SQL 문을 전송할 일괄 처리 명령의 만들려면, 각 SQL 문의 일괄 처리에서를 구분 하려면 세미콜론 (;)를 사용 합니다.  
  
 사용자 테이블, 뷰 또는 필드 이름에 공백이 있으면 이름을 따옴표 뒤에 표시를 묶습니다. 예를 들어, 데이터베이스 내 테이블 및 필드 My Field 라는 테이블에 있으면 묶습니다 식별자의 각 요소를 다음과 같습니다.  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 자세한 내용은 [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) 에 *ODBC 프로그래머 참조*합니다.
