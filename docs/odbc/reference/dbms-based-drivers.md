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
ms.openlocfilehash: fcd2221d9a0bb9cba42745901e5f00a6f8c8415e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68111254"
---
# <a name="dbms-based-drivers"></a>DBMS 기반 드라이버
DBMS 기반 드라이버는 Oracle 또는 SQL Server와 같은 데이터 원본에 사용 되며 드라이버에서 사용할 수 있는 독립 실행형 데이터베이스 엔진을 제공 합니다. 이러한 드라이버는 독립 실행형 엔진을 통해 실제 데이터에 액세스 합니다. 즉,에 SQL 문을 전송 하 고 엔진에서 결과를 검색 합니다.  
  
 DBMS 기반 드라이버는 기존 데이터베이스 엔진을 사용 하므로 일반적으로 파일 기반 드라이버 보다 더 쉽게 작성할 수 있습니다. ODBC 호출을 네이티브 API 호출로 변환 하 여 DBMS 기반 드라이버를 쉽게 구현할 수 있지만이로 인해 드라이버는 느려집니다. DBMS 기반 드라이버를 구현 하는 더 좋은 방법은 기본 API에서 주로 사용 하는 기본 데이터 스트림 프로토콜을 사용 하는 것입니다. 예를 들어 SQL Server 드라이버는 DB 라이브러리가 아닌 TDS (SQL Server의 데이터 스트림 프로토콜)를 사용 해야 합니다 (SQL Server의 기본 API). 이 규칙의 예외는 ODBC가 네이티브 API 인 경우입니다. 예를 들어 Watcom SQL은 응용 프로그램과 동일한 컴퓨터에 상주 하 고 드라이버로 직접 로드 되는 독립 실행형 엔진입니다.  
  
 DBMS 기반 드라이버는 클라이언트/서버 구성에서 데이터 원본이 서버 역할을 하는 클라이언트 역할을 합니다. 대부분의 경우 클라이언트 (드라이버) 및 서버 (데이터 원본)는 멀티태스킹 운영 체제를 실행 하는 동일한 컴퓨터에 있을 수 있지만 서로 다른 컴퓨터에 있습니다. 세 번째 가능성은 드라이버와 데이터 원본 사이에 배치 되는 *게이트웨이입니다* . 게이트웨이는 하나의 DBMS가 다른 DBMS와 같이 보이도록 하는 소프트웨어의 일부입니다. 예를 들어 SQL Server 사용 하도록 작성 된 응용 프로그램은 마이크로 Decisionware DB2 게이트웨이를 통해 DB2 데이터에도 액세스할 수 있습니다. 이 제품을 통해 DB2는 SQL Server 같이 표시 됩니다.  
  
 다음 그림에서는 DBMS 기반 드라이버의 세 가지 구성을 보여 줍니다. 첫 번째 구성에서는 드라이버와 데이터 원본이 동일한 컴퓨터에 상주 합니다. 두 번째에서는 드라이버와 데이터 원본이 서로 다른 컴퓨터에 상주 합니다. 세 번째 방법에서는 드라이버와 데이터 원본이 서로 다른 컴퓨터에 있으며, 다른 컴퓨터에 있는 게이트웨이 사이에 존재 합니다.  
  
 ![DBMS&#45;기반 드라이버에 대 한 세 가지 구성](../../odbc/reference/media/pr07.gif "pr07")
