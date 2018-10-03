---
title: 추적을 사용 하도록 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb6d8eaf4a1f4eaadc4e8e9a7030b81c373d8377
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819921"
---
# <a name="enabling-tracing"></a>추적 사용
추적을 다음 세 가지 방법으로 사용할 수 있습니다.  
  
-   설정 합니다 **추적** 하 고 **TraceFile** Odbc.ini 레지스트리 항목에는 키워드입니다. 이 설정 하거나 해제 될 때 추적 **SQLAllocHandle** 사용 하 여를 *HandleType* SQL_HANDLE_ENV의 호출 됩니다. 이러한 옵션은 데이터 원본 설정 하는 동안 표시 되는 ODBC 데이터 원본 관리자 대화 상자에 있는 추적 탭에서 설정 됩니다. 자세한 내용은 [데이터 원본에 대 한 레지스트리 항목](../../../odbc/reference/install/registry-entries-for-data-sources.md)합니다.  
  
-   호출 **SQLSetConnectAttr** SQL_ATTR_TRACE 연결 특성 SQL_OPT_TRACE_ON을로 설정 합니다. 이 사용 하도록 설정 하거나 연결 기간에 대 한 추적을 사용 하지 않도록 설정 합니다. 자세한 내용은 참조는 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 함수 설명 합니다.  
  
-   사용 하 여 **ODBCSharedTraceFlag** 추적 기능을 켜거나 끄려면를 동적으로 합니다. (자세한 내용은 다음 항목을 참조 하세요 [동적 추적](../../../odbc/reference/develop-app/dynamic-tracing.md).)
