---
title: 보안 고려 사항 Microsoft Drivers for PHP for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- security considerations
ms.assetid: a8c1a570-9204-454f-b94c-ba34f54d487c
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad90c4e05168e54ce9be6b8324539db67d1ccb7e
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="security-considerations-for-the-microsoft-drivers-for-php-for-sql-server"></a>보안 고려 사항 Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]를 사용하는 응용 프로그램 개발, 배포 및 실행과 관련된 보안 고려 사항을 설명합니다. SQL Server 보안에 대 한 정보를 자세한 참조 [SQL Server 보안 개요](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/overview-of-sql-server-security)합니다.  
  
## <a name="connect-using-windows-authentication"></a>Windows 인증을 사용하여 연결  
다음과 같은 이유로 가능하면 SQL Server에 연결하는 데 Windows 인증을 사용해야 합니다.  
  
-   **인증하는 동안 네트워크를 통해 자격 증명이 전달되지 않습니다.** 데이터베이스 연결 문자열에 사용자 이름 및 암호가 포함되지 않습니다. 따라서 악의적인 사용자 또는 공격자가 가져올 수 자격 증명 네트워크를 모니터링 하 여 구성 파일 내의 연결 문자열을 확인 합니다.  
  
-   **사용자가 중앙 집중식 계정 관리를 받습니다.** 암호 만료 기간, 최소 암호 길이 및 잘못된 로그온 요청이 여러 번 있을 경우 계정 잠금 등의 보안 정책을 강제로 적용합니다.  
  
Windows 인증을 사용하여 서버에 연결하는 방법에 대한 정보는 [방법: Windows 인증을 사용하여 연결](../../connect/php/how-to-connect-using-windows-authentication.md)을 참조하세요.  
  
Windows 인증을 사용하여 연결할 때 SQL Server가 Kerberos 인증 프로토콜을 사용할 수 있도록 환경을 구성하는 것이 좋습니다. 자세한 내용은 참조 [인스턴스에 SQL Server 2005의 원격 연결을 만들 때 Kerberos 인증을 사용 하 고 있는지 확인 하는 방법을](https://support.microsoft.com/en-ca/help/909801/how-to-make-sure-that-you-are-using-kerberos-authentication-when-you-c) 또는 [Kerberos 인증 및 SQL Server](https://msdn.microsoft.com/library/cc280744.aspx)합니다.  
  
## <a name="use-encrypted-connections-when-transferring-sensitive-data"></a>중요한 데이터를 전송할 때 암호화된 연결 사용  
중요한 데이터가 전송되거나 SQL Server에서 검색될 때마다 암호화된 연결을 사용해야 합니다. 암호화 된 연결을 설정 하는 방법에 대 한 정보를 참조 하십시오. [(SQL Server 구성 관리자) 데이터베이스 엔진에 암호화 연결 사용 하는 방법을](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)합니다. [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]를 사용하여 보안 연결을 설정하려면 서버에 연결할 때 연결 암호화 특성을 사용합니다. 연결 특성에 대한 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
  
## <a name="use-parameterized-queries"></a>매개 변수가 있는 쿼리 사용  
매개 변수가 있는 쿼리를 사용하여 SQL 주입 공격의 위험을 줄일 수 있습니다. 매개 변수가 있는 쿼리를 실행하는 예제를 보려면 [How to: Perform Parameterized Queries](../../connect/php/how-to-perform-parameterized-queries.md)을 참조하세요.  
  
SQL 주입 공격 및 관련된 보안 고려 사항에 대 한 자세한 내용은 참조 [SQL 주입](https://msdn.microsoft.com/library/ms161953.aspx)합니다.  
  
## <a name="do-not-accept-server-or-connection-string-information-from-end-users"></a>최종 사용자에게서 서버 또는 연결 문자열 정보 허용하지 않음  
최종 사용자가 서버 또는 연결 문자열 정보를 응용 프로그램에 제출할 수 없도록 응용 프로그램을 작성합니다. 서버 및 연결 문자열 정보에 대해 엄격한 제어를 유지하면 악성 활동에 대한 노출 영역이 줄어듭니다.  
  
## <a name="turn-warningsaserrors-on-during-application-development"></a>응용 프로그램을 개발하는 동안 WarningsAsErrors 설정  
드라이버에서 표시하는 경고가 오류로 간주되도록 **WarningsAsErrors** 설정이 **true** 로 설정된 응용 프로그램을 개발합니다. 그러면 응용 프로그램을 배포하기 전에 경고를 전달할 수 있습니다. 자세한 내용은 [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md)을 참조하세요.  
  
## <a name="secure-logs-for-deployed-application"></a>배포된 응용 프로그램에 대한 보안 로그  
배포된 응용 프로그램에 대해 로그가 보안 위치에 기록되거나 해당 로깅이 해제되었는지 확인합니다. 그러면 로그 파일에 기록된 정보에 최종 사용자가 액세스할 가능성이 차단됩니다. 자세한 내용은 [Logging Activity](../../connect/php/logging-activity.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md)
  
