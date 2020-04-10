---
title: Microsoft Drivers for PHP for SQL Server 개요 | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 66559249-34c0-409d-b919-9b5bf0c4c9ec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c8f5cbf011165b41b353a37d8973031f55c2db6
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922820"
---
# <a name="overview-of-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 개요

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]는 Azure SQL Database를 비롯한 SQL Server 2005 이상 버전에 대한 데이터 액세스를 제공하는 PHP 확장입니다. SQL Server 2005부터 모든 SQL Server 버전(Express 포함)의 데이터에 액세스하기 위해 확장에서는 SQLSRV 드라이버가 있는 절차 인터페이스와 PDO_SQLSRV 드라이버가 있는 개체 지향 인터페이스를 제공합니다. 3\.1 이상 버전의 드라이버에 대한 지원은 SQL Server 2008부터 시작됩니다. [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] API에는 Windows 인증, 트랜잭션, 매개 변수 바인딩, 스트리밍, 메타데이터 액세스 및 오류 처리에 대한 지원이 포함됩니다.  
  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]를 사용하려면 PHP가 실행 중인 동일 컴퓨터에 SQL Server Native Client 또는 Microsoft ODBC Driver가 설치되어 있어야 합니다.  자세한 내용은 [Microsoft Drivers for PHP for SQL Server에 대한 시스템 요구 사항](../../connect/php/system-requirements-for-the-php-sql-driver.md)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|---------|---------------|  
| ![Download-DownArrow-Circled](../../ssms/media/download-icon.png)[SQL Server용 PHP 드라이버를 다운로드하려면](download-drivers-php-sql-server.md) | Microsoft Drivers for PHP for SQL Server를 다운로드하는 링크입니다. |
|[Microsoft Drivers for PHP for SQL Server 릴리스 정보](../../connect/php/release-notes-php-sql-driver.md)|버전 4.0, 3.2, 3.1, 3.0 및 2.0에 추가된 기능을 나열합니다.|  
|[Microsoft Drivers for PHP for SQL Server에 대한 지원 리소스](../../connect/php/support-resources-for-the-php-sql-driver.md)|[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]를 사용하는 애플리케이션을 개발할 때 도움이 될 수 있는 리소스에 대한 링크를 제공합니다.|  
|[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)|이 설명서의 코드 예제를 실행할 때 도움이 될 수 있는 정보를 제공합니다.|  
| &nbsp; | &nbsp; |

## <a name="reference"></a>참조

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 드라이버 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)  
[상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

## <a name="see-also"></a>참고 항목

[Microsoft Drivers for PHP for SQL Server 시작](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 프로그래밍 가이드 | Microsoft Docs](../../connect/php/programming-guide-for-php-sql-driver.md)

[예제 애플리케이션&#40;SQLSRV 드라이버&#41;](../../connect/php/example-application-sqlsrv-driver.md)
