---
title: 연결 속성 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c295ce88eedf1d4cddc4173f5dea39c44b01f83d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299044"
---
# <a name="connection-attributes"></a>연결 특성
연결 특성은 연결의 특성입니다. 예를 들어 트랜잭션이 연결 수준에서 발생하기 때문에 트랜잭션 격리 수준은 연결 특성입니다. 마찬가지로, 시간 지정 시간 시간 또는 시간 지정 전에 연결을 시도하는 동안 기다려야 하는 시간(초)은 연결 특성입니다.  
  
 연결 특성은 **SQLSetConnectAttr** 및 **SQLGetConnectAttr로**검색된 현재 설정으로 설정됩니다. 드라이버가 로드되기 전에 **SQLSetConnectAttr이** 호출되면 드라이버 관리자는 연결 구조에 특성을 저장하고 연결 프로세스의 일부로 드라이버에 설정합니다. 응용 프로그램이 연결 특성을 설정할 필요는 없습니다. 모든 연결 특성에는 기본값이 있으며, 그 중 일부는 드라이버에 따라 다릅니다.  
  
 연결 특성은 특성 및 드라이버에 따라 연결 전이나 후에 설정할 수 있습니다. 로그인 시간 제한(SQL_ATTR_LOGIN_TIMEOUT)은 연결 프로세스에 적용되며 연결 하기 전에 설정된 경우에만 적용됩니다. ODBC 커서 라이브러리가 드라이버 관리자와 드라이버 사이에 상주하므로 ODBC 커서 라이브러리(SQL_ATTR_ODBC_CURSORS)와 네트워크 패킷 크기(SQL_ATTR_PACKET_SIZE)를 연결할지 여부를 지정하는 특성을 연결하기 전에 설정해야 합니다.  
  
 데이터 원본이 읽기 전용인지 읽기-쓰기(SQL_ATTR_ACCESS_MODE)인지 를 지정하는 특성과 현재 카탈로그(SQL_ATTR_CURRENT_CATALOG)는 드라이버에 따라 연결 전이나 후에 설정할 수 있습니다. 그러나 일부 드라이버는 연결 후 이러한 변경을 지원하지 않기 때문에 상호 운용 가능한 응용 프로그램은 연결하기 전에 설정합니다.  
  
 일부 연결 특성에는 연결이 이루어지기 전에 기본값이 있지만 다른 연결 특성은 기본값입니다. Those that do are SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE, and SQL_ATTR_TRACEFILE.  
  
 연결 후 변환 연결 특성(SQL_ATTR_TRANSLATE_DLL 및 SQL_ATTR_TRANSLATE_OPTION)을 설정해야 합니다.  
  
 다른 모든 연결 특성은 언제든지 설정할 수 있습니다. 자세한 내용은 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 함수 설명을 참조하십시오. (연결 특성은 **SQLSetEnvAttr에**대 한 호출에 의해 환경 수준에서 설정할 수 없습니다.)
