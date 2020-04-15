---
title: 추적 파일 | 마이크로 소프트 문서
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
ms.openlocfilehash: ddd0ee24649592cf4a1a296a51404334145a3bab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298060"
---
# <a name="trace-file"></a>추적 파일
응용 프로그램은 Odbc.ini 레지스트리 항목에서 **TraceFile** 키워드를 설정하거나 **SQLSetConnectAttr을** SQL_ATTR_TRACEFILE 연결 특성으로 호출하여 추적 파일을 지정합니다. 추적을 사용하도록 설정할 때 파일이 존재하지 않는 경우 드라이버 관리자가 파일을 만듭니다. 각 응용 프로그램에는 경합을 방지하기 위해 고유한 전용 추적 파일이 있어야 합니다. 응용 프로그램은 두 개 이상의 추적 파일을 사용할 수 있습니다. 응용 프로그램의 설치 프로그램은 사용자에게 추적 파일을 선택할 수 있습니다. 추적이 동적으로 활성화된 경우 응용 프로그램은 추적 파일에 로깅하는 대신 추적 결과를 표시할 수도 있습니다.  
  
 추적 파일은 모든 인수의 데이터 형식 및 값을 사용하여 각 ODBC 함수 호출의 로그를 제공합니다. 모든 입력 함수를 기록하고 반환 된 모든 함수를 반환 코드 및 오류 상태로 기록합니다.  
  
 ODBC *3.x에서*연결 함수에 대한 매개 변수는 추적 DLL에 제공되지 않습니다.
