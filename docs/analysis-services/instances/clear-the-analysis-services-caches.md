---
title: "Analysis Services 캐시 지우기 | Microsoft Docs"
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
ms.assetid: 6bf66fdd-6a03-4cea-b7e2-eb676ff276ff
caps.latest.revision: 11
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 11
---
# Analysis Services 캐시 지우기
  Analysis Services는 데이터를 캐시하여 쿼리 성능을 향상시킵니다. 이 항목에서는 XMLA ClearCache 명령을 사용하여 MDX 쿼리에 대한 응답으로 만들어진 캐시를 지우는 데 대한 권장 사항을 제공합니다. ClearCache의 실행 효과는 테이블 형식 모델을 사용하는지 다차원 모델을 사용하는지에 따라 달라집니다.  
  
 **다차원 모델에 대한 캐시를 지우는 경우**  
  
 다차원 데이터베이스의 경우 Analysis Services는 계산을 평가할 때의 수식 엔진과 차원 쿼리 및 측정값 그룹 쿼리의 결과를 위한 저장소 엔진에 캐시를 작성합니다. 측정값 그룹 쿼리는 수식 엔진에 셀 좌표 또는 하위 큐브에 대한 측정값 데이터가 필요한 경우 발생합니다. 차원 쿼리는 비자연 계층을 쿼리할 때와 Autoexists를 적용할 때 발생합니다.  
  
 성능 테스트를 수행할 때 캐시를 지우는 것이 좋습니다. 테스트 실행 간에 캐시를 지움으로써 쿼리 디자인 변경으로 인한 영향을 측정한 테스트 결과가 캐시 때문에 왜곡되지 않도록 할 수 있습니다.  
  
 **테이블 형식 모델에 대한 캐시를 지우는 경우**  
  
 테이블 형식 모델은 일반적으로 메모리에 저장되며, 쿼리가 실행될 때 집계 및 기타 계산이 수행됩니다. 따라서 ClearCache 명령을 사용할 경우 테이블 형식 모델에 대한 효과는 제한적입니다. 테이블 형식 모델에 대해 MDX 쿼리를 실행할 경우 Analysis Services 캐시에 데이터가 추가될 수 있습니다. 특히 MDX 및 Autoexists 작업에서 참조하는 DAX 측정값은 수식 캐시와 차원 캐시 각각의 결과를 캐시할 수 있습니다. 그러나 비자연 계층 및 측정값 그룹 쿼리는 저장소 엔진의 결과를 캐시하지 않습니다. 또한 DAX 쿼리는 수식 엔진 및 저장소 엔진의 결과를 캐시하지 않습니다. MDX 쿼리 결과로 캐시가 존재하는 범위까지는 테이블 형식 모델에 대해 ClearCache를 실행하면 시스템에서 캐시된 데이터가 모두 무효화됩니다.  
  
 ClearCache를 실행하면 xVelocity 메모리 내 분석 엔진(VertiPaq)의 메모리 내 캐시도 지워집니다. xVelocity 엔진에서는 작은 캐시 결과 집합을 유지합니다. ClearCache를 실행하면 xVelocity 엔진의 이러한 캐시가 무효화됩니다.  
  
 마지막으로, ClearCache를 실행하면 **DirectQuery** 모드용으로 테이블 형식 모델이 다시 구성될 때 메모리에 남아 있던 잔여 데이터도 제거됩니다. 이 사실은 모델에 포함되어 있는 중요한 데이터가 엄격하게 제어될 수 있는 경우에 특히 중요합니다. 이 경우에는 중요한 데이터가 필요한 위치에만 존재하도록 하기 위해 수행할 수 있는 예방 조치로 ClearCache를 실행합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 를 사용하여 모델을 배포하고 쿼리 모드를 변경하는 경우에는 캐시를 수동으로 지워야 합니다. 반대로 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]를 사용하여 모델과 파티션에 **DirectQuery**를 지정하면 해당 쿼리 모드를 사용하도록 모드를 전환할 때 캐시가 자동으로 지워집니다.  
  
 성능을 테스트하는 중에 다차원 모델 캐시를 지우기 위한 권장 사항과 비교했을 때 테이블 형식 모델 캐시를 지우기 위한 광범위한 권장 사항은 없습니다. 중요한 데이터가 포함된 테이블 형식 모델에 대한 배포를 관리하는 경우가 아니면 캐시를 지우는 특정 관리 태스크가 없습니다.  
  
