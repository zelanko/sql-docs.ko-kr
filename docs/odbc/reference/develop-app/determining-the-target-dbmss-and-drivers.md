---
title: 대상 Dbms 및 드라이버를 확인 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- target DBMSs and drivers in interoperability [ODBC]
- interoperability [ODBC], target dbmss and drivers
ms.assetid: 23bee0f6-e12a-4598-b34e-df11a8086829
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f275e344b49f62f1ecc55430c603c0f31f333aa6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="determining-the-target-dbmss-and-drivers"></a>대상 Dbms 및 드라이버를 확인합니다.
다음 질문을 고려해 야 응용 프로그램에 대 한 대상 Dbms 이란 이며, 이러한 Dbms를 지 원하는 어떤 드라이버를 사용할 수 있습니까? 때문에 일반 응용 프로그램 상호 운용 가능성이 높은 수, 대상 Dbms의 질문은 사용자 지정 및 세로 응용 프로그램에 가장 적합 합니다. 그러나 대상 드라이버 질문 드라이버 속도, 품질, 기능 지원 및 가용성에 있어 매우 다양 하기 때문에 모든 응용 프로그램에 적용 됩니다. 또한 드라이버 응용 프로그램과 함께 재배포할 수 있는지, 비용 및 라이선스 계획의 가용성을 고려해 야 할 합니다.  
  
 많은 사용자 지정 응용 프로그램에 대 한 대상 Dbms는 명확: 응용 프로그램 디자인 된 Dbms를 기존는 액세스 합니다. 이후의 마이그레이션을 계획 하는 Dbms 고려해 야 합니다. 그러나 이러한 응용 프로그램에 대 한 주요 질문은 드라이버 또는 드라이버를 사용 하는. 다른 사용자 지정 응용 프로그램-기존 DBMS에 액세스 하도록 설계 되지 않은 하는 보안-대상 Dbms의 기능 지원, 동시 사용자 지원, 드라이버 가용성 및 경제성에 따라 선택할 수 있습니다.  
  
 수직 응용 프로그램 대상 Dbms는 일반적으로 선택 하는 기능 지원, 드라이버 가용성 및 시장에 기초 합니다. 중소기업을 위해 설계 된 세로 응용 프로그램은 해당 비즈니스;를 위해 저렴 한 Dbms 예를 들어 대상으로 해야 합니다. Dbms를 사용 하는 기존 Dbms에 추가 된 기능을 광범위 하 게 대상 해야로 세로 응용 프로그램입니다.  
  
 대상 Dbms을 선택할 때는 데스크톱 및 서버 데이터베이스 간의 차이 고려해 야 합니다. DBASE, Paradox Btrieve 등 데스크톱 데이터베이스는 server 데이터베이스 보다 덜 강력 합니다. 일반적으로 대부분의 파일 기반 드라이버에 덜 강력한 SQL 엔진을 통해 액세스 됩니다, 때문에 종종 꽉 찬 트랜잭션이 지원 되지 않는, 더 적은 수의 동시 사용자를 지원 하며 SQL 제한 합니다. 그러나는 저렴 하며 큰에서 설치 된 자료.  
  
 서버 데이터베이스는 Oracle, DB2, 및 SQL Server 등 전체 트랜잭션 지원을 제공 하 고 여러 동시 사용자를 지원 하며 풍부한 sql이 합니다. 훨씬 더 비용이 많이 드는 되며 더 작은 설치 된 자료를 갖게 됩니다. 반면에 소프트웨어 가격 다소 더 작은 잠재적인 시장 오프셋 하는 방법은 더 높은 것으로 경향이 있습니다.  
  
 따라서 대상 Dbms 경우에 따라 응용 프로그램 및 응용 프로그램의 대상 시장에 필요한 기능에 따라 선택할 수 있습니다. 예를 들어 대기업 주문 입력 시스템 적절 한 트랜잭션이 지원 되지 않는 이러한 때문에 데스크톱 데이터베이스 대상화 하지 수도 있습니다. 중소기업을 위해 디자인 된 유사한 시스템 비용 기반으로 대부분의 서버 데이터베이스를 제외 되었을 수 있습니다. 및 일반 응용 프로그램 개발자는 모두 대상으로 하지만 서버 데이터베이스에 대 한 고급 기능을 사용 하지 않도록 수 있습니다.
