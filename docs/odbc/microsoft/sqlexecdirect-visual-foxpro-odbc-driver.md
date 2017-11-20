---
title: "SQLExecDirect (Visual FoxPro ODBC 드라이버) | Microsoft Docs"
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
- SQLExecDirect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5004060f-8510-4018-87a4-d41789e69d3e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3edf8a3bd785d3440af3347d457dd5078e289638
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlexecdirect-visual-foxpro-odbc-driver"></a>SQLExecDirect (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 핵심 수준  
  
 새 실행 [준비할 수 있는 SQL 문을](../../odbc/microsoft/visual-foxpro-terminology.md)합니다. Visual FoxPro ODBC 드라이버는 문에 매개 변수가 있는 경우 매개 변수 표식 변수의 현재 값을 사용 합니다.  
  
 한 번에 둘 이상의 SQL 문을 제출 하는 일괄 처리 명령을 만들려면 세미콜론 (;)를 사용 하 여 일괄 처리의 각 SQL 문을 구분 합니다.  
  
 테이블, 뷰 또는 필드 이름에 공백이 있으면 이름을 따옴표 뒤에 기호를 묶습니다. 예를 들어 경우 데이터베이스 내 테이블 및 필드 My Field 라는 테이블 묶습니다 식별자의 각 요소를 다음과 같습니다.  
  
```  
SELECT `My Table`.`Field1`, `My Table`.`Field2` FROM `My Table`  
```  
  
 자세한 내용은 참조 [SQLExecDirect](../../odbc/reference/syntax/sqlexecdirect-function.md) 에 *ODBC Programmer's Reference*합니다.

