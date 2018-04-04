---
title: sqlsrv_configure | Microsoft Docs
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
apiname:
- sqlsrv_configure
apitype: NA
helpviewer_keywords:
- sqlsrv_configure
- API Reference, sqlsrv_configure
ms.assetid: 9393f975-a4ef-4c50-b4dd-14892fc55cc9
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea82fe41ac7a95fbdf1907709a34ad57f8a82495
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="sqlsrvconfigure"></a>sqlsrv_configure
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

오류 처리 및 로깅 옵션에 대한 설정을 변경합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_configure( string $setting, mixed $value )  
```  
  
#### <a name="parameters"></a>매개 변수  
*$setting*: 구성할 설정의 이름입니다. 설정 목록은 아래 표를 참조 하십시오.  
  
*$value*: *$setting* 매개 변수에 지정된 설정에 적용할 값입니다. 이 매개 변수의 가능한 값은 지정된 설정에 따라 달라집니다. 다음 표에서는 가능한 조합을 나열합니다.  
  
|설정|$value 매개 변수의 가능한 값(괄호 안의 정수)|기본값|  
|-----------|------------------------------------------------------------------------------|-----------------|  
|ClientBufferMaxKBSize<sup>1</sup>|최대 PHP 메모리 제한의 음수가 아닌 숫자<br /><br />0은 버퍼 크기에 제한이 없다는 것입니다.|10240|  
|LogSeverity<sup>2</sup>|SQLSRV_LOG_SEVERITY_ALL(-1)<br /><br />SQLSRV_LOG_SEVERITY_ERROR(1)<br /><br />SQLSRV_LOG_SEVERITY_NOTICE(4)<br /><br />SQLSRV_LOG_SEVERITY_WARNING(2)|SQLSRV_LOG_SEVERITY_ERROR(1)|  
|LogSubsystems<sup>2</sup>|SQLSRV_LOG_SYSTEM_ALL(-1)<br /><br />SQLSRV_LOG_SYSTEM_CONN(2)<br /><br />SQLSRV_LOG_SYSTEM_INIT(1)<br /><br />SQLSRV_LOG_SYSTEM_OFF(0)<br /><br />SQLSRV_LOG_SYSTEM_STMT(4)<br /><br />SQLSRV_LOG_SYSTEM_UTIL(8)|SQLSRV_LOG_SYSTEM_OFF(0)|  
|WarningsReturnAsErrors<sup>3</sup>|**true 이면** (1) 또는 **false** (0)|**true 이면** (1)|  
  
## <a name="return-value"></a>반환 값  
경우 **sqlsrv_configure** 호출 됩니다는 지원 되지 않는 설정 또는 값을 반환 하 고 **false**합니다. 그렇지 않으면 함수에서 **true**를 반환합니다.  
  
## <a name="remarks"></a>주의  
(1) 클라이언트 쪽 쿼리에 대 한 자세한 내용은 참조 [커서 유형 &#40;SQLSRV 드라이버&#41;](../../connect/php/cursor-types-sqlsrv-driver.md)합니다.  
  
(2) 로깅 작업에 대 한 자세한 내용은 참조 [Logging Activity](../../connect/php/logging-activity.md)합니다.  
  
(3) 오류 및 경고 처리 구성에 대 한 자세한 내용은 참조 [하는 방법: 오류 및 경고 처리 SQLSRV 드라이버를 사용 하 여 구성](../../connect/php/how-to-configure-error-and-warning-handling-using-the-sqlsrv-driver.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md) 
  
