---
description: 추적 파일
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba45e44baaba68d1c203e83a25c9db305642e6d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487496"
---
# <a name="trace-file"></a>추적 파일
응용 프로그램은 Odbc.ini 레지스트리 항목에서 **tracefile** 키워드를 설정 하거나 SQL_ATTR_TRACEFILE 연결 특성을 사용 하 여 **SQLSetConnectAttr** 를 호출 하 여 추적 파일을 지정 합니다. 추적을 사용 하는 경우 파일이 없으면 드라이버 관리자가 파일을 만듭니다. 경합을 방지 하려면 각 응용 프로그램에 자체 전용 추적 파일이 있어야 합니다. 응용 프로그램은 둘 이상의 추적 파일을 사용할 수 있습니다. 응용 프로그램의 설치 프로그램에서 사용자에 게 추적 파일을 선택할 수 있습니다. 추적을 동적으로 사용 하는 경우 응용 프로그램은 추적 파일에 기록 하는 대신 추적 결과를 표시할 수도 있습니다.  
  
 추적 파일은 모든 인수의 데이터 형식 및 값을 사용 하 여 각 ODBC 함수 호출에 대 한 로그를 제공 합니다. 모든 입력 함수를 기록 하 고 반환 된 모든 함수에 반환 코드 및 오류 상태를 기록 합니다.  
  
 ODBC 3.x에서 연결 함수에 *대 한 매개*변수는 추적 DLL에 제공 되지 않습니다.
