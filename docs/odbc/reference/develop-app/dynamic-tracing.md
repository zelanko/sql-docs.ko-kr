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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046893"
---
# <a name="dynamic-tracing"></a>동적 추적
응용 프로그램 실행의 특정 지점에서 추적을 사용 하거나 사용 하지 않도록 설정할 수 있습니다. 이렇게 하면 응용 프로그램에서 원하는 수의 함수 호출을 추적할 수 있습니다.  
  
 **ODBCSharedTraceFlag** 변수는 동적으로 추적을 사용 하도록 설정 됩니다. 이 변수는 드라이버 관리자의 모든 실행 중인 복사본에서 공유 됩니다. 응용 프로그램에서이 변수를 설정 하는 경우 현재 실행 중인 모든 ODBC 응용 프로그램에 대 한 추적이 활성화 됩니다. 동적 추적을 사용 하도록 설정 하는 경우 추적을 해제 하려면 응용 프로그램이 **SQLSetConnectAttr** 를 호출 하 여 SQL_ATTR_TRACE를 SQL_TRACE_OFF로 설정 합니다. 이 호출은 해당 응용 프로그램에 대해서만 추적을 해제 합니다. 위한 odbc32.dll와 연결 된 응용 프로그램은이 변수의 사용을 수정할 수 있습니다. 추적 데이터는 ODBC 세션 후에 열려 있어야 하는 추적 파일 대신 실시간 창에 표시 될 수 있습니다. 응용 프로그램의 화면에 컨트롤을 추가 하 여 추적을 설정 하거나 해제할 수 있습니다.  
  
 ODBC 3.x와 함께*제공 되는* 추적 DLL은 스레드로부터 안전 하지 않습니다. 전역 추적을 사용 하도록 설정 하 고 ( **ODBCSharedTraceFlag** 변수가 설정 된 경우) 둘 이상의 응용 프로그램이 동시에 추적 파일에 쓰는 경우에는 로그 파일이 올바르게 작성 되지 않을 수도 있습니다. 이 상태는 오류를 반환 하지 않습니다.
