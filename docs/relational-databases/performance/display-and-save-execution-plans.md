---
title: 실행 계획 표시 및 저장 | Microsoft 문서
ms.custom: ''
ms.date: 08/21/2017
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
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d2d049990cd2c60db36105d3c03da36bc25b4f4b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749546"
---
# <a name="display-and-save-execution-plans"></a>실행 계획 표시 및 저장
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
이 섹션에서는 실행 계획을 표시하는 방법과 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 실행 계획을 XML 형식의 파일로 저장하는 방법에 대해 설명합니다.  
  
실행 계획은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램에서 선택한 데이터 검색 방법을 그래픽으로 표시합니다. 실행 계획은 [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md) 또는 [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md) 문으로 생성되는 테이블 형식이 아닌 아이콘으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 특정 문과 쿼리 실행 비용을 표시합니다. 이러한 그래픽 표시는 쿼리의 성능 특성을 이해하는 데 유용합니다.  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램에서는 하나의 실행 계획만 생성하지만 **예상** 실행 계획과 **실제** 실행 계획이라는 개념이 있습니다.
-  [예상 실행 계획](../../relational-databases/performance/display-the-estimated-execution-plan.md)은 컴파일 시간에 쿼리 최적화 프로그램에서 생성된 실행 계획을 반환합니다. 예상 실행 계획을 생성해도 실제로 쿼리 또는 일괄 처리를 실행하지 않기 때문에 실제 리소스 사용량 메트릭이나 런타임 경고와 같은 런타임 정보가 이 계획에 포함되지 않습니다. 
-  [실제 실행 계획](../../relational-databases/performance/display-an-actual-execution-plan.md)은 쿼리 또는 일괄 처리 실행이 완료된 후 쿼리 최적화 프로그램에서 생성된 실행 계획을 반환합니다. 따라서 리소스 사용량 메트릭 및 런타임 경고에 관한 런타임 정보가 포함됩니다.  

쿼리 실행 계획에 대한 자세한 내용은 [쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md)를 참조하세요.
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [예상 실행 계획 표시](../../relational-databases/performance/display-the-estimated-execution-plan.md)  
  
-   [실제 실행 계획 표시](../../relational-databases/performance/display-an-actual-execution-plan.md)  
  
-   [XML 형식으로 실행 계획 저장](../../relational-databases/performance/save-an-execution-plan-in-xml-format.md)  
  
  
