---
description: SQLPrimaryKeys(Visual FoxPro ODBC 드라이버)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96b333e10c7000a8a44e957e33d0c84a3b004f43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483346"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함 되어 있습니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 2  
  
 테이블의 기본 키를 구성 하는 열 이름을 반환 합니다. **Sqlprimarykeys** 의 VISUAL FoxPro ODBC 드라이버 구현은 다음과 같이 동작 합니다.  
  
-   *Sztableowner* 및 *cbtableowner* 인수를 무시 합니다.  
  
-   [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)의 데이터 원본에 대해서만 작동 합니다. 데이터 원본이 [사용 가능한 테이블](../../odbc/microsoft/visual-foxpro-terminology.md)의 디렉터리인 경우 드라이버는 "이 기능을 지원 하지 않습니다." 라는 오류를 반환 합니다.  
  
 자세한 내용은 *ODBC 프로그래머 참조*에서 [sqlprimarykeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) 를 참조 하세요.
