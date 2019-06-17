---
title: ODBC란? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc9c7a3d9f75e1863d90b16986234e0036229d01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714095"
---
# <a name="what-is-odbc"></a>ODBC란?
ODBC에 대 한 많은 오해 컴퓨팅 전 세계에 존재합니다. 최종 사용자에 게는 Microsoft® Windows® 제어판에 있는 아이콘 것입니다. 응용 프로그램 프로그래머에 게 데이터 액세스 루틴을 포함 하는 라이브러리는 것입니다. 기타 다양 한 항목 것 적이 기대 하는 모든 데이터베이스 액세스 문제에 대 한 답 합니다.  
  
 무엇 보다도, ODBC는 데이터베이스 API에 대 한 사양입니다. 이 API는 하나의 DBMS 또는 운영 체제에 독립적입니다. 이 설명서는 C를 사용 하지만 ODBC API는 언어 독립적입니다. ODBC API는 Open Group 및 ISO/IEC는 CLI 사양을 기반으로 합니다. ODBC 3입니다. *x* 완전히-이전 버전의 ODBC 예비 버전의 이러한 사양 기반 되었지만 완전히 구현 하지 않았습니다.-이러한 사양의 둘 다 구현 하 고 화면 중심의 개발자가 일반적으로 필요한 기능 추가 스크롤 가능 커서와 같은 데이터베이스 응용 프로그램을 합니다.  
  
 ODBC API 함수는 특정 DBMS 드라이버의 개발자가 구현 됩니다. 이러한 드라이버는 DBMS에 관계 없이 데이터에 액세스 하는 함수를 호출 하는 응용 프로그램입니다. 드라이버 관리자는 응용 프로그램 및 드라이버 간의 통신을 관리합니다.  
  
 Microsoft Microsoft Windows® 95를 실행 하는 컴퓨터에 대 한 드라이버 관리자를 제공 하 고 나중에 작성 된 여러 ODBC 드라이버 및 ODBC 함수를 호출 응용 프로그램의 일부 이지만 ODBC 응용 프로그램 및 드라이버를 작성할 수 누구나 합니다. 사실 대부분의 ODBC 응용 프로그램 및 드라이버를 사용할 수 있는 현재 기록 됩니다 Microsoft 이외의 회사에서. 또한 ODBC 드라이버 및 응용 프로그램을 Macintosh® 및 다양 한 UNIX 플랫폼에 존재합니다.  
  
 나중에 제공 하는 드라이버 관리자, 설치 관리자 DLL, 테스트 도구 및 샘플 응용 프로그램 및 응용 프로그램 및 드라이버 개발자를 위해 Microsoft는 ODBC 소프트웨어 개발 키트 (SDK) Windows 95를 실행 하는 컴퓨터에 대 한 제공 합니다. Microsoft가 Visigenic 소프트웨어 Macintosh 및 UNIX 플랫폼의 다양 한이 Sdk 이러한 포트를 사용 하 여 팀으로 구성 됩니다.  
  
 ODBC 데이터베이스 기능을 노출 하지 보완을으로 디자인 되었다는 것을 이해 하는 것이 반드시 합니다. 따라서 응용 프로그램 작성자는는 ODBC를 사용 하 여에서는 갑자기 변환 간단한 데이터베이스 기능 갖춘된 관계형 데이터베이스 엔진을 기대할 수 없습니다. 또는 드라이버 작성자 것으로 예상 되는 기본 데이터베이스에서 찾을 수 없는 기능을 구현 합니다. 이 예외는 파일 데이터 (예: Xbase 파일의 데이터)를 직접 액세스 하는 드라이버를 작성 하는 개발자는 적어도 최소 SQL 기능을 지 원하는 데이터베이스 엔진을 작성 해야 합니다. 다른 예외는 이전에 Microsoft 데이터 액세스 구성 요소 (MDAC) SDK를 포함 하는 Windows SDK의 ODBC 구성 요소, 특정 수준의 기능을 구현 하는 드라이버에 대 한 스크롤 가능 커서를 시뮬레이션 하는 커서 라이브러리를 제공 합니다.  
  
 ODBC를 사용 하는 응용 프로그램은 모든 데이터베이스 간 기능을 담당 합니다. 예를 들어 ODBC는 유형이 다른 조인 엔진을 아닙니다 아니고 분산된 트랜잭션 프로세서. 그러나 DBMS 독립적 이기 때문에 이러한 데이터베이스 간 도구를 빌드하는 사용할 수 있습니다.
