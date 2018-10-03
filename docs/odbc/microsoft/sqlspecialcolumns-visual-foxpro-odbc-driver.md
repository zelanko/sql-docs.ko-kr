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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c4095448b8a9068dad3c4df1c28065e7cffbd67
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721150"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 수준 1 ODBC API 규칙:  
  
 테이블의 행을 고유 하 게 식별 하는 최적의 열 집합을 검색 합니다.  
  
 Visual FoxPro ODBC 드라이버는 FoxPro 테이블에 기본 키를 구성 하는 열을 반환 합니다. (참조 [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md).) 사용 하 여 호출 *fColType* SQL_ROWVER로 열이 없으면 반환 됩니다. **SQLSpecialColumns** 에 있는 데이터 원본에 대해서만 작동 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)합니다.  
  
 자세한 내용은 [SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md) 에 *ODBC 프로그래머 참조*합니다.
