---
title: "ODBC 란? | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 544f4aa32119b0fde5971f76e46a382b92dbd3ef
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="what-is-odbc"></a>ODBC 란?
ODBC에 대 한 많은 오해 컴퓨팅 환경에 존재합니다. 최종 사용자에 게는 Microsoft® Windows® 제어판에 있는 아이콘 응용 프로그램 프로그래머를 데이터 액세스 루틴을 포함 하는 라이브러리입니다. 봄으로써을 상상한 적이 모든 데이터베이스 액세스 문제에 대 한 대답입니다.  
  
 무엇 보다도, ODBC는 데이터베이스 API에 대 한 사양입니다. 이 API는 하나의 DBMS 또는 운영 체제; 독립적입니다. 이 설명서에서는 C 하지만 ODBC API는 언어 독립적입니다. ODBC API Open Group 및 ISO/IEC에서 CLI 사양을 기반으로 합니다. ODBC 3입니다. *x* 완벽 하 게이 내용을 모두 구현-이전 버전의 ODBC 된이 내용을 예비 버전을 기반으로 하지만 완벽 하 게 구현 하지 않은-화면 중심의 개발자가 일반적으로 필요한 기능 추가 스크롤 가능 커서와 같은 데이터베이스 응용 프로그램을 합니다.  
  
 함수는 ODBC API에는 특정 DBMS 드라이버의 개발자가 구현 됩니다. 이러한 드라이버는 DBMS에 관계 없이 데이터에 액세스 하는 함수를 호출 하는 응용 프로그램입니다. 드라이버 관리자는 응용 프로그램 및 드라이버 간의 통신을 관리 합니다.  
  
 Microsoft은 Microsoft Windows® 95를 실행 하는 컴퓨터에 대 한 드라이버 관리자가 제공 하 고 이상 버전에서는 입력 된 몇 가지 ODBC 드라이버 및 ODBC 함수를 호출에서 해당 응용 프로그램을 ODBC 응용 프로그램 및 드라이버를 작성할 수 누구나 합니다. 실제로 대부분의 ODBC 응용 프로그램 및 드라이버를 사용할 수 있는 현재 쓰여집니다 Microsoft 이외의 회사에서. 또한 ODBC 드라이버와 응용 프로그램의 Macintosh®와 다양 한 UNIX 플랫폼의 경우에 존재 합니다.  
  
 응용 프로그램 및 드라이버 개발자를 위해 Microsoft는 ODBC 소프트웨어 개발 키트 (SDK) Windows 95를 실행 하는 컴퓨터에 대 한 소개 하며 드라이버 관리자, 설치 관리자 DLL, 테스트 도구 및 샘플 응용 프로그램을 제공 하는 나중에 합니다. Microsoft가 Visigenic 소프트웨어 Macintosh와 다양 한 UNIX 플랫폼의 경우에이 Sdk를 이식 하는 팀을 구성 합니다.  
  
 ODBC는 데이터베이스 기능을 제공 하려면 하지 보완 하기 위해 설계 되었습니다 이해 하는 것이 유용 합니다. 응용 프로그램 작성자는 ODBC를 사용 하 여에서는 갑자기 변환 간단한 데이터베이스는 완전 한 기능의 관계형 데이터베이스 엔진 기대 하지 따라서 합니다. 또는 드라이버 작성자 것으로 예상 되는 기본 데이터베이스에 없는 기능을 구현 합니다. 이 예외는 하 파일 데이터 (예: Xbase 파일의 데이터)에 직접 액세스 하는 드라이버를 작성 하는 개발자는 이상 최소한의 SQL 기능을 지 원하는 데이터베이스 엔진을 작성 하는 데 필요 합니다. 다른 예외는 이전에 Microsoft 데이터 액세스 구성 요소 (MDAC) SDK를 포함 하는 Windows SDK의 ODBC 구성 요소, 일정 수준의 기능을 구현 하는 드라이버에 대 한 스크롤 가능 커서를 시뮬레이션 하는 커서 라이브러리를 제공 합니다.  
  
 ODBC를 사용 하는 응용 프로그램은 모든 데이터베이스 간 기능을 수행 합니다. 예를 들어 ODBC 형식이 다른 조인 엔진 해당 되지 않으며은 분산 된 트랜잭션 프로세서 아닙니다. 그러나 DBMS 독립적 이기 때문에 이러한 데이터베이스 간 도구를 만들 사용할 수 있습니다.
