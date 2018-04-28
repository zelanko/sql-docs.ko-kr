---
title: 릴리스 정보 Microsoft Drivers for PHP for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
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
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6fc3b3b4e815aaa5dba9d49e90ce7e2a4774c2a9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server에 대 한 릴리스 정보
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 페이지의 각 버전에 추가 된 기능에 대해 설명 된 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다.  

## <a name="whats-new-in-version-52"></a>버전 5.2의에서 새로운 기능

- 7.2.1 PHP에 대 한 지원 및 창 및 7.2.0에 위쪽 및 다른 플랫폼에서 위쪽
- Microsoft ODBC Driver 17에 대 한 지원
  - 17 버전은 모든 플랫폼에 대 한 기본값
- Ubuntu 17.10, Debian 9 및 엔터프라이즈 Suse Linux 12에 대 한 지원
- Ubuntu 15.10 지원 하지 않으므로
- Windows에서 CRUD 기능과 함께 상시 암호화에 대 한 지원. 자세한 내용은 참조 [SQL Server 용 PHP 드라이버를 사용 하 여 항상 암호화를 사용 하 여](../../connect/php/using-always-encrypted-php-drivers.md)
  - Windows 인증서 저장소에 대 한 지원
  - 상시 암호화가만 지원 Microsoft ODBC 드라이버 17 이상
- Linux와 macOS에서 UTF8 이외 로캘에 대 한 지원
  - Linux와 macOS에서 비-UTF8 로캘에서 Microsoft ODBC 드라이버 17 이상에 지원 됩니다.
- Azure SQL 데이터 웨어하우스에 대 한 지원
- Azure SQL 관리 되는 인스턴스 (확장 된 비공개 미리 보기)에 대 한 지원


## <a name="whats-new-in-version-43"></a>버전 4.3의에서 새로운 기능

- 7.1 PHP에 대 한 지원
- El Capitan macOS 및 macOS 시에라 지원
- Ubuntu 15.10, 및 Debian 8에 대 한 지원
- Ubuntu 15.04 지원 하지 않으므로
- 투명 네트워크 IP 확인을 통해 항상 가용성 그룹에 대 한 지원. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.
- 제한이 sql_variant 데이터 형식에 대 한 지원이 추가 되었습니다.
- Windows에서 유휴 연결 복원 력 지원 합니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.
- 연결 풀링 Linux와 macOS에 대 한 지원입니다. 자세한 내용은 참조 [연결 풀링](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)합니다.
- Azure Active Directory 인증 ActiveDirectoryPassword 및 SqlPassword 지원 합니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.

## <a name="whats-new-in-version-40"></a>버전 4.0의에서 새로운 기능

- PHP 7.0에 대 한 지원  
- 완전 한 64 비트 지원
- Ubuntu 15.04, 16.04, Ubuntu 및 RedHat 7에 대 한 지원

## <a name="whats-new-in-version-32"></a>버전 3.2의 새로운 기능

- PHP 5.6을 지원합니다.   
- 이전 PHP 버전 5.5 및 5.4에 대한 최신 업데이트를 포함합니다.   
- Microsoft ODBC Driver 11 for SQL Server 필요  

## <a name="whats-new-in-version-31"></a>버전 3.1의 새로운 기능

- PHP 5.5를 지원합니다.  
- Microsoft ODBC Driver 11 for SQL Server 필요합니다. SQL Native Client에 필요한 이전 버전입니다.  

## <a name="whats-new-in-version-30"></a>버전 3.0의 새로운 기능  

- PHP 5.4를 지원합니다.  PHP 5.2는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 3에서 지원되지 않습니다.  
- AttachDBFileName 연결 옵션이 추가되었습니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
- LocalDB 지원이 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]에 추가되었습니다. 자세한 내용은 참조 [LocalDB에 대 한 지원을](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)합니다.
- AttachDBFileName 연결 옵션이 추가되었습니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
- 고가용성, 재해 복구 기능을 지원합니다. 자세한 내용은 참조 [고가용성, 재해 복구에 대 한 지원을](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.
- 클라이언트 쪽 커서(메모리 내 결과 집합 캐싱)를 지원합니다. 자세한 내용은 참조 [커서 유형 &#40;SQLSRV 드라이버&#41; ](../../connect/php/cursor-types-sqlsrv-driver.md) 및 [커서 유형 &#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)합니다.
- PDO::ATTR_EMULATE_PREPARES 특성이 추가되었습니다. 자세한 내용은 참조 [pdo:: prepare](../../connect/php/pdo-prepare.md)합니다.  

## <a name="whats-new-in-version-20"></a>버전 2.0의 새로운 기능  
버전 2.0에서는 PDO_SQLSRV 드라이버에 대한 지원이 추가되었습니다. 자세한 내용은 [PDO_SQLSRV 드라이버 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)를 참조하세요.  

## <a name="see-also"></a>관련 항목:  
[Microsoft Drivers for PHP for SQL Server의 개요](../../connect/php/overview-of-the-php-sql-driver.md)
