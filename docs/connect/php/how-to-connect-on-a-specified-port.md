---
title: "방법: 지정된 된 포트에서 연결 | Microsoft Docs"
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
- connecting to the server, specifying a port
ms.assetid: 65a154d1-375c-439b-a653-7815c9d70ff3
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 88115d77c56cafed731aa2a9cf6c39afcd191618
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="how-to-connect-on-a-specified-port"></a>방법: 지정된 포트에서 연결
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목은 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]를 사용하여 지정된 포트에서 SQL Server에 연결하는 방법을 설명합니다.  
  
### <a name="to-connect-on-a-specified-port"></a>지정된 포트에서 연결하려면  
  
1.  연결을 허용하도록 서버가 구성된 포트를 확인합니다. 지정된 된 포트에서 연결을 허용 하도록 서버를 구성 하는 방법에 대 한 정보를 참조 하십시오. [하는 방법: 특정 TCP 포트로 (SQL Server 구성 관리자)에서 수신 하도록 서버 구성](http://go.microsoft.com/fwlink/?LinkId=121865)합니다.  
  
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
[PHP SQL 드라이버 프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md)
[PHP SQL 드라이버 시작](../../connect/php/getting-started-with-the-php-sql-driver.md) 
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 드라이버 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  

