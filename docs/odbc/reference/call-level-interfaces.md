---
title: 통화 수준 인터페이스 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4288a278f745d533c92d3d45892753ef1a74c2b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306544"
---
# <a name="call-level-interfaces"></a>호출 수준 인터페이스
SQL 문을 DBMS에 보내는 마지막 기술은 CLI(호출 수준 인터페이스)를 통해서입니다. 호출 수준 인터페이스는 응용 프로그램 프로그램에서 호출할 수 있는 DBMS 함수 라이브러리를 제공합니다. 따라서 SQL을 다른 프로그래밍 언어와 혼합하는 대신 호출 수준 인터페이스는 대부분의 프로그래머가 사용하는 데 익숙한 루틴 라이브러리(예: 문자열, I/O 또는 수학 라이브러리)와 유사합니다. 그러나 이러한 호출은 문서화되지 않았으며 예고 없이 변경될 수 있습니다.  
  
 통화 수준 인터페이스는 일반적으로 응용 프로그램(클라이언트)이 한 컴퓨터에 있고 DBMS(서버)가 다른 컴퓨터에 있는 클라이언트/서버 아키텍처에서 사용됩니다. 응용 프로그램은 로컬 시스템에서 CLI 함수를 호출하고 이러한 호출은 처리를 위해 네트워크를 통해 DBMS로 전송됩니다.  
  
 호출 수준 인터페이스는 SQL 문이 런타임에 처리하기 위해 DBMS에 전달되지만 포함된 SQL 문이 없고 사전 컴파일러가 필요하지 않다는 점에서 포함된 SQL 전체와 다릅니다.  
  
 호출 수준 인터페이스를 사용하면 일반적으로 다음 단계가 포함됩니다.  
  
1.  응용 프로그램은 DBMS에 연결하기 위해 CLI 함수를 호출합니다.  
  
2.  응용 프로그램은 SQL 문을 작성하고 버퍼에 배치합니다. 그런 다음 하나 이상의 CLI 함수를 호출하여 준비 및 실행을 위해 문을 DBMS에 보냅니다.  
  
3.  명령문이 SELECT 문인 경우 응용 프로그램은 CLI 함수를 호출하여 응용 프로그램 버퍼의 결과를 반환합니다. 일반적으로 이 함수는 한 번에 하나의 행 또는 하나의 데이터 열을 반환합니다.  
  
4.  응용 프로그램은 DBMS에서 연결을 끊기 위해 CLI 함수를 호출합니다.
