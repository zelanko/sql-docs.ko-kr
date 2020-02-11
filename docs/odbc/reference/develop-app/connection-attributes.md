---
title: 연결 특성 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 09b29277d74383abff1510ca7394aecad036fc7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036444"
---
# <a name="connection-attributes"></a>연결 특성
연결 특성은 연결의 특징입니다. 예를 들어 트랜잭션이 연결 수준에서 발생하기 때문에 트랜잭션 격리 수준은 연결 특성입니다. 마찬가지로, 제한 시간이 초과 되기 전에 연결을 시도 하는 동안 로그인 제한 시간 (초) 또는 대기 시간 (초)은 연결 특성입니다.  
  
 연결 특성은 **SQLSetConnectAttr** 로 설정 되 고 현재 설정은 **SQLGetConnectAttr**로 검색 됩니다. 드라이버가 로드 되기 전에 **SQLSetConnectAttr** 가 호출 되 면 드라이버 관리자는 해당 연결 구조에 특성을 저장 하 고 연결 프로세스의 일부로 드라이버에서 해당 특성을 설정 합니다. 응용 프로그램에서 연결 특성을 설정 해야 하는 요구 사항은 없습니다. 모든 연결 특성에는 기본값이 있으며, 그 중 일부는 드라이버 마다 다릅니다.  
  
 연결 특성은 연결 전이나 후에 설정 하거나 특성 및 드라이버에 따라 설정할 수 있습니다. 로그인 제한 시간 (SQL_ATTR_LOGIN_TIMEOUT)은 연결 프로세스에 적용 되며 연결 하기 전에 설정 된 경우에만 적용 됩니다. Odbc 커서 라이브러리를 사용할지 여부를 지정 하는 특성 (SQL_ATTR_ODBC_CURSORS)과 네트워크 패킷 크기 (SQL_ATTR_PACKET_SIZE)는 연결 하기 전에 설정 해야 합니다. ODBC 커서 라이브러리는 드라이버 관리자와 드라이버 사이에 있기 때문입니다. 따라서 드라이버 보다 먼저 로드 해야 합니다.  
  
 데이터 원본을 읽기 전용 또는 읽기/쓰기 (SQL_ATTR_ACCESS_MODE)로 지정 하 고, 드라이버에 따라 연결 전이나 후에 현재 카탈로그 (SQL_ATTR_CURRENT_CATALOG)를 설정할 수 있는지 여부를 지정 하는 특성입니다. 그러나 일부 드라이버에서는 연결 후에 이러한 변경이 지원 되지 않으므로 상호 운용 가능한 응용 프로그램은 연결 전에 설정 합니다.  
  
 일부 연결 특성은 연결을 설정 하기 전에 기본값이 있지만 나머지는 그렇지 않습니다. 이러한 작업은 SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT, SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE 및 SQL_ATTR_TRACEFILE입니다.  
  
 연결 후에는 변환 연결 특성 (SQL_ATTR_TRANSLATE_DLL 및 SQL_ATTR_TRANSLATE_OPTION)을 설정 해야 합니다.  
  
 다른 모든 연결 특성은 언제 든 지 설정할 수 있습니다. 자세한 내용은 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 함수 설명을 참조 하세요. **SQLSetEnvAttr**를 호출 하 여 환경 수준에서 연결 특성을 설정할 수 없습니다.
