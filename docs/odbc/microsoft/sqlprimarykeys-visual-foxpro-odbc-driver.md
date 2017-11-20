---
title: "SQLPrimaryKeys (Visual FoxPro ODBC 드라이버) | Microsoft Docs"
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
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8906d8672c44eaf6a2e8cc6fbfc63189a4dcbda2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

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

