---
title: '방법: 지정된 된 포트에서 연결 | Microsoft Docs'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
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
- connecting to the server, specifying a port
ms.assetid: 65a154d1-375c-439b-a653-7815c9d70ff3
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b17dd2bb8df3f7274cb8eea36faf3ee5f320f983
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="how-to-connect-on-a-specified-port"></a>방법: 지정된 포트에서 연결
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]를 사용하여 지정된 포트에서 SQL Server에 연결하는 방법을 설명합니다.  
  
### <a name="to-connect-on-a-specified-port"></a>지정된 포트에서 연결하려면  
  
1.  연결을 허용하도록 서버가 구성된 포트를 확인합니다. 지정된 된 포트에서 연결을 허용 하도록 서버를 구성 하는 방법에 대 한 정보를 참조 하십시오. [하는 방법: 특정 TCP 포트로 (SQL Server 구성 관리자)에서 수신 하도록 서버 구성](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)합니다.  
  
2.  원하는 포트를 추가 *$serverName* 의 매개 변수는 [sqlsrv_connect](../../connect/php/sqlsrv-connect.md) 함수입니다. 서버 이름과 포트를 쉼표로 구분합니다. 예를 들어 다음 코드 줄은 포트 1521에서 *myServer* 라는 서버에 연결하는 방법을 보여 주기 위해 SQLSRV 드라이버를 사용합니다.  
  
    ```  
    $serverName = "myServer, 1521";  
    sqlsrv_connect( $serverName );  
    ```  
  
    다음 코드 줄 라는 서버에 연결 하는 방법을 보여 주기 위해 PDO_SQLSRV 드라이버를 사용 하 여 *myServer* 포트 1521에서:  
  
    ```  
    $serverName = "(local), 1521";  
    $database = "AdventureWorks";  
    $conn = new PDO( "sqlsrv:server=$serverName;Database=$database", "", "");  
    ```  
  
## <a name="see-also"></a>관련 항목:  
[서버에 연결](../../connect/php/connecting-to-the-server.md)

[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md)

[시작 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 드라이버 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
