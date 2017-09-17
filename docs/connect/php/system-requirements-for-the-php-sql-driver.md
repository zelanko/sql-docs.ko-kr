---
title: "PHP SQL 드라이버 시스템 요구 사항 | Microsoft Docs"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- requirements
ms.assetid: 5db4b75f-c605-4785-9560-399a533c0fc9
caps.latest.revision: 93
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba7e8cde4b8d3b77effca06b00303984223551f5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="system-requirements-for-the-php-sql-driver"></a>PHP SQL 드라이버 시스템 요구 사항
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

데이터에는 SQL Server 또는 Azure SQL 데이터베이스를 사용 하 여 액세스할 수는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], 다음 구성 요소가 컴퓨터에 설치 되어 있어야 합니다.  
  
-   PHP가 필요 합니다. 다운로드 하 고 안정적인 최신 이진 파일을 설치 하는 방법에 대 한 정보를 참조 하십시오. [http://php.net](http://go.microsoft.com/fwlink/?LinkId=101876)합니다.  Microsoft Drivers for PHP for SQL Server는 다음 버전 필요합니다.
  
|Microsoft Drivers for PHP for SQL Server 버전|지원되는 PHP 버전|  
|----------------------------------------------------|--------------------------|  
|4.3|PHP 7.0 및 PHP 7.1| 
|4.0|PHP 7.0|  
|3.2|PHP 5.6.4+ 또는<br /><br />PHP 5.5.16+ 또는<br /><br />PHP 5.4.32|  
|3.1|PHP 5.5.16+ 또는<br /><br />PHP 5.4.32|  
|3.0|PHP 5.4.32 또는<br /><br />PHP 5.3.0|  
|2.0|PHP 5.3.0 또는<br /><br />PHP 5.2.4 또는<br /><br />PHP 5.2.13|  
  
-   드라이버 파일의 버전은 PHP 확장 디렉터리에 있어야 합니다. 다른 드라이버 파일에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 드라이버 버전을 참조하세요. PHP 런타임에 대해 드라이버를 구성하는 방법에 대한 자세한 내용은 [PHP SQL 드라이버 로드](../../connect/php/loading-the-php-sql-driver.md)  를 참조하세요. 드라이버를 다운로드하려면 [Microsoft Drivers for PHP for SQL Server](http://www.microsoft.com/download/details.aspx?id=20098)를 참조하세요.  
  
-   웹 서버가 필요합니다. 웹 서버는 PHP를 실행하도록 구성되어야 합니다. 인터넷 정보 서비스 (IIS) 6.0와 PHP 응용 프로그램 호스팅에 대 한 정보를 참조 하십시오. [IIS 6.0에서 PHP 응용 프로그램 호스트를 사용 하 여 FastCGI](http://go.microsoft.com/fwlink/?LinkId=117131)합니다. IIS 7.0에서 PHP 응용 프로그램을 호스트하는 방법에 대한 자세한 내용은 [FastCGI를 사용하여 IIS 7.0에서 PHP 응용 프로그램 호스트](http://go.microsoft.com/fwlink/?LinkId=117132)를 참조하세요.  
  
    [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 가 FastCGI를 사용하는 IIS 6 및 IIS 7에서 테스트되었습니다.  
  
    > [!NOTE]  
    > Microsoft는 IIS에 대해서만 지원합니다.  
  
-   올바른 버전의 Microsoft ODBC Driver for SQL Server 또는 SQL Server Native Client PHP가 실행 중인 컴퓨터에 필요 합니다.  64 비트 운영 체제를 사용 하는 경우 ODBC 64 비트 설치 관리자는 32 비트 및 64 비트 ODBC 드라이버를 설치 합니다. 32 비트 운영 체제를 사용 하는 경우 x86 ODBC를 사용 하 여 설치 합니다.

|Microsoft Drivers for PHP for SQL Server 버전|Microsoft ODBC Driver for SQL Server 또는 SQL Server Native Client의 버전|  
|----------------------------------------------------|--------------------------|
|4.3|Microsoft ODBC Driver 11 for SQL Server 또는 Microsoft ODBC Driver 13.1 for SQL Server. Microsoft ODBC Driver를 다운로드 하려면 참조는 [SQL Server 페이지에 대 한 Microsoft ODBC Driver 11](http://www.microsoft.com/download/details.aspx?id=36434) 또는 [SQL Server 페이지에 대 한 Microsoft ODBC Driver 13.1](https://www.microsoft.com/en-us/download/details.aspx?id=53339)|    
|4.0|Microsoft ODBC Driver 11 for SQL Server 또는 Microsoft ODBC Driver 13 for SQL Server. Microsoft ODBC Driver를 다운로드 하려면 참조는 [SQL Server 페이지에 대 한 Microsoft ODBC Driver 11](http://www.microsoft.com/download/details.aspx?id=36434) 또는 [SQL Server 페이지에 대 한 Microsoft ODBC Driver 13](https://www.microsoft.com/download/details.aspx?id=50420)|  
|3.2 또는 <br><br> 3.1|Microsoft ODBC Driver 11 for SQL Server입니다. Microsoft ODBC Driver를 다운로드 하려면 참조는 [SQL Server 페이지에 대 한 Microsoft ODBC Driver 11](http://www.microsoft.com/download/details.aspx?id=36434)|   
|3.0|Microsoft [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Native Client. Microsoft를 다운로드할 수 있습니다 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 에서 Native Client는 [SQL Server 2012 기능 팩 페이지](http://go.microsoft.com/fwlink/?LinkID=236805)| 
|2.0|Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro_md.md)] Native Client:<br /><br />[X86 패키지 다운로드](http://go.microsoft.com/fwlink/?LinkID=188400&clcid=0x409) 32 비트 운영 체제에 대 한 <br /><br />[X64 패키지 다운로드](http://go.microsoft.com/fwlink/?LinkID=188401&clcid=0x409) 64 비트 운영 체제에 대 한|  

  
SQLSRV 드라이버를 사용 하는 경우 [sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md) 의 버전에 대 한 정보를 반환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Native Client 또는 Microsoft ODBC Driver for SQL Server에서 사용 되 고는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다. PDO_SQLSRV 드라이버를 사용 하는 경우 사용할 수 있습니다 [pdo:: getattribute](../../connect/php/pdo-getattribute.md) 버전을 검색 합니다.  



## <a name="database-versions"></a>데이터베이스 버전
-   Azure SQL 데이터베이스가 지원 됩니다. 자세한 내용은 참조 [Microsoft Azure SQL 데이터베이스에 연결](../../connect/php/connecting-to-microsoft-azure-sql-database.md)합니다. 

- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]버전 4.3 지원 SQL Server 2008 R2 이상
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]SQL Server 2008 이상 버전 4.0 지원
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]SQL Server 2008 이상 버전 3.1 지원
- [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]SQL Server 2005 이상 버전 2.0과 3.0 지원


## <a name="driver-versions"></a>드라이버 버전  
이 섹션의 각 버전에 포함 된 드라이버를 나열는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다.  
  
설치 지침을 따라 PHP 런타임에 사용할 드라이버를 구성 하려면 [PHP SQL 드라이버 로드](../../connect/php/loading-the-php-sql-driver.md)합니다.  
  
**Microsoft Drivers for PHP for SQL Server 4.3:**  

Windows에서 4.3에 대해 다음 버전의 드라이버 설치 됩니다.
  
|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br /><br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|아니요|32 비트 php7.dll| 
|php_sqlsrv_7_ts_x86.dll<br /><br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|예|32 비트 php7ts.dll| 
|php_sqlsrv_7_nts_x64.dll<br /><br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|아니요|64 비트 php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br /><br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|예|64 비트 php7ts.dll| 
|php_sqlsrv_71_nts_x86.dll<br /><br />php_pdo_sqlsrv_71_nts_x86.dll|7.1|아니요|32 비트 php7.dll|  
|php_sqlsrv_71_ts_x86.dll<br /><br />php_pdo_sqlsrv_71_ts_x86.dll|7.1|예|32 비트 php7ts.dll|  
|php_sqlsrv_71_nts_x64.dll<br /><br />php_pdo_sqlsrv_71_nts_x64.dll|7.1|아니요|64 비트 php7.dll|  
|php_sqlsrv_71_ts_x64.dll<br /><br />php_pdo_sqlsrv_71_ts_x64.dll|7.1|예|64 비트 php7ts.dll|   
  
**Microsoft Drivers for PHP for SQL Server 4.0:**  

Windows에서는 4.0에 대 한 다음 버전의 드라이버 설치 됩니다.
  
|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_7_nts_x86.dll<br /><br />php_pdo_sqlsrv_7_nts_x86.dll|7.0|아니요|32 비트 php7.dll|  
|php_sqlsrv_7_ts_x86.dll<br /><br />php_pdo_sqlsrv_7_ts_x86.dll|7.0|예|32 비트 php7ts.dll|  
|php_sqlsrv_7_nts_x64.dll<br /><br />php_pdo_sqlsrv_7_nts_x64.dll|7.0|아니요|64 비트 php7.dll|  
|php_sqlsrv_7_ts_x64.dll<br /><br />php_pdo_sqlsrv_7_ts_x64.dll|7.0|예|64 비트 php7ts.dll|   
  
지원 되는 Linux 버전에서 해당 버전을 sqlsrv 및/또는 pdo_sqlsrv PHP의 PECL 패키지 시스템을 사용 하 여 설치할 수 있습니다. 
  
**Microsoft Drivers 3.2 for PHP for SQL Server는 다음 버전의 드라이버를 설치합니다.**  
  
|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|아니요|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|예|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br /><br />php_pdo_sqlsrv_55_nts.dll|5.5|아니요|php5.dll|  
|php_sqlsrv_55_ts.dll<br /><br />php_pdo_sqlsrv_55_ts.dll|5.5|예|php5ts.dll|  
|php_sqlsrv_56_nts.dll<br /><br />php_pdo_sqlsrv_56_nts.dll|5.6|아니요|php5.dll|  
|php_sqlsrv_56_ts.dll<br /><br />php_pdo_sqlsrv_56_ts.dll|5.6|예|php5ts.dll|  
  
**Microsoft Drivers 3.1 for PHP for SQL Server는 다음 버전의 드라이버를 설치합니다.**  
  
|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|아니요|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|예|php5ts.dll|  
|php_sqlsrv_55_nts.dll<br /><br />php_pdo_sqlsrv_55_nts.dll|5.5|아니요|php5.dll|  
|php_sqlsrv_55_ts.dll<br /><br />php_pdo_sqlsrv_55_ts.dll|5.5|예|php5ts.dll|  
  
**Microsoft Drivers 3.0 for PHP for SQL Server는 다음 버전의 드라이버를 설치합니다.**  
  
|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_53_nts.dll<br /><br />php_pdo_sqlsrv_53_nts.dll|5.3|아니요|php5.dll|  
|php_sqlsrv_53_ts.dll<br /><br />php_pdo_sqlsrv_53_ts.dll|5.3|예|php5ts.dll|  
|php_sqlsrv_54_nts.dll<br /><br />php_pdo_sqlsrv_54_nts.dll|5.4|아니요|php5.dll|  
|php_sqlsrv_54_ts.dll<br /><br />php_pdo_sqlsrv_54_ts.dll|5.4|예|php5ts.dll|  
  
**Microsoft Drivers 2.0 for PHP for SQL Server는 다음 버전의 드라이버를 설치합니다.**  
  
|드라이버 파일|PHP 버전|스레드로부터 안전?|함께 사용되는 PHP .dll|  
|---------------|---------------|----------------|---------------------|  
|php_sqlsrv_53_nts_vc6.dll<br /><br />php_pdo_sqlsrv_53_nts_vc6.dll|5.3|아니요|php5.dll|  
|php_sqlsrv_53_nts_vc9.dll<br /><br />php_pdo_sqlsrv_53_nts_vc9.dll|5.3|아니요|php5.dll|  
|php_sqlsrv_53_ts_vc6.dll<br /><br />php_pdo_sqlsrv_53_ts_vc6.dll|5.3|예|php5ts.dll|  
|php_sqlsrv_53_ts_vc9.dll<br /><br />php_pdo_sqlsrv_53_ts_vc9.dll|5.3|예|php5ts.dll|  
|php_sqlsrv_52_nts_vc6.dll<br /><br />php_pdo_sqlsrv_52_nts_vc6.dll|5.2|아니요|php5.dll|  
|php_sqlsrv_52_ts_vc6.dll<br /><br />php_pdo_sqlsrv_52_ts_vc6.dll|5.2|예|php5ts.dll|  
  
드라이버 파일 이름에 "vc9"가 포함된 경우 Visual C++ 9.0으로 컴파일된 PHP 버전을 사용해야 합니다.  
## <a name="operating-systems"></a>운영 체제 
버전의 드라이버에 대 한 지원 되는 운영 체제는 다음과 같습니다.

-   4.3:
    -   Windows Server 2012  
    -   Windows Server 2012 R2
    -   Windows Server 2016 
    -   Windows 8  
    -   Windows 8.1   
    -   Windows 10
    -   Ubuntu 15.10 (64 비트)
    -   Ubuntu 16.04 (64 비트)
    -   Debian 8 (64 비트)
    -   Red Hat Enterprise Linux 7 (64 비트)
    -   Mac OS 시에라 (64 비트)
    -   Mac OS El Capitan (64 비트)
    
-   4.0:  
    -   Windows Server 2008 SP2
    -   Windows Server 2008 R2 SP1  
    -   Windows Server 2012  
    -   Windows Server 2012 R2  
    -   Windows Vista SP2  
    -   Windows 7 SP1  
    -   Windows 8  
    -   Windows 8.1   
    -   Windows 10 
    -   Ubuntu 15.04 (64 비트)
    -   Ubuntu 16.04 (64 비트)
    -   Red Hat Enterprise Linux 7 (64 비트)

 
-   3.2 및 3.1의 경우:  
    -   Windows Server 2008 R2 SP1  
    -   Windows Vista SP2  
    -   Windows Server 2008 SP2  
    -   Windows 7 SP1  
    -   Windows Server 2012  
    -   Windows Server 2012 R2  
    -   Windows 8  
    -   Windows 8.1  
  
  
-   3.0:  
    -   Windows Server 2008 R2 SP1  
    -   Windows Vista SP2  
    -   Windows Server 2008 SP2  
    -   Windows 7 SP1  


-   2.0:
    -   [!INCLUDE[winxpsvr](../../includes/winxpsvr_md.md)] 서비스 팩 1  
    -   Windows XP 서비스 팩 3  
    -   Windows Vista 서비스 팩 1 이상  
    -   Windows Server 2008  
    -   Windows Server 2008 R2  
    -   Windows 7  
  
## <a name="see-also"></a>참고 항목  
[PHP SQL 드라이버 시작](../../connect/php/getting-started-with-the-php-sql-driver.md)
[PHP SQL 드라이버 프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
  

