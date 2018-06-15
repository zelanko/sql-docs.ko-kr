---
title: 작업 로깅 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logging activity
ms.assetid: a777b3d9-2262-4e82-bc82-b62ad60d0e55
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 146365e4a4a0a287992bb1873a104f62cc79fc0b
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35307892"
---
# <a name="logging-activity"></a>작업 로깅
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

기본적으로 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 에서 생성된 오류 및 경고는 기록되지 않습니다. 이 항목에서는 작업 로깅을 구성하는 방법을 설명합니다.  
  
## <a name="logging-activity-using-the-pdosqlsrv-driver"></a>PDO_SQLSRV 드라이버를 사용하여 작업 로깅  
PDO_SQLSRV 드라이버에 사용할 수 있는 유일한 구성은 php.ini 파일의 pdo_sqlsrv.log_severity 항목입니다.  
  
php.ini 파일의 끝에 다음을 추가합니다.  
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.log_severity = <number>  
```  
  
**log_severity** 는 다음 값 중 하나가 될 수 있습니다.  
  
|값|Description|  
|---------|---------------|  
|0|로깅이 사용되지 않습니다(아무 것도 정의되지 않은 경우 기본값).|  
|-1|오류, 경고 및 알림이 기록 된다는 것을 지정 합니다.|  
|1|오류가 기록 되도록 지정 합니다.|  
|2|경고 기록 되도록 지정 합니다.|  
|4|알림이 기록 된 것을 지정 합니다.|  
  
로깅 정보가 phperrors.log 파일에 추가 됩니다.  
  
PHP가 초기화에서 구성 파일을 읽고 데이터를 캐시에 저장합니다. 이러한 설정을 업데이트, 즉시 사용, 구성 파일에 기록하기 위한 API도 제공합니다. 이 API를 통해 PHP 초기화 후에도 응용 프로그램 스크립트에서 설정을 변경할 수 있습니다.  
  
## <a name="logging-activity-using-the-sqlsrv-driver"></a>SQLSRV 드라이버를 사용하여 작업 로깅  
로깅을 설정 하려면 사용할 수 있습니다는 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md) 함수나 있습니다 php.ini 파일을 변경할 수 있습니다. 초기화, 연결, 문 또는 오류 함수에서 작업을 기록할 수 있습니다. 또한 오류, 경고, 알림 또는 세 가지 모두를 기록할지 여부를 지정할 수도 있습니다.  
  
> [!NOTE]  
> php.ini 파일에서 로그 파일의 위치를 구성할 수 있습니다.  
  
### <a name="turning-logging-on"></a>로깅 설정  
사용 하 여 로깅을 설정할 수 있습니다는 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md) 함수에 대 한 값을 지정 하는 **LogSubsystems** 설정 합니다. 예를 들어 다음 코드 줄은 연결에서 작업을 기록하기 위해 드라이버를 구성합니다.  
  
`sqlsrv_configure("LogSubsystems", SQLSRV_LOG_SYSTEM_CONN);`  
  
다음 표는 **LogSubsystems** 설정에 대한 값으로 사용할 수 있는 상수를 설명합니다.  
  
|값(괄호 안의 정수)|Description|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL(-1)|모든 하위 시스템의 로깅을 설정합니다.|  
|SQLSRV_LOG_SYSTEM_OFF(0)|로깅을 해제합니다. 기본값입니다.|  
|SQLSRV_LOG_SYSTEM_INIT(1)|초기화 작업의 로깅을 설정합니다.|  
|SQLSRV_LOG_SYSTEM_CONN(2)|연결 작업의 로깅을 설정합니다.|  
|SQLSRV_LOG_SYSTEM_STMT(4)|문 작업의 로깅을 설정합니다.|  
|SQLSRV_LOG_SYSTEM_UTIL(8)|오류 함수 작업(예: handle_error 및 handle_warning)의 로깅을 설정합니다.|  
  
에 대 한 한 번에 둘 이상의 값을 설정할 수는 **LogSubsystems** 논리 OR 연산자 (|)를 사용 하 여 설정 합니다. 예를 들어 다음 코드 줄에서는 연결과 문에 대한 작업의 로깅을 설정합니다.  
  
`sqlsrv_configure("LogSubsystems", SQLSRV_LOG_SYSTEM_CONN | SQLSRV_LOG_SYSTEM_STMT);`  
  
에 정수 값을 지정 하 여 로깅에도 설정할 수는 **LogSubsystems** php.ini 파일에서 설정 합니다. 예를 들어, 다음 줄을 추가 `[sqlsrv]` php.ini 파일의 섹션 연결 작업의 로깅을 설정 합니다.  
  
`sqlsrv.LogSubsystems = 2`  
  
정수 값을 함께 추가하여 한 번에 둘 이상의 옵션을 지정할 수 있습니다. 예를 들어, 다음 줄을 추가 `[sqlsrv]` php.ini 파일의 섹션 연결 및 문 작업의 로깅을 설정 합니다.  
  
`sqlsrv.LogSubsystems = 6`  
  
### <a name="logging-errors-warnings-and-notices"></a>로깅 오류, 경고 및 알림  
로깅을 설정한 후 기록할 내용을 지정해야 합니다. 오류, 경고 및 알림 중 하나 이상을 기록할 수 있습니다. 예를 들어 다음 코드 줄은 경고만 기록 지정 합니다.  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> 에 대 한 기본 설정은 **LogSeverity** 은 **SQLSRV_LOG_SEVERITY_ERROR**합니다. 로깅이 설정되고 **LogSeverity** 에 대한 설정이 지정되지 않은 경우 오류만 기록됩니다.  
  
다음 표는 **LogSeverity** 설정에 대한 값으로 사용할 수 있는 상수를 설명합니다.  
  
|값(괄호 안의 정수)|Description|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL(-1)|오류, 경고 및 알림이 기록 된다는 것을 지정 합니다.|  
|SQLSRV_LOG_SEVERITY_ERROR(1)|오류가 기록 되도록 지정 합니다. 기본값입니다.|  
|SQLSRV_LOG_SEVERITY_WARNING(2)|경고 기록 되도록 지정 합니다.|  
|SQLSRV_LOG_SEVERITY_NOTICE(4)|알림이 기록 된 것을 지정 합니다.|  
  
에 대 한 한 번에 둘 이상의 값을 설정할 수는 **LogSeverity** 논리 OR 연산자 (|)를 사용 하 여 설정 합니다. 예를 들어 다음 코드 줄은 오류 및 경고가 기록된다는 것을 지정합니다.  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_ERROR | SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> 에 대 한 값을 지정 하는 **LogSeverity** 설정을 로깅을 설정 하지 않습니다. 에 대 한 값을 지정 하 여 로깅을 설정 해야 합니다는 **LogSubsystems** 설정, 다음에 대 한 값을 설정 하 여 기록 된 값의 심각도 지정 **LogSeverity**합니다.  
  
php.ini 파일에서 정수 값을 사용하여 **LogSeverity** 설정에 대한 설정을 지정할 수도 있습니다. 예를 들어 php.ini 파일의 `[sqlsrv]` 섹션에 다음 줄을 추가하면 경고에 대한 로깅만 사용하도록 설정됩니다.  
  
`sqlsrv.LogSeverity = 2`  
  
정수 값을 함께 추가하여 한 번에 둘 이상의 옵션을 지정할 수 있습니다. 예를 들어, 다음 줄을 추가 `[sqlsrv]` 로깅 오류 및 경고 php.ini 파일의 부분을 사용 합니다.  
  
`sqlsrv.LogSeverity = 3`  
  
## <a name="see-also"></a>관련 항목  
[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md)

[상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)

[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
  
