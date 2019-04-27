---
title: ODBC 서비스 공급자 인터페이스 (SPI) 참조 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e3d83f0aa27641c9dde164f51319a0e78d456ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653251"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>ODBC SPI(서비스 공급자 인터페이스) 참조
일반적으로 ODBC는 API (응용 프로그래밍 인터페이스)를 정의 합니다. 응용 프로그램에서 api에서 함수를 호출할 수 있습니다 하 고 드라이버 및 드라이버 관리자 내에서 구현 되어야 합니다.  
  
 드라이버 인식 연결 풀링 기능을 추가 하 여 ODBC (SPI)의 서비스 공급자 인터페이스를 소개합니다. SPI 함수 드라이버 관리자와 드라이버 간의 통신에 사용 됩니다. SPI 함수 드라이버;에 의해 구현 됩니다. 드라이버 관리자는 응용 프로그램에 SPI 함수를 노출 하지 않습니다. 응용 프로그램에서 이러한 함수를 직접 호출 하지 않습니다.  
  
 ODBC 드라이버 개발을 위한 sqlspi.h 포함 됩니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>관련 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [드라이버 관리자 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
