---
title: 동적 추적 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], dynamic
- dynamic tracing [ODBC]
ms.assetid: ebe58a83-a7b0-4747-86c8-2af2940471ef
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6746566d09d2862275daf508d08e20e2fca8473
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="dynamic-tracing"></a>동적 추적
추적을 사용 하도록 설정 또는 실행 하는 응용 프로그램의 한 지점에서 사용 하지 않도록 설정 수 있습니다. 따라서 응용을 프로그램을 여러 개의 함수 호출을 추적할 수 있습니다.  
  
 변수 **ODBCSharedTraceFlag** 동적으로 추적을 사용 하도록 설정 됩니다. 이 변수는 드라이버 관리자의 모든 실행 중인 복사본 간에 공유 됩니다. 이 변수를 설정 하는 모든 응용 프로그램, 현재 실행 중인 모든 ODBC 응용 프로그램에 대 한 추적을 사용할 수 있습니다. 동적 추적이 활성화 될 때 해제 추적을 설정 하려면 응용 프로그램이 호출 **SQLSetConnectAttr** SQL_ATTR_TRACE SQL_TRACE_OFF로 설정 합니다. 이 호출은 해당 응용 프로그램에 대 한 추적을 해제으로 바뀝니다. Odbc32.lib와 연결 된 응용 프로그램 사용이 변수를 수정할 수 있습니다. 대신 ODBC 세션 후 열어야 하는 추적 파일의 실시간 창에 추적 데이터를 표시할 수 있습니다. 컨트롤에서 추적 설정 하거나 해제 합니다 설정 하려면 응용 프로그램의 화면에 추가할 수 있습니다.  
  
 ODBC 3 함께 제공 된 DLL 추적 *.x* 스레드로부터 안전 하지 않습니다. 글로벌 추적을 사용 하는 경우 로그 파일을 제대로 작성 보장 되지 않습니다 (변수 **ODBCSharedTraceFlag** 설정) 하 고 둘 이상의 응용 프로그램이 동시에 추적 파일에 씁니다. 이 문제는 오류를 반환 하지 않습니다.
