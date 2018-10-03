---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e77be71458eb10e97a82c925d34141a7bcaf1dc4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685937"
---
# <a name="environment-connection-and-statement-attributes"></a>환경, 연결 및 명령문 특성
ODBC 환경, 연결 또는 명령문을 사용 하 여 연관 된 특성의 수를 정의 합니다.  
  
 환경 특성에 연결 풀링을 사용 되는지 여부와 같은 전체 환경을 영향을 줍니다. 환경 특성으로 설정 되어 **SQLSetEnvAttr** 사용 하 여 검색 하 고 **SQLGetEnvAttr**합니다.  
  
 연결 특성에 영향을 줄 각 연결을 개별적으로 하는 방법과 같은 시간이 초과 되기 전에 데이터 원본에 연결 하는 동안 드라이버를 오래 대기 해야 합니다. 연결 특성으로 설정 되어 **SQLSetConnectAttr** 사용 하 여 검색 하 고 **SQLGetConnectAttr**합니다. 연결 특성에 대 한 자세한 내용은 참조 하세요. [연결 특성](../../../odbc/reference/develop-app/connection-attributes.md)합니다.  
  
 문 특성 문이 비동기적으로 하 여 실행 해야 하는지 여부 등을 개별적으로 각 문에 영향을 줍니다. 사용 하 여 문 특성 설정 **SQLSetStmtAttr** 사용 하 여 검색 하 고 **SQLGetStmtAttr**합니다. 몇 가지 문 특성은 읽기 전용 특성이 며 설정할 수 없습니다. 예를 들어 SQL_ATTR_ROW_NUMBER 문 특성에 사용 되는 커서의 현재 행의 수를 검색 하는 읽기 전용입니다. 문 특성에 대 한 자세한 내용은 참조 하세요. [문 특성](../../../odbc/reference/develop-app/statement-attributes.md)합니다.  
  
 ODBC에서 정의 된 특성 외에도 드라이버 자체 연결 및 문 특성을 정의할 수 있습니다. 두 드라이버 공급 업체 다른, 독점 특성에 동일한 정수 값을 할당 하지 않으면 되도록 Open Group 드라이버에서 정의 된 특성에 등록 해야 합니다. 자세한 내용은 [드라이버별 데이터 형식, 설명자 유형, 정보 유형, 진단 유형 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)합니다.  
  
 특성의 전체 목록은 참조 하세요. [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)하십시오 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), 및 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)합니다. 대부분의 특성은 그 영향을 받는 ODBC 함수의 설명에 설명 되어 있습니다.
