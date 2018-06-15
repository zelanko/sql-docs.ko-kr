---
title: ODBC 개요 | Microsoft Docs
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
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39ab7586ebc1cd63d028caab0d3c2f09b82c7172
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916078"
---
# <a name="odbc-overview"></a>ODBC 개요
ODBC open Database Connectivity ()은 데이터베이스 액세스를 위해 널리 사용 되는 응용 프로그램 프로그래밍 인터페이스 (API). 데이터베이스 Api에 대 한 Open Group 및 ISO/IEC 호출 수준 인터페이스 (CLI) 사양을 기반으로 하 고 SQL 구조적 쿼리 언어 ()를 사용 하 여 해당 데이터베이스 액세스 언어입니다.  
  
 ODBC 최대 용인지 *상호 운용성* -즉, 동일한 소스 코드로 구성 된 다른 데이터베이스 관리 시스템 (Dbms)에 액세스 하는 단일 응용 프로그램의 기능입니다. 라는 데이터베이스 관련 모듈에서 구현 되는 ODBC 인터페이스에서 함수를 호출 하는 데이터베이스 응용 프로그램 *드라이버*합니다. 데이터베이스 관련 호출에서 응용 프로그램의 프린터 드라이버에서 프린터 관련 명령 워드 프로세서 프로그램을 격리 하는 것과 같은 방식으로 격리 하는 드라이버를 사용 합니다. 런타임 시 드라이버 로드 되 면 때문에 사용자에 게 새 DBMS;에 액세스 하려면 새 드라이버를 추가 하려면 다시 컴파일하거나 응용 프로그램을 다시 링크할 필요는 없습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC가 만들어진 이유](../../odbc/reference/why-was-odbc-created.md)  
  
-   [ODBC란?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 및 표준 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
