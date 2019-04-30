---
title: DBMS 기반 드라이버 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc35f7bceff2d9e92b70448040bb602117b76c84
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63186291"
---
# <a name="dbms-based-drivers"></a>DBMS 기반 드라이버
DBMS 기반 드라이버는 드라이버 사용에 대 한 독립 실행형 데이터베이스 엔진을 제공 하는 Oracle 또는 SQL Server와 같은 데이터 원본 사용 됩니다. 이러한 드라이버는 독립 실행형 엔진이; 통해 실제 데이터에 액세스 즉, SQL 문을 제출 하며 엔진에서 결과 검색 합니다.  
  
 DBMS 기반 드라이버는 기존 데이터베이스 엔진을 사용 하기 때문에 일반적으로 더 쉽게 작성할 수 파일 기반 드라이버 보다 됩니다. 네이티브 API 호출에 대 한 ODBC 호출을 변환 하 여 DBMS 기반 드라이버를 쉽게 구현할 수 있지만이 인해 느린 드라이버입니다. DBMS 기반 드라이버를 구현 하는 더 나은 방법을 일반적으로 네이티브 API를 수행 하는 기본 데이터 스트림 프로토콜을 사용 하는 것입니다. 예를 들어, SQL Server 드라이버는 Db-library (SQL Server에 대 한 네이티브 API) 대신 TDS (데이터를 SQL Server에 대 한 프로토콜을 스트림 하는 데 사용)을 사용 해야 합니다. ODBC는 네이티브 API 하는 경우이 규칙에는 예외가입니다. 예를 들어 Watcom SQL은 응용 프로그램과 동일한 컴퓨터에 있고 드라이버도 직접 로드 되는 독립 실행형 엔진입니다.  
  
 DBMS 기반 드라이버는 데이터 원본 서버로 작동 하는 위치 클라이언트/서버 구성에서 클라이언트와 작동 합니다. 대부분의 경우에서 (드라이버) 클라이언트와 서버 (데이터 원본)에 서로 다른 컴퓨터에서 멀티태스킹 운영 체제를 실행 하는 동일한 컴퓨터에서 둘 다 수 있지만. 세 번째 가능성은는 *게이트웨이* 드라이버 및 데이터 원본 사이입니다. 게이트웨이 일종의 다른 모양 하나 DBMS는 소프트웨어입니다. 예를 들어, SQL Server를 사용 하도록 작성 된 응용 프로그램 데이터에 액세스할 수도 DB2 마이크로 Decisionware DB2 게이트웨이; 이 제품에는 SQL Server 같은 DB2 발생 합니다.  
  
 다음 그림에서는 DBMS 기반 드라이버의 세 가지 다른 구성을 보여 줍니다. 첫 번째 구성을 드라이버와 데이터 원본이 동일한 컴퓨터에 상주합니다. 두 번째, 드라이버 및 데이터 원본의 서로 다른 컴퓨터에 상주합니다. 세 번째 서로 다른 컴퓨터에 상주 하는 드라이버 및 데이터 원본에 게이트웨이 아직 다른 컴퓨터에 있는 해당 사이입니다.  
  
 ![DBMS에 대 한 세 가지 구성&#45;기반 드라이버](../../odbc/reference/media/pr07.gif "pr07")
