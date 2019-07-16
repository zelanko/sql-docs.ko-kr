---
title: SQLPrimaryKeys (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e85e60cde86c9483e69a8c43de14ef64eb914119
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030697"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보를 포함합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 2  
  
 테이블에 대 한 기본 키를 구성 하는 열 이름을 반환 합니다. Visual FoxPro ODBC 드라이버 구현의 **SQLPrimaryKeys** 다음과 같이 동작 합니다.  
  
-   무시 된 *szTableOwner* 하 고 *cbTableOwner* 인수입니다.  
  
-   데이터 원본에 대해서만 작동 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)합니다. 드라이버 오류 "드라이버가이 함수를 지원 하지 않습니다" 이면 반환 데이터 소스 디렉터리 [테이블을 무료](../../odbc/microsoft/visual-foxpro-terminology.md)합니다.  
  
 자세한 내용은 [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) 에 *ODBC 프로그래머 참조*합니다.
