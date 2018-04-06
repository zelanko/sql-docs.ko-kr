---
title: 추적 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 21f9d8b3d96f2860ed532279acc74ac3f7c717dc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="enabling-tracing"></a>추적 사용
추적을 다음에 세 가지 방법으로 활성화할 수 수 있습니다.  
  
-   설정의 **추적** 및 **TraceFile** Odbc.ini 레지스트리 항목의 키워드입니다. 이 설정 하거나 해제 될 때 추적 **SQLAllocHandle** 와 *HandleType* SQL_HANDLE_ENV의 호출 됩니다. 이러한 옵션은 데이터 소스 설치 하는 동안 표시 된 ODBC 데이터 원본 관리자 대화 상자의 추적 탭에서 설정 됩니다. 자세한 내용은 참조 [데이터 원본에 대 한 레지스트리 항목](../../../odbc/reference/install/registry-entries-for-data-sources.md)합니다.  
  
-   호출 **SQLSetConnectAttr** SQL_ATTR_TRACE 연결 특성 SQL_OPT_TRACE_ON을로 설정 합니다. 연결의 기간에 대 한 추적을 비활성화 하거나 사용 합니다. 자세한 내용은 참조는 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 함수 설명 합니다.  
  
-   사용 하 여 **ODBCSharedTraceFlag** 추적 켜기 / 끄기를 동적으로 합니다. (자세한 내용은 다음 항목을 참조 하십시오. [동적 추적](../../../odbc/reference/develop-app/dynamic-tracing.md).)
