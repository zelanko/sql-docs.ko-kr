---
title: 도구 및 접근 방법 처리 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- process [Analysis Services]
- processing [Analysis Services]
ms.assetid: 82347a16-4145-4655-8adf-2a300f1fdf99
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: edddafdbc51c9f67beb7b0f92efddf1e14f9fc79
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48118473"
---
# <a name="tools-and-approaches-for-processing-analysis-services"></a>도구 및 처리 접근 방법(Analysis Services)
  처리는 Analysis Services가 관계형 데이터 원본을 쿼리하고 해당 데이터를 사용하여 Analysis Services 개체를 채우는 작업입니다.  
  
 Analysis Services 시스템 관리자는 다음과 같은 방법을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체의 처리를 실행하고 모니터링할 수 있습니다.  
  
-   영향 분석을 실행하여 개체 종속성 및 작업 범위 이해  
  
-   개별 개체 처리 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   개별 개체 또는 여러 개체 처리 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   영향 분석을 실행하여 현재 동작의 결과로 처리되지 않는 관련 개체의 목록 검토  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] XMLA 쿼리 창에서 스크립트를 생성하고 실행하여 개별 개체 또는 여러 개체 처리  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] PowerShell cmdlet 사용  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지의 제어 흐름 및 태스크 사용  
  
-   SQL Server 프로파일러를 사용하여 처리 모니터링  
  
-   AMO를 사용하여 사용자 지정 솔루션 프로그래밍. 자세한 내용은 [Programming AMO OLAP Basic Objects](analysis-management-objects/programming-amo-olap-basic-objects.md)을 참조하세요.  
  
 처리는 다양하게 구성 가능한 작업으로, 개체 수준에서 전체 처리가 발생하는지 증분 처리가 발생하는지 결정하는 일련의 처리 옵션으로 제어됩니다. 처리 옵션 및 개체에 대한 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md) 및 [Analysis Services 개체 처리](processing-analysis-services-objects.md)를 참조하세요.  
  
