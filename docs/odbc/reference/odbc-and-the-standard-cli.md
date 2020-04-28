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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56dc0ac73c77cbbb77943d2e9ba308796b259dbb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305144"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC 및 표준 CLI
ODBC는 CLI (호출 수준 인터페이스)를 처리 하는 다음 사양 및 표준에 부합 합니다. ODBC 기능은 이러한 각 표준의 상위 집합입니다.  
  
-   Open Group CAE Specification "데이터 관리: SQL 호출 수준 인터페이스 (CLI)"  
  
-   ISO/IEC 9075-3:1995 (E) 호출 수준 인터페이스 (SQL/CLI)  
  
 이 정렬의 결과로 다음이 적용 됩니다.  
  
-   Open Group 및 ISO CLI 사양에 작성 된 응용 프로그램 *은 odbc 3.x* 드라이버를 사용 하 여 컴파일되고 *, odbc 2.x 라이브러리와* 연결 된 경우 *및 odbc 3.x 드라이버 관리자* 를 통해 드라이버에 대 한 액세스 권한을 얻는 경우에 사용 *됩니다.*  
  
-   Open Group 및 ISO CLI 사양에 작성 된 드라이버는 odbc *3.x 응용 프로그램* 또는 표준 규격 응용 프로그램 *에서 odbc 2.x 헤더 파일* 을 사용 하 여 *컴파일되고 odbc 3.x 라이브러리에* 연결 된 경우와 응용 프로그램이 odbc *2.x 드라이버 관리자를 통해 드라이버에* 액세스할 수 있는 경우에 작동 합니다. 자세한 내용은 [표준 규격 응용 프로그램 및 드라이버](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)를 참조 하세요.  
  
 핵심 인터페이스 규칙 수준은 ISO CLI의 모든 기능과 오픈 그룹 CLI의 모든 비 선택적 기능을 포함 합니다. Open Group CLI의 선택적 기능은 상위 인터페이스 규칙 수준에서 나타납니다. 모든 ODBC 2.x 드라이버는 핵심 인터페이스 규칙 수준의 기능을 지 원하는 데 필요 하기 때문에 다음이 적용 *됩니다.*  
  
-   ODBC 3.x 드라이버는 표준 규격 응용 프로그램에서 사용 하는 모든 기능을 지원 *합니다.*  
  
-   ISO CLI의 기능만 사용 하 *는 ODBC 2.x* 응용 프로그램 및 오픈 그룹 CLI의 선택적 기능은 모든 표준 규격 드라이버에서 작동 합니다.  
  
 ISO/IEC 및 오픈 그룹 CLI 표준에 포함 된 호출 수준 인터페이스 사양 외에도 ODBC는 다음과 같은 기능을 구현 합니다. 이러한 기능 중 일부 *는 odbc 3.x*이전의 odbc 버전에 있었습니다.  
  
-   단일 함수 호출로 다중 행 페치  
  
-   매개 변수 배열에 바인딩  
  
-   책갈피, 가변 길이 책갈피 및 불연속 행에서 책갈피 작업에의 한 대량 업데이트 및 삭제를 포함 한 책갈피 지원  
  
-   행 단위 바인딩  
  
-   바인딩 오프셋  
  
-   저장 프로시저 또는 **Sqlexecute** 또는 **sqlexecdirect** 를 통해 실행 되는 sql 문 시퀀스로 sql 문 일괄 처리 지원  
  
-   정확히 또는 대략적인 커서 행 개수  
  
-   위치 지정 업데이트 및 삭제 작업 및 함수 호출에의 한 일괄 처리 업데이트 및 삭제 (**SQLSetPos**)  
  
-   정보 스키마 뷰를 지원 하지 않고 정보 스키마에서 정보를 추출 하는 카탈로그 함수  
  
-   외부 조인, 스칼라 함수, 날짜/시간 리터럴, 간격 리터럴 및 저장 프로시저에 대 한 이스케이프 시퀀스  
  
-   코드 페이지 변환 라이브러리  
  
-   드라이버의 ANSI 규칙 수준 및 SQL 지원 보고  
  
-   구현 매개 변수 설명자의 주문형 자동 채우기  
  
-   향상 된 진단 및 행 및 매개 변수 상태 배열  
  
-   Datetime, interval, numeric/decimal 및 64 비트 정수 응용 프로그램 버퍼 형식  
  
-   비동기 실행  
  
-   이스케이프 시퀀스, 출력 매개 변수 바인딩 메커니즘 및 카탈로그 함수를 비롯 한 저장 프로시저 지원  
  
-   연결 특성 및 특성 검색에 대 한 지원을 포함 하는 연결 향상
