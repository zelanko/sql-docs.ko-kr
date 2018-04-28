---
title: 시스템 요구 사항을 Microsoft Drivers for PHP for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/23/2018
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
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
caps.latest.revision: 93
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 44a18257abc758ee910fb9c4953cbdef02239fbd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="system-requirements-for-the-microsoft-drivers-for-php-for-sql-server"></a>시스템 요구 사항을 Microsoft Drivers for PHP for SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 문서에서는 SQL Server 또는 Azure SQL 데이터베이스 사용 하 여 데이터 액세스는 시스템에 설치 해야 하는 구성 요소는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다.

버전 3.1 및 SQL Server 용 Microsoft PHP 드라이버의 나중에 공식적으로 지원 됩니다. 지원 수명 주기 및 이전 버전의 PHP 드라이버를 포함 하 여 요구 사항에 자세한 내용은 참조는 [지원 매트릭스](../../connect/php/microsoft-php-drivers-for-sql-server-support-matrix.md)합니다.

## <a name="php"></a>PHP

안정적인 최신 PHP 바이너리를 설치 하는 방법에 대 한 정보를 참조 하십시오. [PHP 웹 사이트](http://php.net)합니다.  Microsoft Drivers for PHP for SQL Server에는 다음 버전의 PHP 필요:

|PHP for SQL Server 드라이버 버전&#8594;<br />&#8595;PHP 버전|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|7.2|Windows에서 7.2.1+<br/>다른 플랫폼에서 7.2.0+ | | | | |
|7.1|7.1.0+ |7.1.0+ |       |        |        |
|7.0|7.0.0+ |7.0.0+ |7.0.0+ |        |        |
|5.6|       |       |       |5.6.4+  |        |
|5.5|       |       |       |5.5.16+ |5.5.16+ |
|5.4|       |       |       |5.4.32  |5.4.32  |

-   드라이버 파일의 버전은 PHP 확장 디렉터리에 있어야 합니다. 참조 [드라이버 버전](#driver-versions) 다른 드라이버 파일에 대 한 정보에 대 한 합니다.  드라이버를 다운로드 하려면 [SQL Server 용 Microsoft Drivers for PHP 다운로드](download-drivers-php-sql-server.md)합니다. PHP에 대 한 드라이버를 구성 하는 방법에 대 한 정보를 참조 하십시오. [SQL Server 용 Microsoft Drivers for PHP 로드](../../connect/php/loading-the-php-sql-driver.md)합니다.

-   웹 서버가 필요합니다. 웹 서버는 PHP를 실행하도록 구성되어야 합니다. IIS에서 PHP 응용 프로그램 호스팅에 대 한 정보를 참조 하십시오.는 [PHP의 웹 사이트의 자습서](http://php.net/manual/fa/install.windows.iis.php)합니다.  

    [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] FastCGI와 함께 IIS 10을 사용 하 여 테스트 되었습니다.  

    > [!NOTE]  
    > Microsoft는 IIS에 대해서만 지원합니다.  

## <a name="odbc-driver"></a>ODBC 드라이버

PHP가 실행 중인 컴퓨터에 올바른 버전의 Microsoft ODBC Driver for SQL Server 필요 합니다. 다음 링크에서 다운로드 하세요.
- [17 Microsoft ODBC Driver for SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=56567)
- [Microsoft ODBC Driver 13.1 for SQL Server](https://www.microsoft.com/en-us/download/details.aspx?id=53339)
- [Microsoft ODBC Driver 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=50420)
- [Microsoft ODBC Driver 11 for SQL Server](http://www.microsoft.com/download/details.aspx?id=36434)

64 비트 운영 체제를 사용 하는 경우 ODBC 64 비트 설치 관리자는 32 비트 및 64 비트 ODBC 드라이버를 설치 합니다. 32 비트 운영 체제를 사용 하는 경우 x86 ODBC를 사용 하 여 설치 합니다.

|PHP for SQL Server 드라이버 버전&#8594;<br />&#8595;ODBC 드라이버 버전|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|ODBC 드라이버 17  |Y| | | | |
|ODBC Driver 13.1|Y|Y|Y| | |
|ODBC Driver 13  | | |Y| | |
|ODBC Driver 11  |Y|Y|Y|Y|Y|

SQLSRV 드라이버를 사용 하는 경우 [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) 의 버전에 대 한 정보를 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Microsoft ODBC Driver for SQL Server에서 사용 되 고는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다. PDO_SQLSRV 드라이버를 사용 하는 경우 사용할 수 있습니다 [pdo:: getattribute](../../connect/php/pdo-getattribute.md) 버전을 검색 합니다.  

## <a name="sql-server"></a>SQL Server

Azure SQL 데이터베이스가 지원 됩니다. 자세한 내용은 참조 [Microsoft Azure SQL 데이터베이스에 연결](../../connect/php/connecting-to-microsoft-azure-sql-database.md)합니다.

|PHP for SQL Server 드라이버 버전&#8594;<br />&#8595;SQL Server 버전|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|관리 되는 azure SQL 인스턴스<br/> (확장 비공개 미리 보기)|Y|Y| | | |
|Azure SQL 데이터 웨어하우스|Y|Y| | | |
|SQL Server 2017   |Y|Y| | | |
|SQL Server 2016   |Y|Y|Y| | |
|SQL Server 2014   |Y|Y|Y|Y|Y|
|SQL Server 2012   |Y|Y|Y|Y|Y|
|SQL Server 2008 R2|Y|Y|Y|Y|Y|
|SQL Server 2008   | | |Y|Y|Y|

## <a name="operating-systems"></a>운영 체제
버전의 드라이버에 대 한 지원 되는 운영 체제는 다음과 같습니다.

|PHP for SQL Server 드라이버 버전&#8594;<br />&#8595;운영 체제|5.2<br />&nbsp;|4.3<br />&nbsp;|4.0<br />&nbsp;|3.2<br />&nbsp;|3.1<br />&nbsp;|
|---|---|---|---|---|---|
|Windows Server 2016                      |Y|Y| | | |
|Windows Server 2012 R2                   |Y|Y|Y|Y|Y|
|Windows Server 2012                      |Y|Y|Y|Y|Y|
|Windows Server 2008 R2 SP1               | | |Y|Y|Y|
|Windows Server 2008 SP2                  | | |Y|Y|Y|
|Windows 10                               |Y|Y|Y| | |
|Windows 8.1                              |Y|Y|Y|Y|Y|
|Windows 8                                | |Y|Y|Y|Y|
|Windows 7 SP1                            | | |Y|Y|Y|
|Windows Vista SP2                        | | |Y|Y|Y|
|Ubuntu 17.10 (64 비트)                    |Y| | | | |
|Ubuntu 16.04 (64 비트)                    |Y|Y|Y| | |
|Ubuntu 15.10 (64 비트)                    | |Y| | | |
|Ubuntu 15.04 (64 비트)                    | | |Y| | |
|Debian 9 (64 비트)                        |Y| | | | |
|Debian 8 (64 비트)                        |Y|Y| | | |
|Red Hat Enterprise Linux 7 (64 비트)      |Y|Y|Y| | |
|엔터프라이즈 Suse Linux (64 비트) 12        |Y| | | | |
|macOS 시에라 (64 비트)                    |Y|Y| | | |
|macOS El Capitan (64 비트)                |Y|Y| | | |

## <a name="driver-versions"></a>드라이버 버전  
이 섹션의 각 버전에 포함 된 드라이버 파일을 나열는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다. 각 설치 패키지는 스레드 및 스레드 비 variants에 SQLSRV 및 PDO_SQLSRV 드라이버 파일을 포함 합니다. windows에서 32 비트 및 64 비트 변형에서 사용할 수 있습니다. 설치 지침을 따라 PHP 런타임에 사용할 드라이버를 구성 하려면 [SQL Server 용 Microsoft Drivers for PHP 로드](../../connect/php/loading-the-php-sql-driver.md)합니다.

Linux와 macOS의 지원 되는 버전을 해당 하는 드라이버를 설치할 수 다음 PHP의 PECL 패키지 시스템을 사용 하 여 [Linux와 macOS 설치 지침](../../connect/php/installation-tutorial-linux-mac.md)합니다. 또는에서 사용 중인 플랫폼에 대 한 미리 작성 된 이진 파일을 다운로드할 수 있습니다는 [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 프로젝트 페이지-아래 표에서 미리 작성 된 이진 패키지에 있는 파일입니다.

**Microsoft Drivers for PHP for SQL Server 5.2:**  

Windows에서는 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |32 비트 php7.dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|예|32 비트 php7ts.dll|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |64 비트 php7.dll|  
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|예|64 비트 php7ts.dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |32 비트 php7.dll|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|예|32 비트 php7ts.dll|  
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |64 비트 php7.dll|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|예|64 비트 php7ts.dll|   
|32-bit php_sqlsrv_72_nts.dll<br />32-bit php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |32 비트 php7.dll|  
|32-bit php_sqlsrv_72_ts.dll <br />32-bit php_pdo_sqlsrv_72_ts.dll |7.2|예|32 비트 php7ts.dll|  
|64-bit php_sqlsrv_72_nts.dll<br />64-bit php_pdo_sqlsrv_72_nts.dll|7.2|아니요 |64 비트 php7.dll|  
|64-bit php_sqlsrv_72_ts.dll <br />64-bit php_pdo_sqlsrv_72_ts.dll |7.2|예|64 비트 php7ts.dll|  

Linux에서 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|아니요 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|예|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|아니요 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|예|  
|php_sqlsrv_72_nts.so<br />php_pdo_sqlsrv_72_nts.so|7.2|아니요 |
|php_sqlsrv_72_ts.so <br />php_pdo_sqlsrv_72_ts.so |7.2|예|

**Microsoft Drivers for PHP for SQL Server 4.3:**  

Windows에서는 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|32-bit php_sqlsrv_7_nts.dll <br />32-bit php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |32 비트 php7.dll|
|32-bit php_sqlsrv_7_ts.dll  <br />32-bit php_pdo_sqlsrv_7_ts.dll  |7.0|예|32 비트 php7ts.dll|
|64-bit php_sqlsrv_7_nts.dll <br />64-bit php_pdo_sqlsrv_7_nts.dll |7.0|아니요 |64 비트 php7.dll|  
|64-bit php_sqlsrv_7_ts.dll  <br />64-bit php_pdo_sqlsrv_7_ts.dll  |7.0|예|64 비트 php7ts.dll|
|32-bit php_sqlsrv_71_nts.dll<br />32-bit php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |32 비트 php7.dll|  
|32-bit php_sqlsrv_71_ts.dll <br />32-bit php_pdo_sqlsrv_71_ts.dll |7.1|예|32 비트 php7ts.dll|  
|64-bit php_sqlsrv_71_nts.dll<br />64-bit php_pdo_sqlsrv_71_nts.dll|7.1|아니요 |64 비트 php7.dll|  
|64-bit php_sqlsrv_71_ts.dll <br />64-bit php_pdo_sqlsrv_71_ts.dll |7.1|예|64 비트 php7ts.dll|   

Linux에서 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|아니요 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|예|
|php_sqlsrv_71_nts.so<br />php_pdo_sqlsrv_71_nts.so|7.1|아니요 |
|php_sqlsrv_71_ts.so <br />php_pdo_sqlsrv_71_ts.so |7.1|예|  

**Microsoft Drivers for PHP for SQL Server 4.0:**  

Windows에서는 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|아니요|32 비트 php7.dll|  
|php_sqlsrv_7_ts_x86.dll<br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|예|32 비트 php7ts.dll|  
|php_sqlsrv_7_nts_x64.dll<br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|아니요|64 비트 php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|예|64 비트 php7ts.dll|   

Linux에서 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|
|---------------|---------------|----------------|
|php_sqlsrv_7_nts.so <br />php_pdo_sqlsrv_7_nts.so |7.0|아니요 |
|php_sqlsrv_7_ts.so  <br />php_pdo_sqlsrv_7_ts.so  |7.0|예|

**Microsoft Drivers 3.2 for PHP for SQL Server:**  

Windows에서는 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|아니요|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|예|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|아니요|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|예|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br />php_pdo_sqlsrv_56_nts.dll|5.6|아니요|php5.dll|  
|php_sqlsrv_56_ts.dll<br />php_pdo_sqlsrv_56_ts.dll|5.6|예|php5ts.dll|  

**Microsoft Drivers 3.1 for PHP for SQL Server:**  

Windows에서는 다음 버전의 드라이버 포함 되어 있습니다.

|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br />php_pdo_sqlsrv_54_nts.dll|5.4|아니요|php5.dll|  
|php_sqlsrv_54_ts.dll<br />php_pdo_sqlsrv_54_ts.dll|5.4|예|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br />php_pdo_sqlsrv_55_nts.dll|5.5|아니요|php5.dll|  
|php_sqlsrv_55_ts.dll<br />php_pdo_sqlsrv_55_ts.dll|5.5|예|php5ts.dll|  

## <a name="see-also"></a>관련 항목:  
[시작 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)  
