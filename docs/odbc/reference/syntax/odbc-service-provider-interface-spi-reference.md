---
title: ODBC 서비스 공급자 인터페이스(SPI) 참조 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e9739abd13bf2c4bed1b1b3a31c18c683594705a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298911"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>ODBC SPI(서비스 공급자 인터페이스) 참조
일반적으로 ODBC는 응용 프로그램 프로그래밍 인터페이스(API)를 정의했습니다. API의 함수는 응용 프로그램에서 호출할 수 있으며 드라이버 관리자와 드라이버 모두에서 구현해야 합니다.  
  
 ODBC는 드라이버 인식 연결 풀링 기능을 추가하여 서비스 공급자 인터페이스(SPI)를 도입했습니다. SPI의 함수는 드라이버 관리자와 드라이버 간의 통신에 사용됩니다. SPI 함수는 드라이버에 의해 구현됩니다. 드라이버 관리자는 SPI 함수를 응용 프로그램에 노출시키지 않습니다. 응용 프로그램은 이러한 함수를 직접 호출해서는 안 됩니다.  
  
 ODBC 드라이버 개발을 위해 sqlspi.h를 포함합니다.  
  
 이 단원에는 다음 항목이 포함되어 있습니다.  
  
-   [SQL클린업커넥션풀ID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQL풀커넥트](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRate 연결](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSet커넥트트트르포트bcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSet드라이버연결정보](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>참고 항목  
 [ODBC 드라이버 개발](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ODBC 드라이버에서 연결 풀 인식 개발](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [드라이버 관리자 연결 풀링](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
