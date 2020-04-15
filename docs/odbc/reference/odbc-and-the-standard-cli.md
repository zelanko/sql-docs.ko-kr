---
title: ODBC 및 표준 CLI | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305144"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC 및 표준 CLI
ODBC는 CLI(통화 수준 인터페이스)를 처리하는 다음 사양 및 표준과 일치합니다. ODBC 기능은 이러한 각 표준의 수퍼셋입니다.  
  
-   개방형 그룹 CAE 사양 "데이터 관리: SQL 통화 수준 인터페이스(CLI)"  
  
-   ISO/IEC 9075-3:1995(E) 통화 수준 인터페이스(SQL/CLI)  
  
 이 정렬의 결과로 다음과 같은 것이 사실입니다.  
  
-   오픈 그룹 및 ISO CLI 사양에 기록된 응용 프로그램은 ODBC *3.x* 헤더 파일로 컴파일되고 ODBC *3.x* 라이브러리와 연결되고 ODBC 3.x 드라이버 관리자를 통해 드라이버에 액세스할 수 있는 경우 ODBC *3.x* 드라이버 또는 표준을 준수하는 드라이버와 함께 작동합니다. *3.x*  
  
-   오픈 그룹 및 ISO CLI 사양에 기록된 드라이버는 ODBC *3.x* 헤더 파일로 컴파일되고 ODBC *3.x* 라이브러리와 연결되고 응용 프로그램이 ODBC *3.x* 드라이버 관리자를 통해 드라이버에 액세스할 수 있는 경우 ODBC *3.x* 응용 프로그램 또는 표준을 준수하는 응용 프로그램과 함께 작동합니다. 자세한 내용은 표준을 [준수하는 응용 프로그램 및 드라이버를](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)참조하십시오.  
  
 코어 인터페이스 적합성 수준은 ISO CLI의 모든 기능과 오픈 그룹 CLI의 모든 선택 사항이 아닌 기능을 포함합니다. 오픈 그룹 CLI의 선택적 기능은 더 높은 인터페이스 적합성 수준에 나타납니다. 모든 ODBC *3.x* 드라이버는 코어 인터페이스 준수 수준에서 기능을 지원해야 하므로 다음과 같습니다.  
  
-   ODBC *3.x* 드라이버는 표준을 준수하는 응용 프로그램에서 사용하는 모든 기능을 지원합니다.  
  
-   ISO CLI의 기능과 Open 그룹 CLI의 선택 사항이 아닌 기능만 사용하는 ODBC *3.x* 응용 프로그램은 표준을 준수하는 모든 드라이버와 함께 작동합니다.  
  
 ODBC는 ISO/IEC 및 개방형 그룹 CLI 표준에 포함된 호출 수준 인터페이스 사양 외에도 다음 기능을 구현합니다. (이러한 기능 중 일부는 ODBC *3.x*이전에 ODBC 버전에 존재합니다.)  
  
-   단일 함수 호출로 멀티로 가져오기  
  
-   매개 변수 배열에 바인딩  
  
-   책갈피, 가변 길이 북마크, 대량 업데이트 및 불협화음 행의 책갈피 작업으로 삭제를 포함한 북마크 지원  
  
-   행 단위 바인딩  
  
-   바인딩 오프셋  
  
-   저장 프로시저 또는 **SQLExecute** 또는 **SQLExecDirect를** 통해 실행되는 SQL 문의 시퀀스로 SQL 문의 일괄 처리 지원  
  
-   정확하거나 대략적인 커서 행 개수  
  
-   위치 업데이트 및 삭제 작업 및 일괄 처리 된 업데이트 및 함수 호출 **(SQLSetPos)에**의해 삭제  
  
-   정보 스키마 뷰를 지원할 필요 없이 정보 스키마에서 정보를 추출하는 카탈로그 기능  
  
-   외부 조인, 스칼라 함수, 날짜 시간 리터럴, 인터벌 리터럴 및 저장 프로시저에 대한 이스케이프 시퀀스  
  
-   코드 페이지 번역 라이브러리  
  
-   드라이버의 ANSI 준수 수준 및 SQL 지원 보고  
  
-   구현 매개 변수 설명자의 온디맨드 자동 모집단  
  
-   향상된 진단 및 행 및 매개 변수 상태 배열  
  
-   날짜 시간, 간격, 숫자/소수점 및 64비트 정수 응용 프로그램 버퍼 형식  
  
-   비동기 실행  
  
-   이스케이프 시퀀스, 출력 매개 변수 바인딩 메커니즘 및 카탈로그 함수를 포함한 저장 프로시저 지원  
  
-   연결 특성 및 특성 검색 에 대한 지원을 포함한 연결 향상
