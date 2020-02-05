---
title: DTA 권장 성능 향상
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor, performance improvements
ms.assetid: 2e51ea06-81cb-4454-b111-da02808468e6
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 48614ea63ab56974e3eafb55b0f43dd83436ec85
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74164924"
---
# <a name="performance-improvements-using-database-engine-tuning-advisor-dta-recommendations"></a>DTA(데이터베이스 엔진 튜닝 관리자) 권장 사항을 사용한 성능 향상
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]


---
데이터 웨어하우징 및 분석 작업은 **columnstore** 인덱스를 사용하면 성능이 향상될 수 있습니다. 특히 큰 테이블을 검색해야 하는 쿼리에 매우 유리합니다. **Rowstore**(B+-tree) 인덱스는 특정 값이나 값 범위를 검색하여 상대적으로 적은 양의 데이터에 액세스하는 쿼리에 가장 효과적입니다. Rowstore 인덱스는 정렬 순서에 따라 행을 제공하므로 쿼리 실행 계획에서 정렬 비용을 줄일 수도 있습니다. 따라서 빌드할 rowstore 및 columnstore 인덱스의 조합을 선택하는 것은 애플리케이션의 워크로드에 따라 달라집니다.

SQL Server 2016부터 DTA(데이터베이스 엔진 튜닝 관리자)는 지정된 데이터베이스 작업을 분석하여 적절한 **rowstore 및 columnstore 조합** 인덱스를 추천할 수 있습니다. 

작업 성능에 대한 DTA 권장 사항의 이점을 설명하기 위해 몇몇 실제 고객 작업에서 실험했습니다. 각 고객 작업에서 DTA가 쿼리의 전체 작업뿐만 아니라 개별 쿼리를 분석하도록 합니다. 다음 세 가지 대안을 고려해 보겠습니다.
  
  1. **Columnstore 전용**: DTA를 사용하지 않고 모든 테이블에 대해 columnstore 인덱스만 빌드합니다. 
  2. **DTA(rowstore 전용)** : rowstore 인덱스에만 권장되는 옵션을 사용하여 DTA를 실행합니다.
  3. **DTA(rowstore + columnstore)** : rowstore 인덱스와 columnstore 인덱스에 모두 권장되는 옵션을 사용하여 DTA를 실행합니다.  
   
각각의 경우에 권장 인덱스를 구현했습니다. 쿼리 또는 작업을 여러 번 실행 시 평균 CPU 시간(밀리초)을 보고합니다. 아래 그림은 두 개의 서로 다른 고객 데이터베이스 작업의 CPU 시간(밀리초)을 나타냅니다. y-축(CPU 시간)은 로그 눈금 간격을 사용합니다.   


![DTA-columnstore-rowstore-performance](../../relational-databases/performance/media/dta-columnstore-rowstore-performance.gif)



**혼합 물리적 디자인에 필요**: 고객 1 쿼리 1에 해당하는 첫 번째 막대 집합입니다. DTA(rowstore + columnstore)에는 4개의 columnstore와 6개의 rowstore 인덱스 세트가 권장됩니다. 이 세트를 사용하면 columnstore 인덱스 전용 및 DTA(rowstore 전용)와 비교하여 CPU 시간이 2.5-4배 낮아집니다. 이는 *단일 쿼리에도* rowstore 및 columnstore 인덱스를 구성하는 혼합 물리적 디자인이 유리함을 나타냅니다. 

**rowstore 인덱스 권장 구성의 효율성**: 두 번째와 세 번째 막대 집합(고객 1 쿼리 2 및 고객 2 쿼리 1에 해당)은 쿼리에 적절한 rowstore 인덱스의 이점을 활용하는 선택적 필터 조건자가 있는 경우입니다. 이러한 두 쿼리에 대해 DTA(rowstore 전용) 및 DTA(rowstore + columnstore)는 rowstore 인덱스 전용을 권장합니다. 또한 이러한 예는 DTA가 columnstore 인덱스를 권장하는 옵션을 사용하여 호출되는 경우에도 비용을 기반으로 하는 방법에서는 작업이 실제로 columnstore 인덱스의 이점을 활용할 수 있는 경우에만 columnstore 인덱스 전용을 권장합니다.

**columnstore 인덱스 권장 구성의 효율성**: 고객 2 쿼리 2에 해당하는 네 번째 막대 집합은 쿼리가 columnstore 인덱스의 이점을 활용하는 큰 테이블을 검색하는 경우를 나타냅니다. DTA(rowstore 전용)는 columnstore 인덱스가 있을 때보다 CPU 시간이 더 높은 권장 사항을 생성합니다. 따라서 DTA(rowstore + columnstore)는 columnstore 전용 옵션의 쿼리 실행 성능과 일치하는 적합한 columnstore 인덱스를 권장합니다.

**여러 개의 쿼리가 있는 워크로드에 대한 권장 구성의 효율성**: 고객 2의 전체 워크로드에 해당하는 마지막 막대 세트는 워크로드에서 여러 쿼리를 분석하는 DTA의 기능을 예시하여 전반적인 워크로드의 실행 비용을 개선할 수 있는 적합한 rowstore 및 columnstore 인덱스 세트를 권장합니다. DTA(rowstore + columnstore)는 4개의 columnstore 인덱스와 수십 개의 rowstore 인덱스를 권장하며 이는 columnstore 전용 인덱스를 빌드하는 옵션에 비해 상당히 워크로드가 향상되고 DTA(rowstore 전용)에 비해서는 약 4-5배가 향상됩니다.

요약하면 위의 예제에서는 SQL Server 데이터베이스 엔진에서 지원되는 rowstore 및 columnstore 인덱스를 적절히 활용하도록 DTA의 기능을 설명하고 워크로드의 CPU 시간을 크게 줄일 수 있는 적합한 인덱스 조합을 권장합니다. 

<a name="see-also"></a>참고 항목
---
[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)

[DTA(데이터베이스 엔진 튜닝 관리자)의 Columnstore 인덱스 권장 사항](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)

[Columnstore 인덱스 가이드](~/relational-databases/indexes/columnstore-indexes-overview.md)

[데이터 웨어하우스용 Columnstore 인덱스](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

[CREATE COLUMNSTORE INDEX(Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)

[CREATE INDEX(Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)



