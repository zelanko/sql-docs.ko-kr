---
title: Microsoft Drivers for PHP for SQL Server에 대한 시스템 요구 사항 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0cea4c62c7976e1f6d84dc046abc1046179ef125
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66803910"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server에 대한 시스템 요구 사항
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 문서에서는 SQL Server 또는 Azure SQL Database 사용 하 여 데이터에 액세스 하기 위해 시스템에 설치 해야 하는 구성 요소는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다.

버전 3.1 및 SQL Server 용 Microsoft PHP 드라이버의 나중에 공식적으로 지원 됩니다. 지원 수명 주기 및 이전 버전의 PHP 드라이버를 포함 하 여 요구 사항에 대 한 전체 내용은 참조는 [지원 매트릭스](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md)합니다.

## <a name="php"></a>PHP

안정적인 최신 PHP 이진 파일을 다운로드하고 설치하는 방법에 대한 자세한 내용은 [PHP 웹 사이트](https://php.net)를 참조하세요.  Microsoft Drivers for PHP for SQL Server에는 다음 버전의 PHP 필요합니다.

|SQL Server 드라이버 버전에 대 한 PHP&#8594;<br />&#8595; PHP 버전|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|:---:|---|---|---|---|---|---|---|
|7.3|7.3.0+ | | | | | | |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>| | | | |
|7.1|7.1.0+ |7.1.0+ |7.1.0+ |7.1.0+ |       |        |        |
|7.0|       |7.0.0+ |7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |       |       |5.6.4+  |        |
|5.5|       |       |       |       |       |5.5.16+ |5.5.16+ |
|5.4|       |       |       |       |       |5.4.32  |5.4.32  |

1. 7\.2.1 버전 이상에서 사용할 Windows, 버전 7.2.0 하는 동안 및 나중에 Linux 및 macOS에서 지원 됩니다.

-   드라이버 파일의 버전은 PHP 확장 디렉터리에 있어야 합니다. 참조 [드라이버 버전](#driver-versions) 다른 드라이버 파일에 대 한 정보에 대 한 합니다.  드라이버를 다운로드하려면 [Microsoft Drivers for PHP for SQL Server 다운로드](../../connect/php/download-drivers-php-sql-server.md)를 참조하세요. PHP에 대한 드라이버를 구성하는 방법에 대한 자세한 내용은 [Microsoft Drivers for PHP for SQL Server 로드](../../connect/php/loading-the-php-sql-driver.md)를 참조하세요.

-   웹 서버가 필요합니다. 웹 서버는 PHP를 실행하도록 구성되어야 합니다. IIS 사용 하 여 PHP 응용 프로그램을 호스트 하는 방법에 대 한 정보를 참조 하세요. 합니다 [PHP의 웹 사이트의 자습서](http://docs.php.net/manual/da/install.windows.iis7.php)합니다.

    [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]가 FastCGI에서 IIS 10을 사용하여 테스트되었습니다.  

    > [!NOTE]  
    > Microsoft는 IIS에 대해서만 지원합니다.  

## <a name="odbc-driver"></a>ODBC 드라이버

PHP가 실행 중인 컴퓨터의 올바른 버전의 Microsoft ODBC Driver for SQL Server 필요 합니다. 지원 되는 모든 버전의 지원 되는 플랫폼에 대 한 드라이버를 다운로드할 수 있습니다 [이 페이지](https://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017)합니다.

Windows 버전의 64 비트 버전 Windows의 드라이버를 다운로드 하는 경우 ODBC 64 비트 설치 관리자는 32 비트 및 64 비트 ODBC 드라이버를 설치 합니다. Windows의 32 비트 버전을 사용 하는 경우 x86 ODBC를 사용 하 여 설치 합니다. 비 Windows 플랫폼에서 64 비트 버전의 드라이버를 사용할 수 있습니다.

|SQL Server 드라이버 버전에 대 한 PHP&#8594;<br />&#8595; ODBC 드라이버 버전|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|ODBC 드라이버 17+ |Y|Y|Y| | | | |
|ODBC 드라이버 13.1|Y|Y|Y|Y|Y| | |
|ODBC 드라이버 13  | | | | |Y| | |
|ODBC 드라이버 11  |Y|Y|Y|Y|Y|Y|Y|

SQLSRV 드라이버를 사용 하는 경우 [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) 버전에 대 한 정보가 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft ODBC Driver for SQL Server에서 사용 되 고는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다. PDO_SQLSRV 드라이버를 사용하는 경우 [PDO::getAttribute](../../connect/php/pdo-getattribute.md)를 사용하여 버전을 검색할 수 있습니다.  

## <a name="sql-server"></a>SQL Server

Azure SQL Database 지원 됩니다. 자세한 내용은 [Microsoft Azure SQL Database에 연결](../../connect/php/connecting-to-microsoft-azure-sql-database.md)을 참조하세요.

|SQL Server 드라이버 버전에 대 한 PHP&#8594;<br />&#8595; SQL Server 버전|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL 데이터베이스        |Y|Y|Y|Y| | | |
|Azure SQL 관리되는 인스턴스|Y|Y|Y|Y| | | |
|Azure SQL 데이터 웨어하우스  |Y|Y|Y|Y| | | |
|SQL Server 2017           |Y|Y|Y|Y| | | |
|SQL Server 2016           |Y|Y|Y|Y|Y| | |
|SQL Server 2014           |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2012           |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008 R2        |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008           | | | | |Y|Y|Y|

## <a name="operating-systems"></a>운영 체제
각 버전의 드라이버에 대 한 지원 되는 운영 체제는 다음과 같습니다.

|SQL Server 드라이버 버전에 대 한 PHP&#8594;<br />&#8595; 운영 체제|5.6|5.3|5.2|4.3|4.0|3.2|3.1|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2016                 |Y  |Y  |Y  |Y  |   |   |   |
|Windows Server 2012 R2              |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows Server 2012                 |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows Server 2008 R2 SP1          |   |   |   |   |Y  |Y  |Y  |
|Windows Server 2008 SP2             |   |   |   |   |Y  |Y  |Y  |
|Windows 10                          |Y  |Y  |Y  |Y  |Y  |   |   |
|Windows 8.1                         |Y  |Y  |Y  |Y  |Y  |Y  |Y  |
|Windows 8                           |   |   |   |Y  |Y  |Y  |Y  |
|Windows 7 SP1                       |   |   |   |   |Y  |Y  |Y  |
|Windows Vista SP2                   |   |   |   |   |Y  |Y  |Y  |
|Ubuntu 18.10 (64 비트)               |Y  |   |   |   |   |   |   |
|Ubuntu 18.04 (64 비트)               |Y  |Y  |   |   |   |   |   |
|Ubuntu 17.10 (64 비트)               |   |Y  |Y  |   |   |   |   |
|Ubuntu 16.04 (64 비트)               |Y  |Y  |Y  |Y  |Y  |   |   |
|Ubuntu 15.10 (64 비트)               |   |   |   |Y  |   |   |   |
|Ubuntu 15.04 (64 비트)               |   |   |   |   |Y  |   |   |
|Debian 9 (64 비트)                   |Y  |Y  |Y  |   |   |   |   |
|Debian 8 (64 비트)                   |Y  |Y  |Y  |Y  |   |   |   |
|Red Hat Enterprise Linux 7(64비트) |Y  |Y  |Y  |Y  |Y  |   |   |
|Suse Enterprise Linux 15 (64 비트)   |Y  |   |   |   |   |   |   |
|Suse Enterprise Linux 12 (64 비트)   |Y  |Y  |Y  |   |   |   |   |
|macOS Mojave (64 비트)               |Y  |   |   |   |   |   |   |
|macOS High Sierra (64 비트)          |Y  |Y  |   |   |   |   |   |
|macOS Sierra (64 비트)               |Y  |Y  |Y  |Y  |   |   |   |
|macOS El Capitan (64 비트)           |   |Y  |Y  |Y  |   |   |   |

## <a name="driver-versions"></a>드라이버 버전  
이 섹션의 각 버전에 포함 된 드라이버 파일을 나열 합니다 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다. 각 설치 패키지는 스레드 및 스레드 비 variant의 SQLSRV 및 PDO_SQLSRV 드라이버 파일을 포함합니다. Windows에서 32 비트 및 64 비트 변형에서 사용할 수 있습니다. 설치 지침을 따라 PHP 런타임에 사용할 드라이버를 구성 하려면 [Loading the Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)합니다.

Linux 및 macOS의 지원 되는 버전에 적절 한 드라이버를 설치할 수 있습니다 다음 PHP의 PECL 패키지 시스템을 사용 하 여 [Linux 및 macOS 설치 지침](../../connect/php/installation-tutorial-linux-mac.md)합니다. 또는에서 사용 중인 플랫폼에 대 한 미리 작성 된 이진 파일을 다운로드할 수 있습니다 합니다 [&#40;microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 프로젝트 페이지-아래 표에서 미리 작성 된 이진 패키지에 있는 파일입니다.

**Microsoft Drivers 5.6 for PHP for SQL Server:**  

다음 버전의 드라이버를 Windows에 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|32비트 php_sqlsrv_71_nts.dll<br />32비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |32비트 php7.dll|  
|32비트 php_sqlsrv_71_ts.dll <br />32비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|32 비트 php7ts.dll|  
|64비트 php_sqlsrv_71_nts.dll<br />64비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |64비트 php7.dll|  
|64비트 php_sqlsrv_71_ts.dll <br />64비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|64 비트 php7ts.dll|   
|32비트 php_sqlsrv_72_nts.dll<br />32비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |32비트 php7.dll|  
|32비트 php_sqlsrv_72_ts.dll <br />32비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|32 비트 php7ts.dll|  
|64비트 php_sqlsrv_72_nts.dll<br />64비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |64비트 php7.dll|  
|64비트 php_sqlsrv_72_ts.dll <br />64비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|64 비트 php7ts.dll|  
|32비트 php_sqlsrv_73_nts.dll<br />32비트 php_pdo_sqlsrv_73_nts.dll|7.3|아니요 |32비트 php7.dll|  
|32비트 php_sqlsrv_73_ts.dll <br />32비트 php_pdo_sqlsrv_73_ts.dll |7.3|예|32 비트 php7ts.dll|  
|64비트 php_sqlsrv_73_nts.dll<br />64비트 php_pdo_sqlsrv_73_nts.dll|7.3|아니요 |64비트 php7.dll|  
|64비트 php_sqlsrv_73_ts.dll <br />64비트 php_pdo_sqlsrv_73_ts.dll |7.3|예|64 비트 php7ts.dll|  

Linux에서는 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|아니요 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|예|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|아니요 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|예|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|아니요 |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|예|

**Microsoft Drivers 5.3 for PHP for SQL Server:**  

다음 버전의 드라이버를 Windows에 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|32비트 php_sqlsrv_7_nts.dll <br />32비트 php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_7_ts.dll  <br />32비트 php_pdo_sqlsrv_7_ts.dll  |7.0|예|32 비트 php7ts.dll|
|64비트 php_sqlsrv_7_nts.dll <br />64비트 php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |64비트 php7.dll|  
|64비트 php_sqlsrv_7_ts.dll  <br />64비트 php_pdo_sqlsrv_7_ts.dll  |7.0|예|64 비트 php7ts.dll|
|32비트 php_sqlsrv_71_nts.dll<br />32비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |32비트 php7.dll|  
|32비트 php_sqlsrv_71_ts.dll <br />32비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|32 비트 php7ts.dll|  
|64비트 php_sqlsrv_71_nts.dll<br />64비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |64비트 php7.dll|  
|64비트 php_sqlsrv_71_ts.dll <br />64비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|64 비트 php7ts.dll|   
|32비트 php_sqlsrv_72_nts.dll<br />32비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |32비트 php7.dll|  
|32비트 php_sqlsrv_72_ts.dll <br />32비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|32 비트 php7ts.dll|  
|64비트 php_sqlsrv_72_nts.dll<br />64비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |64비트 php7.dll|  
|64비트 php_sqlsrv_72_ts.dll <br />64비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|64 비트 php7ts.dll|  

Linux에서는 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|아니요 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|예|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|아니요 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|예|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|아니요 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|예|

**Microsoft Drivers 5.2 for PHP for SQL Server:**  

다음 버전의 드라이버를 Windows에 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|32비트 php_sqlsrv_7_nts.dll <br />32비트 php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_7_ts.dll  <br />32비트 php_pdo_sqlsrv_7_ts.dll  |7.0|예|32 비트 php7ts.dll|
|64비트 php_sqlsrv_7_nts.dll <br />64비트 php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |64비트 php7.dll|  
|64비트 php_sqlsrv_7_ts.dll  <br />64비트 php_pdo_sqlsrv_7_ts.dll  |7.0|예|64 비트 php7ts.dll|
|32비트 php_sqlsrv_71_nts.dll<br />32비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |32비트 php7.dll|  
|32비트 php_sqlsrv_71_ts.dll <br />32비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|32 비트 php7ts.dll|  
|64비트 php_sqlsrv_71_nts.dll<br />64비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |64비트 php7.dll|  
|64비트 php_sqlsrv_71_ts.dll <br />64비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|64 비트 php7ts.dll|   
|32비트 php_sqlsrv_72_nts.dll<br />32비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |32비트 php7.dll|  
|32비트 php_sqlsrv_72_ts.dll <br />32비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|32 비트 php7ts.dll|  
|64비트 php_sqlsrv_72_nts.dll<br />64비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |64비트 php7.dll|  
|64비트 php_sqlsrv_72_ts.dll <br />64비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|64 비트 php7ts.dll|  

Linux에서는 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|아니요 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|예|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|아니요 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|예|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|아니요 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|예|

**Microsoft Drivers 4.3 for PHP for SQL Server:**  

다음 버전의 드라이버를 Windows에 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|32비트 php_sqlsrv_7_nts.dll <br />32비트 php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_7_ts.dll  <br />32비트 php_pdo_sqlsrv_7_ts.dll  |7.0|예|32 비트 php7ts.dll|
|64비트 php_sqlsrv_7_nts.dll <br />64비트 php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |64비트 php7.dll|  
|64비트 php_sqlsrv_7_ts.dll  <br />64비트 php_pdo_sqlsrv_7_ts.dll  |7.0|예|64 비트 php7ts.dll|
|32비트 php_sqlsrv_71_nts.dll<br />32비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |32비트 php7.dll|  
|32비트 php_sqlsrv_71_ts.dll <br />32비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|32 비트 php7ts.dll|  
|64비트 php_sqlsrv_71_nts.dll<br />64비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |64비트 php7.dll|  
|64비트 php_sqlsrv_71_ts.dll <br />64비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|64 비트 php7ts.dll|   

Linux에서는 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|아니요 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|예|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|아니요 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|예|  

**Microsoft Drivers 4.0 for PHP for SQL Server:**  

다음 버전의 드라이버를 Windows에 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|아니요|32비트 php7.dll|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|예|32 비트 php7ts.dll|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|아니요|64비트 php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|예|64 비트 php7ts.dll|   

Linux에서는 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|아니요 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|예|

**Microsoft Drivers 3.2 for PHP for SQL Server:**  

다음 버전의 드라이버를 Windows에 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|아니요|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|예|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|아니요|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|예|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|아니요|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|예|php5ts.dll|  

**Microsoft Drivers 3.1 for PHP for SQL Server:**  

다음 버전의 드라이버를 Windows에 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|:---------------:|:----------------:|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|아니요|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|예|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|아니요|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|예|php5ts.dll|  

## <a name="see-also"></a>참고 항목  
[Microsoft Drivers for PHP for SQL Server 시작](../../connect/php/getting-started-with-the-php-sql-driver.md)

[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)  
