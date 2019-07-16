---
title: SQLPrepare (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5835ddaf27d097dcfff608649f50c1f7f41a93df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996309"
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 코어 수준  
  
 최적화 하 고 문을 실행 하는 방법을 계획 하 여 SQL 문을 준비 합니다. 실행에 대 한 SQL 문이 컴파일된 [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)합니다.  
  
 사용자 테이블, 뷰 또는 필드 이름에 공백이 있으면 이름을 뒤에 따옴표 (') 표시를 묶습니다. 예를 들어, 데이터베이스 내 테이블 및 필드 My Field 라는 테이블에 있으면 묶습니다 식별자의 각 요소를 다음과 같습니다.  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 자세한 내용은 [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) 에 *ODBC 프로그래머 참조*합니다.
