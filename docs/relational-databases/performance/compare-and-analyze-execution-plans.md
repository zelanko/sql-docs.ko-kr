---
title: 실행 계획 비교 및 분석 | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Showplan results
- execution plans [SQL Server]
- queries [SQL Server], tuning
- execution plans [SQL Server], how-to topics
- SQL Server Management Studio [SQL Server], execution plans
- tuning queries [SQL Server]
ms.assetid: bcd6f094-c613-4835-ae19-4caaadb4bb17
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 4b300d1fbc144f25b3f725f34e49d961953c434c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72289335"
---
# <a name="compare-and-analyze-execution-plans"></a>실행 계획 비교 및 분석
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 섹션에서는 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]을(를) 사용하여 실행 계획을 비교하고 분석하는 방법을 설명합니다. 이 기능은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v17.4부터 사용할 수 있습니다.  
  
실행 계획은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램에서 선택한 데이터 검색 방법을 그래픽으로 표시합니다. 실행 계획은 [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md) 또는 [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md) 문으로 생성되는 테이블 형식이 아닌 아이콘으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 특정 문과 쿼리 실행 비용을 표시합니다. 이러한 그래픽 표시는 쿼리의 성능 특성을 이해하는 데 매우 유용합니다. 

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에는 사용자가 두 실행 계획을 비교하고(예: 동일한 쿼리에 대해 인지된 올바른 계획과 잘못된 계획 간) 근본 원인 분석을 수행할 수 있는 기능이 포함되어 있습니다. 또한 해당 실행 계획의 분석을 통해 쿼리의 성능에 영향을 줄 수 있는 시나리오로 인사이트를 허용하는 단일 쿼리 계획 분석을 수행하는 기능도 포함됩니다.

쿼리 실행 계획에 대한 자세한 내용은 [예상된 실행 계획](../../relational-databases/performance/display-the-estimated-execution-plan.md), [실제 실행 계획](../../relational-databases/performance/display-an-actual-execution-plan.md) 및 [쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md)를 참조하세요.
  
## <a name="in-this-section"></a>섹션 내용  
[실행 계획 비교](../../relational-databases/performance/display-the-estimated-execution-plan.md)     
[실제 실행 계획 분석](../../relational-databases/performance/display-an-actual-execution-plan.md)      
  
