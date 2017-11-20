---
title: "SQLSpecialColumns (Visual FoxPro ODBC 드라이버) | Microsoft Docs"
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
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3128dca9f473008b5e5fcae234fd9ba119911e81
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 수준 1 ODBC API 적용:  
  
 테이블의 행을 고유 하 게 식별 하는 열의 최적 집합을 검색 합니다.  
  
 Visual FoxPro ODBC 드라이버는 FoxPro 테이블에 기본 키를 구성 하는 열을 반환 합니다. (참조 [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md).) 호출 *fColType* SQL_ROWVER로 설정, 열이 없으면 반환 됩니다. **SQLSpecialColumns** 인 데이터 원본에 대해서만 작동 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)합니다.  
  
 자세한 내용은 참조 [SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md) 에 *ODBC Programmer's Reference*합니다.

