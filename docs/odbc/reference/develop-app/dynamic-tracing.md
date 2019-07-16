---
title: 동적 추적 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8420589761a1f8cb1f9cf8a3022842863fd30758
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046893"
---
# <a name="dynamic-tracing"></a>동적 추적
추적을 사용 하도록 설정 또는 언제 든 지 실행 응용 프로그램에서 사용 하지 않도록 설정 수 있습니다. 이렇게 하면 응용 프로그램을 여러 개의 함수 호출을 추적 합니다.  
  
 변수의 **ODBCSharedTraceFlag** 동적으로 추적을 사용 하도록 설정 됩니다. 이 변수는 모든 실행 중인 복사본의 드라이버 관리자 간에 공유 됩니다. 이 변수를 설정 하는 모든 응용 프로그램, 현재 실행 중인 모든 ODBC 응용 프로그램에 대 한 추적을 사용할 수 있습니다. 동적 추적이 설정 되 면 해제 추적을 설정 하려면 응용 프로그램 호출 **SQLSetConnectAttr** SQL_ATTR_TRACE SQL_TRACE_OFF로 설정 합니다. 이 호출은 해당 응용 프로그램에 대 한 추적을 해제 바뀝니다. Odbc32.lib를 사용 하 여 연결 된 응용 프로그램 사용이 변수를 수정할 수 있습니다. ODBC 세션이 끝난 후 열려 있어야 하는 추적 파일 대신 실시간 창에서 추적 데이터를 표시할 수 있습니다. 컨트롤에서 추적 또는 해제를 설정 하려면 응용 프로그램의 화면에 추가할 수 있습니다.  
  
 ODBC 3을 사용 하 여 DLL 배송 추적 *.x* 는 스레드로부터 안전 하지 않습니다. 글로벌 추적을 사용 하는 경우 로그 파일은 올바르게 기록 하는 보장 되지 않습니다 (변수의 **ODBCSharedTraceFlag** 설정할지) 둘 이상의 응용 프로그램 동시에 추적 파일에 씁니다. 이 문제는 오류를 반환 하지 않습니다.
