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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286503"
---
# <a name="what-is-odbc"></a>ODBC란?
ODBC에 대한 많은 오해는 컴퓨팅 세계에서 존재합니다. 최종 사용자에 게, 그것은 마이크로소프트의 아이콘® 윈도우® 제어판. 응용 프로그램 프로그래머에게 는 데이터 액세스 루틴이 포함된 라이브러리입니다. 다른 많은 사람들에게는 지금까지 상상했던 모든 데이터베이스 액세스 문제에 대한 해답입니다.  
  
 무엇보다도 ODBC는 데이터베이스 API에 대한 사양입니다. 이 API는 하나의 DBMS 또는 운영 체제와 독립적입니다. 이 설명서는 C를 사용하지만 ODBC API는 언어독립적입니다. ODBC API는 오픈 그룹 및 ISO/IEC의 CLI 사양을 기반으로 합니다. ODBC 3. *x는* 이러한 사양을 모두 완전히 구현합니다 - 이전 버전의 ODBC는 이러한 사양의 예비 버전을 기반으로 했지만 완전히 구현하지 는 않았으며 스크롤 가능한 커서와 같은 화면 기반 데이터베이스 응용 프로그램의 개발자가 일반적으로 필요로 하는 기능을 추가합니다.  
  
 ODBC API의 함수는 DBMS 별 드라이버 개발자가 구현합니다. 응용 프로그램은 이러한 드라이버의 함수를 호출하여 DBMS 독립적인 방식으로 데이터에 액세스합니다. 드라이버 관리자는 응용 프로그램과 드라이버 간의 통신을 관리합니다.  
  
 Microsoft는 Microsoft Windows® 95 이상 을 실행하는 컴퓨터에 대한 드라이버 관리자를 제공하고 여러 ODBC 드라이버를 작성했으며 일부 응용 프로그램에서 ODBC 함수를 호출하지만 누구나 ODBC 응용 프로그램 및 드라이버를 작성할 수 있습니다. 사실, 현재 사용 가능한 대부분의 ODBC 응용 프로그램 및 드라이버는 Microsoft 이외의 회사에서 작성합니다. 또한 ODBC 드라이버와 응용 프로그램은 매킨토시® 및 다양한 UNIX 플랫폼에 존재합니다.  
  
 응용 프로그램 및 드라이버 개발자를 돕기 위해 Microsoft는 Windows 95 이상 실행 중인 컴퓨터에 대해 드라이버 관리자, 설치 관리자 DLL, 테스트 도구 및 샘플 응용 프로그램을 제공하는 SDK(ODBC 소프트웨어 개발 키트)를 제공합니다. 마이크로소프트는 Visigenic 소프트웨어와 협력 하 고 매킨토시와 다양 한 UNIX 플랫폼에 이러한 SDK를 포팅.  
  
 ODBC는 데이터베이스 기능을 보완하지 않고 노출하도록 설계되었다는 것을 이해하는 것이 중요합니다. 따라서 응용 프로그램 작성기는 ODBC를 사용하면 간단한 데이터베이스가 완전히 기능을 갖춘 관계형 데이터베이스 엔진으로 갑자기 변환될 것으로 예상해서는 안 됩니다. 또한 드라이버 작성기는 기본 데이터베이스에서 찾을 수 없는 기능을 구현할 것으로 예상되지 않습니다. 이에 대한 예외는 파일 데이터(예: Xbase 파일의 데이터)에 직접 액세스하는 드라이버를 작성하는 개발자는 최소한의 SQL 기능을 지원하는 데이터베이스 엔진을 작성해야 한다는 것입니다. 또 다른 예외는 이전에 Microsoft 데이터 액세스 구성 요소(MDAC) SDK에 포함된 Windows SDK의 ODBC 구성 요소가 특정 수준의 기능을 구현하는 드라이버에 대해 스크롤 가능한 커서를 시뮬레이션하는 커서 라이브러리를 제공한다는 것입니다.  
  
 ODBC를 사용하는 응용 프로그램은 모든 데이터베이스 간 기능을 담당합니다. 예를 들어 ODBC는 이기종 조인 엔진이 아니며 분산 트랜잭션 프로세서도 아닙니다. 그러나 DBMS독립적이기 때문에 이러한 데이터베이스 간 도구를 빌드하는 데 사용할 수 있습니다.