> [!NOTE]  
>  이 항목에서는 다차원 모델을 처리하기 위한 도구와 방법에 대해 설명합니다. 테이블 형식 모델을 처리 하는 방법에 대 한 자세한 내용은 참조 하세요. [Process Database, 테이블 또는 파티션](../tabular-models/process-database-table-or-partition-analysis-services.md) 하 고 [데이터 처리 &#40;&AMP;#40;SSAS 테이블 형식&#41;](../process-data-ssas-tabular.md).  
  
### <a name="processing-objects-in-sql-server-management-studio"></a>SQL Server Management Studio에서 개체 처리  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 시작하고 Analysis Services에 연결합니다.  
  
2.  처리할 Analysis Services 개체를 마우스 오른쪽 단추로 클릭한 다음 **처리**를 클릭합니다. 다음과 같은 수준 모두에서 데이터를 처리할 수 있습니다.  
  
    -   데이터베이스  
  
    -   큐브  
  
    -   측정값 그룹 또는 측정값 그룹의 개별 파티션  
  
    -   차원  
  
    -   마이닝 모델  
  
    -   마이닝 구조  
  
     Analysis Services 개체는 계층적입니다. 데이터베이스를 선택하면 데이터베이스에 포함된 모든 개체에 대해 처리가 발생할 수 있습니다. 처리가 실제로 발생하는지 여부는 선택한 처리 옵션과 개체 상태에 따라 달라집니다. 개체가 처리되지 않은 경우 해당 부모를 처리하면 해당 개체가 처리됩니다. 개체 종속성에 대한 자세한 내용은 [Processing Analysis Services Objects](processing-analysis-services-objects.md)를 참조하십시오.  
  
3.  **처리** 대화 상자의 **처리 옵션**에서 제공된 기본값을 사용하거나 목록에서 다른 옵션을 선택합니다. 각 옵션에 대한 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
4.  **영향 분석** 을 클릭하면 처리 대화 상자에 나열된 개체를 처리하는 경우 영향을 받는 종속 개체를 식별하고 선택적으로 처리할 수 있습니다.  
  
5.  원하는 경우 **설정 변경** 을 클릭하여 처리 순서, 특정 오류 유형에 대한 처리 동작 및 기타 설정을 수정할 수 있습니다.  
  
6.  **확인**을 클릭합니다.  
  
     프로세스 진행률 대화 상자에 각 명령의 현재 상태가 표시됩니다. 상태 메시지가 잘리는 경우 **자세히 보기** 를 클릭하면 전체 메시지를 읽을 수 있습니다.  
  
### <a name="processing-objects-in-sql-server-data-tools"></a>SQL Server 데이터 도구에서 개체 처리  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 시작하고 배포된 프로젝트를 엽니다.  
  
2.  솔루션 탐색기의 배포된 프로젝트에서 **차원** 폴더를 확장합니다.  
  
3.  차원을 마우스 오른쪽 단추로 클릭한 다음 **처리**를 클릭합니다. 여러 차원을 마우스 오른쪽 단추로 클릭하여 여러 개체를 한 번에 처리할 수 있습니다. 자세한 내용은 [일괄 처리&#40;Analysis Services&#41;](batch-processing-analysis-services.md)를 참조하세요.  
  
4.  **차원 처리** 대화 상자에 있는 **개체 목록** 의 **처리 옵션**열에서 이 열에 대한 옵션이 **전체 처리**인지 확인합니다. 그렇지 않을 경우 **처리 옵션**에서 해당 옵션을 클릭한 다음 드롭다운 목록에서 **전체 처리** 를 선택합니다.  
  
5.  **실행**을 클릭합니다.  
  
6.  처리를 마치면 **닫기**를 클릭합니다.  
  
##  <a name="bkmk_impactanalysis"></a> 영향 분석을 실행하여 개체 종속성 및 작업 범위 식별  
  
1.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 또는 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 의 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]개체를 처리하기 전에 **개체 처리** 대화 상자 중 하나에서 **영향 분석** 을 클릭하여 관련 개체에 대한 영향을 분석할 수 있습니다.  
  
2.  차원, 큐브, 측정값 그룹 또는 파티션을 마우스 오른쪽 단추로 클릭하여 **개체 처리** 대화 상자를 엽니다.  
  
3.  **영향 분석**을 클릭합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 모델을 검색한 후 처리하기 위해 선택한 모델과 관련된 개체에 대한 다시 처리 요구 사항에 대해 보고합니다.  
  
### <a name="processing-objects-using-xmla"></a>XMLA를 사용하여 개체 처리  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 시작하고 Analysis Services에 연결합니다.  
  
2.  처리할 개체를 마우스 오른쪽 단추로 클릭한 다음 **처리**를 클릭합니다.  
  
3.  **처리** 대화 상자에서 사용할 처리 옵션을 선택합니다. 기타 설정을 수정합니다. 영향 분석을 실행하여 변경해야 할 사항을 식별합니다.  
  
4.  **개체 처리** 화면에서 **스크립트** 를 클릭합니다.  
  
     이렇게 하면 XMLA 스크립트가 생성되고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XMLA 쿼리 창이 열립니다.  
  
5.  대화 상자를 닫습니다. 스크립트에는 대화 상자에 지정된 처리 명령과 옵션이 포함되어 있습니다.  
  
6.  필요에 따라 동일한 일괄 처리의 추가 개체를 처리하려는 경우 스크립트에 계속해서 추가할 수 있습니다. 계속하려면 이전 단계를 반복하여 모든 처리 작업에 단일 스크립트를 사용할 수 있도록 생성된 스크립트를 추가합니다. 예를 보려면 [Schedule SSAS Administrative Tasks with SQL Server Agent](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)을 참조하십시오.  
  
7.  메뉴 모음에서 **쿼리**를 클릭한 다음 **실행**을 클릭합니다.  
  
### <a name="processing-objects-using-powershell"></a>PowerShell을 사용하여 개체 처리  
  
1.  이 SQL Server 릴리스부터는 Analysis Services PowerShell cmdlet을 사용하여 개체를 처리할 수 있습니다. 다음 cmdlet은 대화형으로 실행하거나 스크립트로 실행할 수 있습니다.  
  
    -   [Invoke-ProcessCube cmdlet](/sql/analysis-services/powershell/invoke-processcube-cmdlet)  
  
    -   [Invoke-ProcessDimension cmdlet](/sql/analysis-services/powershell/invoke-processdimension-cmdlet)  
  
    -   [Invoke-ProcessPartition cmdlet](/sql/analysis-services/powershell/invoke-processpartition-cmdlet)  
  
    -   [Invoke-ASCmd cmdlet](/sql/analysis-services/powershell/invoke-ascmd-cmdlet)- 처리 명령을 포함하는 XMLA, MDX 또는 DMX 스크립트를 실행하는 데 사용할 수 있습니다.  
  
### <a name="monitoring-object-processing-using-sql-server-profiler"></a>SQL Server 프로파일러를 사용하여 개체 처리 모니터링  
  
1.  SQL Server 프로파일러의 Analysis Services 인스턴스에 연결합니다.  
  
2.  이벤트 선택에서 **모든 이벤트 표시** 를 클릭하여 목록에 모든 이벤트를 추가합니다.  
  
3.  다음 이벤트를 선택합니다.  
  
    -   처리가 시작되고 중지되는 때를 표시하려면**명령 시작** 및 **Comm및 End** to show when processing starts 및 stops  
  
    -   오류를 캡처하려면**오류** 를 선택합니다.  
  
    -   처리 상태에 대해 보고하고 데이터를 검색하는 데 사용되는 SQL 쿼리를 표시하려면**진행률 보고서 시작**, **진행률 보고서 현재 부분**및 **진행률 보고서 끝** 을 선택합니다.  
  
    -   큐브 계산을 표시하려면**MDX 스크립트 실행의 시작** 및 **MDX 스크립트 실행의 끝** 을 선택합니다.  
  
    -   필요에 따라 처리와 관련된 성능 문제를 진단하려는 경우 잠금 이벤트를 추가합니다.  
  
### <a name="process-analysis-services-objects-using-integration-services"></a>Integration Services를 사용하여 Analysis Services 개체 처리  
  
1.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 Analysis Services 처리 태스크를 사용하여 원본 관계형 데이터베이스를 정기적으로 업데이트할 때 자동으로 개체를 새 데이터로 채우는 패키지를 만듭니다.  
  
2.  **SSIS 도구 상자**에서 **Analysis Services 처리** 를 두 번 클릭하여 패키지에 추가합니다.  
  
3.  태스크를 편집하여 데이터베이스에 대한 연결, 처리할 개체 및 처리 옵션을 지정합니다. 이 태스크의 구현 방법은 [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [다차원 모델 개체 처리](processing-a-multidimensional-model-analysis-services.md)  
  
  
