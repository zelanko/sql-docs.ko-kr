---
title: sqlsrv_configure | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_configure
apitype: NA
helpviewer_keywords:
- sqlsrv_configure
- API Reference, sqlsrv_configure
ms.assetid: 9393f975-a4ef-4c50-b4dd-14892fc55cc9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b98533dcc1589e07bc8ae37562bf6734077a78f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935800"
---
# <a name="sqlsrvconfigure"></a>sqlsrv_configure
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

오류 처리 및 로깅 옵션에 대한 설정을 변경합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_configure( string $setting, mixed $value )  
```  
  
#### <a name="parameters"></a>매개 변수  
*$setting*: 구성할 설정의 이름입니다. 설정 목록은 아래 표를 참조 하세요.  
  
*$value*: *$setting* 매개 변수에 지정된 설정에 적용할 값입니다. 이 매개 변수의 가능한 값은 지정된 설정에 따라 달라집니다. 다음 표에서는 가능한 조합을 나열합니다.  
  
|설정|$value 매개 변수의 가능한 값(괄호 안의 정수)|기본값|  
|-----------|------------------------------------------------------------------------------|-----------------|  
|ClientBufferMaxKBSize<sup>1</sup>|최대 PHP 메모리 제한의 음수가 아닌 숫자<br /><br />0과 음수는 허용되지 않습니다.|10240KB|  
|LogSeverity<sup>2</sup>|SQLSRV_LOG_SEVERITY_ALL(-1)<br /><br />SQLSRV_LOG_SEVERITY_ERROR(1)<br /><br />SQLSRV_LOG_SEVERITY_NOTICE(4)<br /><br />SQLSRV_LOG_SEVERITY_WARNING(2)|SQLSRV_LOG_SEVERITY_ERROR(1)|  
|LogSubsystems<sup>2</sup>|SQLSRV_LOG_SYSTEM_ALL(-1)<br /><br />SQLSRV_LOG_SYSTEM_CONN(2)<br /><br />SQLSRV_LOG_SYSTEM_INIT(1)<br /><br />SQLSRV_LOG_SYSTEM_OFF(0)<br /><br />SQLSRV_LOG_SYSTEM_STMT(4)<br /><br />SQLSRV_LOG_SYSTEM_UTIL(8)|SQLSRV_LOG_SYSTEM_OFF(0)|  
|WarningsReturnAsErrors<sup>3</sup>|**true**(1) 또는 **false**(0)|**true**(1)|  
  
## <a name="return-value"></a>반환 값  
**sqlsrv_configure**가 지원되지 않는 설정 또는 값을 사용하여 호출된 경우 함수가 **false**를 반환합니다. 그렇지 않으면 함수에서 **true**를 반환합니다.  
  
## <a name="remarks"></a>Remarks  
(1) 클라이언트 쪽 쿼리에 대한 자세한 내용은 [커서 유형&#40;SQLSRV 드라이버&#41;](../../connect/php/cursor-types-sqlsrv-driver.md)를 참조하세요.  
  
(2) 작업 로깅에 대한 자세한 내용은 [작업 로깅](../../connect/php/logging-activity.md)을 참조하세요.  
  
(3) 오류 및 경고 처리 구성에 대한 자세한 내용은 [방법: SQLSRV 드라이버를 사용하여 오류 및 경고 처리 구성](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[Microsoft Drivers for PHP for SQL Server 프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md) 
  
