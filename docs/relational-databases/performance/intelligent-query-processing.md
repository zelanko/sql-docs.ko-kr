---
title: Microsoft SQL 데이터베이스의 지능형 쿼리 처리 | Microsoft Docs
description: SQL Server 및 Azure SQL Database에서 쿼리 성능을 향상시키는 지능형 쿼리 처리 기능입니다.
ms.custom: ''
ms.date: 07/25/2018
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f36910f24b976b1c27f51ab45db40265a71c3c02
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43072996"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>SQL 데이터베이스의 지능형 쿼리 처리
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

**지능형 쿼리 처리** 기능 제품군에는 최소한의 구현 노력으로 기존 워크로드의 성능을 개선하는 광범위한 영향을 가진 기능이 포함됩니다.

![지능형 쿼리 처리 기능](./media/1_IQPFeatureFamily.png)

## <a name="adaptive-query-processing"></a>적응 쿼리 처리
적응 쿼리 처리 기능 제품군에는 응용 프로그램 워크로드의 런타임 조건에 대한 최적화 전략을 적용한 쿼리 처리 개선 사항이 포함됩니다. 이러한 개선 사항에는 다중 문 테이블 반환 함수에 대한 일괄 처리 모드 적응 조인, 메모리 부여 피드백 및 인터리브 실행이 포함됩니다.

### <a name="batch-mode-adaptive-joins"></a>일괄 처리 모드 적응 조인
이 기능을 사용하면 단일 캐시된 계획을 사용하여 실행 중에 더 나은 조인 전략으로 동적으로 전환하도록 계획할 수 있습니다.

### <a name="row-and-batch-mode-memory-grant-feedback"></a>행 및 일괄 처리 모드 메모리 부여 피드백
이 기능은 쿼리에 필요한 실제 메모리를 다시 계산한 다음, 캐시된 계획에 대한 부여 값을 업데이트하여 동시성에 영향을 주는 과도한 메모리 부여를 줄이고 디스크에 비용이 많이 발생하는 과소 평가된 메모리 부여를 해결합니다.

### <a name="interleaved-execution-for-multi-statement-table-valued-functions-mstvfs"></a>MSTVF(다중 문 테이블 반환 함수)에 대한 인터리브 실행
인터리브 실행에서 함수의 실제 행 개수는 다운스트림 쿼리 계획을 보다 잘 결정하는 데 사용됩니다. 

자세한 내용은 [SQL 데이터베이스의 적응 쿼리 처리](../../relational-databases/performance/adaptive-query-processing.md)를 참조하세요.

## <a name="table-variable-deferred-compilation"></a>테이블 변수 지연 컴파일
테이블 변수 지연 컴파일은 테이블 변수를 참조하는 쿼리의 계획 품질 및 전체 성능을 개선합니다. 최적화 및 초기 컴파일 중에 이 기능은 실제 테이블 변수 행 수를 기반으로 하는 카디널리티 예측을 전파합니다.  이 정확한 행 수 정보는 다운스트림 계획 작업을 최적화하는 데 사용됩니다.

테이블 변수 지연 컴파일을 사용하면 테이블 변수를 참조하는 문 컴파일은 문이 실제로 처음 실행될 때까지 지연됩니다. 이 지연 컴파일 동작은 임시 테이블의 동작과 동일하고, 이 변경으로 인해 원래 1행 추측 대신에 실제 카디널리티가 사용됩니다. Azure SQL Database에서 테이블 변수 지연 컴파일의 공개 미리 보기를 사용하도록 설정하려면 쿼리를 실행할 때 연결된 데이터베이스의 데이터베이스 호환성 수준 150을 사용하도록 설정합니다.

자세한 내용은 [테이블 변수 지연 컴파일](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation )을 참조하세요.

## <a name="approximate-query-processing"></a>대략적인 쿼리 처리
대략적인 쿼리 처리는 절대적인 정밀도보다 응답성이 더 중요한 큰 데이터 집합을 기반으로 집계를 제공하도록 디자인된 새로운 기능 제품군입니다.  예를 들어 대시보드에 표시하기 위해 100억 개 행을 기반으로 COUNT(DISTINCT())를 계산할 수 있습니다.  이 경우 절대적인 정밀도가 아니라 응답성이 중요합니다. 새 APPROX_COUNT_DISTINCT 집계 함수는 그룹에 있는 고유한 null이 아닌 값의 대략적인 개수를 반환합니다.

자세한 내용은 [APPROX_COUNT_DISTINCT(Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md)를 참조하세요.

## <a name="see-also"></a>관련 항목:
[SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대한 성능 센터](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md)    
[실행 계획 논리 및 물리 연산자 참조](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[조인](../../relational-databases/performance/joins.md)    
[Demonstrating Adaptive Query Processing](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)(적응 쿼리 처리 시연)        
