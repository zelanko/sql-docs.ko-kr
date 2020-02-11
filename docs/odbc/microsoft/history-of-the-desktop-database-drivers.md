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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67952367"
---
# <a name="history-of-the-desktop-database-drivers"></a>데스크톱 데이터베이스 드라이버의 기록
다음 표에서는 데스크톱 데이터베이스 드라이버 버전 기록을 보여 줍니다.  
  
|버전|릴리스 날짜|Description|  
|-------------|------------------|-----------------|  
|1.0|8 월 1993|PageAhead 소프트웨어에 의해 생성 된 SIMBA 쿼리 프로세서를 사용 했습니다. SIMBA는 ODBC 호출 및 SQL 문을 수신 하 고, Microsoft Jet 설치 가능 ISAM 호출로 처리 한 다음, Microsoft Jet ISAM 디스패치 계층을 호출 하 여 설치 가능한 적절 한 ISAM 드라이버를 로드 하 고 호출 합니다.|  
|2.0|12 월 1994|Odbc 기능이 크게 확장 된 ODBC 2.0와 함께 사용 됩니다. 버전 2.0의 주요 변경 내용은 Microsoft Jet 데이터베이스 엔진이 SIMBA 쿼리 프로세서를 대체 한 것입니다. Microsoft Jet 데이터베이스 엔진을 사용 하면 데스크톱 데이터베이스 드라이버가 Microsoft Jet 설치 가능 ISAM 드라이버 및 Microsoft 액세스 기술과 훨씬 더 긴밀 하 게 통합 되었습니다. 크게 향상 된 기능은 다음과 같습니다.<br /><br /> -스크롤 가능 커서를 기본적으로 지원 합니다.<br />-외부 조인, 업데이트 가능 하 고 유형이 다른 조인 및 트랜잭션에 대 한 기본 지원입니다.<br />-32 비트 버전의 Microsoft Windows NT 용 드라이버.|  
|3.0|10 월 1995|Windows 95 및 Windows NT 워크스테이션 또는 NT Server 3.51에 대 한 지원이 제공 됩니다. 이 릴리스에는 32 비트 드라이버만 포함 되어 있습니다. Windows 버전 3.1에 대 한 16 비트 드라이버가 제거 되었습니다.|  
|3.5|10 월 1996|이러한 드라이버는 DBCS (더블 바이트 문자 집합)를 사용 하며, 이전 버전 보다 인터넷 응용 프로그램에서 사용 하기에 더 적합 하 고, 파일 Dsn (데이터 원본 이름)의 사용을 수용 했습니다. Microsoft Access driver는 Windows 95/98 및 Windows NT 3.51 이상의 운영 체제에 대 한 알파 플랫폼에서 사용할 RISC 버전으로 출시 되었습니다.|  
|4.0|늦은 1998|에서는 이전 버전의 ANSI 형식에 대 한 호환성과 함께 Microsoft Jet 엔진 유니코드 형식을 지원 합니다.|  
  
> [!NOTE]  
>  버전 3.5 드라이버는 ODBC2에서 작동 하도록 설계 되었습니다. *x*. ODBC 3.0 에서도 작동 하지만 일부 ODBC 3.0 기능은 지원 하지 않습니다. 이러한 드라이버가 ODBC 3.0에서 작동 하는 방식에 대 한 자세한 내용은 [이전 버전과의 호환성 및 표준 준수](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)를 참조 하세요.
