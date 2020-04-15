---
title: ODBC 개요 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a0515a882cd7d1c97a60e9262942bd7c397b0b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298293"
---
# <a name="odbc-overview"></a>ODBC 개요
개방형 데이터베이스 연결(ODBC)은 데이터베이스 액세스를 위해 널리 사용되는 응용 프로그램 프로그래밍 인터페이스(API)입니다. 데이터베이스 API에 대한 개방형 그룹 및 ISO/IEC의 CLI(통화 수준 인터페이스) 사양을 기반으로 하며 SQL(구조화 쿼리 언어)을 데이터베이스 액세스 언어로 사용합니다.  
  
 ODBC는 최대 *상호 운용성을* 위해 설계되었습니다- 즉, 단일 응용 프로그램이 동일한 소스 코드로 다른 DBMS(데이터베이스 관리 시스템)에 액세스할 수 있는 기능입니다. 데이터베이스 응용 프로그램은 ODBC 인터페이스에서 함수를 호출하며, 이 함수는 *드라이버라는*데이터베이스 별 모듈에서 구현됩니다. 드라이버를 사용하면 프린터 드라이버가 워드 프로세싱 프로그램을 프린터 별 명령에서 격리하는 것과 같은 방식으로 데이터베이스별 호출에서 응용 프로그램을 격리합니다. 드라이버는 런타임에 로드되므로 새 DBMS에 액세스하려면 새 드라이버만 추가하면 됩니다. 응용 프로그램을 다시 컴파일하거나 다시 연결할 필요는 없습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC가 만들어진 이유](../../odbc/reference/why-was-odbc-created.md)  
  
-   [ODBC란?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 및 표준 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
