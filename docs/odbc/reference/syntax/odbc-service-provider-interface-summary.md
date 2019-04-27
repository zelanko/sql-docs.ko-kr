---
title: ODBC 서비스 공급자 인터페이스 요약 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ace6085b-355b-435b-8734-503fc3c12ec2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d5f3c133b105c905b79589d86952658b6d39f0f6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62653390"
---
# <a name="odbc-service-provider-interface-summary"></a>ODBC SPI(서비스 공급자 인터페이스) 요약
다음 표에서 ODBC 서비스 공급자 인터페이스 함수에 설명 합니다. 구문 및 각 함수에 대 한 의미 체계에 대 한 자세한 내용은 참조 하세요. [ODBC 서비스 공급자 인터페이스 (SPI) 참조](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)합니다.  
  
|함수 이름|용도|  
|-------------------|-------------|  
|[SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|동일 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), 하지만 연결 핸들에 연결 정보 토큰 대신에 특성을 설정 하는 것입니다.|  
|[SQLSetDriverConnectInfo](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|응용 프로그램에 대 한 연결 정보 토큰에는 연결 문자열 설정 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 호출 합니다.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|응용 프로그램에 대 한 연결 정보 토큰에는 데이터 원본, 사용자 ID 및 암호를 설정 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 호출 합니다.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|풀 ID를 검색합니다.|  
|[SQLRateConnection](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|드라이버에서 연결 풀의 기존 연결을 다시 사용할 수를 결정 합니다.|  
|[SQLPoolConnect](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|풀에서 연결을 다시 사용할 수 있으면 새 연결을 만듭니다.|  
|[SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|풀 ID를 초과 하는 드라이버를 알립니다.|
