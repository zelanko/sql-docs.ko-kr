---
title: 포함 된 SQL 프로그램 컴파일 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 92c464cb751bccc4393c219f0312ec8a89691df1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="compiling-an-embedded-sql-program"></a>포함 된 SQL 프로그램 컴파일
포함된 된 SQL 프로그램에는 다양 한 SQL 및 호스트 언어 문 포함 된, 호스트 언어에 대 한 컴파일러에 직접 전송할 수 없습니다. 대신 다중 단계 프로세스를 통해 컴파일됩니다. 이 프로세스 다른 제품으로 있지만 단계는 대략 모든 제품에 대해 동일 합니다.  
  
 이 그림 포함된 된 SQL 프로그램을 컴파일하는 데 필요한 단계를 보여 줍니다.  
  
 ![포함된 된 SQL 프로그램을 컴파일하는 데 단계](../../odbc/reference/media/pr02.gif "pr02")  
  
 포함된 된 SQL 프로그램을 컴파일하 다섯 단계가 있습니다.  
  
1.  포함 된 SQL 프로그램 SQL 프리 프로그래밍 도구에 제출 됩니다. 프리는 프로그램 검사 포함 된 SQL 문을 찾아서 처리 합니다. 다른 프리 DBMS에서 지 원하는 각 프로그래밍 언어에 대 한 필요 합니다. DBMS 제품에는 일반적으로 C, Pascal, COBOL, 포트란, Ada, PL 포함 한 하나 이상의 언어에 대 한 precompilers 제공 / I, 및 다양 한 어셈블리 언어입니다.  
  
2.  프리 두 출력 파일을 생성합니다. 첫 번째 파일이 포함 된 SQL 문은 하이픈이 제거 되어 소스 파일을 보여 줍니다. 그 대신 프리 프로그램과 DBMS 간에 런타임에 링크를 제공 하는 전용 DBMS 루틴에 대 한 호출을 대체 합니다. 일반적으로 이름 및 이러한 루틴의 호출 시퀀스는 자신만 아는 프리 및 DBMS; 공용 인터페이스는 DBMS 하지 않습니다. 두 번째 파일은 모든 포함 된 SQL 문은 프로그램에서 사용할의 복사본입니다. 이 파일에는 데이터베이스 요청 모듈 또는 DBRM 라고도 합니다.  
  
3.  프리에서 출력 되는 원본 파일은 프로그래밍 언어 (예: C 또는 COBOL 컴파일러) 호스트에 대 한 표준 컴파일러에 제출 됩니다. 컴파일러는 소스 코드를 처리 하 고 출력으로 개체 코드를 생성 합니다. 이 단계는 DBMS와 또는 SQL로 실행 하도록 주지 참고 합니다.  
  
4.  링커는 컴파일러에 의해 생성 된 개체 모듈을 수용 하 고, 다양 한 라이브러리 루틴을 사용 하 여 연결 하 실행 프로그램을 생성 합니다. 실행 프로그램에 연결 하는 라이브러리 루틴은 2 단계에서 설명한 전용 DBMS 루틴을 포함 합니다.  
  
5.  프리에 의해 생성 된 데이터베이스 요청 모듈 특별 한 바인딩 유틸리티에 제출 됩니다. 이 유틸리티 SQL 문을 검사 하 여, 구문 분석, 유효성을 검사 하 고 최적화, 하 고 각 문에 대 한 액세스 계획을 생성 합니다. 결과 포함 된 SQL 문의 실행 된 버전을 나타내는 전체 프로그램에 대 한 결합 된 액세스 계획입니다. 바인딩 유틸리티는 일반적으로 사용 하 여 응용 프로그램의 이름을 할당 하는 데이터베이스에 계획을 저장 합니다. 이 단계에서 컴파일 타임 또는 런타임에 일어나 여부는 DBMS에 따라 달라 집니다.  
  
 포함된 된 SQL 프로그램을 컴파일하는 데 사용 하는 단계에서 이전에 설명 된 단계와 매우 밀접 하 게 상관 관계 지정 사라졌는지 [SQL 문 처리](../../odbc/reference/processing-a-sql-statement.md)합니다. 특히, 고 해당 데이터베이스 프리는 호스트 언어 코드에서 SQL 문을 구분 합니다. 바인딩 유틸리티 구문 분석 하 고 SQL 문을 유효성을 검사 하 고 액세스 계획을 만듭니다. Dbms 5 단계 발생 컴파일 타임에, SQL 문 처리의 처음 네 단계 수행 컴파일 타임에는 마지막 단계 (실행) 런타임 시 발생 하는 동안 됩니다. 이러한 Dbms 매우 빠르게에 쿼리 실행을 만드는 것과 효과가 있습니다.
