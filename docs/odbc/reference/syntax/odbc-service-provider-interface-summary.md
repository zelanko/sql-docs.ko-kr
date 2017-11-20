---
title: "ODBC 서비스 공급자 인터페이스 요약 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 82610a48532970f14800574155db89929e371baf
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-service-provider-interface-summary"></a>ODBC 서비스 공급자 인터페이스 요약
다음 표에서 ODBC 서비스 공급자 인터페이스 함수를 설명합니다. 구문 및 각 함수에 대 한 의미 체계에 대 한 자세한 내용은 참조 [ODBC 서비스 공급자 인터페이스 (SPI) 참조](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)합니다.  
  
|함수 이름|용도|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|와 동일 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), 하지만 연결 핸들에 연결 정보 토큰 대신에 특성을 설정 합니다.|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|응용 프로그램에 대 한 연결 정보 토큰에는 연결 문자열 설정 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 호출 합니다.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|응용 프로그램에 대 한 연결 정보 토큰으로 데이터 원본, 사용자 ID 및 암호를 설정 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 호출 합니다.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|풀 ID를 검색합니다.|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|드라이버는 기존 연결이 연결 풀에서 다시 사용할 수를 결정 합니다.|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|연결 풀에서 다시 사용할 수 있으면 새 연결을 만듭니다.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|풀 ID를 초과 하는 드라이버를 알립니다.|

