---
title: ODBC 개요 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6b064436dae6cb2f3d5f37fa02ab57a1e4a3f015
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63272926"
---
# <a name="odbc-overview"></a>ODBC 개요
개방형 데이터베이스 연결 (ODBC)는 널리 사용 되는 응용 프로그램 프로그래밍 인터페이스 (API) 데이터베이스 액세스에 대 한 경우 데이터베이스 Api에 대 한 Open Group 및 ISO/IEC 호출 수준 인터페이스 (CLI) 사양을 기반으로 하 고 해당 데이터베이스 액세스 언어로 SQL 구조적 쿼리 언어 ()를 사용 합니다.  
  
 ODBC 최대 용인지 *상호 운용성* -즉, 동일한 소스 코드를 사용 하 여 다른 데이터베이스 관리 시스템 (Dbms)에 액세스 하는 단일 응용 프로그램의 기능입니다. ODBC 인터페이스에서 호출 하는 데이터베이스 관련 모듈에서 구현 된 함수를 호출 하는 데이터베이스 응용 프로그램 *드라이버*합니다. 드라이버를 사용할 프린터 드라이버 격리 프린터 관련 명령의 워드 프로세서 프로그램은 동일한 방식으로 데이터베이스 관련 호출에서 응용 프로그램을 격리 합니다. 새 DBMS;에 액세스 하는 새 드라이버를 추가 하려면 사용자에만 드라이버가 런타임에 로드 되 면 되므로 다시 컴파일하거나 응용 프로그램을 다시 연결 하는 데 필요한 것입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC가 만들어진 이유](../../odbc/reference/why-was-odbc-created.md)  
  
-   [ODBC란?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 및 표준 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
