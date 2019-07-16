---
title: 데스크톱 데이터베이스 드라이버의 기록 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d225bac273558b928e3e8fd2f41bd121a723f6ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952367"
---
# <a name="history-of-the-desktop-database-drivers"></a>데스크톱 데이터베이스 드라이버의 기록
다음 표에서 데스크톱 데이터베이스 드라이버 버전 기록을 보여 줍니다.  
  
|버전|출시 날짜|설명|  
|-------------|------------------|-----------------|  
|1.0|1993 년 8 월|PageAhead 소프트웨어에 의해 생성 된 SIMBA 쿼리 프로세서를 사용 합니다. SIMBA는 ODBC 호출 및 SQL 문, Microsoft Jet 설치할 ISAM 호출을 처리 하 받았으며 호출한 다음 로드 하 고 설치할 수 있는 적절 한 ISAM 드라이버를 호출 하는 Microsoft Jet ISAM 디스패치 계층입니다.|  
|2.0|1994 년 12 월|ODBC 기능으로 대폭 확장 ODBC 2.0을 사용 합니다. 버전 2.0의에서 주요 변경 내용을 Microsoft Jet 데이터베이스 엔진 대체 SIMBA 쿼리 프로세서는 했습니다. Microsoft Jet 데이터베이스 엔진을 사용 하 여 데스크톱 데이터베이스 드라이버 ISAM 드라이버를 설치할 수 있는 Microsoft Jet 및 Microsoft Access 기술을 사용 하 여 훨씬 더 밀접 하 게 통합 합니다. 크게 향상 되었습니다.<br /><br /> -스크롤 가능 커서에 대 한 지원 네이티브 합니다.<br />-외부 조인, 업데이트할 수 있는 다른 유형의 조인 및 트랜잭션에 대해 네이티브 지원 합니다.<br />-32 비트 버전의 Microsoft Windows NT 용 드라이버입니다.|  
|3.0|1995 년 10 월|Windows 95 및 Windows NT 워크스테이션 또는 서버 NT 3.51에 대 한 지원을 제공 합니다. 이 릴리스에서;만 32 비트 드라이버 포함 된 Windows 버전 3.1의 16 비트 드라이버가 제거 되었습니다.|  
|3.5|1996 년 10 월|이러한 드라이버 된 더블 바이트 문자 집합 (DBCS)-사용 하도록 설정 하 고 이전 버전 보다 더 적합 인터넷 응용 프로그램에 사용 된 파일 데이터 원본 이름 (Dsn)의 사용을 수용 합니다. Windows 95/98 및 Windows NT 3.51 이상 운영 체제에 대 한 Alpha 플랫폼에서 사용 하기 위해 RISC 버전에서 Microsoft Access 드라이버를 출시 되었습니다.|  
|4.0|1998 년 후반|이전 버전의 ANSI 형식에 대 한 호환성과 함께 Microsoft Jet 엔진 유니코드 형식에 대 한 지원을 제공합니다.|  
  
> [!NOTE]  
>  Version3.5 드라이버 ODBC2를 사용 하 여 작동 하도록 설계 되었습니다. *x*합니다. ODBC 3.0 에서도 작동 하지만 모든 ODBC 3.0 기능 지원 하지 않습니다. ODBC 3.0을 사용 하 여 이러한 드라이버 작동 하는 방법에 대 한 자세한 내용은 참조 하세요. [이전 버전과 호환성 및 표준 준수](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)합니다.
