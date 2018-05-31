---
title: Microsoft SQL 데이터베이스의 지능형 쿼리 처리 | Microsoft Docs
description: SQL Server 및 Azure SQL Database에서 쿼리 성능을 향상시키는 지능형 쿼리 처리 기능입니다.
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7786fd048f1698c90f379450b31e0bac3457706e
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34455773"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 데이터베이스의 지능형 쿼리 처리
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

**지능형 쿼리 처리** 기능 제품군에는 최소한의 구현 노력으로 기존 워크로드의 성능을 개선하는 광범위한 영향을 가진 기능이 포함됩니다.   여기에는 기존 생성의 향상된 기능 및 적응 메서드 및 기능 소개가 포함됩니다.  

## <a name="adaptive-query-processing"></a>적응 쿼리 처리
적응 쿼리 처리 기능 제품군은 지능형 쿼리 처리 기능 제품군 내에서 SQL Server 2017 및 Azure SQL Database에서 추가되었습니다. 여기에는 응용 프로그램 워크로드의 런타임 조건에 대한 최적화 전략을 조정하는 전반적으로 새로운 쿼리 처리 기능이 추가되었습니다.
- **일괄 처리 모드 적응 조인** 이 기능을 사용하면 단일 캐시된 계획을 사용하여 실행 중에 더 나은 조인 전략으로 동적으로 전환하도록 계획할 수 있습니다.
- **일괄 처리 모드 메모리 부여 피드백** 이 기능은 쿼리에 필요한 실제 메모리를 다시 계산한 다음, 캐시된 계획에 대한 부여 값을 업데이트하여 동시성에 영향을 주는 과도한 메모리 부여를 줄이고 디스크에 비용이 많이 발생하는 과소 평가된 메모리 부여를 해결합니다.
- **MSTVF(다중 문 테이블 반환 함수)에 대한 인터리브 실행** 인터리브 실행에서 다운스트림 쿼리 계획을 보다 잘 결정할 수 있도록 함수에서 실제 행 개수를 사용합니다. 

적응 쿼리 처리에 대한 자세한 내용은 [SQL 데이터베이스의 적응 쿼리 처리](../../relational-databases/performance/adaptive-query-processing.md)를 참조하세요.

## <a name="see-also"></a>관련 항목:
[SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대한 성능 센터](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md)    
[실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[조인](../../relational-databases/performance/joins.md)    
[Demonstrating Adaptive Query Processing](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)(적응 쿼리 처리 시연)        
