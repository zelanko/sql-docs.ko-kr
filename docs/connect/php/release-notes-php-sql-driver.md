---
title: Microsoft Drivers for PHP for SQL Server 릴리스 정보 | Microsoft Docs
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: v-dapugl, kenvh
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23ac53a8515f55dfc0cad282fd14294e5f285af9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935912"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 릴리스 정보

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 페이지에서는 각 버전 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의에 추가 된 기능을 설명 합니다.  

<!--
Hello, We are standardizing the format of content inside our Release Notes (or What's New) articles.
Instead of bullets (or paragraphs), we have shifted to the 2-column format you see for H2 **What's New in Version 5.6**.
It is not necessary to reformat all the older H2 sections in this Release Notes file, but.....

Going forward, please be sure to use the 2-column format.

Also, all Release Notes .md file names now must begin with 'release-notes-*.md'.  And no filler words.
The 5.6 edition of this file is being renamed.....
FROM:  'release-notes-for-the-php-sql-driver.md'
TO  :  'release-notes-php-sql-driver.md'

For any questions, ask GeneMi or CraigG.
Thanks a lot.  2019-03-28  (DevO= 1467988)
-->

## <a name="whats-new-in-version-56"></a>버전 5.6의 새로운 기능

| 새 항목 | 세부 정보 |
| :------- | :------ |
| PHP 7.3을 지원합니다. | &nbsp; |
| PHP 7.0에 대 한 지원이 삭제 되었습니다. | &nbsp; |
| 모든 플랫폼에서 Microsoft ODBC Driver 17.3을 지원 합니다. | &nbsp; |
| MacOS Mojave 지원. | ODBC 드라이버 17.3 이상이 필요 합니다. |
| Ubuntu 18.10 및 Suse Linux 15를 지원 합니다. | 둘 다 ODBC Driver 17.3 이상이 필요 합니다. |
| Linux Ubuntu 17.10 및 macOS El Capitan에 대 한 지원이 삭제 되었습니다. | &nbsp; |
| Azure AD 액세스 토큰을 지원 합니다. | Linux 및 macOS에서에는 ODBC Driver 17.2 + 및 unixODBC 2.3.6 +가 필요 합니다. |
| Azure 리소스에 대 한 관리 Id를 사용 하 여 Azure AD에서 인증을 지원 합니다. | ODBC 드라이버를 이상 사용 해야 합니다. |
| 새로운 fetch 기능 | &bull;&nbsp; Pdo_sqlsrv를 개체로 반환 하는 New PDO:: SQLSRV_ATTR_FETCHES_DATETIME_TYPE 플래그입니다.<br/><br/>&bull;&nbsp; Sqlsrv의 문 수준에에서 returndatesasstrings 옵션을 추가 합니다.<br/><br/>&bull;&nbsp; 인출 된 결과에서 decimal 값의 형식을 지정 하기 위해 두 드라이버에 대 한 연결 및 문 수준의 새로운 옵션입니다. |
| 사용자가 원본에서 빌드를 선택 하는 경우 드라이버의 정적 컴파일을 지원 합니다. | &nbsp; |
| 페치 시 메타 데이터를 캐시 하 고 유니코드 문자열 변환의 속도를 높여 성능을 향상 시킵니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="whats-new-in-version-53"></a>버전 5.3의 새로운 기능

- 모든 플랫폼에서 Microsoft ODBC Driver 17.2에 대 한 지원
- MacOS High 시에라리온 지원 (ODBC 드라이버 17 이상 필요)
- Always Encrypted 기능을 지원 되는 모든 Windows, Linux 또는 macOS Always Encrypted 플랫폼에서 사용할 수 있도록 하는 기본 CRUD 기능의 Always Encrypted에 대 한 Azure Key Vault 지원 [SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)
- Ubuntu 18.04 LTS 지원 (ODBC Driver 17.2 필요)
- Linux 또는 macOS에서 연결 복원 력을 지원 합니다 (ODBC 드라이버 17.2 필요).

## <a name="whats-new-in-version-52"></a>버전 5.2의 새로운 기능

- PHP 7.2.1 및 Windows에 대 한 지원 및 다른 플랫폼의 7.2.0 이상 지원
- Microsoft ODBC 드라이버 17에 대 한 지원
  - 이제 모든 플랫폼에서 버전 17이 기본값으로 설정 됩니다.
- Ubuntu 17.10, Debian 9 및 Suse Enterprise Linux 12에 대 한 지원
- Ubuntu 15.10에 대 한 지원 삭제
- Windows에서 CRUD 기능을 사용 하는 Always Encrypted에 대 한 지원. 자세한 내용은 [Using Always Encrypted with the PHP Drivers for SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)(SQL Server용 PHP 드라이버와 함께 Always Encrypted 사용)를 참조하세요.
  - Windows 인증서 저장소에 대 한 지원
  - Always Encrypted은 Microsoft ODBC Driver 17 이상 에서만 지원 됩니다.
- Linux 및 macOS에서 비 UTF8 로캘에 대 한 지원
  - Linux 및 macOS의 비 UTF8 로캘은 Microsoft ODBC Driver 17 이상 에서만 지원 됩니다.
- Azure SQL Data Warehouse 지원
- Azure SQL Managed Instance 지원(프라이빗 미리 보기 확장)

## <a name="whats-new-in-version-43"></a>버전 4.3의 새로운 기능

- PHP 7.1 지원
- macOS Sierra 및 macOS El Capitan 지원
- Ubuntu 15.10 및 Debian 8 지원
- Ubuntu 15.04에 대 한 지원 삭제
- 투명 네트워크 IP 확인을 통해 Always On 가용성 그룹을 지원 합니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.
- 제한 사항이 있는 sql_variant 데이터 형식에 대 한 지원이 추가 되었습니다.
- Windows에서 유휴 연결 복원 력을 지원 합니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.
- Linux 및 macOS에 대 한 연결 풀링을 지원 합니다. 자세한 내용은 [Connection Pooling](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)을 참조하세요.
- ActiveDirectoryPassword 및 SqlPassword를 사용 하 여 Azure Active Directory 인증을 지원 합니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.

## <a name="whats-new-in-version-40"></a>버전 4.0의 새로운 기능

- PHP 7.0 지원  
- 전체 64 비트 지원
- Ubuntu 15.04, Ubuntu 16.04 및 RedHat 7 지원

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
- LocalDB 지원이 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 추가되었습니다. 자세한 내용은 [LocalDB 지원](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)을 참조 하세요.
- AttachDBFileName 연결 옵션이 추가되었습니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
- 고가용성, 재해 복구 기능을 지원합니다. 자세한 내용은 [고가용성, 재해 복구를 위한 JDBC 드라이브 지원](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)을 참조하세요.
- 클라이언트 쪽 커서(메모리 내 결과 집합 캐싱)를 지원합니다. 자세한 내용은 [커서 유형&#40;SQLSRV 드라이버&#41;](../../connect/php/cursor-types-sqlsrv-driver.md) 및 [커서 유형&#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)를 참조하세요.
- PDO::ATTR_EMULATE_PREPARES 특성이 추가되었습니다. 자세한 내용은 [PDO::prepare](../../connect/php/pdo-prepare.md)을 참조하세요.  

## <a name="whats-new-in-version-20"></a>버전 2.0의 새로운 기능

버전 2.0에서는 PDO_SQLSRV 드라이버에 대한 지원이 추가되었습니다. 자세한 내용은 [PDO_SQLSRV 드라이버 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)를 참조하세요.  

## <a name="see-also"></a>참고 항목

[Microsoft Drivers for PHP for SQL Server 개요](../../connect/php/overview-of-the-php-sql-driver.md)
