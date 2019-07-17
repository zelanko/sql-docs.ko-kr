---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6c37084ad91a931c4479ecf826c5cb554765412
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135669"
---
# <a name="call-level-interfaces"></a>호출 수준 인터페이스
DBMS SQL 문을 보내기 위한 최종 기술을 호출 수준 인터페이스 (CLI)를 통해 이루어집니다. 호출 수준 인터페이스를 응용 프로그램에서 호출할 수 있는 DBMS 함수 라이브러리를 제공 합니다. 따라서 다른 프로그래밍 언어를 사용 하 여 SQL을 혼합 하는 대신 호출 수준 인터페이스를 비슷합니다 대부분의 프로그래머와 같은 문자열, I/O 또는 3. 포함 된 SQL을 지원 하는 Dbms의에서 수학 라이브러리 사용에 익숙한 일상적인 라이브러리 호출 하 여 프리에서 생성 되는 호출 수준 인터페이스를 이미 있습니다. 그러나 이러한 호출은 문서화 되지 않은 정보 및 통지 없이 변경 됩니다.  
  
 호출 수준 인터페이스는 응용 프로그램 (클라이언트)는 한 컴퓨터에 상주 하며 DBMS (서버) 다른 컴퓨터에 있는 클라이언트/서버 아키텍처에서 자주 사용 됩니다. 응용 프로그램이 로컬 시스템에 CLI 함수를 호출 하 고 해당 호출 처리를 위해 DBMS를 네트워크를 통해 전송 됩니다.  
  
 호출 수준 인터페이스에는 SQL 문 실행 시 처리를 위해 DBMS에 전달 되지만 다른 embedded SQL에서 전체적으로 포함 된 SQL 문이 및 없습니다 다르거나 필요에 동적 SQL와 비슷합니다.  
  
 일반적으로 호출 수준 인터페이스를 사용 하 여 단계는 다음과 같습니다.  
  
1.  응용 프로그램에 DBMS를 연결할 CLI 함수를 호출 합니다.  
  
2.  응용 프로그램이 SQL 문이 빌드되고 버퍼에 배치 합니다. 다음 문을 준비 및 실행에 DBMS를 보낼 하나 이상의 CLI 함수를 호출 합니다.  
  
3.  문이 SELECT 문의 경우 응용 프로그램 응용 프로그램 버퍼에 결과 반환 하는 CLI 함수를 호출 합니다. 일반적으로이 함수는 한 번에 한 행 또는 데이터 열이 하나를 반환합니다.  
  
4.  DBMS에서 연결을 끊으려면 CLI 함수를 호출 하는 응용 프로그램.
