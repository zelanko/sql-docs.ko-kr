---
title: "ODBC 및 표준 CLI | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 068750e91f59a20976113277ad8871723d045acd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-and-the-standard-cli"></a>ODBC 및 표준 CLI
ODBC 사양 호출 수준 인터페이스 (CLI)으로 처리 하는 표준으로 맞춥니다. (이러한 표준의 각각의 상위 집합 ODBC 기능에는 있습니다.)  
  
-   Open Group CAE 사양 "데이터 관리: SQL 호출 수준 인터페이스 (CLI)"  
  
-   ISO/IEC 9075-3:1995 (E) 호출 수준 인터페이스 (CLI/SQL)  
  
 이 맞춤으로 인해 다음에 해당 합니다.  
  
-   ODBC 3은 Open Group 및 ISO CLI 사양에 작성 된 응용 프로그램 작동 합니다. *x* 드라이버 또는 ODBC 3로 컴파일할 때 표준 규격 드라이버입니다. *x* 헤더 파일 및 연결 된 ODBC 3. *x* 라이브러리가 ODBC 3를 통해 드라이버에 액세스할 때 및. *x* 드라이버 관리자입니다.  
  
-   Open Group 및 ISO CLI 사양을 작성 된 드라이버는 ODBC 3 작동할지*.x* 응용 프로그램 또는 ODBC 3로 컴파일할 때 표준 호환 응용 프로그램*.x* 헤더 파일 및 연결 ODBC 3*.x* 라이브러리, 응용 프로그램에서 ODBC 3를 통해 드라이버에 대 한 액세스를 획득 하는 경우 및*.x* 드라이버 관리자입니다. (자세한 내용은 참조 [표준 호환 응용 프로그램 및 드라이버](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)합니다.  
  
 핵심 인터페이스 규칙 수준 ISO CLI의 모든 기능 및 모든 nonoptional 기능 Open 그룹 CLI에 포함 됩니다. Open 그룹 CLI의 선택적 기능이 더 높은 인터페이스 받는 규칙 수준에 나타납니다. 때문에 모든 ODBC 3. *x* true, 드라이버는 핵심 인터페이스 규칙 수준에서 기능을 지 원하는 데 필요 합니다.  
  
-   ODBC 3입니다. *x* 드라이버는 표준 호환 응용 프로그램에서 사용 되는 모든 기능을 지원 합니다.  
  
-   ODBC 3입니다. *x* ISO CLI 기능만 및 Open 그룹 cli nonoptional 기능을 사용 하는 응용 프로그램 모든 표준 규격 드라이버를 사용 합니다.  
  
 ODBC는 ISO/IEC 및 Open 그룹 CLI 표준에 포함 된 호출 수준 인터페이스 사양, 외에도 다음과 같은 기능을 구현 합니다. (이러한 기능 중 일부에 있던 ODBC 3 이전 ODBC의 버전입니다. *x*.)  
  
-   단일 함수 호출을 통해 다중 행 인출  
  
-   매개 변수 배열에 바인딩  
  
-   업데이트 하 고 연속 하지 않는 행의 책갈피 작업으로 삭제 하는 책갈피, 가변 길이 책갈피 및 대량 가져오는 포함 하 여 책갈피 지원  
  
-   행 단위 바인딩  
  
-   오프셋 바인딩  
  
-   저장된 프로시저 또는 일련의 SQL 문을 통해 실행 된 SQL 문의 일괄 처리에 대 한 지원 **SQLExecute** 또는 **SQLExecDirect**  
  
-   정확한 수 또는 대략적인 커서 행 개수  
  
-   함수 호출에 의해 업데이트 및 삭제 작업 및 일괄 처리 된 업데이트 및 삭제를 배치 (**SQLSetPos**)  
  
-   정보 스키마 뷰를 지원 하기 위한 필요 없이 정보 스키마 정보를 추출 하는 카탈로그 함수  
  
-   외부 조인, 스칼라 함수, 날짜/시간 리터럴, 간격 리터럴 및 저장된 프로시저에 대 한 이스케이프 시퀀스  
  
-   코드 페이지 변환 라이브러리  
  
-   드라이버의 ANSI 규칙 수준과 SQL 지원 등의 보고  
  
-   구현 매개 변수 설명자의 자동 채우기를 요청 시  
  
-   향상 된 진단 및 행과 매개 변수 상태 배열을  
  
-   날짜/시간, 간격, decimal, numeric/및 64 비트 정수 응용 프로그램 버퍼 형식  
  
-   비동기 실행  
  
-   저장된 프로시저 이스케이프 시퀀스를 포함 하 여 출력 매개 변수 바인딩 메커니즘 지원과 카탈로그 함수  
  
-   연결 특성 및 특성 탐색에 대 한 지원을 비롯 하 여 연결 개선 사항

