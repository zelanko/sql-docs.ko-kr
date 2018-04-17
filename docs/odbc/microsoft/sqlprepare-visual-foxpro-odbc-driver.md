---
title: SQLPrepare (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- SQLPrepare function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 0c4cb5a4-9729-4b2e-a0c6-52027b92e8fc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 55217c84b7cb32f35f83a9741057230721f724fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlprepare-visual-foxpro-odbc-driver"></a>SQLPrepare (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 핵심 수준  
  
 최적화 하 고 문을 실행 하는 방법을 계획 하 여 SQL 문을 준비 합니다. 실행 SQL 문이 컴파일된 [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)합니다.  
  
 테이블, 뷰 또는 필드 이름에 공백이 있으면 이름을 뒤에 따옴표 (') 기호를 묶습니다. 예를 들어 경우 데이터베이스 내 테이블 및 필드 My Field 라는 테이블 묶습니다 식별자의 각 요소를 다음과 같습니다.  
  
```  
SELECT * FROM `My Table`.`My Field`  
```  
  
 자세한 내용은 참조 [SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md) 에 *ODBC Programmer's Reference*합니다.
