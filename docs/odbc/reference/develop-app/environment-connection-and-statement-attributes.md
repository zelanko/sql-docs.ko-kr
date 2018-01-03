---
title: "환경, 연결 및 문 특성 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- environment attributes [ODBC]
- connection attributes [ODBC]
- statement attributes [ODBC]
ms.assetid: 9e15b276-3b7a-428a-b72f-a3ddfe1ba1ce
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7d1270026a19c0e5c07a9590f70096046984e455
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="environment-connection-and-statement-attributes"></a>환경, 연결 및 문 특성
ODBC 환경, 연결 또는 문이 연관 된 특성의 수를 정의 합니다.  
  
 환경 특성 연결 풀링을 활성화 되어 있는지 여부와 같은 전체 환경을 영향을 줍니다. 환경 특성으로 설정 되어 **SQLSetEnvAttr** 및와 검색 된 **SQLGetEnvAttr**합니다.  
  
 연결 특성에 영향을 줄 각 연결 개별적으로 방법 등 시간이 초과 되기 전에 데이터 원본에 연결 하는 동안 드라이버를 대기 하는 시간입니다. 연결 특성으로 설정 되어 **SQLSetConnectAttr** 및와 검색 된 **SQLGetConnectAttr**합니다. 연결 특성에 대 한 자세한 내용은 참조 [연결 특성](../../../odbc/reference/develop-app/connection-attributes.md)합니다.  
  
 문 특성 문이 비동기적으로 실행 되어야 해야 하는지 여부와 같은 개별적으로 각 문에 영향을 줍니다. 문 특성 설정 됩니다 **SQLSetStmtAttr** 및와 검색 된 **SQLGetStmtAttr**합니다. 몇 가지 문 특성은 읽기 전용 특성 및 설정할 수 없습니다. 예를 들어, 커서의 현재 행의 수를 검색에 사용 되는 SQL_ATTR_ROW_NUMBER 문 특성에는 읽기 전용입니다. 문 특성에 대 한 자세한 내용은 참조 [문 특성](../../../odbc/reference/develop-app/statement-attributes.md)합니다.  
  
 드라이버는 ODBC에 정의 된 특성 뿐 아니라 자체 연결 및 문 특성을 정의할 수 있습니다. 드라이버에서 정의 된 특성 두 드라이버 공급 업체 독점, 서로 다른 특성에 동일한 정수 값을 할당 하지 않습니다 확인 하려면 Open Group으로 등록 되어야 합니다. 자세한 내용은 참조 [드라이버 관련 데이터 형식, 형식 설명자, 정보 유형, 진단 형식 및 특성](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)합니다.  
  
 특성의 전체 목록은 참조 하십시오. [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md), [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md), 및 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)합니다. 대부분의 특성에 영향을 주는지 ODBC 함수에 대 한 설명을 설명 합니다.
