---
title: SQLSpecialColumns (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96b439674c8bda3494b4cefd0c1118602b537cd0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299383"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 1  
  
 테이블에서 행을 고유 하 게 식별 하는 최적의 열 집합을 검색 합니다.  
  
 Visual FoxPro ODBC 드라이버는 FoxPro 테이블의 기본 키를 구성 하는 열을 반환 합니다. [Sqlprimarykeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)를 참조 하세요. *Fcoltype* 을 SQL_ROWVER로 설정 하 여 호출 하면 열이 반환 되지 않습니다. **SQLSpecialColumns** 는 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)에 해당 하는 데이터 원본에 대해서만 작동 합니다.  
  
 자세한 내용은 *ODBC 프로그래머 참조*에서 [SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md) 를 참조 하세요.
