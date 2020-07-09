---
title: 실제 실행 계획 분석 | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- analyzing execution plans
- analyzing actual execution plans
- execution plans [SQL Server], analyzing
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 089cc2fd9a2131ab18fea01262f9bc0d476355e4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773139"
---
# <a name="analyze-an-actual-execution-plan"></a>실제 실행 계획 분석

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 계획 분석 기능을 사용하여 실제 그래픽 실행 계획을 분석하는 방법에 대해 설명합니다. 이 기능은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v17.4부터 사용할 수 있습니다. 일반적으로 [최신 버전의 SSMS를 설치](../../ssms/download-sql-server-management-studio-ssms.md)하는 것이 좋습니다.

> [!NOTE]
> [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 또는 일괄 처리가 실행된 후 실제 실행 계획이 실행됩니다. 이 때문에 실제 실행 계획에는 실제 행 수, 리소스 사용량 메트릭 및 런타임 경고(있는 경우)와 같은 런타임 정보가 포함됩니다. 자세한 내용은 [실제 실행 계획 표시](../../relational-databases/performance/display-an-actual-execution-plan.md)를 참조하세요.
  
쿼리 성능 문제 해결에는 실제로 근본 원인을 찾고 해결하기 위해 쿼리 처리 및 실행 계획을 이해하는 중요한 전문 지식이 필요합니다.

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에는 특히 크고 복잡한 계획과 같은 실제 실행 계획 분석 작업에서 일정 수준의 자동화를 구현하는 기능이 포함되어 있습니다. 목표는 정확하지 않은 [카디널리티 추정](../../relational-databases/performance/cardinality-estimation-sql-server.md)의 시나리오를 쉽게 찾도록 하고 사용할 수 있는 가능한 해결 방법에 대한 권장 사항을 가져오는 것입니다.

> [!IMPORTANT]
> 프로덕션 환경에 적용하기 전에 제안된 완화에 대한 적절한 테스트를 수행해야 합니다.
  
## <a name="to-analyze-an-execution-plan-for-a-query"></a>쿼리에 대한 실행 계획을 분석하려면  
  
1.  **파일** 메뉴를 사용하고 **파일 열기**를 클릭하여 이전에 저장된 쿼리 실행 계획 파일(.sqlplan)을 열거나 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 창으로 계획 파일을 끌어 놓습니다. 또는 쿼리를 실행하고 해당 실행 계획을 표시하도록 선택한 경우 결과 창의 **실행 계획** 탭으로 이동합니다. 

2.  실행 계획의 빈 영역을 마우스 오른쪽 단추로 클릭하고 **실제 실행 계획 분석**을 클릭합니다. 

    ![실제 실행 계획 분석을 마우스 오른쪽 단추로 클릭](../../relational-databases/performance/media/plananalysismenuoption.png "실제 실행 계획 분석을 마우스 오른쪽 단추로 클릭")   

3.  **실행 계획 분석** 창이 아래쪽에 열립니다. 분석할 올바른 명령문 쌍을 허용하여 다중 명령문으로 계획을 분석할 때 **다중 명령문** 탭은 유용합니다.

4.  실제 실행 계획에 대해 찾은 문제에 대한 세부 정보를 보려면 [시나리오] 탭을 선택합니다. 왼쪽 창에서 나열된 각 연산자의 경우 오른쪽 창은 *이 시나리오에 대한 자세한 내용은 여기를 클릭하세요* 링크의 시나리오에 대한 세부 정보를 보여주며, 해당 시나리오를 설명하는 가능한 원인이 나열됩니다.

    ![실행 계획 분석 결과](../../relational-databases/performance/media/plananalysis-scenarios.png "실행 계획 분석 결과") 
