---
title: 추적 사용 | Microsoft Docs
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
ms.openlocfilehash: 24f80e0e81e4be8895d59256492b868c53aab7b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046796"
---
# <a name="enabling-tracing"></a>추적 사용
다음 세 가지 방법으로 추적을 사용 하도록 설정할 수 있습니다.  
  
-   Odbc .ini 레지스트리 항목에서 **Trace** 및 **tracefile** 키워드를 설정 합니다. 이를 통해 *HandleType* SQL_HANDLE_ENV의 **SQLAllocHandle** 가 호출 되는 경우 추적을 사용 하거나 사용 하지 않도록 설정할 수 있습니다. 이러한 옵션은 데이터 원본 설정 중에 표시 되는 ODBC 데이터 원본 관리자 대화 상자의 추적 탭에서 설정 합니다. 자세한 내용은 [데이터 원본에 대 한 레지스트리 항목](../../../odbc/reference/install/registry-entries-for-data-sources.md)을 참조 하세요.  
  
-   **SQLSetConnectAttr** 를 호출 하 여 SQL_ATTR_TRACE 연결 특성을 SQL_OPT_TRACE_ON로 설정 합니다. 이렇게 하면 연결 기간 동안 추적을 사용 하거나 사용 하지 않도록 설정할 수 있습니다. 자세한 내용은 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 함수 설명을 참조 하세요.  
  
-   **ODBCSharedTraceFlag** 를 사용 하 여 추적을 동적으로 설정 하거나 해제할 수 있습니다. 자세한 내용은 다음 항목인 [동적 추적](../../../odbc/reference/develop-app/dynamic-tracing.md)을 참조 하세요.
