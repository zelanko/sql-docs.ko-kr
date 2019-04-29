---
title: 대상 Dbms 및 드라이버 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- target DBMSs and drivers in interoperability [ODBC]
- interoperability [ODBC], target dbmss and drivers
ms.assetid: 23bee0f6-e12a-4598-b34e-df11a8086829
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 92da788205213394edc75257d8266752a2a9d8df
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63034950"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>대상 DBMS 및 드라이버 확인
고려해 야 할 다음 질문을 응용 프로그램의 경우 대상 Dbms는 무엇 이며, 해당 Dbms를 지 원하는 어떤 드라이버를 사용할 수 있습니까? 일반 응용 프로그램 상호 운용성이 매우 경향이, 대상 Dbms에 대 한 문제 이므로 사용자 지정 및 세로 응용 프로그램에 가장 적합 합니다. 그러나 대상 드라이버에 대 한 문제 드라이버 속도, 품질, 기능 지원 및 가용성에 있어 매우 다양 하기 때문에 모든 응용 프로그램에 적용 됩니다. 또한 드라이버 응용 프로그램을 사용 하 여 다시 배포 될 경우의 비용 및 라이선스 계획의 가용성을 고려해 야 할 합니다.  
  
 많은 사용자 지정 응용 프로그램에 대 한 대상 Dbms는 확실 한: 이러한 응용 프로그램 설계 된 Dbms는 기존에 액세스 합니다. Dbms는 향후 마이그레이션 계획은 고려해 야 합니다. 그러나 이러한 응용 프로그램에 대 한 주요 질문은 드라이버 또는 드라이버를 사용 하는 합니다. -있는 기존는 DBMS에 액세스 하도록 설계 되지-다른 사용자 지정 응용 프로그램에 대 한 대상 Dbms 선택할 수 있습니다 기능 지원, 동시 사용자 지원, 드라이버 가용성 및 경제성 기반으로 합니다.  
  
 세로 응용 프로그램의 경우 Dbms는 일반적으로 선택한 대상 지원 되는 기능, 드라이버 가용성 및 시장에 기반 합니다. 중소기업을 위해 설계 된 세로 응용 프로그램을 경제적으로 이러한 기업은; 된 Dbms 예를 들어 대상으로 해야 합니다. Dbms를 사용 하는 세로 응용 프로그램을 광범위 하 게 대상 기존 Dbms에 추가 된 기능으로 디자인 되었습니다.  
  
 대상 Dbms를 선택한 경우에 데스크톱 및 서버 데이터베이스 간의 차이점을 고려 되어야 합니다. Paradox, dBASE와 Btrieve 데스크톱 데이터베이스는 server 데이터베이스 보다 덜 강력 합니다. 일반적으로 대부분의 파일 기반 드라이버에 덜 강력한 SQL 엔진을 통해 액세스할 수 있는, 때문에 동시 사용자 수가 적은 지원 하며 SQL 제한 된 전체 트랜잭션 지원이 부족 경우도 많습니다. 그러나 이러한 비용이 별로 들지 않습니다 않으며, 큰 설치 자료가 있어야 합니다.  
  
 Oracle, DB2 및 SQL Server와 같은 서버 데이터베이스 많은 동시 사용자를 지원 하며가 다양 한 SQL 꽉 찬 트랜잭션 지원을 제공 합니다. 훨씬 더 비용이 많이 드는 되며 작은 설치 기반을 갖습니다. 다른 한편으로 소프트웨어 가격 약간 잠재적인 더 작은 시장 오프셋 높을 수 하는 경향이 있습니다.  
  
 따라서 대상 Dbms 경우에 따라 응용 프로그램 및 응용 프로그램의 대상 시장에 필요한 기능에 따라 선택할 수 있습니다. 예를 들어 대기업에 대 한 주문 입력 시스템 적절 한 트랜잭션 지원을이 없기 때문에 데스크톱 데이터베이스를 대상 하지 할 수 있습니다. 중소기업을 위해 설계 된 유사한 시스템 비용 기준으로 대부분의 서버 데이터베이스를 제외 되었을 수 있습니다. 및 일반 응용 프로그램의 개발자 모두를 대상으로 하지만 서버 데이터베이스에 있는 고급 기능을 사용 하지 않도록 수 있습니다.
