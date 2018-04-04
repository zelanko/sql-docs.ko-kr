---
title: 연결 풀링 (Microsoft Drivers for PHP for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/10/2017
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
helpviewer_keywords:
- connection pooling support
ms.assetid: 4d9a83d4-08de-43a1-975c-0a94005edc94
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 287cba2cbca687ef5006ae0410b2cd6a0f2598b7
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="connection-pooling-microsoft-drivers-for-php-for-sql-server"></a>연결 풀링(Microsoft Drivers for PHP for SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

다음은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]에서 연결 풀링에 대해 유의할 중요한 사항입니다.  
  
-   [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 ODBC 연결 풀링을 사용합니다.  
  
-   기본적으로 연결 풀링이 Windows에서 사용 됩니다. Linux 및 Mac OS X에서 ODBC 연결 풀링을 사용할 수 있는 경우에 연결 풀링 되기도 합니다. 연결 풀링을 사용 하는 서버에 연결 하는 경우 드라이버는 새 만들기 전에 풀링된 연결을 사용 하려고 합니다. 해당 연결이 풀에 없는 경우 새 연결이 만들어지고 풀에 추가됩니다. 드라이버가 연결 문자열을 비교하여 연결이 동일한지 여부를 확인합니다.  
  
-   풀에서 연결이 사용되는 경우 연결 상태가 재설정됩니다.  
  
-   연결을 닫으면 풀에 대한 연결을 반환합니다.  
  
연결 풀링에 대 한 자세한 내용은 참조 [드라이버 관리자 연결 풀링](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)합니다.  
  
## <a name="enablingdisabling-connection-pooling"></a>활성화/비활성화 해도 연결 풀링
### <a name="windows"></a>창
드라이버의 값을 설정 하 여 연결 풀에서 동일한 연결을 찾는) (대신 새 연결을 만들려고 할 수 있습니다는 *ConnectionPooling* 특성에 대 한 연결 문자열 **false**  (또는 0).  
  
경우는 *ConnectionPooling* 특성이 연결 문자열에서 생략 되거나로 설정 되 면 **true** (또는 1)에 해당 연결이 존재 하지 않는 경우만 새 연결을 만듭니다는 드라이버는 연결 풀입니다.  
  
다른 연결 특성에 대한 자세한 내용은 [Connection Options](../../connect/php/connection-options.md)을 참조하세요.  
### <a name="linux-and-mac-os-x"></a>Linux 및 Mac OS X
*ConnectionPooling* 특성을 설정/해제 연결 풀링을 사용할 수 없습니다. 

연결 풀링을 수 수 사용/사용 안 함 odbcinst.ini 구성 파일을 편집 하 여 합니다. 드라이버 변경 내용을 적용 하려면에 대 한 다시 로드 해야 합니다.

설정 `Pooling` 를 `Yes` 및 양의 `CPTimeout`odbcinst.ini에는 값 연결 풀링을 사용 하도록 설정 합니다. 
```
[ODBC]
Pooling=Yes

[ODBC Driver 13 for SQL Server]
CPTimeout=<int value>
```
설정 `Pooling` 를 `No` odbcinst.ini에서 하면 드라이버는 새 연결을 만듭니다.
```
[ODBC]
Pooling=No
```
  
## <a name="see-also"></a>관련 항목:  
[방법: Windows 인증을 사용하여 연결](../../connect/php/how-to-connect-using-windows-authentication.md)

[방법: SQL Server 인증을 사용하여 연결](../../connect/php/how-to-connect-using-sql-server-authentication.md)  
  
