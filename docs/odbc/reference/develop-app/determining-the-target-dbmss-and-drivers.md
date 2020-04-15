---
title: 대상 DBMS 및 드라이버 결정 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f8811e4d289a8fc89c2c3773aab973df523025f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305874"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>대상 DBMS 및 드라이버 확인
다음으로 고려해야 할 질문은 응용 프로그램의 대상 DBMS가 무엇이며 이러한 DBMS를 지원하는 드라이버를 사용할 수 있는지입니다. 일반 응용 프로그램은 상호 운용성이 매우 높은 경향이 있으므로 대상 DBMS의 문제는 사용자 지정 및 수직 응용 프로그램에 가장 많이 적용됩니다. 그러나 대상 드라이버의 문제는 드라이버가 속도, 품질, 기능 지원 및 가용성에 따라 매우 다양하기 때문에 모든 응용 프로그램에 적용됩니다. 또한 드라이버를 응용 프로그램과 함께 재배포해야 하는 경우 라이선스 계획의 비용과 가용성을 고려해야 합니다.  
  
 많은 사용자 지정 응용 프로그램의 경우 대상 DBMS는 응용 프로그램이 액세스하도록 설계된 기존 DBMS입니다. 향후 마이그레이션을 계획하는 DBMS도 고려해야 합니다. 그러나 이러한 응용 프로그램의 주요 질문은 어떤 드라이버 또는 드라이버를 함께 사용할 것인가하는 것입니다. 기존 DBMS에 액세스하도록 설계되지 않은 다른 사용자 지정 응용 프로그램의 경우 기능 지원, 동시 사용자 지원, 드라이버 가용성 및 경제성에 따라 대상 DBMS를 선택할 수 있습니다.  
  
 수직 응용 프로그램의 경우 대상 DBMS는 일반적으로 기능 지원, 드라이버 가용성 및 시장에 따라 선택됩니다. 예를 들어, 중소기업을 위해 설계된 수직 응용 프로그램은 해당 비즈니스에 저렴한 DBMS를 대상으로 해야 합니다. 기존 DBMS에 추가 기능으로 설계된 수직 응용 프로그램은 널리 사용되는 DBMS를 대상으로 해야 합니다.  
  
 대상 DBMS를 선택할 때는 데스크톱데이터베이스와 서버 데이터베이스간의 차이점을 고려해야 합니다. dBASE, 역설 및 Btrieve와 같은 데스크톱 데이터베이스는 서버 데이터베이스보다 덜 강력합니다. 일반적으로 대부분의 파일 기반 드라이버에서 발견되는 덜 강력한 SQL 엔진을 통해 액세스하기 때문에 트랜잭션 지원이 부족하고 동시 사용자를 더 적게 지원하며 SQL이 제한되는 경우가 많습니다. 그러나, 그들은 저렴하고 큰 설치 기반을 가지고있다.  
  
 Oracle, DB2 및 SQL Server와 같은 서버 데이터베이스는 전체 트랜잭션 지원을 제공하고 많은 동시 사용자를 지원하며 풍부한 SQL을 제공합니다. 그들은 훨씬 더 비싸고 작은 설치 기반을 가지고있다. 다른 한편으로는, 소프트웨어 가격은 더 높은 경향이, 다소 작은 잠재적 인 시장을 상쇄.  
  
 따라서 대상 DBMS는 응용 프로그램 및 응용 프로그램의 대상 시장에 필요한 기능에 따라 선택할 수 있습니다. 예를 들어 대기업의 주문 입력 시스템은 적절한 트랜잭션 지원이 부족하여 데스크톱 데이터베이스를 대상으로 하지 않을 수 있습니다. 중소기업을 위해 설계된 유사한 시스템은 비용을 기준으로 대부분의 서버 데이터베이스를 제외할 수 있습니다. 또한 일반 응용 프로그램의 개발자는 둘 다를 대상으로 하지만 서버 데이터베이스에 있는 고급 기능을 사용하지 않을 수 있습니다.
