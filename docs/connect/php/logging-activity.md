---
title: "작업 로깅 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logging activity
ms.assetid: a777b3d9-2262-4e82-bc82-b62ad60d0e55
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d748bac061fdd4b76b1df0b9a6cf0a8101f21092
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

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
  
|값|설명|  
|---------|---------------|  
|0|로깅이 사용되지 않습니다(아무 것도 정의되지 않은 경우 기본값).|  
|-1|오류, 경고 및 알림이 기록된다는 것을 지정합니다.|  
|1|오류가 기록된다는 것을 지정합니다.|  
|2|경고가 기록된다는 것을 지정합니다.|  
|4|알림이 기록된다는 것을 지정합니다.|  
  
로깅 정보가 phperrors.log 파일에 추가됩니다.  
  
PHP가 초기화에서 구성 파일을 읽고 데이터를 캐시에 저장합니다. 이러한 설정을 업데이트, 즉시 사용, 구성 파일에 기록하기 위한 API도 제공합니다. 이 API를 통해 PHP 초기화 후에도 응용 프로그램 스크립트에서 설정을 변경할 수 있습니다.  
  
## <a name="logging-activity-using-the-sqlsrv-driver"></a>SQLSRV 드라이버를 사용하여 작업 로깅  
로깅을 설정하려면 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md) 함수를 사용하거나 php.ini 파일을 변경하면 됩니다. 초기화, 연결, 문 또는 오류 함수에서 작업을 기록할 수 있습니다. 또한 오류, 경고, 알림 또는 세 가지 모두를 기록할지 여부를 지정할 수도 있습니다.  
  
> [!NOTE]  
> php.ini 파일에서 로그 파일의 위치를 구성할 수 있습니다.  
  
### <a name="turning-logging-on"></a>로깅 설정  
[sqlsrv_configure](../../connect/php/sqlsrv-configure.md) 함수를 사용하여 로깅을 설정하면 **LogSubsystems** 설정에 대한 값을 지정할 수 있습니다. 예를 들어 다음 코드 줄은 연결에서 작업을 기록하기 위해 드라이버를 구성합니다.  
  
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
  
php.ini 파일에서 **LogSubsystems** 설정에 대한 정수 값을 지정하여 로깅을 설정할 수도 있습니다. 예를 들어 php.ini 파일의 `[sqlsrv]` 섹션에 다음 줄을 추가하면 연결 작업의 로깅이 설정됩니다.  
  
`sqlsrv.LogSubsystems = 2`  
  
정수 값을 함께 추가하여 한 번에 둘 이상의 옵션을 지정할 수 있습니다. 예를 들어 다음 줄을 php.ini 파일의 `[sqlsrv]` 섹션에 추가하면 연결 및 문 작업의 로깅이 설정됩니다.  
  
`sqlsrv.LogSubsystems = 6`  
  
### <a name="logging-errors-warnings-and-notices"></a>로깅 오류, 경고 및 알림  
로깅을 설정한 후 기록할 내용을 지정해야 합니다. 오류, 경고 및 알림 중 하나 이상을 기록할 수 있습니다. 예를 들어 다음 코드 줄은 경고만 기록된다는 것을 지정합니다.  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> 에 대 한 기본 설정은 **LogSeverity** 은 **SQLSRV_LOG_SEVERITY_ERROR**합니다. 로깅이 설정되고 **LogSeverity** 에 대한 설정이 지정되지 않은 경우 오류만 기록됩니다.  
  
다음 표는 **LogSeverity** 설정에 대한 값으로 사용할 수 있는 상수를 설명합니다.  
  
|값(괄호 안의 정수)|Description|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL(-1)|오류, 경고 및 알림이 기록된다는 것을 지정합니다.|  
|SQLSRV_LOG_SEVERITY_ERROR(1)|오류가 기록된다는 것을 지정합니다. 기본값입니다.|  
|SQLSRV_LOG_SEVERITY_WARNING(2)|경고가 기록된다는 것을 지정합니다.|  
|SQLSRV_LOG_SEVERITY_NOTICE(4)|알림이 기록된다는 것을 지정합니다.|  
  
에 대 한 한 번에 둘 이상의 값을 설정할 수는 **LogSeverity** 논리 OR 연산자 (|)를 사용 하 여 설정 합니다. 예를 들어 다음 코드 줄은 오류 및 경고가 기록된다는 것을 지정합니다.  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_ERROR | SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> **LogSeverity** 설정에 대한 값을 지정하면 로깅을 설정하지 않습니다. **LogSubsystems** 설정에 대한 값을 지정하여 로깅을 설정한 다음 **LogSeverity**에 대한 값을 설정하여 기록된 값의 심각도를 지정해야 합니다.  
  
php.ini 파일에서 정수 값을 사용하여 **LogSeverity** 설정에 대한 설정을 지정할 수도 있습니다. 예를 들어 php.ini 파일의 `[sqlsrv]` 섹션에 다음 줄을 추가하면 경고에 대한 로깅만 사용하도록 설정됩니다.  
  
`sqlsrv.LogSeverity = 2`  
  
정수 값을 함께 추가하여 한 번에 둘 이상의 옵션을 지정할 수 있습니다. 예를 들어 php.ini 파일의 `[sqlsrv]` 섹션에 다음 줄을 추가하면 오류 및 경고에 대한 로깅을 사용하도록 설정됩니다.  
  
`sqlsrv.LogSeverity = 3`  
  
## <a name="see-also"></a>관련 항목:  
[PHP SQL 드라이버 프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md)
[상수 &#40; Microsoft Drivers for PHP for SQL server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  
[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
  

