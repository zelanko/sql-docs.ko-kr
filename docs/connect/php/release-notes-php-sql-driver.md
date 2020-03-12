---
title: Microsoft Drivers for PHP for SQL Server 릴리스 정보 | Microsoft Docs
ms.custom: ''
ms.date: 03/05/2020
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
ms.openlocfilehash: edc5d8122f1cb2c0fad747e480843c559f650434
ms.sourcegitcommit: 86268d297e049adf454b97858926d8237d97ebe2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78866513"
---
# <a name="release-notes-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 릴리스 정보

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 페이지에서는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 각 버전에 추가된 기능에 대해 설명합니다.  

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

## <a name="58"></a>5.8

![다운로드](../../ssms/media/download-icon.png) [Windows 패키지 다운로드](https://go.microsoft.com/fwlink/?linkid=2120362)  
[GitHub 릴리스 태그(Linux 및 macOS 패키지 확인 가능)](https://github.com/Microsoft/msphpsql/releases/tag/v5.8.0)

### <a name="version-information"></a>버전 정보

- 릴리스 번호: 5.8.0
- 릴리스 날짜: 2020년 1월 31일

## <a name="whats-new-in-58"></a>5\.8의 새로운 기능

| 새 항목 | 세부 정보 |
| :------- | :------ |
| PHP 7.4에 대한 지원을 추가했습니다. | &nbsp; |
| PHP 7.1에 대한 지원을 삭제했습니다. | &nbsp; |
| 모든 플랫폼에서 Microsoft ODBC 드라이버 17.5에 대한 지원을 추가했습니다. | &nbsp; |
| Debian 10 및 Red Hat 8에 대한 지원을 추가했습니다. | 모두 ODBC 드라이버 17.4 이상이 필요합니다. |
| macOS Catalina, Alpine Linux 3.11<sup>1</sup> 및 Ubuntu 19.10에 대한 지원을 추가했습니다. | 모두 ODBC 드라이버 17.5 이상이 필요합니다. |
| SQL Server 2008 R2, macOS Sierra, Ubuntu 18.10 및 Ubuntu 19.04에 대한 지원을 삭제했습니다. | &nbsp; |
| SQL Server에 연결할 때 언어 옵션을 지원합니다. | &nbsp; |
| PHP 7.2에 도입된 PHP 확장 문자열 형식을 지원합니다. | &nbsp; |
| 데이터 분류 민감도 메타데이터 검색을 지원합니다. | SQL Server 2019 및 ODBC 드라이버 17.4.2 이상이 필요합니다. |
| 보안 Enclave를 사용한 Always Encrypted 지원 | ODBC 드라이버 17.4 이상이 필요합니다. |
| Linux 및 macOS에서 로캘 설정에 대한 구성 가능한 옵션을 지원합니다. |
| 페치 시 메타데이터를 캐시하고 중복 호출을 생략하여 성능을 개선했습니다. | &nbsp; |
| &nbsp; | &nbsp; |

<sup>1</sup> Alpine Linux 지원은 버전 5.8에서 실험적입니다.

## <a name="previous-releases"></a>이전 릴리스

## <a name="561"></a>5.6.1

![다운로드](../../ssms/media/download-icon.png) [Windows 패키지 다운로드](https://go.microsoft.com/fwlink/?linkid=2120446)  
[GitHub 릴리스 태그(Linux 및 macOS 패키지 확인 가능)](https://github.com/Microsoft/msphpsql/releases/tag/v5.6.1)

### <a name="version-information"></a>버전 정보

- 릴리스 번호: 5.6.1
- 릴리스 날짜: 2019년 3월 19일

## <a name="whats-new-in-561"></a>5\.6.1의 새로운 기능

| 새 항목 | 세부 정보 |
| :------- | :------ |
| 버그 수정 | 필드 또는 열 메타데이터를 계산할 때 생성된 가정이 애플리케이션 종료로 이어질 수 있으므로 수정했습니다. |
| 버그 수정 | Pdo_sqlsrv와 별개로 컴파일할 수 있도록 sqlsrv 구성 파일을 수정했습니다. |
| 버그 수정 | 문제가 발생하는 경우 false를 반환하도록 PDOStatement::getColumnMeta()를 수정했습니다. |
| &nbsp; | &nbsp; |

## <a name="56"></a>5.6

![다운로드](../../ssms/media/download-icon.png) [Windows 패키지 다운로드](https://go.microsoft.com/fwlink/?linkid=2120450)  
[GitHub 릴리스 태그(Linux 및 macOS 패키지 확인 가능)](https://github.com/Microsoft/msphpsql/releases/tag/v5.6.0)

### <a name="version-information"></a>버전 정보

- 릴리스 번호: 5.6.0
- 릴리스 날짜: 2019년 2월 21일

## <a name="whats-new-in-56"></a>5\.6의 새로운 기능

| 새 항목 | 세부 정보 |
| :------- | :------ |
| PHP 7.3을 지원합니다. | &nbsp; |
| PHP 7.0에 대한 지원을 삭제했습니다. | &nbsp; |
| 모든 플랫폼에서 Microsoft ODBC 드라이버 17.3을 지원합니다. | &nbsp; |
| macOS Mojave를 지원합니다. | ODBC 드라이버 17.3 이상이 필요합니다. |
| Ubuntu 18.10 및 Suse Linux 15를 지원합니다. | 모두 ODBC 드라이버 17.3 이상이 필요합니다. |
| Linux Ubuntu 17.10 및 macOS El Capitan에 대한 지원을 삭제했습니다. | &nbsp; |
| Azure AD 액세스 토큰을 지원합니다. | Linux 및 macOS에서는 ODBC 드라이버 17.2 이상 및 unixODBC 2.3.6 이상이 필요합니다. |
| Azure 리소스에 대한 관리 ID를 사용하여 Azure AD 인증을 지원합니다. | ODBC 드라이버 17.3 이상이 필요합니다. |
| 새로운 페치 기능 | &bull; &nbsp; pdo_sqlsrv가 날짜/시간을 개체로 반환하기 위한 새로운 PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE 플래그입니다.<br/><br/>&bull; &nbsp; sqlsrv의 문 수준에 ReturnDatesAsStrings 옵션을 추가합니다.<br/><br/>&bull; &nbsp; 페치된 결과의 10진수 값 서식 지정을 위한 두 드라이버에 대한 연결 및 문 수준의 새로운 옵션입니다. |
| 사용자가 원본에서 빌드를 선택하는 경우 드라이버의 정적 컴파일을 지원합니다. | &nbsp; |
| 페치 시 메타데이터를 캐시하고 유니코드 문자열 변환 속도를 높여 성능을 개선했습니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="53"></a>5.3

![다운로드](../../ssms/media/download-icon.png) [Windows 패키지 다운로드](https://go.microsoft.com/fwlink/?linkid=2120447)  
[GitHub 릴리스 태그(Linux 및 macOS 패키지 확인 가능)](https://github.com/Microsoft/msphpsql/releases/tag/v5.3.0)

### <a name="version-information"></a>버전 정보

- 릴리스 번호: 5.3.0
- 릴리스 날짜: 2018년 7월 20일

## <a name="whats-new-in-53"></a>5\.3의 새로운 기능

- 모든 플랫폼에서 Microsoft ODBC 드라이버 17.2를 지원합니다.
- macOS High Sierra를 지원합니다(ODBC 드라이버 17 이상 필요).
- 모든 지원되는 Windows, Linux 또는 macOS 플랫폼에서 Always Encrypted 기능을 사용할 수 있도록 기본 CRUD 기능에 대해 Always Encrypted용 Azure Key Vault를 지원합니다. [SQL Server용 PHP 드라이버와 함께 Always Encrypted 사용](../../connect/php/using-always-encrypted-php-drivers.md)
- Ubuntu 18.04 LTS를 지원합니다(ODBC Driver 17.2 필요).
- Linux 또는 macOS에서 연결 복원력을 지원합니다(ODBC 드라이버 17.2 필요).

## <a name="52"></a>5.2

![다운로드](../../ssms/media/download-icon.png) [Windows 패키지 다운로드](https://go.microsoft.com/fwlink/?linkid=2120451)  
[GitHub 릴리스 태그(Linux 및 macOS 패키지 확인 가능)](https://github.com/Microsoft/msphpsql/releases/tag/v5.2.0)

### <a name="version-information"></a>버전 정보

- 릴리스 번호: 5.2.0
- 릴리스 날짜: 2018년 3월 23일

## <a name="whats-new-in-52"></a>5\.2의 새로운 기능

- Windows에서 PHP 7.2.1 이상을 지원, 그 외 플랫폼에서 7.2.0 이상을 지원합니다.
- Microsoft ODBC 드라이버 17을 지원합니다.
  - 이제 모든 플랫폼에서 버전 17이 기본 버전입니다.
- Ubuntu 17.10, Debian 9 및 Suse Enterprise Linux 12를 지원합니다.
- Ubuntu 15.10에 대한 지원을 삭제했습니다.
- Windows에서 CRUD 기능을 사용하는 Always Encrypted를 지원합니다. 자세한 내용은 [Using Always Encrypted with the PHP Drivers for SQL Server](../../connect/php/using-always-encrypted-php-drivers.md)(SQL Server용 PHP 드라이버와 함께 Always Encrypted 사용)를 참조하세요.
  - Windows 인증서 저장소를 지원합니다.
  - Always Encrypted는 Microsoft ODBC 드라이버 17 이상에서만 지원됩니다.
- Linux 및 macOS에서 비 UTF8 로캘을 지원합니다.
  - Linux 및 macOS의 비 UTF8 로캘은 Microsoft ODBC 드라이버 17 이상에서만 지원됩니다.
- Azure SQL Data Warehouse 지원
- Azure SQL Managed Instance를 지원합니다.

## <a name="43"></a>4.3

![다운로드](../../ssms/media/download-icon.png) [Windows 패키지 다운로드](https://go.microsoft.com/fwlink/?linkid=2120616)  
[GitHub 릴리스 태그(Linux 및 macOS 패키지 확인 가능)](https://github.com/Microsoft/msphpsql/releases/tag/v4.3.0)

### <a name="version-information"></a>버전 정보

- 릴리스 번호: 4.3.0
- 릴리스 날짜: 2017년 7월 6일

## <a name="whats-new-in-43"></a>4\.3의 새로운 기능

- PHP 7.1 지원
- macOS Sierra 및 macOS El Capitan을 지원합니다.
- Ubuntu 15.10 및 Debian 8을 지원합니다.
- Ubuntu 15.04에 대한 지원을 삭제했습니다.
- 투명 네트워크 IP 확인을 통해 Always On 가용성 그룹을 지원합니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.
- 제한 사항이 있는 sql_variant 데이터 형식에 대한 지원을 추가했습니다.
- Windows에서 유휴 연결 복원력을 지원합니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.
- Linux 및 macOS에서 연결 풀링을 지원합니다. 자세한 내용은 [Connection Pooling](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)을 참조하세요.
- ActiveDirectoryPassword 및 SqlPassword를 사용한 Azure Active Directory 인증을 지원합니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.

## <a name="40"></a>4.0

![다운로드](../../ssms/media/download-icon.png) [Windows 패키지 다운로드](https://go.microsoft.com/fwlink/?linkid=2120448)  
[GitHub 릴리스 태그(Linux 및 macOS 패키지 확인 가능)](https://github.com/microsoft/msphpsql/releases/tag/v4.0-RTW)

### <a name="version-information"></a>버전 정보

- 릴리스 번호: 4.0
- 릴리스 날짜: 2016년 7월 1일

## <a name="whats-new-in-40"></a>4\.0의 새로운 기능

- PHP 7.0 지원  
- 64비트를 완벽하게 지원합니다.
- Ubuntu 15.04, Ubuntu 16.04 및 RedHat 7을 지원합니다.

## <a name="32"></a>3.2

![다운로드](../../ssms/media/download-icon.png) [Windows 패키지 다운로드](https://go.microsoft.com/fwlink/?linkid=2120449)  
[GitHub 릴리스 태그(Linux 및 macOS 패키지 확인 가능)](https://github.com/microsoft/msphpsql/releases/tag/v3.2.0.0)

### <a name="version-information"></a>버전 정보

- 릴리스 번호: 3.2
- 릴리스 날짜: 2015년 3월 9일

## <a name="whats-new-in-32"></a>3\.2의 새로운 기능

- PHP 5.6을 지원합니다.  
- 이전 PHP 버전 5.5 및 5.4에 대한 최신 업데이트를 포함합니다.  
- Microsoft ODBC Driver 11 for SQL Server 필요  

## <a name="31"></a>3.1

[GitHub 릴리스 태그(Linux 및 macOS 패키지 확인 가능)](https://github.com/microsoft/msphpsql/releases/tag/v3.1.0.0)

### <a name="version-information"></a>버전 정보

- 릴리스 번호: 3.1
- 릴리스 날짜: 2014년 12월 12일

## <a name="whats-new-in-31"></a>3\.1의 새로운 기능

- PHP 5.5를 지원합니다.  
- Microsoft ODBC Driver 11 for SQL Server가 필요합니다. SQL Native Client에 필요한 이전 버전입니다.  

## <a name="whats-new-in-30"></a>3\.0의 새로운 기능  

- PHP 5.4를 지원합니다.  PHP 5.2는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 3에서 지원되지 않습니다.  
- AttachDBFileName 연결 옵션이 추가되었습니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
- LocalDB 지원이 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 추가되었습니다. 자세한 내용은 [LocalDB 지원](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)을 참조하세요.
- AttachDBFileName 연결 옵션이 추가되었습니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
- 고가용성, 재해 복구 기능을 지원합니다. 자세한 내용은 [고가용성, 재해 복구를 위한 JDBC 드라이브 지원](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)을 참조하세요.
- 클라이언트 쪽 커서(메모리 내 결과 집합 캐싱)를 지원합니다. 자세한 내용은 [커서 유형&#40;SQLSRV 드라이버&#41;](../../connect/php/cursor-types-sqlsrv-driver.md) 및 [커서 유형&#40;PDO_SQLSRV 드라이버&#41;](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)를 참조하세요.
- PDO::ATTR_EMULATE_PREPARES 특성이 추가되었습니다. 자세한 내용은 [PDO::prepare](../../connect/php/pdo-prepare.md)을 참조하세요.  

## <a name="whats-new-in-20"></a>2\.0의 새로운 기능

버전 2.0에서는 PDO_SQLSRV 드라이버에 대한 지원이 추가되었습니다. 자세한 내용은 [PDO_SQLSRV 드라이버 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)를 참조하세요.  

## <a name="see-also"></a>참고 항목

[Microsoft Drivers for PHP for SQL Server 개요](../../connect/php/overview-of-the-php-sql-driver.md)
