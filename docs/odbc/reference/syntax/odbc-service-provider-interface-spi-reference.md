---
title: ODBC 서비스 공급자 인터페이스 (SPI) 참조 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1bd481d7344345578f830374f7049a917e60eb68
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-service-provider-interface-spi-reference"></a>ODBC 서비스 공급자 인터페이스 (SPI) 참조
일반적으로, ODBC (API) 응용 프로그래밍 인터페이스를 정의합니다. 내 드라이버 관리자와 드라이버를 모두 구현 해야 및 응용 프로그램에서 API에 포함 된 함수를 호출할 수 있습니다.  
  
 ODBC는 드라이버 인식 연결 풀링 기능을 추가 하 여 서비스 공급자 인터페이스 (SPI)을 소개합니다. SPI의 함수는 드라이버 및 드라이버 관리자 간 통신에 사용 됩니다. 드라이버; SPI 함수 구현 드라이버 관리자는 응용 프로그램에 SPI 함수를 노출 하지 않습니다. 응용 프로그램에서 이러한 함수를 직접 호출 하지 않습니다.  
  
 ODBC 드라이버 개발에 대 한 sqlspi.h를 포함 됩니다.  
  
 이 단원의 다음 항목에서는  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 드라이버를 개발합니다.](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [드라이버 관리자 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
