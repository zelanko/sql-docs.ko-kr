---
description: ODBC 개요
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 13f34a1ef329957854a8b33916b6b29506fc0ad9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421317"
---
# <a name="odbc-overview"></a>ODBC 개요
ODBC (Open Database Connectivity)는 데이터베이스 액세스를 위해 널리 사용 되는 API (응용 프로그래밍 인터페이스)입니다. Open Group의 CLI (호출 수준 인터페이스) 사양과 데이터베이스 Api에 대 한 ISO/IEC를 기반으로 하며, 구조적 쿼리 언어 (SQL)를 데이터베이스 액세스 언어로 사용 합니다.  
  
 ODBC는 최대 *상호 운용성* 을 위해 설계 되었습니다. 즉, 단일 응용 프로그램이 동일한 소스 코드를 사용 하 여 다른 dbms (데이터베이스 관리 시스템)에 액세스 하는 기능을 제공 합니다. 데이터베이스 응용 프로그램은 ODBC 인터페이스의 함수를 호출 합니다 .이 함수는 *드라이버*라는 데이터베이스 전용 모듈에서 구현 됩니다. 드라이버를 사용 하는 경우 프린터 드라이버와 동일한 방식으로 응용 프로그램을 데이터베이스 관련 호출에서 격리 합니다. 드라이버는 런타임에 로드 되므로 사용자는 새 DBMS에 액세스 하기 위해 새 드라이버만 추가 하면 됩니다. 응용 프로그램을 다시 컴파일하거나 다시 연결할 필요는 없습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC가 만들어진 이유](../../odbc/reference/why-was-odbc-created.md)  
  
-   [ODBC란?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC 및 표준 CLI](../../odbc/reference/odbc-and-the-standard-cli.md)
