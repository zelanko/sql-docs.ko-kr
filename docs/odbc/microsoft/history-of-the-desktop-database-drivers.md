---
title: "데스크톱 데이터베이스 드라이버의 기록을 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6dfa1dc1b533c9e40175e9a3d29dc872344bd664
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="history-of-the-desktop-database-drivers"></a>데스크톱 데이터베이스 드라이버의 기록
다음 표에서 데스크톱 데이터베이스 드라이버 버전 기록을 보여 줍니다.  
  
|버전 옵션|출시 날짜|Description|  
|-------------|------------------|-----------------|  
|1.0|1993 년 8 월|PageAhead 소프트웨어에 의해 생성 된 SIMBA 쿼리 프로세서를 사용 합니다. SIMBA는 ODBC 호출 및 SQL 문을 수신, ISAM 호출을 설치할 수 있는 Microsoft Jet, 처리 및 로드 하 고 적절 한 설치 가능한 ISAM 드라이버 호출 Microsoft Jet ISAM 디스패치 계층을 호출 합니다.|  
|2.0|1994 년 12 월|ODBC 기능으로 대폭 확장 ODBC 2.0을 사용 합니다. 버전 2.0의에서 주요 변경 내용을 확인 Microsoft Jet 데이터베이스 엔진 SIMBA 쿼리 프로세서를 교체 했습니다. Microsoft Jet 데이터베이스 엔진과 데스크톱 데이터베이스 드라이버 ISAM 드라이버를 설치할 수 있는 Microsoft Jet 및 Microsoft Access 기술을 사용 하 여 훨씬 더 밀접 하 게 통합 합니다. 크게 향상 된 기능이 다음과 같았습니다.<br /><br /> -기본적으로 스크롤 가능 커서 지원 합니다.<br />-외부 조인, 업데이트할 수 있는 다른 유형의 조인 및 트랜잭션을 지원 네이티브 합니다.<br />-32 비트 버전의 Microsoft Windows NT 용 드라이버입니다.|  
|3.0|1995 년 10 월|Windows 95 및 Windows NT 워크스테이션이 나 서버 NT 3.51에 대 한 지원을 제공 했습니다. 이 릴리스에서;만 32 비트 드라이버가 포함 된 Windows 버전 3.1의 16 비트 드라이버가 제거 되었습니다.|  
|3.5|1996 년 10 월|이러한 드라이버 된 더블 바이트 문자 집합 (DBCS)-사용, 인터넷 응용 프로그램에 사용 하도록 이전 버전 보다 더 적합 된 및 파일 데이터 원본 이름 (Dsn)의 사용을 수용 합니다. Microsoft Access 드라이버는 Windows 95/98 및 Windows NT 3.51 이상 운영 체제에 대 한 Alpha 플랫폼에서 사용 하기 위해 RISC 버전에서 릴리스 되었습니다.|  
|4.0|1998 년 후반|이전 버전의 ANSI 형식에 대 한 호환성 함께 Microsoft Jet 엔진 유니코드 형식에 대 한 지원을 제공합니다.|  
  
> [!NOTE]  
>  Version3.5 드라이버 ODBC2와 작동 하도록 설계 되었습니다. *x*합니다. ODBC 3.0 에서도 작동 하지만 모든 ODBC 3.0 기능을 지원 하지 않습니다. 이러한 드라이버 ODBC 3.0과 함께 작동 하는 방식에 대 한 자세한 내용은 참조 [이전 버전과 호환성 및 표준 준수](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)합니다.
