---
title: "추적 파일 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- trace files [ODBC]
- tracing options [ODBC], trace files
ms.assetid: ec97f949-126f-40a2-b67e-e74520a524cb
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f14ddeafa35a91dc73a9540a63de805a2e16242f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="trace-file"></a>추적 파일
응용 프로그램이 지정 추적 파일 설정 하거나는 **TraceFile** 키워드를 호출 하거나 Odbc.ini 레지스트리 항목에 **SQLSetConnectAttr** SQL_ATTR_TRACEFILE 연결 특성을 사용 합니다. 파일이 추적을 사용 하는 경우 없으면 드라이버 관리자는 파일이 만들어집니다. 각 응용 프로그램에 경합이 발생 하지 않도록 자체 전용된 추적 파일이 있어야 합니다. 응용 프로그램에 여러 개의 추적 파일; 사용할 수 있습니다. 응용 프로그램의 설치 프로그램의 추적 파일 선택을 사용 하 여 사용자를 제공할 수 있습니다. 추적을 동적으로 사용 하는 경우 응용 프로그램 표시할 수도 로그온 하지 않고 추적 결과 추적 파일에 있습니다.  
  
 추적 파일 데이터 형식에는 각 ODBC 함수 호출의 로그 및 모든 인수의 값을 제공합니다. 모든 입력된 함수를 기록 하 고 반환 코드 및 오류 상태 모두를 사용 하 여 반환 된 모든 기능을 기록 합니다.  
  
 ODBC 3에서*.x*, 추적 DLL에 연결 함수에 매개 변수가 제공 되지 않습니다.
