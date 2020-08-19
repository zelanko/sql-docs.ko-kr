---
description: 호출 수준 인터페이스
title: 호출 수준 인터페이스 | Microsoft Docs
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
ms.openlocfilehash: ad1e89f945dbb739c4c20103fc2330cbf4e562b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448961"
---
# <a name="call-level-interfaces"></a>호출 수준 인터페이스
DBMS에 SQL 문을 전송 하는 최종 방법은 CLI (호출 수준 인터페이스)를 통하는 것입니다. 호출 수준 인터페이스는 응용 프로그램에서 호출할 수 있는 DBMS 함수 라이브러리를 제공 합니다. 따라서 SQL을 다른 프로그래밍 언어와 혼합 하는 대신 호출 수준 인터페이스는 C의 문자열, i/o 또는 수학 라이브러리와 같이 대부분의 프로그래머가 사용 하는 데 익숙한 일상적인 라이브러리와 비슷합니다. 포함 된 SQL을 지 원하는 Dbms에는 미리 컴파일된에서 생성 되는 호출에 대 한 호출 수준 인터페이스가 이미 있습니다. 그러나 이러한 호출은 문서화 되지 않으며 예 고 없이 변경 될 수 있습니다.  
  
 호출 수준 인터페이스는 응용 프로그램 프로그램 (클라이언트)이 한 대의 컴퓨터에 상주 하 고 DBMS (서버)가 다른 컴퓨터에 상주 하는 클라이언트/서버 아키텍처에서 일반적으로 사용 됩니다. 응용 프로그램은 로컬 시스템에서 CLI 함수를 호출 하 고, 이러한 호출은 처리를 위해 네트워크를 통해 DBMS에 전송 됩니다.  
  
 호출 수준 인터페이스는 동적 SQL과 유사 하지만, SQL 문이 런타임에 처리를 위해 DBMS로 전달 되지만 포함 된 SQL 문이 없고 미리 컴파일된가 필요 하지 않은 경우에 전체 포함 된 SQL과는 다릅니다.  
  
 일반적으로 호출 수준 인터페이스를 사용 하려면 다음 단계를 수행 해야 합니다.  
  
1.  응용 프로그램은 DBMS에 연결 하기 위해 CLI 함수를 호출 합니다.  
  
2.  응용 프로그램은 SQL 문을 작성 하 여 버퍼에 배치 합니다. 그런 다음 하나 이상의 CLI 함수를 호출 하 여 준비 및 실행을 위해 문을 DBMS로 보냅니다.  
  
3.  문이 SELECT 문인 경우 응용 프로그램은 CLI 함수를 호출 하 여 결과를 응용 프로그램 버퍼에 반환 합니다. 일반적으로이 함수는 한 번에 하나의 행 또는 한 개의 데이터 열을 반환 합니다.  
  
4.  응용 프로그램은 CLI 함수를 호출 하 여 DBMS와의 연결을 끊습니다.
