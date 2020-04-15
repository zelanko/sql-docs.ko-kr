---
title: ODBC 서비스 공급자 인터페이스 요약 | 마이크로 소프트 문서
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
ms.openlocfilehash: b2f7e459cc7b89106bf1b7ebcd49c699d43da9f6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298900"
---
# <a name="odbc-service-provider-interface-summary"></a>ODBC SPI(서비스 공급자 인터페이스) 요약
다음 표는 ODBC 서비스 공급자 인터페이스 함수에 대해 설명합니다. 각 함수에 대한 구문 및 의미 체계에 대한 자세한 내용은 [SPI(ODBC 서비스 공급자 인터페이스) 참조를](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)참조하십시오.  
  
|함수 이름|용도|  
|-------------------|-------------|  
|[SQLSet커넥트트트르포트bcInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|[SQLSetConnectAttr와](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)동일하지만 연결 핸들 대신 연결 정보 토큰에 대한 특성을 설정합니다.|  
|[SQLSet드라이버연결정보](../../../odbc/reference/syntax/sqldrivertodatasource-function.md)|응용 프로그램의 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 호출에 대 한 연결 정보 토큰에 연결 문자열을 설정 합니다.|  
|[SQLSetConnectInfo](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|응용 프로그램의 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 호출에 대 한 연결 정보 토큰에 데이터 원본, 사용자 ID 및 암호를 설정 합니다.|  
|[SQLGetPoolID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|풀 ID를 검색합니다.|  
|[SQLRate 연결](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|드라이버가 연결 풀에서 기존 연결을 다시 사용할 수 있는지 여부를 결정합니다.|  
|[SQL풀커넥트](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|풀에서 연결을 다시 사용할 수 없는 경우 새 연결을 만듭니다.|  
|[SQL클린업커넥션풀ID](../../../odbc/reference/syntax/sqldatasourcetodriver-function.md)|드라이버에게 풀 ID가 시간 만료되었다는 것을 알립니다.|
