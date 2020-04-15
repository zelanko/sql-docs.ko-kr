---
title: DBMS 기반 드라이버 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e7b7b153d0b0cb0a3e6a3d738908b0039b95679
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306489"
---
# <a name="dbms-based-drivers"></a>DBMS 기반 드라이버
DBMS 기반 드라이버는 Oracle 또는 SQL Server와 같은 데이터 원본과 함께 사용되며 드라이버가 사용할 독립 실행형 데이터베이스 엔진을 제공합니다. 이러한 드라이버는 독립 실행형 엔진을 통해 물리적 데이터에 액세스합니다. 즉, SQL 문을 제출하고 엔진에서 결과를 검색합니다.  
  
 DBMS 기반 드라이버는 기존 데이터베이스 엔진을 사용하기 때문에 일반적으로 파일 기반 드라이버보다 쓰기가 더 쉽습니다. ODBC 호출을 네이티브 API 호출로 변환하여 DBMS 기반 드라이버를 쉽게 구현할 수 있지만 이로 인해 드라이버 속도가 느려집니다. DBMS 기반 드라이버를 구현하는 더 좋은 방법은 기본 데이터 스트림 프로토콜을 사용하는 것입니다. 예를 들어 SQL Server 드라이버는 DB 라이브러리(SQL Server의 기본 API)가 아닌 TDS(SQL Server의 데이터 스트림 프로토콜)를 사용해야 합니다. 이 규칙의 예외는 ODBC가 네이티브 API인 경우입니다. 예를 들어 Watcom SQL은 응용 프로그램과 동일한 컴퓨터에 상주하고 드라이버로 직접 로드되는 독립 실행형 엔진입니다.  
  
 DBMS 기반 드라이버는 데이터 원본이 서버 역할을 하는 클라이언트/서버 구성에서 클라이언트 역할을 합니다. 대부분의 경우 클라이언트(드라이버)와 서버(데이터 원본)는 서로 다른 컴퓨터에 상주하지만 둘 다 멀티태스킹 운영 체제를 실행하는 동일한 컴퓨터에 상주할 수 있습니다. 세 번째 가능성은 드라이버와 데이터 원본 사이에 있는 *게이트웨이입니다.* 게이트웨이는 한 DBMS를 다른 DBMS처럼 보이게 하는 소프트웨어입니다. 예를 들어 SQL Server를 사용하도록 작성된 응용 프로그램은 마이크로 의사 결정기 DB2 게이트웨이를 통해 DB2 데이터에 액세스할 수도 있습니다. 이 제품으로 인해 DB2가 SQL 서버처럼 보입니다.  
  
 다음 그림에서는 DBMS 기반 드라이버의 세 가지 구성을 보여 주며 있습니다. 첫 번째 구성에서 드라이버와 데이터 원본은 동일한 컴퓨터에 상주합니다. 두 번째로 드라이버와 데이터 원본은 서로 다른 컴퓨터에 상주합니다. 셋째, 드라이버와 데이터 원본은 서로 다른 컴퓨터에 상주하며 게이트웨이는 다른 컴퓨터에 상주합니다.  
  
 ![DBMS&#45;기반 드라이버에 대한 세 가지 구성](../../odbc/reference/media/pr07.gif "pr07")
