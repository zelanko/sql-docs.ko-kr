---
title: Microsoft Drivers for PHP for SQL Server에 대한 IIS 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- configuring, Internet Information Services
ms.assetid: d2dc75d3-9bf7-481c-85f2-8b6310b21461
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b550fb7300ffdb2d37ae4407aaeeb43a49c89f4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654781"
---
# <a name="configuring-iis-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server에 대한 IIS 구성
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 IIS에서 PHP 응용 프로그램을 호스트하도록 구성하는 방법과 관련된 [IIS(인터넷 정보 서비스) 웹 사이트](https://www.iis.net/)의 리소스에 대한 링크를 제공합니다. 여기에 나열된 리소스는 IIS에서 FASTCGI 사용과 관련됩니다. FastCGI는 응용 프로그램 프레임워크의 CGI(Common Gateway Interface) 실행 파일이 웹 서버와 인터페이스하는 데 사용되는 표준 프로토콜입니다. FastCGI는 여러 요청에 대해 CGI 프로세스를 다시 사용한다는 점에서 표준 CGI 프로토콜과 다릅니다.  
  
## <a name="tutorials"></a>자습서  
다음은 PHP에 대해 FastCGI를 설정하는 방법과 IIS 6.0 및 IIS 7.0에서 PHP 응용 프로그램을 호스트하는 방법이 있는 자습서에 대한 링크입니다.  
  
-   [PHP에서 FastCGI](https://docs.microsoft.com/iis/web-hosting/web-server-for-shared-hosting/fastcgi-with-php)  
-   [FastCGI를 사용하여 IIS 7.0에서 PHP 응용 프로그램 호스트](https://docs.microsoft.com/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis)  
-   [FastCGI를 사용하여 IIS 6.0에서 PHP 응용 프로그램 호스트](https://docs.microsoft.com/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis-60)  
-   [IIS 6.0에 대해 FastCGI 확장 구성](https://docs.microsoft.com/iis/application-frameworks/install-and-configure-php-on-iis/configuring-the-fastcgi-extension-for-iis-60)  
  
## <a name="video-presentations"></a>비디오 프레젠테이션  
다음은 PHP에 대해 FastCGI를 설정하는 방법과 IIS 7.0 기능을 사용하여 PHP 응용 프로그램을 호스트하는 방법을 보여 주는 비디오 프레젠테이션에 대한 링크입니다.  
  
-   [PHP에 대해 FastCGI 설정](https://docs.microsoft.com/iis/application-frameworks/running-php-applications-on-iis/set-up-fastcgi-for-php)  
-   [Microsoft 인터넷 정보 서비스 7에서 PHP 활용](https://docs.microsoft.com/iis/application-frameworks/running-php-applications-on-iis/mix08-partying-with-php-on-microsoft-internet-information-services-7-and-above)  
  
## <a name="support-resources"></a>지원 리소스  
다음 포럼에서는 IIS에서 FastCGI에 대한 커뮤니티 지원을 제공합니다.  
  
-   [FastCGI 처리기](https://forums.iis.net/1103.aspx)  
-   [IIS 7 - FastCGI 모듈](https://forums.iis.net/1104.aspx)  
  
## <a name="see-also"></a>참고 항목  
[시작 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
  
