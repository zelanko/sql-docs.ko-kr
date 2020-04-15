---
title: 데스크톱 데이터베이스 드라이버의 기록 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89434b397c07fdee751ca4272b65ac2eada94cf3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304984"
---
# <a name="history-of-the-desktop-database-drivers"></a>데스크톱 데이터베이스 드라이버의 기록
다음 표에서는 데스크톱 데이터베이스 드라이버 버전 기록을 보여 주며,  
  
|버전|출시 날짜|설명|  
|-------------|------------------|-----------------|  
|1.0|1993년 8월|PageAhead 소프트웨어에서 생성한 SIMBA 쿼리 프로세서를 사용했습니다. SIMBA는 ODBC 호출 및 SQL 문을 수신하여 Microsoft Jet 설치 가능한 ISAM 호출로 처리한 다음 Microsoft Jet ISAM 디스패치 계층을 호출하여 적절한 설치 가능한 ISAM 드라이버를 로드하고 호출했습니다.|  
|2.0|1994년 12월|ODBC 2.0과 함께 사용되어 ODBC 기능을 크게 확장했습니다. 버전 2.0의 주요 변경 사항은 Microsoft Jet 데이터베이스 엔진이 SIMBA 쿼리 프로세서를 대체했다는 것입니다. 마이크로소프트 제트 데이터베이스 엔진, 데스크톱 데이터베이스 드라이버 는 마이크로소프트 제트 설치 ISAM 드라이버와 마이크로소프트 액세스 기술 훨씬 더 밀접 하 게 통합. 크게 향상된 기능은 다음과 같은 사항입니다.<br /><br /> - 스크롤 가능한 커서에 대한 기본 지원.<br />- 외부 조인, 업데이트 및 이기종 조인 및 트랜잭션에 대한 기본 지원입니다.<br />- 마이크로 소프트 윈도우 NT에 대한 드라이버의 32 비트 버전.|  
|3.0|1995년 10월|Windows 95 및 Windows NT 워크스테이션 또는 NT 서버 3.51에 대한 지원을 제공했습니다. 이 릴리스에는 32비트 드라이버만 포함되었습니다. Windows 버전 3.1의 16비트 드라이버가 제거되었습니다.|  
|3.5|1996년 10월|이러한 드라이버는 DBCS(이중 바이트 문자 집합)를 사용했으며 이전 버전보다 인터넷 응용 프로그램에 더 적합했으며 파일 데이터 원본 이름(DSN)의 사용을 수용했습니다. Microsoft Access 드라이버는 Windows 95/98 및 Windows NT 3.51 및 이후 운영 체제용 알파 플랫폼에서 사용하기 위해 RISC 버전으로 릴리스되었습니다.|  
|4.0|1998년 말|이전 버전의 ANSI 형식에 대한 호환성과 함께 Microsoft Jet Engine 유니코드 형식에 대한 지원을 제공합니다.|  
  
> [!NOTE]  
>  버전3.5 드라이버는 ODBC2와 함께 작동하도록 설계되었습니다. *x*. ODBC 3.0에서도 작동하지만 모든 ODBC 3.0 기능을 지원하지는 않습니다. 이러한 드라이버가 ODBC 3.0에서 작동하는 방식에 대한 자세한 내용은 [이전 버전과의 호환성 및 표준 준수를](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)참조하십시오.
