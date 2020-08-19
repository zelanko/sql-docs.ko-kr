---
description: 대상 DBMS 및 드라이버 확인
title: 대상 Dbms 및 드라이버 결정 | Microsoft Docs
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
ms.openlocfilehash: 8dfbc11e96577e9027d1cc6e17701a82b89061be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429325"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>대상 DBMS 및 드라이버 확인
고려할 다음 질문은, 응용 프로그램에 대 한 대상 Dbms 및 해당 Dbms를 지 원하는 사용 가능한 드라이버는 무엇 인가요? 제네릭 응용 프로그램의 상호 운용성이 매우 일반적 이기 때문에 대상 Dbms의 질문은 사용자 지정 및 수직 응용 프로그램에 가장 적합 합니다. 그러나 드라이버는 속도, 품질, 기능 지원 및 가용성에 따라 크게 달라 지므로 대상 드라이버의 질문은 모든 응용 프로그램에 적용 됩니다. 또한 응용 프로그램과 함께 드라이버를 재배포 하려면 라이선스 계획의 비용 및 가용성을 고려해 야 합니다.  
  
 많은 사용자 지정 응용 프로그램의 경우 대상 Dbms가 분명 합니다. 이러한 dbms는 응용 프로그램이 액세스 하도록 디자인 된 기존 Dbms입니다. 향후 마이그레이션을 계획할 Dbms도 고려해 야 합니다. 그러나 이러한 응용 프로그램에 대 한 주요 질문은 해당 응용 프로그램에 사용할 드라이버 또는 드라이버입니다. 다른 사용자 지정 응용 프로그램의 경우-기존 DBMS에 액세스 하도록 설계 되지 않은 응용 프로그램-기능 지원, 동시 사용자 지원, 드라이버 가용성 및 경제성에 따라 대상 Dbms를 선택할 수 있습니다.  
  
 수직 응용 프로그램의 경우 일반적으로 대상 Dbms가 기능 지원, 드라이버 가용성 및 시장에 따라 선택 됩니다. 예를 들어 중소기업을 위해 설계 된 수직 응용 프로그램은 해당 비즈니스에 적합 한 Dbms를 대상으로 해야 합니다. 기존 Dbms에 대 한 추가 기능으로 디자인 된 세로 응용 프로그램은 널리 사용 되는 Dbms를 대상으로 해야 합니다.  
  
 대상 Dbms를 선택할 때 데스크톱과 서버 데이터베이스 간의 차이점을 고려해 야 합니다. DBASE, Paradox 및 Btrieve와 같은 데스크톱 데이터베이스는 서버 데이터베이스 보다 더 강력 하지 않습니다. 일반적으로 대부분의 파일 기반 드라이버에서 발견 된 덜 강력한 SQL 엔진을 통해 액세스 되기 때문에 대부분의 경우에는 완전 한 트랜잭션 지원이 없고, 더 작은 동시 사용자를 지원 하며, SQL이 제한 됩니다. 그러나이 경우에는 비용이 많이 들며 설치 된 기반이 매우 커집니다.  
  
 Oracle, DB2, SQL Server 등의 서버 데이터베이스는 전체 트랜잭션 지원을 제공 하 고 많은 동시 사용자를 지원 하며 다양 한 SQL을 제공 합니다. 이는 훨씬 더 많은 비용이 들고 설치 된 기반이 더 작습니다. 반면에 소프트웨어 가격은 더 높을 수 있으며, 더 작은 규모의 시장을 약간 오프셋 하는 경향이 있습니다.  
  
 따라서 응용 프로그램 및 응용 프로그램의 대상 시장에서 요구 하는 기능에 따라 대상 Dbms를 선택할 수 있습니다. 예를 들어 대기업의 주문 입력 시스템은 적절 한 트랜잭션 지원이 부족 하기 때문에 데스크톱 데이터베이스를 대상으로 하지 않을 수 있습니다. 중소 기업을 위해 설계 된 유사한 시스템은 비용을 기준으로 대부분의 서버 데이터베이스를 제외할 수 있습니다. 그리고 제네릭 응용 프로그램의 개발자는 둘 모두를 대상으로 하지만 서버 데이터베이스에 있는 고급 기능을 사용 하지 않을 수 있습니다.
