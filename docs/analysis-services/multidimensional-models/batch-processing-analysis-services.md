---
title: "일괄 처리(Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "일괄 처리 [Analysis Services]"
ms.assetid: ba4dcf72-0667-41d0-816b-ab8ff9a7d9cb
caps.latest.revision: 39
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 39
---
# 일괄 처리(Analysis Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 일괄 처리 명령을 사용하여 여러 처리 명령을 단일 요청으로 서버에 보낼 수 있습니다. 일괄 처리를 사용하여 처리할 개체와 처리 순서를 제어할 수 있습니다. 또한 일괄 처리는 일련의 독립 실행형 작업으로 실행되거나 한 프로세스가 실패하면 완료된 일괄 처리가 롤백되는 트랜잭션으로 실행될 수 있습니다.  
  
 일괄 처리는 변경 내용을 커밋하는 데 걸리는 시간을 줄이고 통합함으로써 데이터 가용성을 최대화합니다. 차원을 전체 처리할 경우 해당 차원을 사용하는 파티션은 처리되지 않은 것으로 표시됩니다. 따라서 처리되지 않은 파티션이 포함된 큐브는 검색할 수 없습니다. 영향을 받는 파티션과 함께 차원을 처리하는 일괄 처리 작업을 수행하여 이 문제를 해결할 수 있습니다. 일괄 처리 작업을 트랜잭션으로 실행하면 모든 처리가 완료될 때까지 트랜잭션에 포함된 모든 개체를 쿼리에 사용할 수 있습니다. 트랜잭션이 변경 내용을 커밋하면 개체를 일시적으로 사용할 수 없게 되지만 변경 내용을 커밋하는 데 걸리는 총 시간은 개체를 개별적으로 처리할 때보다 줄어듭니다.  
  
 이 항목의 절차에서는 차원과 파티션을 완전히 처리하는 단계에 대해 설명합니다. 일괄 처리에는 증분 처리 등과 같은 다른 처리 옵션도 포함되어 있습니다. 이러한 절차를 올바르게 수행하려면 둘 이상의 차원과 하나 이상의 파티션이 들어 있는 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 사용해야 합니다.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
 [SQL Server Data Tools에서 일괄 처리](#bkmk_ssdt)  
  
 [Management Studio에서 XMLA를 사용하여 일괄 처리](#bkmk_xmla)  
  
##  <a name="bkmk_ssdt"></a> SQL Server Data Tools에서 일괄 처리  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 개체를 처리하기 전에 개체가 포함된 프로젝트를 배포해야 합니다. 자세한 내용은 [Analysis Services 프로젝트 배포&#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)를 참조하세요.  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]를 엽니다.  
  
2.  배포된 프로젝트를 엽니다.  
  
3.  솔루션 탐색기의 배포된 프로젝트에서 **차원** 폴더를 확장합니다.  
  
4.  Ctrl 키를 누른 채로 **차원** 폴더에 나열된 각 차원을 클릭합니다.  
  
5.  선택한 차원을 마우스 오른쪽 단추로 클릭한 다음 **처리**를 클릭합니다.  
  
6.  Ctrl 키를 누른 채로 **개체 목록**에 나열된 각 차원을 클릭합니다.  
  
7.  선택한 차원을 마우스 오른쪽 단추로 클릭한 다음 **전체 처리**를 선택합니다.  
  
8.  일괄 처리 작업을 사용자 지정하려면 **설정 변경**을 클릭합니다.  
  
9. **처리 옵션**에서 다음과 같이 설정합니다.  
  
    -   **처리 순서** 는 **순차**로, **트랜잭션 모드** 는 **단일 트랜잭션**으로 설정합니다.  
  
    -   **쓰기 저장(writeback) 테이블 옵션** 을 **기존 테이블 사용**으로 설정합니다.  
  
    -   **영향을 받는 개체**에서 **영향을 받는 개체 처리** 확인란을 선택합니다.  
  
10. **차원 키 오류** 탭을 클릭합니다. **기본 오류 구성 사용** 이 선택되어 있는지 확인합니다.  
  
11. **확인** 을 클릭하여 **설정 변경** 화면을 닫습니다.  
  
12. **개체 처리** 화면에서 **실행** 을 클릭하여 처리 작업을 시작합니다.  
  
13. **상태** 상자에 **처리에 성공했습니다**가 표시되면 **닫기**를 클릭합니다.  
  
14. **개체 처리** 화면에서 **닫기** 를 클릭합니다.  
  
##  <a name="bkmk_xmla"></a> Management Studio에서 XMLA를 사용하여 일괄 처리  
 일괄 처리를 수행하는 XMLA 스크립트를 만들 수 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 각 개체에 대한 XMLA 스크립트 생성을 시작한 다음 해당 스크립트를 예약된 태스크 내부에서 실행되거나 대화형으로 실행되는 단일 XMLA 쿼리에 결합합니다.  
  
 단계별 지침은 [SQL Server 에이전트를 사용하여 SSAS 관리 태스크 예약](../../analysis-services/instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)의 **예제 2**를 참조하세요.  
  
## 관련 항목:  
 [다차원 모델 처리&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  