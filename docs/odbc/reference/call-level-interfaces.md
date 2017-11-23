---
title: "호출 수준 인터페이스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 051a94e77b5a53d2a87b3310048da9f8d67260fd
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="call-level-interfaces"></a>호출 수준 인터페이스
DBMS SQL 문을 보내기 위한 final 기술은 호출 수준 인터페이스 (CLI)를 통해는 합니다. 호출 수준 인터페이스 응용 프로그램에서 호출할 수 있는 DBMS 함수 라이브러리를 제공 합니다. 따라서 다른 프로그래밍 언어와 SQL 결합을 하려고 하지 않고 호출 수준 인터페이스가 비슷합니다를 사용 하 여 문자열, I/O, 또는 3. note embedded SQL을 지 원하는 해당 Dbms 수학 라이브러리와 같은 대부분의 프로그래머가 쉽게는 대개 일상적인 라이브러리 호출 프리에 의해 생성 된 경우 호출 수준 인터페이스를 이미 있습니다. 그러나 이러한 호출은 문서화 되지 않은 정보 및 예 고 없이 변경 될 수 있습니다.  
  
 호출 수준 인터페이스는 응용 프로그램 (클라이언트) 있고에 있는 한 대의 컴퓨터 (서버) DBMS 다른 컴퓨터에 클라이언트/서버 아키텍처에 일반적으로 사용 됩니다. 로컬 시스템에서 CLI 함수를 호출 하는 응용 프로그램 하 고 해당 호출이 처리를 위해 DBMS를 네트워크를 통해 전송 됩니다.  
  
 호출 수준 인터페이스는 동적 SQL, 비슷합니다 SQL 문 실행 시 처리를 위해 DBMS에 전달 되 하지만 다릅니다 embedded SQL을 전체적으로 없는 프리가 필요 하 고 포함 된 SQL 문이 없습니다.  
  
 호출 수준 인터페이스를 사용 하 여 일반적으로 다음 단계가 포함 됩니다.  
  
1.  응용 프로그램은 DBMS에 연결 하는 CLI 함수를 호출 합니다.  
  
2.  응용 프로그램 SQL 문을 작성 하 고 버퍼에 배치 합니다. 다음 문을 준비 및 실행을 위한 DBMS에 보낼 하나 이상의 CLI 함수를 호출 합니다.  
  
3.  문이 SELECT 문의 경우 응용 프로그램이 응용 프로그램 버퍼에 결과 반환 하는 CLI 함수를 호출 합니다. 일반적으로이 함수는 한 번에 한 행 또는 하나의 데이터 열을를 반환합니다.  
  
4.  응용 프로그램 DBMS에서 연결을 끊을 CLI 함수를 호출 합니다.
