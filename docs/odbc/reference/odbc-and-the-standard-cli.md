---
title: ODBC 및 표준 CLI | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: adddf32a29d3a891a4a2c6fb2353648e62b0d9c5
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794099"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC 및 표준 CLI
ODBC 사양 호출 수준 인터페이스 (CLI)으로 처리 하는 표준으로 맞춥니다. (ODBC 기능은 이러한 표준의 각 상위 집합입니다.)  
  
-   Open Group CAE 사양 "데이터 관리: SQL 호출 수준 인터페이스 (CLI) "  
  
-   ISO/IEC 9075-3:1995 (E) 호출 수준 인터페이스 (SQL/CLI)  
  
 이 맞춤으로 인해 다음에 해당 합니다.  
  
-   ODBC를 사용 하 여 Open Group 및 ISO CLI 사양에 작성 된 응용 프로그램 작동 *3.x* 드라이버나 ODBC를 사용 하 여 컴파일할 때 표준 규격 드라이버 *3.x* 헤더 파일 및 연결 ODBC *3.x* 라이브러리를 통해 ODBC 드라이버에 대 한 액세스를 얻을 때와 *3.x* 드라이버 관리자입니다.  
  
-   Open Group 및 ISO CLI 사양에 작성 된 드라이버는 ODBC를 사용 하 여 작동 *3.x* 응용 프로그램 또는 ODBC를 사용 하 여 컴파일할 때 표준 호환 응용 프로그램 *3.x* 헤더 파일 및 연결 ODBC를 사용 하 여 *3.x* 라이브러리 및 응용 프로그램에서 ODBC 통해 드라이버에 대 한 액세스를 향상 하는 경우 *3.x* 드라이버 관리자입니다. (자세한 내용은 [표준 호환 응용 프로그램 및 드라이버](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)합니다.  
  
 핵심 인터페이스 적합성 수준 ISO CLI의 모든 기능 및 열린 그룹 CLI에서 모든 nonoptional 기능을 포함합니다. 선택적 기능의 그룹 CLI를 열고 상위 인터페이스 적합성 수준에 나타납니다. 때문에 모든 ODBC *3.x* 드라이버는 핵심 인터페이스 적합성 수준에서 기능을 지 원하는 데 필요한, 다음은 true입니다.  
  
-   ODBC *3.x* 드라이버는 표준 호환 응용 프로그램에서 사용 되는 모든 기능을 지원 합니다.  
  
-   ODBC *3.x* ISO CLI에서 기능만 및 nonoptional 기능의 열기 그룹 CLI를 사용 하 여 응용 프로그램이 표준 호환 드라이버를 사용 하 여 작동 합니다.  
  
 ISO/IEC 및 열린 그룹 CLI 표준에 포함 된 호출 수준 인터페이스 사양, 외에도 ODBC는 다음 기능을 구현 합니다. (이러한 기능 중 일부 이전 ODBC는 ODBC의 버전에 존재 *3.x*.)  
  
-   단일 함수 호출 하 여 다중 행 인출  
  
-   매개 변수 배열에 바인딩  
  
-   책갈피 지원 책갈피, 가변 길이 책갈피 및 대량으로 가져오는 포함 하 여 업데이트 및 연속 하지 않는 행에서 책갈피 작업 삭제  
  
-   행 단위 바인딩  
  
-   바인딩 오프셋  
  
-   저장된 프로시저 또는 SQL 문을 통해 실행 시퀀스로 SQL 문의 일괄 처리에 대 한 지원을 **SQLExecute** 또는 **SQLExecDirect**  
  
-   커서를 정확 하거나 대략적인 행 개수  
  
-   위치 지정 업데이트 및 삭제 작업 및 일괄 처리 된 업데이트 및 삭제 함수 호출에서 (**SQLSetPos**)  
  
-   정보 스키마 뷰 지원 없이 정보 스키마에서 정보를 추출 하는 카탈로그 함수  
  
-   외부 조인, 스칼라 함수, 날짜/시간 리터럴, 간격 리터럴 및 저장된 프로시저에 대 한 이스케이프 시퀀스  
  
-   코드 페이지 변환 라이브러리  
  
-   드라이버의 ANSI 규칙 수준 및 SQL 지원 보고  
  
-   주문형 구현 매개 변수 설명자의 자동 채우기  
  
-   향상 된 진단 및 매개 변수 및 행 상태 배열  
  
-   날짜/시간, 간격, decimal/numeric, 및 64 비트 정수 응용 프로그램 버퍼 형식  
  
-   비동기 실행  
  
-   저장된 프로시저 지원, 이스케이프 시퀀스를 포함 하 여 출력 매개 변수 바인딩 메커니즘 및 카탈로그 함수  
  
-   연결 특성 및 특성 탐색에 대 한 연결을 비롯 한 향상을 지원 합니다.
