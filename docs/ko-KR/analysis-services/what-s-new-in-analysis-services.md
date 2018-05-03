---
title: 기능 Analysis Services의 새로운 | Microsoft Docs
ms.custom: ''
ms.date: 03/24/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
ms.assetid: aa69c299-b8f4-4969-86d8-b3292fe13f08
caps.latest.revision: 97
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 75d2f8519d66ca80b90477711fd5b41dbc1f5100
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="what39s-new-in-analysis-services"></a>기능 Analysis Services의 새로운
[!INCLUDE[ssas-appliesto-sql2016](../includes/ssas-appliesto-sql2016.md)]

SQL Server 2016 Analysis Services는 많은 향상 된 성능, 쉽게 솔루션 작성, 자동화 된 데이터베이스 관리를 제공 하는 향상 된 새로운 기능, 향상 된 관계가 양방향 교차 필터링, 병렬 파티션 처리 및 등 다양 합니다. 이번 릴리스에서 향상된 기능 대부분의 중심에는 테이블 형식 model 데이터베이스에 대한 새로운 호환성 수준 1200이 있습니다.     

## <a name="azure-analysis-services"></a>Azure Analysis Services
2016 SQL PASS Conference에서 발표된 Analysis Services를 이제 클라우드에서 Azure 서비스로 사용할 수 있습니다. **Azure Analysis Services** 이상은 1200 호환성 수준의 테이블 형식 모델을 지원 합니다. DirectQuery, 파티션, 행 수준 보안, 양방향 관계, 변환이 모두 지원됩니다. 자세한 내용을 알아보고 무료 시험 버전을 사용하려면 [Azure Analysis Services](http://azure.microsoft.com/services/analysis-services/)를 참조하세요. 

## <a name="whats-new-in-sql-server-2016-service-pack-1-sp1-analysis-services"></a>SQL Server 2016 서비스 팩 1(SP1) Analysis Services의 새로운 기능

[SQL Server 2016 SP1 다운로드](http://www.microsoft.com/download/details.aspx?id=54276) 

SQL Server 2016 Service SP1 Analysis Services는 NUMA(Non-Uniform Memory Access) 인식 및 **Intel TBB** (Intel Threading Building Blocks)를 기반으로 한 최적화된 메모리 할당을 통해 향상된 성능 및 확장성을 제공합니다. 이 새로운 기능은 더 적은 수의 보다 강력한 엔터프라이즈 서버에서 더 많은 사용자를 지원하여 TCO(총 소유 비용)를 낮추는 데 도움이 됩니다. 

특히 SQL Server 2016 SP1 Analysis Services는 다음과 같은 주요 영역에서 향상된 기능을 제공합니다.

-   **NUMA 인식** - NUMA에 대한 지원을 개선하기 위해 이제 Analysis Services 내의 메모리 내(VertiPaq) 엔진이 각 NUMA 노드에서 별도의 작업 큐를 유지 관리합니다. 따라서 세그먼트에 대해 메모리가 할당된 것과 동일한 노드에서 세그먼트 검색 작업이 실행되도록 합니다. 기본적으로 NUMA 인식은 4 개 이상의 NUMA 노드가 있는 시스템에서만 사용됩니다. 2노드 시스템에서는 할당된 원격 메모리에 액세스하는 비용이 일반적으로 NUMA 고유 정보를 관리하는 오버헤드를 보증하지 않습니다.
-   **메모리 할당** - Analysis Services는 모든 코어에 별도의 메모리 풀을 제공하는 확장 가능한 할당자인 Intel Threading Building Blocks로 가속화되었습니다. 코어 수가 증가하면 시스템이 거의 선형으로 확장됩니다.
-   **힙 조각화** - 또한 Intel TBB 기반의 확장 가능한 할당자를 사용하면 Windows 힙에서 발생하는 것으로 나타난 힙 조각화로 인한 성능 문제를 완화할 수 있습니다.

성능 및 확장성 테스트는 대규모의 다중 노드 엔터프라이즈 서버에서 SQL Server 2016 SP1 Analysis Services를 실행하는 경우 쿼리 처리량이 크게 향상되는 것을 보여 주었습니다.


## <a name="whats-new-in-sql-server-2016-analysis-services"></a>SQL Server 2016 Analysis Services의 새로운 기능

이번 릴리스에서 향상된 기능 대부분은 테이블 형식 모델과 관련이 있지만 다차원 모델에서도 여러 가지 기능이 향상되었습니다. 예를 들어 DB2 및 Oracle과 같은 데이터 원본에 대한 고유 카운트 ROLAP 최적화, Excel 2016의 드릴스루 다중 선택 지원 및 Excel 쿼리 최적화가 있습니다.    

#### <a name="get-the-latest-tools"></a>최신 도구 다운로드
이 릴리스에서 모든 향상 된 기능을 완전히 활용을 사용 하려면 최신 버전의 SSDT 및 SSMS를 설치 해야 합니다.    
- [SSDT(SQL Server Data Tools) 다운로드](http://msdn.microsoft.com/library/mt204009.aspx)    
- [SSMS(SQL Server Management Studio) 다운로드](http://msdn.microsoft.com/library/mt238290.aspx)   

사용자 지정 AMO 종속 응용 프로그램이 있으면 업데이트된 AMO 버전을 설치해야 할 수 있습니다. 자세한 내용은 [Analysis Services 데이터 공급자&#40;AMO, ADOMD.NET, MSOLAP&#41; 설치](../analysis-services/instances/install-windows/install-analysis-services-data-providers-amo-adomd-net-msolap.md)를 참조하세요.    

 #### <a name="technet-virtual-labs-sql-server-2016-analysis-services"></a>TechNet 가상 랩: SQL Server 2016 Analysis Services
보다 효과적으로 배우려면 [What's New in SQL Server 2016 Analysis Services Virtual Lab](http://vlabs.holsystems.com/vlabs/technet?eng=VLabs&auth=none&src=vlabs&altadd=true&labid=23110&lod=true)(SQL Server 2016 Analysis Services의 새로운 기능 가상 랩)을 단계별로 수행하세요.
이 랩에서는 xEvents(확장 이벤트) 만들기 및 모니터, 테이블 형식 프로젝트를 호환성 수준 1200으로 업그레이드, Visual Studio 구성 작업, 새 계산 기능 구현, 새 테이블 관계 기능 구현, 표시 폴더 구성, 모델 번역 관리, 새 TMSL(Tabular Model Scripting Language) 작업, PowerShell 사용 및 새로운 DirectQuery 모드 기능 체험을 수행합니다.

## <a name="modeling"></a>모델링    
### <a name="improved-modeling-performance-for-tabular-1200-models"></a>테이블 형식 1200 모델의 모델링 성능 향상    
테이블 형식 1200 모델에서는 SSDT의 메타데이터 작업이 테이블 형식 1100 또는 1103 모델보다 훨씬 더 빠릅니다. 비교해 보면, 같은 하드웨어에서 23개 테이블이 포함된 SQL Server 2014 호환성 수준(1103)으로 설정된 모델에 대한 관계를 만드는 데는 3초가 걸리지만, 호환성 수준 1200으로 설정된 모델에서 동일한 관계를 만드는 데는 1초도 걸리지 않습니다.    
### <a name="project-templates-added-for-tabular-1200-models-in-ssdt"></a>SSDT의 테이블 형식 1200 모델에 프로젝트 템플릿 추가    
이번 릴리스부터는 관계형 및 BI 프로젝트를 빌드하는 데 두 가지 SSDT 버전이 더 이상 필요하지 않습니다. [Visual Studio 2015용 SQL Server Data Tools](http://msdn.microsoft.com/library/mt204009.aspx) 는 호환성 수준 1200에서 모델을 빌드하는 데 사용되는 **Analysis Services 테이블 형식 프로젝트** 를 비롯하여 Analysis Services 솔루션용 프로젝트 템플릿을 추가합니다. 다차원 및 데이터 마이닝 솔루션용 기타 Analysis Services 프로젝트 템플릿도 포함되지만 이전 릴리스와 같은 기능 수준(1100 또는 1103)입니다.    
### <a name="display-folders"></a>표시 폴더
이제 테이블 형식 1200 모델에 표시 폴더를 사용할 수 있습니다. SQL Server Data Tools에서 정의되고 Excel 또는 Power BI Desktop 등의 클라이언트 응용 프로그램에서 렌더링된 표시 폴더를 사용하여 많은 측정값을 개별 폴더로 구성하여 필드 목록을 더 쉽게 탐색하기 위한 시각적 계층 구조를 추가할 수 있습니다.
### <a name="bi-directional-cross-filtering"></a>양방향 교차 필터링
이번 릴리스의 새로운 기능에는 테이블 형식 모델에서 양방향 교차 필터를 사용하는 기본 제공 접근 방식이 있습니다. 이 방식을 사용하면 테이블 관계에서 필터 컨텍스트를 전파하기 위한 수동 DAX 해결 방법이 필요 없습니다. 필터는 높은 수준의 확신도를 기반으로 방향을 설정할 수 있을 경우에만 자동 생성됩니다. 테이블 관계에서 여러 쿼리 경로의 형식에 모호성이 있으면 필터가 자동으로 생성되지 않습니다. 자세한 내용은 [SQL Server 2016 Analysis Services의 테이블 형식 모델에 대한 양방향 교차 필터](../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) 를 참조하세요.
 ### <a name="translations"></a>번역    
 이제 번역된 메타데이터를 테이블 형식 1200 모델에 저장할 수 있습니다. 모델의 메타데이터에는 **Culture**에 대한 필드, 번역된 캡션, 번역된 설명이 포함됩니다. 번역을 추가하려면 **에서** > **모델** 번역 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]명령을 사용합니다. 자세한 내용은 [테이블 형식 모델 번역&#40;Analysis Services&#41;](../analysis-services/tabular-models/translations-in-tabular-models-analysis-services.md)을 참조하세요.    
 ### <a name="pasted-tables"></a>붙여넣은 테이블    
 이제 모델에 붙여넣은 테이블이 포함되어 있으면 1100 또는 1103 테이블 형식 모델을 1200으로 업그레이드할 수 있습니다. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]를 사용하는 것이 좋습니다. SSDT에서 **CompatibilityLevel** 을 1200으로 설정하고 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 의 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스에 배포합니다. 자세한 내용은 [Compatibility Level for Tabular models in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) 를 참조하세요.    
 ### <a name="calculated-tables-in-ssdt"></a>SSDT의 계산된 테이블    
*계산된 테이블* 은 SSDT의 DAX 식 또는 쿼리를 기반으로 하는 모델 전용 생성입니다. 데이터베이스에 배포되면 계산된 테이블을 일반 테이블과 구분할 수 없습니다.    

 기존 테이블을 특정 역할로 표시할 새 테이블을 만드는 등의 다양한 용도에 계산된 테이블을 사용합니다. 기본적인 예로는 주문 날짜, 배송 날짜 등의 여러 컨텍스트에서 작동하는 날짜 테이블이 있습니다. 지정된 역할에 대한 계산된 테이블을 만들면 테이블 관계를 활성화하여 계산된 테이블을 사용하여 쿼리 또는 데이터 조작을 이용할 수 있습니다. 기존 테이블의 부분을 모델에만 있는 완전히 새로운 테이블로 결합하는 데도 계산된 테이블을 사용할 수 있습니다.  참조 [계산 테이블을 만들](../analysis-services/tabular-models/create-a-calculated-table-ssas-tabular.md) 자세한 합니다.    
 ### <a name="formula-fixup"></a>수식 수정    
 테이블 형식 1200 모델의 수식 수정을 사용하면 SSDT에서는 이름이 바뀐 열 또는 테이블을 참조하고 있는 모든 측정값을 자동으로 업데이트합니다.    
 ### <a name="support-for-visual-studio-configuration-manager"></a>Visual Studio 구성 관리자 지원    
 테스트 및 사전 프로덕션 환경과 같은 여러 환경을 지원하기 위해 개발자는 Visual Studio의 구성 관리자를 사용하여 여러 프로젝트 구성을 만들 수 있습니다. 다차원 모델에서는 이미 이 기능이 사용되지만 테이블 형식 모델에서는 사용되지 않습니다. 이번 릴리스부터는 구성 관리자를 사용하여 여러 서버에 배포할 수 있습니다.    

## <a name="instance-management"></a>인스턴스 관리    
 ### <a name="administer-tabular-1200-models-in-ssms"></a>SSMS에서 테이블 형식 1200 모델 관리    
 이번 릴리스에서 테이블 형식 서버 모드의 Analysis Services 인스턴스는 모든 호환성 수준(1100, 1103, 1200)에서 테이블 형식 모델을 실행할 수 있습니다. 최신 [SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx) 가 업데이트되어 1200 호환성 수준에서 테이블 형식 모델에 대한 속성을 표시하고 데이터베이스 모델 관리를 제공합니다.    
 ### <a name="parallel-processing-for-multiple-table-partitions-in-tabular-models"></a>테이블 형식 모델의 여러 테이블 파티션에 대한 병렬 처리    
 이번 릴리스에는 파티션이 두 개 이상 포함된 테이블에 대한 새로운 병렬 처리 기능이 포함되어 처리 성능이 향상됩니다. 이 기능에 대한 구성 설정은 없습니다. 파티션을 구성 하 고 테이블을 처리 하는 방법에 대 한 자세한 내용은 참조 [테이블 형식 모델 파티션](../analysis-services/tabular-models/tabular-model-partitions-ssas-tabular.md)합니다.    
 ### <a name="add-computer-accounts-as-administrators-in-ssms"></a>SSMS에서 관리자로 컴퓨터 계정 추가    
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 관리자는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 사용하여 컴퓨터 계정을 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 관리자 그룹의 멤버로 구성할 수 있습니다. **사용자 또는 그룹 선택** 대화 상자에서 컴퓨터 도메인의 **위치** 를 선택하고 **Computers** 개체 형식을 추가합니다. 자세한 내용은 [Analysis Services 인스턴스에 서버 관리 권한 부여](../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)를 참조하세요.    
 ### <a name="dbcc-for-analysis-services"></a>Analysis Services에 대한 DBCC    
 DBCC(Database Consistency Checker)는 내부적으로 실행되어 데이터베이스 로드 시 발생할 수 있는 데이터 손상 문제를 감지하지만, 데이터나 모델에 문제가 있다고 의심될 경우 필요 시 실행될 수도 있습니다. DBCC는 모델이 테이블 형식인지, 아니면 다차원 형식인지에 따라 다른 검사를 실행합니다. 자세한 내용은 [Analysis Services의 테이블 형식 및 다차원 데이터베이스에 대한 DBCC&#40;데이터베이스 일관성 검사기&#41;](../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md)를 참조하세요.    
 ### <a name="extended-events-updates"></a>확장 이벤트 업데이트    
 이번 릴리스에서는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 확장 이벤트를 구성 및 관리하기 위한 그래픽 사용자 인터페이스를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에 추가합니다. 서버 활동을 실시간 모니터링하거나, 더 신속한 분석을 위해 메모리에 로드된 세션 데이터를 유지하거나, 오프라인 분석을 위해 데이터 스트림을 파일에 저장하도록 라이브 데이터 스트림을 설정할 수 있습니다. 자세한 내용은 [SQL Server 확장 이벤트를 사용하여 Analysis Services 모니터](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) 및 [Using extended events with Analysis Services (Guy in a Cube blog post and video)](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx)(Analysis Services에서 확장 이벤트 사용(큐브 블로그 게시물 및 비디오의 사람))를 참조하세요.    



## <a name="scripting"></a>스크립팅
 ### <a name="powershell-for-tabular-models"></a>테이블 형식 모델에 대한 PowerShell    
 이번 릴리스에서는 호환성 수준 1200의 테이블 형식 모델에 대한 PowerShell 기능이 향상되었습니다. 적용되는 모든 cmdlet과 테이블 형식 모드 관련 cmdlet인 [Invoke-ProcessASDatabase](../analysis-services/powershell/invoke-processasdatabase.md) 및 [Invoke-ProcessTable cmdlet](../analysis-services/powershell/invoke-processtable-cmdlet.md)을 사용할 수 있습니다.    
 ### <a name="ssms-scripting-database-operations"></a>SSMS 스크립팅 데이터베이스 작업    
 이제 [최신 SSMS(SQL Server Management Studio)](http://msdn.microsoft.com/library/mt238290.aspx)에서 스크립트는 Create, Alter, Delete, Backup, Restore, Attach, Detach를 비롯한 데이터베이스 명령에 사용됩니다. 출력은 JSON의 TMSL(Tabular Model Scripting Language)입니다. 자세한 내용은 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)를 참조하세요.    
 ### <a name="analysis-services-execute-ddl-task"></a>Analysis Services DDL 실행 태스크    
 이제[Analysis Services 실행 DDL 태스크](../integration-services/control-flow/analysis-services-execute-ddl-task.md) 에서도 TMSL(Tabular Model Scripting Language) 명령을 허용합니다.     
 ### <a name="ssas-powershell-cmdlet"></a>SSAS PowerShell cmdlet    
 SSAS PowerShell cmdlet **Invoke-ASCmd** 에서 TMSL(Tabular Model Scripting Language) 명령을 허용합니다. 기타 SSAS PowerShell cmdlet은 새 테이블 형식 메타데이터를 사용하도록 이후 릴리스에서 업데이트될 수 있습니다(예외는 릴리스 정보에 명시되어 있음).    
자세한 내용은 [Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) 를 참조하세요.    
 ### <a name="tabular-model-scripting-language-tmsl-supported-in-ssms"></a>SSMS에서 TMSL(Tabular Model Scripting Language) 지원    
  [최신 버전의 SSMS](http://msdn.microsoft.com/library/mt238290.aspx)를 사용하여 테이블 형식 1200 모델에 대한 대부분의 관리 태스크를 자동화하는 스크립트를 만들 수 있습니다. 현재 모든 수준의 Process 및 데이터베이스 수준의 CREATE, ALTER, DELETE 작업을 스크립팅할 수 있습니다.    
    
 TMSL이 **model**, **table**, **relationship** 등의 네이티브 설명자를 사용하여 테이블 형식 메타데이터를 설명한다는 점을 제외하고 기능상, TMSL은 다차원 개체 정의를 제공하는 XMLA ASSL 확장에 해당합니다. 스키마에 대한 자세한 내용은 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)를 참조하세요.    
    
 테이블 형식 모델에 대해 생성된 JSON 기반 스크립트가 다음과 같이 표시될 수 있습니다.    
    
```    
{    
  "create": {    
    "database": { 
      "name": "AdventureWorksTabular1200",    
      "id": "AdventureWorksTabular1200",    
      "compatibilityLevel": 1200,    
      "readWriteMode": "readWrite",    
      "model": {}    
    }    
  }    
}    
```    

페이로드는 위에 표시된 예제처럼 최소화되거나 전체 개체 정의 집합으로 세밀하게 장식될 수 있는 JSON 문서입니다. [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../analysis-services/tabular-model-scripting-language-tmsl-reference.md)에서는 구문에 대해 설명합니다.

데이터베이스 수준에서 CREATE, ALTER 및 DELETE 명령은 TMSL 스크립트를 친숙한 XMLA 창에 출력합니다.  이 릴리스에서는 Process와 같은 기타 명령도 스크립팅할 수 있습니다. 이후 릴리스에서 다른 많은 작업에 대한 스크립트 지원이 추가될 수 있습니다.    

**스크립트 가능한 명령** | **설명**
--------------- | ----------------
만들기|데이터베이스, 연결 또는 파티션을 추가합니다. ASSL에서는 CREATE에 해당합니다.
createOrReplace|이전 버전을 덮어써서 기존 개체 정의(데이터베이스, 연결 또는 파티션)를 업데이트합니다. ASSL에서는 AllowOverwrite가 true로 설정되고 ObjectDefinition이 ExpandFull로 설정된 ALTER에 해당합니다.
삭제|개체 정의를 제거합니다. ASSL에서는 DELETE에 해당합니다.
refresh|개체를 처리합니다. ASSL에서는 PROCESS에 해당합니다.

## <a name="dax"></a>DAX
### <a name="improved-dax-formula-editing"></a>DAX 수식 편집 기능 향상
수식 입력줄이 업데이트되어 구문 색 지정을 사용하여 함수, 필드, 측정값을 구분하는 방식으로 더 쉽게 수식을 작성할 수 있습니다. 이 기능은 지능형 함수 및 필드 제안을 제공하고 오류 *물결선*을 사용하여 DAX 식의 일부가 잘못된 경우 잘못된 부분을 알립니다. 또한 여러 줄(Alt + Enter) 및 들여쓰기(Tab)를 사용할 수 있습니다. 이제 수식 입력줄에서 측정값 부분으로 주석을 작성할 수 있습니다. “//”를 입력하면 같은 줄에서 이 문자 뒤의 모든 내용이 주석으로 간주됩니다.

### <a name="dax-variables"></a>DAX 변수    
이번 릴리스에서는 DAX의 변수를 지원합니다. 이제 나중에 다른 측정값 식에 인수로 전달될 수 있는 명명된 변수로 식의 결과를 저장할 수 있습니다. 일단 변수 식에 대한 결과 값이 계산되면 변수가 다른 식에서 참조되더라도 해당 값은 변경되지 않습니다. 자세한 내용은 [VAR Function](http://msdn.microsoft.com/library/mt243785.aspx)(VAR 함수)을 참조하세요.    
### <a name="new-dax-functions"></a>새로운 DAX 함수
이번 릴리스에서 DAX는 Power BI에서 보다 빠른 계산 및 향상된 시각화를 지원하기 위해 50 가지 이상의 새로운 함수를 사용합니다. 자세한 내용은 [New DAX Functions(새 DAX 함수)](http://msdn.microsoft.com/library/mt704075.aspx)를 참조하세요.
### <a name="save-incomplete-measures"></a>완료되지 않은 측정값 저장
완료되지 않은 DAX 측정값을 테이블 형식 1200 모델 프로젝트에 직접 저장하고 계속할 수 있을 때 다시 선택할 수 있습니다.
### <a name="additional-dax-enhancements"></a>DAX의 추가 기능 향상
- 비어 있지 않은 계산 - 비어 있지 않은 계산에 필요한 검색 수를 줄입니다.
- 측정값 결합 - 동일한 테이블의 여러 측정값이 단일 저장소 엔진 쿼리로 결합됩니다.
- 그룹화 집합 - 쿼리에서 다양하게 세분화된 측정값(합계/연도/월)을 요청하는 경우 단일 쿼리는 최하위 수준에서 전송되고 나머지 세분성은 최하위 수준에서 파생됩니다.     
- 중복 조인 제거 - 저장소 엔진에 대한 단일 쿼리에서 차원 열과 측정값을 모두 반환합니다.
- IF/SWITCH의 엄격한 평가 - 조건이 false인 분기는 더 이상 저장소 엔진 쿼리를 생성하지 않습니다. 이전에는 분기가 적극적으로 평가되었지만 결과는 나중에 삭제되었습니다.     
    
## <a name="developer"></a>개발자    
 ### <a name="microsoftanalysisservicestabular-namespace-for-tabular-1200-programmability-in-amo"></a>AMO의 테이블 형식 1200 프로그래밍 기능에 대한 Microsoft.AnalysisServices.Tabular 네임스페이스
 AMO(Analysis Services 관리 개체)가 업데이트되어 SQL Server 2016 Analysis Services의 테이블 형식 인스턴스를 관리하기 위한 새 테이블 형식 네임스페이스를 포함하고 프로그래밍 방식으로 테이블 형식 1200 모델을 만들거나 수정하는 데이터 정의 언어를 제공합니다. API에 대한 자세한 내용은 [Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) 를 참조하세요.    
 ### <a name="analysis-services-management-objects-amo-updates"></a>AMO(Analysis Services Management Objects) 업데이트
 [AMO&#40;Analysis Services Management Objects&#41;](http://msdn.microsoft.com/library/mt436122.aspx)가 두 번째 어셈블리인 Microsoft.AnalysisServices.Core.dll을 포함하도록 리팩터링되었습니다. 새 어셈블리는 서버, 데이터베이스 및 역할과 같이 서버 모드와 관계없이 Analysis Services에 광범위한 응용 프로그램이 있는 일반 클래스를 분리합니다.    
    
 이전에 이들 클래스는 원래 Microsoft.AnalysisServices 어셈블리의 부분이었습니다. 이들 클래스를 새 어셈블리로 이동하면 이후 AMO로 확장할 수 있는 환경이 조성되고 제네릭 API와 컨텍스트별 API를 분명히 구분됩니다.    
    
 기존 응용 프로그램은 새 어셈블리의 영향을 받지 않습니다. 그러나 어떤 이유로 새 AMO 어셈블리를 사용하여 응용 프로그램을 다시 빌드해야 한다면 Microsoft.AnalysisServices.Core에 대한 참조를 추가해야 합니다.    
    
 마찬가지로 이제 AMO를 로드하고 호출하는 PowerShell 스크립트는 Microsoft.AnalysisServices.Core.dll을 로드해야 합니다. 모든 스크립트를 업데이트 해야 합니다.  

### <a name="json-editor-for-bim-files"></a>BIM 파일에 대한 JSON 편집기
Visual Studio 2015의 코드 보기는 테이블 형식 1200 모델에 대한 JSON 형식으로 BIM 파일을 렌더링합니다. Visual Studio 버전에 따라 BIM 파일이 JSON에서 기본 제공 JSON 편집기를 통해 렌더링되는지, 아니면 단순 텍스트로 렌더링되는지 결정됩니다.

모델의 섹션을 확장 및 축소하는 기능이 포함된 JSON 편집기를 사용하려면 SQL Server Data Tools의 최신 버전 및 Visual Studio 2015(무료 Community Edition을 비롯한 모든 버전)가 필요합니다. SSDT 또는 Visual Studio의 모든 다른 버전의 경우 BIM 파일은 JSON에서 단순 텍스트로 렌더링됩니다.
최소한 빈 모델에는 다음 JSON이 포함됩니다.

    ```    
    {    
      "name": "SemanticModel",
      "id": "SemanticModel",
      "compatibilityLevel": 1200,
      "readWriteMode": "readWrite",
      "model": {}
    }    
    ```    
    
> [!WARNING]    
> JSON을 직접 편집하지 마세요. 직접 편집하면 모델이 손상될 수 있습니다.    
 ### <a name="new-elements-in-ms-csdlbi-20-schema"></a>MS-CSDLBI 2.0 스키마의 새로운 요소    
 [MS-CSDLBI] 2.0 스키마에 정의된 **TProperty** 복합 형식에 다음 요소가 추가되었습니다.    
    
|요소|정의|    
|-------------|----------------|    
|DefaultValue|쿼리를 계산할 때 사용되는 값을 지정하는 속성입니다. DefaultValue 속성은 선택 사항이지만, 멤버의 값을 집계할 수 없을 경우 자동으로 선택됩니다.|    
|통계|열과 연결된 기본 데이터의 통계 집합입니다. 이러한 통계는 TPropertyStatistics 복합 형식에 의해 정의되고 비즈니스 인텔리전스 주석이 포함된 개념 스키마 정의 파일 형식의 섹션 2.1.13.5에 설명된 대로 계산 시 생성에 큰 비용이 들지 않을 경우에만 제공됩니다.|    
    
## <a name="directquery"></a>DirectQuery    
### <a name="new-directquery-implementation"></a>새 DirectQuery 구현    
이번 릴리스에서는 테이블 형식 1200 모델의 DirectQuery가 크게 향상되었습니다. 다음은 요약 내용입니다.    
-   이제 DirectQuery에서 향상된 성능을 제공하는 보다 간단한 쿼리를 생성합니다.    
-   모델 디자인 및 테스트에 사용되는 샘플 데이터 집합을 추가로 제어할 수 있습니다.    
-   이제 테이블 형식 1200 모델의 DirectQuery 모드에서 RLS(행 수준 보안)가 지원됩니다. 이전에는 RLS를 사용하여 DirectQuery 모드에서 테이블 형식 모델을 배포할 수 없도록 했습니다.    
-   DirectQuery 모드의 테이블 형식 1200 모델에 대해서는 계산 열이 지원되지 않습니다. 이전에는 계산 열을 사용하여 DirectQuery 모드에서 테이블 형식 모델을 배포할 수 없도록 했습니다.    
-   성능 최적화에 VertiPaq 및 DirectQuery에 대한 중복 조인 제거가 포함됩니다. 

### <a name="new-data-sources-for-directquery-mode"></a>DirectQuery 모드의 새 데이터 원본    
 이제 DirectQuery 모드에서 테이블 형식 1200 모델에 대해 지원 되는 데이터 원본 Oracle, Teradata 및 Microsoft 분석 플랫폼 (이전의 병렬 데이터 웨어하우스)를 포함 합니다.    
    
자세한 내용은 참고 [DirectQuery 모드](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)합니다.    

## <a name="see-also"></a>관련 항목:
[Analysis Services 팀 블로그](http://blogs.msdn.microsoft.com/analysisservices/)    
[SQL Server 2016의 새로운 기능](../sql-server/what-s-new-in-sql-server-2016.md)    
     

