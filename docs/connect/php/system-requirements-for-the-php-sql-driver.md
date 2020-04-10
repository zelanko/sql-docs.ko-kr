---
title: Microsoft Drivers for PHP for SQL Server에 대한 시스템 요구 사항 | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
author: David-Engel
ms.reviewer: carlrab
ms.author: v-daenge
ms.openlocfilehash: 2e48fcb222575095fab4c313102de8abc4e3efa0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926864"
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server에 대한 시스템 요구 사항

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 문서에서는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]를 사용하여 SQL Server 또는 Azure SQL Database의 데이터에 액세스하기 위해 시스템에 설치해야 하는 구성 요소를 나열합니다.

Microsoft PHP Drivers for SQL Server 버전 3.2 이상이 공식적으로 지원됩니다. PHP 드라이버의 지원 주기 및 요구 사항에 대한 자세한 내용은 [지원 매트릭스](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md)를 참조하세요.

## <a name="php"></a>PHP

안정적인 최신 PHP 이진 파일을 다운로드하고 설치하는 방법에 대한 자세한 내용은 [PHP 웹 사이트](https://php.net)를 참조하세요.  Microsoft Drivers for PHP for SQL Server에는 [PHP 버전 지원](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md#php-version-support)에 설명된 대로 올바른 버전의 PHP가 필요합니다.

-   해당하는 PHP 버전을 사용하여 올바른 버전의 드라이버 파일을 사용하도록 설정해야 합니다. 다른 드라이버 파일에 대한 자세한 내용은 [드라이버 버전](#driver-versions)을 참조하세요.  드라이버를 다운로드하려면 [Microsoft Drivers for PHP for SQL Server 다운로드](../../connect/php/download-drivers-php-sql-server.md)를 참조하세요. PHP에 대한 드라이버를 구성하는 방법에 대한 자세한 내용은 [Microsoft Drivers for PHP for SQL Server 로드](../../connect/php/loading-the-php-sql-driver.md)를 참조하세요.

-   웹 서버가 필요합니다. 웹 서버는 PHP를 실행하도록 구성되어야 합니다. IIS를 통한 PHP 애플리케이션 호스트에 대한 자세한 내용은 [PHP 웹 사이트의 자습서](http://docs.php.net/manual/da/install.windows.iis7.php)를 참조하세요.

    [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]가 FastCGI에서 IIS 10을 사용하여 테스트되었습니다.

    > [!NOTE]
    > Microsoft는 IIS에 대해서만 지원합니다.

## <a name="odbc-driver"></a>ODBC 드라이버

PHP가 실행되는 컴퓨터에 Microsoft ODBC Driver for SQL Server의 올바른 버전이 필요합니다. [이 페이지](https://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2017)에서 지원되는 플랫폼에 대해 지원되는 모든 버전의 드라이버를 다운로드할 수 있습니다.

64비트 버전의 Windows에서 Windows 버전의 드라이버를 다운로드하는 경우 ODBC 64비트 설치 프로그램은 32비트 및 64비트 ODBC 드라이버를 모두 설치합니다. 32비트 버전의 Windows를 사용하는 경우 ODBC x86 설치 프로그램을 사용합니다. Windows가 아닌 플랫폼에서는 64비트 버전의 드라이버만 사용할 수 있습니다.

|SQL Server 드라이버 버전용 PHP &#8594;<br />&#8595; ODBC 드라이버 버전|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|ODBC 드라이버 17+ |Y|Y|Y|Y| | | |
|ODBC 드라이버 13.1|Y|Y|Y|Y|Y|Y| |
|ODBC 드라이버 13  | | | | | |Y| |
|ODBC 드라이버 11  |Y|Y|Y|Y|Y|Y|Y|

SQLSRV 드라이버를 사용하는 경우 [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용되는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] Microsoft ODBC Driver for SQL Server 버전에 대한 정보를 반환합니다. PDO_SQLSRV 드라이버를 사용하는 경우 [PDO::getAttribute](../../connect/php/pdo-getattribute.md)를 사용하여 버전을 검색할 수 있습니다.

## <a name="sql-server"></a>SQL Server

Azure SQL Database에서 PHP를 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure SQL Database에 연결](../../connect/php/connecting-to-microsoft-azure-sql-database.md)을 참조하세요.

|SQL Server 드라이버 버전용 PHP &#8594;<br />&#8595; SQL Server 버전|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL Database(모든 배포 옵션)        |Y|Y|Y|Y| | | |
|Azure SQL Synapse  |Y|Y|Y|Y| | | |
|SQL Server 2019           |Y|Y|Y|Y| | | |
|SQL Server 2017           |Y|Y|Y|Y| | | |
|SQL Server 2016           |Y|Y|Y|Y|Y| | |
|SQL Server 2014           |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2012           |Y|Y|Y|Y|Y|Y|Y|
|SQL Server 2008 R2        | |Y|Y|Y|Y|Y|Y|
|SQL Server 2008           | | | | |Y|Y|Y|

## <a name="operating-systems"></a>운영 체제

지원되는 운영 체제에 대한 자세한 내용은 [지원되는 운영 체제](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md#supported-operating-systems)를 참조하세요.

## <a name="driver-versions"></a>드라이버 버전

이 섹션에는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 각 버전에 포함된 드라이버 파일이 나와 있습니다. 각 설치 패키지에는 스레드 및 비스레드 변형의 SQLSRV 및 PDO_SQLSRV 드라이버 파일이 포함되어 있습니다. Windows에서는 32비트 및 64비트 변형도 사용할 수 있습니다. PHP 런타임에 사용할 드라이버를 구성하려면 [Microsoft Drivers for PHP for SQL Server 로드](../../connect/php/loading-the-php-sql-driver.md)의 설치 지침을 따릅니다.

지원되는 Linux 및 macOS 버전에서 [Linux 및 macOS 설치 지침](../../connect/php/installation-tutorial-linux-mac.md)에 따라 PHP의 PECL 패키지 시스템을 사용하여 적절한 드라이버를 설치할 수 있습니다. 또는 [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) GitHub 프로젝트 페이지에서 해당 플랫폼용으로 사전 빌드된 바이너리를 다운로드할 수 있습니다. 아래 표에는 사전 빌드된 바이너리 패키지의 파일이 나열되어 있습니다.

**Microsoft Drivers 5.8 for PHP for SQL Server:**

Windows에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|
|---------------|:---------------:|:----------------:|---------------------|
|32비트 php_sqlsrv_72_nts.dll<br />32비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_72_ts.dll <br />32비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_72_nts.dll<br />64비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_72_ts.dll <br />64비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|64비트 php7ts.dll|
|32비트 php_sqlsrv_73_nts.dll<br />32비트 php_pdo_sqlsrv_73_nts.dll|7.3|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_73_ts.dll <br />32비트 php_pdo_sqlsrv_73_ts.dll |7.3|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_73_nts.dll<br />64비트 php_pdo_sqlsrv_73_nts.dll|7.3|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_73_ts.dll <br />64비트 php_pdo_sqlsrv_73_ts.dll |7.3|예|64비트 php7ts.dll|
|32비트 php_sqlsrv_74_nts.dll<br />32비트 php_pdo_sqlsrv_74_nts.dll|7.4|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_74_ts.dll <br />32비트 php_pdo_sqlsrv_74_ts.dll |7.4|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_74_nts.dll<br />64비트 php_pdo_sqlsrv_74_nts.dll|7.4|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_74_ts.dll <br />64비트 php_pdo_sqlsrv_74_ts.dll |7.4|예|64비트 php7ts.dll|

Linux에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|아니요 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|예|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|아니요 |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|예|
|php_sqlsrv_74_nts.so<br />php_pdo_sqlsrv_74_nts.so|7.4|아니요 |
|php_sqlsrv_74_ts.so <br />php_pdo_sqlsrv_74_ts.so |7.4|예|

**Microsoft Drivers 5.6 for PHP for SQL Server:**

Windows에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|
|---------------|:---------------:|:----------------:|---------------------|
|32비트 php_sqlsrv_71_nts.dll<br />32비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_71_ts.dll <br />32비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_71_nts.dll<br />64비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_71_ts.dll <br />64비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|64비트 php7ts.dll|
|32비트 php_sqlsrv_72_nts.dll<br />32비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_72_ts.dll <br />32비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_72_nts.dll<br />64비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_72_ts.dll <br />64비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|64비트 php7ts.dll|
|32비트 php_sqlsrv_73_nts.dll<br />32비트 php_pdo_sqlsrv_73_nts.dll|7.3|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_73_ts.dll <br />32비트 php_pdo_sqlsrv_73_ts.dll |7.3|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_73_nts.dll<br />64비트 php_pdo_sqlsrv_73_nts.dll|7.3|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_73_ts.dll <br />64비트 php_pdo_sqlsrv_73_ts.dll |7.3|예|64비트 php7ts.dll|

Linux에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|아니요 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|예|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|아니요 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|예|
|php_sqlsrv_73_nts.so<br />php_pdo_sqlsrv_73_nts.so|7.3|아니요 |
|php_sqlsrv_73_ts.so <br />php_pdo_sqlsrv_73_ts.so |7.3|예|

**Microsoft Drivers 5.3 for PHP for SQL Server:**

Windows에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|
|---------------|:---------------:|:----------------:|---------------------|
|32비트 php_sqlsrv_7_nts.dll <br />32비트 php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_7_ts.dll  <br />32비트 php_pdo_sqlsrv_7_ts.dll  |7.0|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_7_nts.dll <br />64비트 php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_7_ts.dll  <br />64비트 php_pdo_sqlsrv_7_ts.dll  |7.0|예|64비트 php7ts.dll|
|32비트 php_sqlsrv_71_nts.dll<br />32비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_71_ts.dll <br />32비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_71_nts.dll<br />64비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_71_ts.dll <br />64비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|64비트 php7ts.dll|
|32비트 php_sqlsrv_72_nts.dll<br />32비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_72_ts.dll <br />32비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_72_nts.dll<br />64비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_72_ts.dll <br />64비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|64비트 php7ts.dll|

Linux에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|아니요 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|예|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|아니요 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|예|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|아니요 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|예|

**Microsoft Drivers 5.2 for PHP for SQL Server:**

Windows에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|
|---------------|:---------------:|:----------------:|---------------------|
|32비트 php_sqlsrv_7_nts.dll <br />32비트 php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_7_ts.dll  <br />32비트 php_pdo_sqlsrv_7_ts.dll  |7.0|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_7_nts.dll <br />64비트 php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_7_ts.dll  <br />64비트 php_pdo_sqlsrv_7_ts.dll  |7.0|예|64비트 php7ts.dll|
|32비트 php_sqlsrv_71_nts.dll<br />32비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_71_ts.dll <br />32비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_71_nts.dll<br />64비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_71_ts.dll <br />64비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|64비트 php7ts.dll|
|32비트 php_sqlsrv_72_nts.dll<br />32비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_72_ts.dll <br />32비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_72_nts.dll<br />64비트 php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_72_ts.dll <br />64비트 php_pdo_sqlsrv_72_ts.dll |7.2|예|64비트 php7ts.dll|

Linux에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|아니요 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|예|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|아니요 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|예|
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|아니요 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|예|

**Microsoft Drivers 4.3 for PHP for SQL Server:**

Windows에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|
|---------------|:---------------:|:----------------:|---------------------|
|32비트 php_sqlsrv_7_nts.dll <br />32비트 php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_7_ts.dll  <br />32비트 php_pdo_sqlsrv_7_ts.dll  |7.0|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_7_nts.dll <br />64비트 php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_7_ts.dll  <br />64비트 php_pdo_sqlsrv_7_ts.dll  |7.0|예|64비트 php7ts.dll|
|32비트 php_sqlsrv_71_nts.dll<br />32비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |32비트 php7.dll|
|32비트 php_sqlsrv_71_ts.dll <br />32비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|32비트 php7ts.dll|
|64비트 php_sqlsrv_71_nts.dll<br />64비트 php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |64비트 php7.dll|
|64비트 php_sqlsrv_71_ts.dll <br />64비트 php_pdo_sqlsrv_71_ts.dll |7.1|예|64비트 php7ts.dll|

Linux에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|아니요 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|예|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|아니요 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|예|

**Microsoft Drivers 4.0 for PHP for SQL Server:**

Windows에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|
|---------------|:---------------:|:----------------:|---------------------|
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|아니요|32비트 php7.dll|
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|예|32비트 php7ts.dll|
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|아니요|64비트 php7.dll|
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|예|64비트 php7ts.dll|

Linux에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|:---------------:|:----------------:|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|아니요 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|예|

**Microsoft Drivers 3.2 for PHP for SQL Server:**

Windows에는 다음 버전의 드라이버가 포함되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|
|---------------|:---------------:|:----------------:|---------------------|
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|아니요|php5.dll|
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|예|php5ts.dll|
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|아니요|php5.dll|
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|예|php5ts.dll|
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|아니요|php5.dll|
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|예|php5ts.dll|

## <a name="see-also"></a>참고 항목

- [Microsoft Drivers for PHP for SQL Server 시작](../../connect/php/getting-started-with-the-php-sql-driver.md)
- [Microsoft Drivers for PHP for SQL Server 프로그래밍 가이드 | Microsoft Docs](../../connect/php/programming-guide-for-php-sql-driver.md)
- [SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)
- [PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)
