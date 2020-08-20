---
description: ODBC SPI(서비스 공급자 인터페이스) 요약
title: ODBC 서비스 공급자 인터페이스 요약 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 00d15d33fba1e697eebbe6a640c4f8a4d8eadea7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487346"
---
# <a name="odbc-service-provider-interface-summary"></a>ODBC SPI(서비스 공급자 인터페이스) 요약
다음 표에서는 ODBC 서비스 공급자 인터페이스 함수에 대해 설명 합니다. 각 함수의 구문 및 의미 체계에 대 한 자세한 내용은 [SPI (ODBC 서비스 공급자 인터페이스) 참조](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)를 참조 하세요.  
  
|함수 이름|용도|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)와 동일 하지만 연결 핸들 대신 연결 정보 토큰에 대 한 특성을 설정 합니다.|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|응용 프로그램의 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 호출에 대 한 연결 정보 토큰으로 연결 문자열을 설정 합니다.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|응용 프로그램의 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 호출에 대 한 연결 정보 토큰으로 데이터 원본, 사용자 ID 및 암호를 설정 합니다.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|풀 ID를 검색 합니다.|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|드라이버가 연결 풀에서 기존 연결을 다시 사용할 수 있는지 여부를 확인 합니다.|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|풀의 연결을 다시 사용할 수 없는 경우 새 연결을 만듭니다.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|풀 ID의 시간이 초과 되었음을 드라이버에 알립니다.|
