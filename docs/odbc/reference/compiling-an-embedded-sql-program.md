---
title: 포함 된 SQL 프로그램 컴파일 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb801dc532009410055b67031b3e036cc6b9c3d0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306534"
---
# <a name="compiling-an-embedded-sql-program"></a>Embedded SQL 프로그램 컴파일
포함 된 SQL 프로그램에는 SQL 및 호스트 언어 문이 혼합 되어 있으므로 호스트 언어의 컴파일러에 직접 제출할 수 없습니다. 대신 다단계 프로세스를 통해 컴파일됩니다. 이 프로세스는 제품과 제품의 차이점에도 불구 하 고 모든 제품에 대 한 단계는 거의 동일 합니다.  
  
 이 그림은 포함 된 SQL 프로그램을 컴파일하는 데 필요한 단계를 보여 줍니다.  
  
 ![포함된 SQL 프로그램을 컴파일하는 단계](../../odbc/reference/media/pr02.gif "pr02")  
  
 포함 된 SQL 프로그램을 컴파일하는 데는 5 단계가 포함 됩니다.  
  
1.  포함 된 SQL 프로그램은 프로그래밍 도구인 SQL 미리 컴파일된에 제출 됩니다. 미리 컴파일된는 프로그램을 검색 하 고 포함 된 SQL 문을 찾아서 처리 합니다. DBMS에서 지 원하는 각 프로그래밍 언어에 대해 다른 미리 컴파일된 필요 합니다. DBMS 제품은 일반적으로 C, 파스칼, COBOL, 포트란, Ada, PL/I 및 다양 한 어셈블리 언어를 비롯 한 하나 이상의 언어에 대해 precompilers를 제공 합니다.  
  
2.  미리 컴파일된는 두 개의 출력 파일을 생성 합니다. 첫 번째 파일은 포함 된 SQL 문을 제거 하는 소스 파일입니다. 미리 컴파일된는 프로그램 및 DBMS 간에 런타임 링크를 제공 하는 전용 DBMS 루틴에 대 한 호출을 대체 합니다. 일반적으로 이러한 루틴의 이름 및 호출 시퀀스는 미리 컴파일된 및 DBMS 에서만 인식 됩니다. DBMS에 대 한 공용 인터페이스가 아닙니다. 두 번째 파일은 프로그램에서 사용 되는 모든 포함 된 SQL 문의 복사본입니다. 이 파일을 데이터베이스 요청 모듈 또는 DBRM 라고도 합니다.  
  
3.  미리 컴파일된의 소스 파일 출력은 호스트 프로그래밍 언어 (예: C 또는 COBOL 컴파일러)에 대 한 표준 컴파일러에 전송 됩니다. 컴파일러는 소스 코드를 처리 하 고 개체 코드를 출력으로 생성 합니다. 이 단계는 DBMS 또는 SQL과는 관련이 없습니다.  
  
4.  링커는 컴파일러에 의해 생성 된 개체 모듈을 수락 하 고, 다양 한 라이브러리 루틴을 사용 하 여 연결 하 고, 실행 가능한 프로그램을 생성 합니다. 실행 프로그램에 연결 된 라이브러리 루틴에는 2 단계에서 설명 하는 소유 DBMS 루틴이 포함 됩니다.  
  
5.  미리 컴파일된에서 생성 된 데이터베이스 요청 모듈은 특수 바인딩 유틸리티에 전송 됩니다. 이 유틸리티는 SQL 문을 검사 하 고, 구문 분석 하 고, 유효성을 검사 하 고, 최적화 한 다음 각 문에 대 한 액세스 계획을 생성 합니다. 결과는 전체 프로그램에 대 한 결합 된 액세스 계획으로, 포함 된 SQL 문의 실행 가능 버전을 나타냅니다. 바인딩 유틸리티는 데이터베이스에 계획을 저장 합니다. 일반적으로 해당 계획을 사용 하는 응용 프로그램의 이름을 할당 합니다. 이 단계가 컴파일 타임에 발생 하는지, 아니면 런타임에 발생 하는지는 DBMS에 따라 결정 됩니다.  
  
 포함 된 SQL 프로그램을 컴파일하는 데 사용 되는 단계는 앞서 [SQL 문 처리](../../odbc/reference/processing-a-sql-statement.md)에 설명 된 단계와 매우 밀접 한 관련이 있습니다. 특히 미리 컴파일된는 호스트 언어 코드에서 SQL 문을 분리 하 고 바인딩 유틸리티는 SQL 문을 구문 분석 하 고 유효성을 검사 하 고 액세스 계획을 만듭니다. 컴파일 시간에 5 단계가 수행 되는 Dbms에서, SQL 문을 처리 하는 처음 네 단계는 컴파일 타임에 수행 되는 반면, 마지막 단계 (실행)는 런타임에 발생 합니다. 이러한 Dbms에서 쿼리를 실행 하는 것이 매우 빠릅니다.
