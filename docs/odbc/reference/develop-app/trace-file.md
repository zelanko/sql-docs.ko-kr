---
title: 추적 파일 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace files [ODBC]
- tracing options [ODBC], trace files
ms.assetid: ec97f949-126f-40a2-b67e-e74520a524cb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8138a0cef3a28d31242a74162f0024e28e8b8fe9
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793927"
---
# <a name="trace-file"></a>추적 파일
응용 프로그램 추적 파일을 지정 하거나 설정 합니다 **TraceFile** Odbc.ini 레지스트리 항목 또는 호출 하 여 키워드 **SQLSetConnectAttr** SQL_ATTR_TRACEFILE 연결 특성을 사용 하 여 합니다. 추적을 사용 하는 경우 파일이 없으면, 드라이버 관리자는 파일을 만듭니다. 각 응용 프로그램에는 경합을 방지 하는 자체 전용된 추적 파일이 있어야 합니다. 응용 프로그램이 둘 이상의 추적 파일을 사용할 수 있습니다. 응용 프로그램의 설치 프로그램을 다양 한 추적 파일을 사용 하 여 사용자를 제공할 수 있습니다. 추적을 동적으로 사용 하는 경우 응용 프로그램이 표시할 수도 있습니다 로그온 하지 않고 추적 결과 추적 파일에.  
  
 추적 파일을 각 ODBC 함수 호출 데이터 형식에 대 한 로그 및 모든 인수의 값을 제공합니다. 모든 입력된 함수를 기록 하 고 반환 코드 및 오류 상태를 사용 하 여 반환 된 모든 함수를 기록 합니다.  
  
 Odbc에서 *3.x*, 연결 함수에 매개 변수는 추적 DLL에 제공 되지 않습니다.
