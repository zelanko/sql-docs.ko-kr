---
title: SQLPrimaryKeys (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8e026ae53e7b69e3a060d8fe42c8be70f5d4f43
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에서는 Visual FoxPro ODBC 드라이버 관련 정보입니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 지원: 전체  
  
 ODBC API 규칙: 수준 2  
  
 테이블에 대 한 기본 키를 구성 하는 열 이름을 반환 합니다. Visual FoxPro ODBC 드라이버 구현의 **SQLPrimaryKeys** 다음과 같이 동작 합니다.  
  
-   무시 된 *szTableOwner* 및 *cbTableOwner* 인수입니다.  
  
-   데이터 원본에 대해서만 작동 [데이터베이스](../../odbc/microsoft/visual-foxpro-terminology.md)합니다. 드라이버는 경우 오류를 반환 "드라이버가이 함수를 지원 하지 않습니다" 데이터 소스 디렉터리가 [테이블 있음](../../odbc/microsoft/visual-foxpro-terminology.md)합니다.  
  
 자세한 내용은 참조 [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) 에 *ODBC Programmer's Reference*합니다.
