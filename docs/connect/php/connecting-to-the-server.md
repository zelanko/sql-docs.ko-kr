---
title: 서버에 연결
description: Microsoft Drivers for PHP for SQL Server를 사용하여 데이터베이스에 연결하는 다양한 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c251a239-e0bd-4f45-9207-b76651072dd0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a2ec027a72bd96b567b08639568b6ead8e5dc64
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87410979"
---
# <a name="connecting-to-the-server"></a>서버에 연결
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 섹션의 항목에서는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하기 위한 옵션 및 절차를 설명합니다.  

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]는 Windows 인증 또는 SQL Server 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 수 있습니다. 기본적으로 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 Windows 인증을 사용하여 서버에 연결합니다.  

## <a name="in-this-section"></a>섹션 내용  

|항목|설명|  
|---------|---------------|  
|[방법: Windows 인증을 사용하여 연결](../../connect/php/how-to-connect-using-windows-authentication.md)|Windows 인증을 사용하여 연결을 설정하는 방법을 설명합니다.|  
|[방법: SQL Server 인증을 사용하여 연결](../../connect/php/how-to-connect-using-sql-server-authentication.md)|SQL Server 인증을 사용하여 연결을 설정하는 방법을 설명합니다.|  
|[방법: Azure Active Directory 인증을 사용하여 연결](../../connect/php/azure-active-directory.md)|인증 모드를 설정하고 Azure Active Directory ID를 사용하여 연결하는 방법을 설명합니다.|  
|[방법: 지정된 포트에서 연결](../../connect/php/how-to-connect-on-a-specified-port.md)|특정 포트에서 서버에 연결하는 방법을 설명합니다.|  
|[연결 풀링](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)|드라이버의 연결 풀링에 대한 정보를 제공합니다.|  
|[방법: MARS(Multiple Active Resultsets)를 사용하지 않도록 설정](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)|연결할 때 MARS 기능을 사용하지 않도록 설정하는 방법을 설명합니다.|  
|[연결 옵션](../../connect/php/connection-options.md)|연결 특성을 포함하는 결합형 배열에서 허용되는 옵션을 나열합니다.|  
|[LocalDB 지원](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]에 추가된 LocalDB 기능에 대한 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 지원을 설명합니다.|  
|[고가용성, 재해 복구 지원](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 추가된 고가용성의 재해 복구 기능을 활용하도록 애플리케이션을 구성할 수 있는 방법을 설명합니다.|  
|[Microsoft Azure SQL Database에 연결](../../connect/php/connecting-to-microsoft-azure-sql-database.md)|Azure SQL Database에 연결하는 방법에 대해 설명합니다.|  
|[연결 복원력](../../connect/php/connection-resiliency.md)|끊어진 연결을 다시 설정하는 연결 복원력 기능에 대해 설명합니다.|  

## <a name="see-also"></a>참고 항목  
[Microsoft Drivers for PHP for SQL Server 프로그래밍 가이드 | Microsoft Docs](../../connect/php/programming-guide-for-php-sql-driver.md)

[예제 애플리케이션&#40;SQLSRV 드라이버&#41;](../../connect/php/example-application-sqlsrv-driver.md)  
