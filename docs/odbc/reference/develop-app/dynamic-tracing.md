---
title: 동적 추적 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], dynamic
- dynamic tracing [ODBC]
ms.assetid: ebe58a83-a7b0-4747-86c8-2af2940471ef
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8cbd2dbae4f4b437f45845ce2791f4a9b0aa8c8b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305772"
---
# <a name="dynamic-tracing"></a>동적 추적
추적은 응용 프로그램 실행의 어느 지점에서나 활성화하거나 비활성화할 수 있습니다. 이렇게 하면 응용 프로그램에서 함수 호출 수를 추적할 수 있습니다.  
  
 변수 **ODBCSharedTraceFlag는** 동적으로 추적을 사용하도록 설정되어 있습니다. 이 변수는 드라이버 관리자의 실행 중인 모든 복사본 간에 공유됩니다. 응용 프로그램이 이 변수를 설정하면 현재 실행 중인 모든 ODBC 응용 프로그램에 대해 추적이 활성화됩니다. 동적 추적이 활성화된 경우 추적을 해제하려면 응용 프로그램에서 **SQLSetConnectAttr을** 호출하여 SQL_ATTR_TRACE SQL_TRACE_OFF 설정합니다. 이 호출은 해당 응용 프로그램에 대해서만 추적을 해제합니다. Odbc32.lib에 연결된 응용 프로그램은 이 변수의 사용을 수정할 수 있습니다. 추적 데이터는 ODBC 세션 후에 열어야 하는 추적 파일 대신 실시간 창에 표시할 수 있습니다. 컨트롤을 응용 프로그램의 화면에 추가하여 추적을 원지에 켜거나 끌 수 있습니다.  
  
 ODBC 3 *.x와* 함께 제공된 추적 DLL은 스레드에 안전하지 않습니다. 전역 추적이 활성화되고(변수 **ODBCSharedTraceFlag가** 설정) 동시에 두 개 이상의 응용 프로그램이 추적 파일에 기록되는 경우 로그 파일이 올바르게 기록되지 않는다고 보장할 수는 없습니다. 이 조건은 오류를 반환하지 않습니다.
