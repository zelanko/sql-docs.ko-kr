---
title: "연결 특성 | Microsoft Docs"
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
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8674cb60df26d15539beef1f46a74233bf838625
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="connection-attributes"></a>연결 특성
연결 특성은 연결의 특성입니다. 예를 들어 트랜잭션이 연결 수준에서 발생하기 때문에 트랜잭션 격리 수준은 연결 특성입니다. 마찬가지로, 로그인 제한 시간 또는 시간 초과 하기 전에 연결 하는 동안 대기할 시간 (초) 연결 특성입니다.  
  
 연결 특성으로 설정 되어 **SQLSetConnectAttr** 의 현재 설정은 사용 하 여 검색 및 **SQLGetConnectAttr**합니다. 경우 **SQLSetConnectAttr** 드라이버가 로드 되는 드라이버 관리자 연결 구조에 특성을 저장 하 고 드라이버에서 연결 프로세스의 일부로 설정 하기 전에 호출 됩니다. 응용 프로그램 설정 연결 특성; 있는지 요구 사항은 없습니다. 모든 연결 특성에는 기본값, 일부는 드라이버별 있어야 합니다.  
  
 특성 및 드라이버에 따라 하나 또는 연결을 앞 이나 뒤에 연결 특성을 설정할 수 있습니다. 로그인 제한 시간 (SQL_ATTR_LOGIN_TIMEOUT) 연결 프로세스에 적용 하 고 연결 하기 전에 유효한 경우에만 설정 됩니다. ODBC 커서 라이브러리 드라이버 관리자와 드라이버 사이의 있기 때문에 ODBC 커서 라이브러리 (SQL_ATTR_ODBC_CURSORS)와 네트워크 패킷 크기 (SQL_ATTR_PACKET_SIZE)을 사용할지 여부를 지정 하는 특성으로 연결 하기 전에 설정 해야 하 고 따라서 있어야 드라이버 하기 전에 로드 합니다.  
  
 특성을 지정 여부를 데이터 소스는 읽기 전용 또는 읽기 / 쓰기 (SQL_ATTR_ACCESS_MODE) 및 (SQL_ATTR_CURRENT_CATALOG) 현재 카탈로그의 이전 또는 드라이버에 따라 연결한 후 설정할 수 있습니다. 반면 상호 운용 가능한 응용 프로그램 설정에 연결 하기 전에 일부 드라이버에 연결한 후 이러한 변경 지원 하지 않기 때문입니다.  
  
 일부 연결 특성에 연결 하기 전에, 하지 않지만 기본값을 갖고 있어야 합니다. 수행 하는 것은 SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE, 및 SQL_ATTR_TRACEFILE입니다.  
  
 연결한 후 번역 연결 특성 (SQL_ATTR_TRANSLATE_DLL 및 SQL_ATTR_TRANSLATE_OPTION)를 설정 해야 합니다.  
  
 언제 든 지 다른 모든 연결 특성을 설정할 수 있습니다. 자세한 내용은 참조는 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 함수 설명 합니다. (호출을 통해 환경 수준에 연결 특성을 설정할 수 없습니다 **SQLSetEnvAttr**.)
