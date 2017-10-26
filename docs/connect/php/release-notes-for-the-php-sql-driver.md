---
title: "PHP SQL 드라이버에 대 한 릴리스 정보 | Microsoft Docs"
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
- what's new in version 1.1
ms.assetid: 91cca3d2-ba99-4a6d-b0de-beb9699cb3f8
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2c63079bda91844995540aade94bac397be6b94c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="release-notes-for-the-php-sql-driver"></a>PHP SQL 드라이버에 대한 릴리스 정보
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 각 버전에 추가 된 기능을 설명는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]합니다.  

## <a name="whats-new-in-version-43"></a>버전 4.3의에서 새로운 기능

- 7.1 PHP에 대 한 지원
- Mac OS 시에라 및 Mac OS El Capitan에 대 한 지원
- Ubuntu 15.10, 및 Debian 8에 대 한 지원
- Ubuntu 15.04 지원 하지 않으므로
- 투명 네트워크 IP 확인을 통해 항상 가용성 그룹에 대 한 지원. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요. 
- 제한이 sql_variant 데이터 형식에 대 한 지원이 추가 되었습니다.
- Windows에서 유휴 연결 복원 력 지원 합니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.
- 연결 풀링 Linux와 macOS에 대 한 지원입니다. 자세한 내용은 참조 [연결 풀링](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)합니다.
- Azure Active Directory 인증 ActiveDirectoryPassword 및 SqlPassword 지원 합니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.
  
## <a name="whats-new-in-version-40"></a>버전 4.0의에서 새로운 기능 

- PHP 7.0에 대 한 지원  
- 완전 한 64 비트 지원
- Ubuntu 15.04, 16.04, Ubuntu 및 RedHat 7에 대 한 지원

## <a name="whats-new-in-version-32"></a>버전 3.2의 새로운 기능 

- PHP 5.6을 지원합니다.   
- 이전 PHP 버전 5.5 및 5.4에 대한 최신 업데이트를 포함합니다.   
- Microsoft ODBC Driver 11 for SQL Server 필요  
  
## <a name="whats-new-in-version-31"></a>버전 3.1의 새로운 기능
 
- PHP 5.5를 지원합니다.  
- Microsoft ODBC Driver 11 for SQL Server 필요합니다. SQL Native Client에 필요한 이전 버전입니다.  
  
## <a name="whats-new-in-version-30"></a>버전 3.0의 새로운 기능  

- PHP 5.4를 지원합니다.  PHP 5.2는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 3에서 지원되지 않습니다.  
- AttachDBFileName 연결 옵션이 추가되었습니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
- LocalDB 지원이 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]에 추가되었습니다. 자세한 내용은 [PHP Driver for SQL Server Support for LocalDB](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)을 참조하세요.
- AttachDBFileName 연결 옵션이 추가되었습니다. 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
- 고가용성, 재해 복구 기능을 지원합니다. 자세한 내용은 [PHP Driver for SQL Server Support for High Availability, Disaster Recovery](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)(PHP Driver for SQL Server의 고가용성, 재해 복구 지원)를 참조하세요.
- 클라이언트 쪽 커서(메모리 내 결과 집합 캐싱)를 지원합니다. 자세한 내용은 참조 [커서 유형 &#40; SQLSRV 드라이버 &#41; ](../../connect/php/cursor-types-sqlsrv-driver.md) 및 [커서 유형 &#40; PDO_SQLSRV 드라이버 &#41; ](../../connect/php/cursor-types-pdo-sqlsrv-driver.md).
- PDO::ATTR_EMULATE_PREPARES 특성이 추가되었습니다. 자세한 내용은 참조 [pdo:: prepare](../../connect/php/pdo-prepare.md)합니다.  
  
## <a name="whats-new-in-version-20"></a>버전 2.0의 새로운 기능  
버전 2.0에서는 PDO_SQLSRV 드라이버에 대한 지원이 추가되었습니다. 자세한 내용은 [PDO_SQLSRV 드라이버 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[PHP SQL 드라이버 개요](../../connect/php/overview-of-the-php-sql-driver.md)
  

