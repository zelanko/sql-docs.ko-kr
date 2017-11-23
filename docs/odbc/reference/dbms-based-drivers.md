---
title: "DBMS 기반 드라이버 | Microsoft Docs"
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
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b806f4c887af3f1ba80ee3321820e97dd336fad
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="dbms-based-drivers"></a>DBMS 기반 드라이버
드라이버가 DBMS 기반 드라이버에 대 한 독립 실행형 데이터베이스 엔진을 제공 하는 Oracle 또는 SQL Server와 같은 데이터 원본 사용 됩니다. 이러한 드라이버는 독립 실행형 엔진; 통해 실제 데이터에 액세스 즉, SQL 문을 제출 하며 엔진에서 결과 검색 합니다.  
  
 DBMS 기반 드라이버는 기존 데이터베이스 엔진을 사용 하기 때문에 일반적으로 더 쉽게 작성할 수 파일 기반 드라이버 보다 됩니다. 네이티브 API 호출에 대 한 ODBC 호출을 변환 하 여 DBMS 기반 드라이버를 쉽게 구현할 수 있지만이 인해 더 느린 드라이버입니다. DBMS 기반 드라이버를 구현 하는 더 나은 방법을 네이티브 API에서 수행 하는 작업은 일반적으로 기본 데이터 스트림 프로토콜을 사용 하는 것입니다. 예를 들어 SQL Server 드라이버는 Db-library (SQL Server에 대 한 네이티브 API) 하는 대신 TDS (데이터 스트림 SQL Server에 대 한 프로토콜)를 사용 해야 합니다. ODBC는 네이티브 API 경우이 규칙에는 예외가입니다. 예를 들어 Watcom SQL은 응용 프로그램과 동일한 컴퓨터에 상주 하며 드라이버로 직접 로드 되는 독립 실행형 엔진입니다.  
  
 DBMS 기반 드라이버 역할을 클라이언트는 클라이언트/서버 구성에 있는 데이터 원본 서버 역할을 합니다. 대부분의 경우에서 (데이터 원본) 서버와 클라이언트 (드라이버)에 있는 서로 다른 컴퓨터 둘 다 멀티태스킹 운영 체제를 실행 하는 동일한 컴퓨터에 있을 수 있지만 합니다. 세 번째 가능성은는 *게이트웨이* 드라이버 및 데이터 원본 사이 있는 합니다. 게이트웨이 다른 모양 하나의 DBMS 시키는 소프트웨어. 예를 들어 SQL Server를 사용 하도록 작성 된 응용 프로그램 데이터에 액세스할 수도 DB2 마이크로 Decisionware DB2 게이트웨이; 이 제품에는 d b 2를 SQL Server 같이 하면 됩니다.  
  
 다음은 DBMS 기반 드라이버의 세 가지 구성입니다. 첫 번째 구성 드라이버와 데이터 원본이 동일한 컴퓨터에 상주합니다. 두 번째, 드라이버 및 데이터 원본의 서로 다른 컴퓨터에 상주합니다. 세 번째, 드라이버 및 데이터 원본에 서로 다른 컴퓨터 있으며 게이트웨이 또 다른 시스템에 있는 해당 사이 배치 합니다.  
  
 ![DBMS에 대 한 세 가지 구성 &#45; 기반된 드라이버](../../odbc/reference/media/pr07.gif "pr07")
