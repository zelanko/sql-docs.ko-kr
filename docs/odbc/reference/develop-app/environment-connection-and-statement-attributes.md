---
description: 환경, 연결 및 명령문 특성
title: 환경, 연결 및 문 특성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment attributes [ODBC]
- connection attributes [ODBC]
- statement attributes [ODBC]
ms.assetid: 9e15b276-3b7a-428a-b72f-a3ddfe1ba1ce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6bc37e05f2c8847ff9a4828a5d2e9e7456732a41
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482956"
---
# <a name="environment-connection-and-statement-attributes"></a>환경, 연결 및 명령문 특성
ODBC는 환경, 연결 또는 문과 연결 된 여러 특성을 정의 합니다.  
  
 환경 특성은 연결 풀링을 사용 하도록 설정 되었는지 여부와 같은 전체 환경에 영향을 줍니다. 환경 특성은 **SQLSetEnvAttr** 로 설정 되 고 **SQLGetEnvAttr**로 검색 됩니다.  
  
 연결 특성은 제한 시간이 초과 되기 전에 데이터 원본에 연결을 시도 하는 동안 드라이버가 기다려야 하는 시간 등 각 연결에 개별적으로 영향을 줍니다. 연결 특성은 **SQLSetConnectAttr** 로 설정 되 고 **SQLGetConnectAttr**로 검색 됩니다. 연결 특성에 대 한 자세한 내용은 [연결 특성](../../../odbc/reference/develop-app/connection-attributes.md)을 참조 하세요.  
  
 문 특성은 문을 비동기적으로 실행할지 여부와 같이 각 문에 개별적으로 영향을 줍니다. Statement 특성은 **SQLSetStmtAttr** 로 설정 되 고 **SQLGetStmtAttr**로 검색 됩니다. 몇 가지 문 특성은 읽기 전용 특성이 며 설정할 수 없습니다. 예를 들어 커서의 현재 행 번호를 검색 하는 데 사용 되는 SQL_ATTR_ROW_NUMBER statement 특성은 읽기 전용입니다. 문 특성에 대 한 자세한 내용은 [Statement 특성](../../../odbc/reference/develop-app/statement-attributes.md)을 참조 하세요.  
  
 ODBC에서 정의 되는 특성 외에도 드라이버는 자체 연결 및 문 특성을 정의할 수 있습니다. 두 드라이버 공급 업체가 서로 다른 소유 특성에 동일한 정수 값을 할당 하지 않도록 하려면 드라이버 정의 특성을 Open Group에 등록 해야 합니다. 자세한 내용은 [드라이버별 데이터 형식, 설명자 형식, 정보 형식, 진단 유형 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)을 참조 하세요.  
  
 특성의 전체 목록은 [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)및 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)를 참조 하세요. 대부분의 특성은 영향을 주는 ODBC 함수 설명에도 설명 되어 있습니다.