## Analysis Services 모델에 대한 캐시 지우기  
 캐시를 지우려면 XMLA와 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용합니다. 데이터베이스, 큐브, 차원이나 테이블 또는 측정값 그룹 수준에서 캐시를 지울 수 있습니다. 데이터베이스 수준에서 캐시를 지우는 데 필요한 다음 단계는 다차원 모델과 테이블 형식 모델 모두에 적용됩니다.  
  
> [!NOTE]  
>  엄격한 성능 테스트를 위해서는 캐시를 지우는 데 대한 더욱 포괄적인 접근이 필요할 수 있습니다. Analysis Services 및 파일 시스템 캐시를 플러시하는 방법은 [SQL Server 2008 R2 Analysis Services 작업 가이드](http://go.microsoft.com/fwlink/?linkID=http://go.microsoft.com/fwlink/?LinkID=225539)에서 캐시 지우기에 대한 섹션을 참조하십시오.  
  
 다차원 모델과 테이블 형식 모델 모두 두 단계의 프로세스를 통해 이러한 캐시를 지울 수 있습니다. 이 프로세스는 ClearCache를 실행할 때 캐시를 무효화하고 다음 쿼리를 받을 때 캐시를 지우는 단계로 구성되어 있습니다. 실제로 캐시를 비운 후에만 메모리 사용량의 감소가 확실히 나타납니다.  
  
 캐시를 지우려면 XMLA 쿼리의 **ClearCache** 문에 개체 식별자를 제공해야 합니다. 이 항목의 첫 번째 단계에서는 개체 식별자를 가져오는 방법에 대해 설명합니다.  
  
#### 1단계: 개체 식별자 가져오기  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 개체를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 다음 **속성** 창에서 ID 속성 값을 복사합니다. 이 방법은 데이터베이스, 큐브, 차원 또는 테이블에 사용할 수 있습니다.  
  
2.  측정값 그룹 ID를 가져오려면 측정값 그룹을 마우스 오른쪽 단추로 클릭하고 **측정값 그룹 스크립팅**을 선택합니다. **만들기** 또는 **변경**을 선택하고 창에 쿼리를 보냅니다. 측정값 그룹의 ID가 개체 정의에 표시됩니다. 개체 정의의 ID를 복사합니다.  
  
#### 2단계: 쿼리 실행  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 가리킨 다음 **XMLA**를 선택합니다.  
  
2.  다음 코드 예제를 XMLA 쿼리 창에 복사합니다. **DatabaseID** 를 현재 연결 데이터베이스의 ID로 변경합니다.  
  
    ```  
    <ClearCache xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
      <Object>  
        <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
      </Object>  
    </ClearCache>  
  
    ```  
  
     또는 측정값 그룹과 같은 자식 개체의 경로를 지정하여 해당 개체에 대한 캐시만 지울 수 있습니다.  
  
    ```  
    <ClearCache xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
            <CubeID>Adventure Works</CubeID>  
            <MeasureGroupID>Fact Currency Rate</MeasureGroupID>  
      </Object>  
    </ClearCache>  
    ```  
  
3.  F5 키를 눌러 쿼리를 실행합니다. 다음과 같은 결과가 나타납니다.  
  
    ```  
    <return xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <root xmlns="urn:schemas-microsoft-com:xml-analysis:empty" />  
    </return>  
    ```  
  
## 관련 항목:  
 [Analysis Services의 스크립트 관리 태스크](../../analysis-services/instances/script-administrative-tasks-in-analysis-services.md)   
 [Analysis Services 인스턴스 모니터](../../analysis-services/instances/monitor-an-analysis-services-instance.md)  
  
  