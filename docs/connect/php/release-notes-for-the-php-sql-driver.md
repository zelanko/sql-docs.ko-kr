---
title: Microsoft Drivers for PHP for SQL Server 릴리스 정보 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0c2e7377b1072c30e5c5ef038b93a88f0c222260
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744353"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 릴리스 정보
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 페이지의 각 버전에 추가 된 기능에 대해 설명 합니다 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다.  

## <a name="whats-new-in-version-56"></a>버전 5.6의 새로운 기능

- PHP 7.3 지원
- 모든 플랫폼에서 Microsoft ODBC Driver 17.3 용 지원
- MacOS Mojave 지원 (ODBC 드라이버 17.3 필요 이상)
- Ubuntu 18.10 및 Suse Linux 15에 대 한 지원 (둘 다 필요 ODBC 드라이버 17.3 이상)
- PHP 7.0 지원 하지 않으므로
- Linux Ubuntu 17.10 및 El Capitan macOS에 대 한 지원을 삭제
- Azure AD 액세스 토큰에 대 한 지원 (Linux 및 macOS에서 ODBC 드라이버 17.2 + 및 필요 unixODBC 2.3.6+)
- 관리 Id를 사용 하 여 Azure 리소스 (ODBC 드라이버 17.3 + 필요)에 대 한 Azure AD 사용 하 여 인증에 대 한 지원
- 새 인출 기능:
  - Datetime 개체로 반환할 pdo_sqlsrv에 대 한 새 PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE 플래그
  - Sqlsrv에 대 한 문 수준 ReturnDatesAsStrings 옵션 추가
  - 인출한 결과에 10 진수 값의 서식을 지정 하는 것에 대 한 두 드라이버에 대 한 연결 및 문 수준에서 새 옵션
- 사용자가 원본에서 빌드를 선택 하는 경우 드라이버의 정적 컴파일 지원
- 메타 데이터 인출에서 캐싱 유니코드 문자열 변환 속도를 성능 향상된

## <a name="whats-new-in-version-53"></a>버전 5.3의 새로운 기능

- 모든 플랫폼에서 Microsoft ODBC Driver 17.2에 대 한 지원
- MacOS High Sierra에 대 한 지원 (ODBC 드라이버 17 필요 이상)
- Azure Key Vault에 대 한 Always Encrypted에 대 한 기본 CRUD 기능 이러한 Always Encrypted 기능은 모두 사용할 수 있으며 지원 Windows, Linux 또는 macOS 플랫폼 [SQL Server 용 PHP 드라이버를 사용 하 여 상시 암호화 사용](../../connect/php/using-always-encrypted-php-drivers.md)
- Ubuntu 18.04 LTS (ODBC 드라이버 17.2 필요)를 지원 합니다.
- 연결 복원 력 (ODBC 드라이버 17.2 필요)도 macOS 또는 Linux에 대 한 지원

## <a name="whats-new-in-version-52"></a>버전 5.2의 새로운 기능

- 7.2.1 PHP에 대 한 지원 및 Windows를 및 7.2.0 및 다른 플랫폼에서
- Microsoft ODBC Driver 17에 대 한 지원
  - 버전 17 모든 플랫폼에서 기본 되었습니다.
- Ubuntu 17.10, Debian 9 및 Suse Enterprise Linux 12에 대 한 지원
- Ubuntu 15.10 지원 하지 않으므로
- Windows에서 CRUD 기능을 사용 하 여 Always Encrypted에 대 한 지원. 자세한 내용은 참조 하세요. [SQL Server 용 PHP 드라이버를 사용 하 여 상시 암호화 사용](../../connect/php/using-always-encrypted-php-drivers.md)
  - Windows 인증서 저장소에 대 한 지원
  - 상시 암호화만 지원 됩니다 Microsoft ODBC Driver 17 이상
- Linux 및 macOS에서 UTF8 이외 로캘에 대 한 지원
  - Linux 및 macOS에서 비-UTF8 로캘에서 Microsoft ODBC Driver 17 이상 에서만 지원 됩니다.
- Azure SQL Data Warehouse 지원
- Azure SQL 관리 되는 인스턴스 (확장 된 비공개 미리 보기)에 대 한 지원


## <a name="whats-new-in-version-43"></a>버전 4.3의 새로운 기능

- PHP 7.1 지원
- MacOS Sierra에 대 한 지원 및 El Capitan macOS
- Ubuntu 15.10, 및 Debian 8에 대 한 지원
- Ubuntu 15.04 지원 하지 않으므로
- 투명 네트워크 IP 확인을 통해 Always On 가용성 그룹에 대 한 지원. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.
- Sql_variant 데이터 형식 제한에 대 한 지원이 추가 되었습니다.
- Windows에서 유휴 연결 복원 력을 지원 합니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.
- 연결 풀링 Linux 및 macOS에 대 한 지원입니다. 자세한 내용은 [Connection Pooling](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)을 참조하세요.
- ActiveDirectoryPassword SqlPassword와 Azure Active Directory 인증이 지원 됩니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.

## <a name="whats-new-in-version-40"></a>버전 4.0의 새로운 기능

- PHP 7.0 지원  
- 전체 64 비트 지원
- Ubuntu 15.04, Ubuntu 16.04 및 RedHat 7에 대 한 지원

## <a name="whats-new-in-version-32"></a>버전 3.2의 새로운 기능

- PHP 5.6을 지원합니다.   
- 이전 PHP 버전 5.5 및 5.4에 대한 최신 업데이트를 포함합니다.   
- Microsoft ODBC Driver 11 for SQL Server 필요  

## <a name="whats-new-in-version-31"></a>버전 3.1의 새로운 기능

- PHP 5.5를 지원합니다.  
- Microsoft ODBC Driver 11 for SQL Server가 필요합니다. SQL Native Client에 필요한 이전 버전입니다.  

## <a name="whats-new-in-version-30"></a>버전 3.0의 새로운 기능  

- PHP 5.4를 지원합니다.  PHP 5.2는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 3에서 지원되지 않습니다.  
- AttachDBFileName 연결 옵션이 추가되었습니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
- LocalDB 지원이 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 추가되었습니다. 자세한 내용은 [LocalDB에 대 한 지원을](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)합니다.
- AttachDBFileName 연결 옵션이 추가되었습니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
- 고가용성, 재해 복구 기능을 지원합니다. 자세한 내용은 [High Availability, Disaster Recovery에 대 한 지원을](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)합니다.
- 클라이언트 쪽 커서(메모리 내 결과 집합 캐싱)를 지원합니다. 자세한 내용은 [커서 유형&#40;SQLSRV 드라이버&#41;](../../connect/php/cursor-types-sqlsrv-driver.md) 및 [커서 유형&#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)를 참조하세요.
- PDO::ATTR_EMULATE_PREPARES 특성이 추가되었습니다. 자세한 내용은 [PDO::prepare](../../connect/php/pdo-prepare.md)을 참조하세요.  

## <a name="whats-new-in-version-20"></a>버전 2.0의 새로운 기능  
버전 2.0에서는 PDO_SQLSRV 드라이버에 대한 지원이 추가되었습니다. 자세한 내용은 [PDO_SQLSRV 드라이버 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)를 참조하세요.  

## <a name="see-also"></a>참고 항목  
[Microsoft Drivers for PHP for SQL Server 개요](../../connect/php/overview-of-the-php-sql-driver.md)
