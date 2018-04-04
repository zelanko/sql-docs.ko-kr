---
title: 서버에 연결 | Microsoft Docs
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
ms.assetid: c251a239-e0bd-4f45-9207-b76651072dd0
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 818a71b8e0bc60168602e7fc0228c21319d08a21
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="connecting-to-the-server"></a>서버에 연결
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 섹션의 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 를 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]에 연결하기 위한 옵션 및 절차를 설명합니다.  

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 Windows 인증 또는 SQL Server 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에 연결할 수 있습니다. 기본적으로 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 Windows 인증을 사용하여 서버에 연결합니다.  

## <a name="in-this-section"></a>섹션 내용  

|항목|Description|  
|---------|---------------|  
|[방법: Windows 인증을 사용하여 연결](../../connect/php/how-to-connect-using-windows-authentication.md)|Windows 인증을 사용하여 연결을 설정하는 방법을 설명합니다.|  
|[방법: SQL Server 인증을 사용하여 연결](../../connect/php/how-to-connect-using-sql-server-authentication.md)|SQL Server 인증을 사용하여 연결을 설정하는 방법을 설명합니다.|  
|[방법: Azure Active Directory 인증을 사용하여 연결](../../connect/php/azure-active-directory.md)|인증 모드를 설정 하 고 Azure Active Directory id를 사용 하 여 연결 하는 방법에 설명 합니다.|  
|[방법: 지정된 포트에서 연결](../../connect/php/how-to-connect-on-a-specified-port.md)|특정 포트에서 서버에 연결하는 방법을 설명합니다.|  
|[연결 풀링](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)|드라이버의 연결 풀링에 대한 정보를 제공합니다.|  
|[방법: MARS(Multiple Active Result Set)를 사용하지 않도록 설정](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)|연결할 때 MARS 기능을 사용하지 않도록 설정하는 방법을 설명합니다.|  
|[연결 옵션](../../connect/php/connection-options.md)|연결 특성을 포함하는 결합형 배열에서 허용되는 옵션을 나열합니다.|  
|[LocalDB에 대 한 지원](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 에 추가된 LocalDB 기능에 대한 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]지원을 설명합니다.|  
|[고가용성, 재해 복구에 대 한 지원](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)|고가용성, 재해 복구에 추가 된 기능을 활용 하도록 응용 프로그램을 구성할 수 있는 방법을 설명 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]합니다.|  
|[Microsoft Azure SQL Database에 연결](../../connect/php/connecting-to-microsoft-azure-sql-database.md)|Azure SQL 데이터베이스에 연결 하는 방법을 설명 합니다.|  
|[연결 복원력](../../connect/php/connection-resiliency.md)|끊어진된 연결을 다시 설정 하는 연결 복원 기능을 설명 합니다.|  

## <a name="see-also"></a>관련 항목:  
[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md)

[예제 응용 프로그램&#40;SQLSRV 드라이버&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
