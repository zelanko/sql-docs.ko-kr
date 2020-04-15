---
title: 임베디드 SQL 프로그램 컴파일 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306534"
---
# <a name="compiling-an-embedded-sql-program"></a>Embedded SQL 프로그램 컴파일
포함된 SQL 프로그램에는 SQL 및 호스트 언어 문이 혼합되어 있으므로 호스트 언어에 대한 컴파일러에 직접 제출할 수 없습니다. 대신 다단계 프로세스를 통해 컴파일됩니다. 이 프로세스는 제품마다 다르지만 모든 제품에 대해 단계는 거의 동일합니다.  
  
 이 그림에서는 포함된 SQL 프로그램을 컴파일하는 데 필요한 단계를 보여 주며 있습니다.  
  
 ![포함된 SQL 프로그램을 컴파일하는 단계](../../odbc/reference/media/pr02.gif "pr02")  
  
 포함된 SQL 프로그램을 컴파일하는 데 는 다섯 단계가 있습니다.  
  
1.  임베디드 SQL 프로그램은 프로그래밍 도구인 SQL 프리컴파일러에 제출됩니다. 사전 컴파일러는 프로그램을 검사하고 포함된 SQL 문을 찾아 처리합니다. DBMS에서 지원하는 각 프로그래밍 언어에 대해 다른 사전 컴파일러가 필요합니다. DBMS 제품은 일반적으로 C, 파스칼, 코볼, 포트란, Ada, PL/I 및 다양한 어셈블리 언어를 포함하여 하나 이상의 언어에 대한 사전 컴파일러를 제공합니다.  
  
2.  사전 컴파일러는 두 개의 출력 파일을 생성합니다. 첫 번째 파일은 포함된 SQL 문을 제거한 원본 파일입니다. 그 자리에서 프리컴파일러는 프로그램과 DBMS 간의 런타임 링크를 제공하는 독점 DBMS 루틴을 대체합니다. 일반적으로 이러한 루틴의 이름과 호출 시퀀스는 프리컴파일러와 DBMS에만 알려져 있습니다. DBMS에 대한 공용 인터페이스가 아닙니다. 두 번째 파일은 프로그램에 사용된 모든 포함된 SQL 문의 복사본입니다. 이 파일을 데이터베이스 요청 모듈 또는 DBRM이라고도 합니다.  
  
3.  사전 컴파일러의 소스 파일 출력은 호스트 프로그래밍 언어(예: C 또는 COBOL 컴파일러)의 표준 컴파일러에 제출됩니다. 컴파일러는 소스 코드를 처리하고 개체 코드를 출력으로 생성합니다. 이 단계는 DBMS 또는 SQL과는 아무 관련이 없습니다.  
  
4.  링커는 컴파일러에서 생성된 개체 모듈을 수락하고 다양한 라이브러리 루틴과 연결하고 실행 프로그램을 생성합니다. 실행 프로그램에 연결된 라이브러리 루틴에는 2단계에서 설명된 독점적인 DBMS 루틴이 포함됩니다.  
  
5.  사전 컴파일러에서 생성된 데이터베이스 요청 모듈이 특수 바인딩 유틸리티에 제출됩니다. 이 유틸리티는 SQL 문을 검사하고, 구문 분석하고, 유효성을 검사하고, 최적화한 다음 각 명령문에 대한 액세스 계획을 생성합니다. 그 결과 포함된 SQL 문의 실행 버전을 나타내는 전체 프로그램에 대한 통합 액세스 계획이 생성됩니다. 바인딩 유틸리티는 계획을 데이터베이스에 저장하며 일반적으로 계획을 사용할 응용 프로그램 이름을 할당합니다. 이 단계가 컴파일 타임또는 런타임에 발생하는지 여부는 DBMS에 따라 다릅니다.  
  
 임베디드 SQL 프로그램을 컴파일하는 데 사용되는 단계는 SQL [문 처리의](../../odbc/reference/processing-a-sql-statement.md)앞에서 설명한 단계와 매우 밀접하게 연관되어 있습니다. 특히 사전 컴파일러는 호스트 언어 코드에서 SQL 문을 분리하고 바인딩 유틸리티는 SQL 문을 구문 분석및 유효성 검사하고 액세스 계획을 만듭니다. 5단계가 컴파일 시간에 수행되는 DBMS에서는 SQL 문을 처리하는 처음 네 단계가 컴파일 시간에 수행되는 반면 마지막 단계(실행)는 런타임에 수행됩니다. 이는 이러한 DBMS에서 쿼리 실행을 매우 빠르게 만드는 효과가 있습니다.
