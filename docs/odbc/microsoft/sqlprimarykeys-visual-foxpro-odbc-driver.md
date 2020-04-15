---
title: SQLPrimary키(비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
ms.openlocfilehash: 83631d22bd07017c4eba8f6af171443ab8c76d9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301548"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys(Visual FoxPro ODBC 드라이버)
> [!NOTE]  
>  이 항목에는 Visual FoxPro ODBC 드라이버 관련 정보가 포함되어 있습니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 지원: 전체  
  
 ODBC API 적합성: 수준 2  
  
 테이블의 기본 키를 구성하는 열 이름을 반환합니다. **SQLPrimary키의** 시각적 FoxPro ODBC 드라이버 구현은 다음과 같이 실행됩니다.  
  
-   *szTable소유자* 및 *cbTableOwner* 인수를 무시합니다.  
  
-   데이터베이스인 데이터 원본에대해서만 [작동합니다.](../../odbc/microsoft/visual-foxpro-terminology.md) 데이터 원본이 [사용 이 테이블의](../../odbc/microsoft/visual-foxpro-terminology.md)디렉토리인 경우 드라이버는 "드라이버가 이 기능을 지원하지 않습니다"라는 오류를 반환합니다.  
  
 자세한 내용은 *ODBC 프로그래머 의 참조에서* [SQLPrimary키를](../../odbc/reference/syntax/sqlprimarykeys-function.md) 참조하십시오.
