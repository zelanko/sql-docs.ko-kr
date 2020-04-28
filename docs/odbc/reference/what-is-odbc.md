---
title: ODBC란? | Microsoft 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea0aa81188e5e58d3a66032af38700ece2d4e5b4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286503"
---
# <a name="what-is-odbc"></a>ODBC란?
ODBC에 대 한 많은 오해 컴퓨팅 환경에 있습니다. 최종 사용자에 게는 Microsoft® Windows® 제어판의 아이콘이 있습니다. 응용 프로그램 프로그래머는 데이터 액세스 루틴이 포함 된 라이브러리입니다. 다른 많은 데이터베이스 액세스 문제에 대 한 답입니다.  
  
 무엇 보다도 ODBC는 데이터베이스 API에 대 한 사양입니다. 이 API는 하나의 DBMS 또는 운영 체제에 독립적입니다. 이 설명서에서는 C를 사용 하지만 ODBC API는 언어에 독립적입니다. ODBC API는 Open Group 및 ISO/IEC의 CLI 사양을 기반으로 합니다. ODBC 3. *x* 는 이러한 사양을 모두 완전히 구현 합니다. 이전 버전의 ODBC는 이러한 사양의 예비 버전을 기반으로 하지만 완전히 구현 하지는 않았으며 스크롤 가능 커서와 같은 화면 기반 데이터베이스 응용 프로그램 개발자가 일반적으로 필요로 하는 기능을 추가 합니다.  
  
 ODBC API의 함수는 DBMS 관련 드라이버의 개발자에 의해 구현 됩니다. 응용 프로그램은 이러한 드라이버의 함수를 호출 하 여 DBMS 독립적 방식으로 데이터에 액세스 합니다. 드라이버 관리자는 응용 프로그램과 드라이버 간의 통신을 관리 합니다.  
  
 Microsoft에서 Microsoft Windows® 95 이상을 실행 하는 컴퓨터에 대 한 드라이버 관리자를 제공 하 고,에서는 몇 가지 ODBC 드라이버를 작성 하 고 일부 응용 프로그램에서 ODBC 함수를 호출 하 고, 누구나 ODBC 응용 프로그램 및 드라이버를 작성할 수 있습니다. 실제로 현재 사용할 수 있는 대부분의 ODBC 응용 프로그램 및 드라이버는 Microsoft 이외의 회사에서 작성 한 것입니다. 또한 ODBC 드라이버 및 응용 프로그램은 Macintosh®와 다양 한 UNIX 플랫폼에 있습니다.  
  
 응용 프로그램 및 드라이버 개발자를 지원 하기 위해 Microsoft는 Windows 95 이상을 실행 하는 컴퓨터에 대 한 ODBC SDK (소프트웨어 개발 키트)를 제공 하며,이를 통해 드라이버 관리자, 설치 관리자 DLL, 테스트 도구 및 샘플 응용 프로그램을 제공 합니다. Microsoft는 이러한 Sdk를 Macintosh와 다양 한 UNIX 플랫폼으로 이식할 수 있도록 Visigenic 소프트웨어를 팀으로 구성 했습니다.  
  
 ODBC는 데이터베이스 기능을 보완 하는 것이 아니라 데이터베이스 기능을 노출 하도록 설계 되었다는 점을 이해 하는 것이 중요 합니다. 따라서 응용 프로그램 작성자는 ODBC를 사용 하는 것으로 인해 간단한 데이터베이스를 완전 한 기능을 갖춘 관계형 데이터베이스 엔진으로 변환할 수 없습니다. 및는 기본 데이터베이스에서 찾을 수 없는 기능을 구현 하는 데 필요한 드라이버 기록기입니다. 단, 파일 데이터에 직접 액세스 하는 드라이버 (예: Xbase 파일의 데이터)를 작성 하는 개발자는 최소한의 SQL 기능을 지 원하는 데이터베이스 엔진을 작성 해야 합니다. 또 다른 예외로, 이전에는 MDAC (Microsoft Data Access Components) SDK에 포함 된 Windows SDK의 ODBC 구성 요소가 특정 수준의 기능을 구현 하는 드라이버에 대해 스크롤 가능한 커서를 시뮬레이트하는 커서 라이브러리를 제공 합니다.  
  
 ODBC를 사용 하는 응용 프로그램은 데이터베이스 간 기능을 담당 합니다. 예를 들어 ODBC는 다른 유형의 조인 엔진이 아니며 분산 트랜잭션 프로세서가 아닙니다. 그러나 DBMS 독립적 이기 때문에 이러한 데이터베이스 간 도구를 빌드하는 데 사용할 수 있습니다.
