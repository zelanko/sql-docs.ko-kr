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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036444"
---
# <a name="connection-attributes"></a>연결 특성
연결 특성은 연결의 특성입니다. 예를 들어 트랜잭션이 연결 수준에서 발생하기 때문에 트랜잭션 격리 수준은 연결 특성입니다. 마찬가지로, 초과 되기 전에 연결 하는 동안 대기할 시간 (초)을 로그인 제한 시간에는 연결 특성입니다.  
  
 연결 특성으로 설정 되어 **SQLSetConnectAttr** 사용 하 여 현재 설정을 검색 하 고 **SQLGetConnectAttr**합니다. 하는 경우 **SQLSetConnectAttr** 드라이버 로드 되는 드라이버 관리자 연결 구조에 특성을 저장 하 고 드라이버에서 연결 프로세스의 일부로 설정 하기 전에 호출 됩니다. 응용 프로그램 연결 특성;를 설정 하도록 요구 사항은 없습니다. 모든 연결 특성에는 기본값을 일부는 드라이버별 있어야 합니다.  
  
 특성 및 드라이버에 따라 하나 또는 연결 앞 이나 뒤에 연결 특성을 설정할 수 있습니다. 로그인 제한 시간 (SQL_ATTR_LOGIN_TIMEOUT) 연결 프로세스에 적용 하 고 연결 하기 전에 유효한 경우에만 설정 됩니다. 드라이버 관리자 사이의 드라이버에서 ODBC 커서 라이브러리 있기 때문에 연결 하기 전에 ODBC 커서 라이브러리 (SQL_ATTR_ODBC_CURSORS) 및 네트워크 패킷 크기 (SQL_ATTR_PACKET_SIZE)를 사용할지 여부를 지정 하는 특성을 설정 해야 하 고 따라서 로드 해야 드라이버 하기 전에 합니다.  
  
 특성 데이터 원본 읽기 전용인 지 아니면 읽기 / 쓰기 (SQL_ATTR_ACCESS_MODE) 및 현재 카탈로그 (SQL_ATTR_CURRENT_CATALOG) 앞 이나 뒤에 연결 하는 드라이버에 따라 설정할 수 있습니다입니다. 그러나 상호 운용 가능한 응용 프로그램 설정에 연결 하기 전에 일부 드라이버는 연결 되 면 이러한 변경를 지원 하지 않기 때문입니다.  
  
 일부 연결 특성 기본값이 있어야 하지 않지만 연결이 설정 됩니다. 수행 하는 것은 SQL_ATTR_ACCESS_MODE, SQL_ATTR_AUTOCOMMIT을 SQL_ATTR_LOGIN_TIMEOUT, SQL_ATTR_ODBC_CURSORS, SQL_ATTR_TRACE, 및 SQL_ATTR_TRACEFILE입니다.  
  
 번역 연결 특성 (SQL_ATTR_TRANSLATE_DLL 및 SQL_ATTR_TRANSLATE_OPTION) 연결한 후 설정 되어야 합니다.  
  
 언제 든 지 다른 모든 연결 특성을 설정할 수 있습니다. 자세한 내용은 참조는 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 함수 설명 합니다. (연결 특성에 대 한 호출 하 여 환경 수준에서 설정할 수 없습니다 **SQLSetEnvAttr**.)
