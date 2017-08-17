---
title: "Analysis Services 업그레이드 | Microsoft Docs"
ms.custom: 
ms.date: 07/17/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
caps.latest.revision: 79
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3b3ad4ecf62f3a30882720140f2f362007f8428b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="upgrade-analysis-services"></a>Analysis Services 업그레이드
  Analysis Services 인스턴스는 [Analysis Services의 새로운 기능](../../analysis-services/what-s-new-in-analysis-services.md)에서 설명한 대로 현재 릴리스에 도입된 기능을 활용하기 위해 동일한 서버 모드의 SQL Server 버전으로 업그레이드할 수 있습니다.  
  
 동일한 하드웨어에서 실행 중인 다른 인스턴스와 독립적으로 각 인스턴스 내부를 업그레이드할 수 있습니다. 그러나 대부분의 관리자는 프로덕션 작업을 새 서버로 전송하기 전에 응용 프로그램 테스트에 대한 새 버전의 새 인스턴스를 설치하도록 선택합니다. 하지만 개발 또는 테스트 서버의 경우 내부 업그레이드가 더 편리할 수 있습니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]로 업그레이드하기 전에 다음을 검토하십시오.  

- [SQL Server 2017 릴리스 정보](../../sql-server/sql-server-2017-release-notes.md)는 알려진 문제 및 해결 방법을 설명합니다.  
- [SQL Server 2016 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md) 는 알려진 문제 및 해결 방법을 설명합니다.  
- [Analysis Services Backward Compatibility](../../analysis-services/analysis-services-backward-compatibility.md) 은(는) 지원되지 않고 사용되지 않는 기능 및 변경된 기능을 요약합니다. 모델, 스크립트 또는 사용자 지정 코드에 대한 제품 변경 내용의 영향을 평가하기 위해 이 목록을 정기적으로 검토해야 합니다. 일반적으로 기능 전환은 다음 주요 릴리스의 시험판 중에 발표됩니다.  
  
## <a name="server-upgrade"></a>서버 업그레이드  
 서버 및 데이터베이스를 업그레이드하기 위한 두 가지 기본 방법은 다음과 같습니다.  
  
-   **현재 위치 업그레이드** 는 기존 프로그램 파일을 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 프로그램 파일로 바꿉니다. 데이터베이스 위치는 동일하게 유지됩니다. 프로그램 폴더는 새 이름을 반영하여 업데이트됩니다.  
  
-   **병렬 업그레이드** 는 동시에 하드웨어를 업그레이드하지 않는 한 일반적으로 동일한 컴퓨터에 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 새 설치를 만듭니다. 이 방법은 새 인스턴스로 데이터베이스를 이동한 다음 필요에 따라 디스크 공간을 확보하도록 이전 버전을 제거해야 합니다.  
  
 수동으로 변경하지 않는 한 지정된 서버에 연결되어 있는 데이터베이스의 호환성 수준은 동일하게 유지됩니다.  
  
### <a name="in-place-upgrade"></a>내부 업그레이드  
 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] and, as part of the upgrade process, au인스턴스를matically migrate existing databases from the old instance 인스턴스를 the new instance. 메타데이터와 이진 데이터는 두 버전 간에 호환되므로 업그레이드 후 이 데이터를 보존하면 수동으로 마이그레이션할 필요가 없습니다.  
  
 기존 인스턴스를 업그레이드하려면 설치 프로그램을 실행하고 기존 인스턴스의 이름을 새 인스턴스의 이름으로 지정합니다.  
  
### <a name="side-by-side-upgrade"></a>병렬 업그레이드  
  
-   모든 데이터베이스를 백업하고 각각 복원할 수 있는지 확인합니다. [Backup and Restore of Analysis Services Databases](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)을 참조하세요.  
  
-   보고서의 하위 집합, 스프레드시트 또는 대시보드 스냅숏을 식별하여 업그레이드 후 서버 작업 확인에 대한 기준으로 나중에 사용합니다. 가능한 경우 업그레이드된 서버의 동일한 작업에 대한 비교를 실행할 수 있도록 성능 측정값을 수집합니다.  
  
-   교체하려고 하는 서버와 동일한 서버 모드(테이블 형식 또는 다차원)를 선택하는 Analysis Services의 새 인스턴스를 설치합니다. [Install Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)을 참조하세요.  
  
     포트 구성 및 서버 관리자 추가를 위해 설치 후 작업을 수행합니다. [설치 후 구성&#40;Analysis Services&#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md)을 참조하세요.  
  
-   각 데이터베이스를 연결 또는 복원합니다.  
  
-   DBCC를 실행하여 데이터베이스 무결성을 확인합니다. 모델 계층 구조 전체에서 분리된 개체에 대한 테스트를 사용하여 테이블 형식 모델은 보다 철저한 검사를 수행합니다. 다차원 모델의 경우 파티션 인덱스만 검사됩니다. [Analysis Services의 테이블 형식 및 다차원 데이터베이스에 대한 DBCC&#40;데이터베이스 일관성 검사기&#41;](../../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md)를 참조하세요.  
  
-   보고서, 스프레드시트 대시보드를 테스트하여 동작 또는 계산에 부정적인 변경 내용이 없는지 확인합니다. 다차원 및 테이블 형식 작업에 대한 성능 향상이 표시됩니다.  
  
-   모든 로그인 또는 사용 권한 문제를 수정하는 처리 작업을 테스트합니다. 연결에 기본 서비스 계정을 사용하는 경우 새 서비스는 다른 계정으로 실행됩니다. Analysis Services의 시작 계정에 대한 자세한 내용은 [서비스 계정 구성&#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)을 참조하세요.  
  
-   새 서버 이름을 사용하도록 스크립트를 조정하는 업그레이드된 서버에 대한 백업 및 복원 작업을 테스트합니다.  
  
## <a name="database-upgrade"></a>데이터베이스 업그레이드  
 이전 버전 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 작성된 데이터베이스는 이전 데이터베이스 호환성 수준 설정을 사용하여 업그레이드된 서버에서 실행됩니다. 일반적으로 새로운 기능에 대한 액세스 권한을 얻기 위해 높은 호환성 수준에서 작동하도록 데이터베이스 또는 모델을 업그레이드할 수 있지만 이렇게 하면 특정 서버 버전으로 바인딩됩니다.  
  
 데이터베이스를 업그레이드하려면 일반적으로 SSDT(SQL Server Data Tools)에서 모델을 업그레이드한 다음 업그레이드된 서버 인스턴스에 솔루션을 배포합니다. 최신 버전을 가져오려면 [SQL Server Data Tools 다운로드](https://msdn.microsoft.com/library/mt204009.aspx) 를 참조하세요.  
  
 테이블 형식 및 다차원 데이터베이스는 서로 다른 버전 경로를 따릅니다. 다차원 및 테이블 형식 모델 모두에 호환성 수준 1100이 있는 것은 우연의 일치입니다.  기능 변경 내용이 둘 중 하나에만 영향을 주는 경우 모드는 서로 다른 속도로 진행됩니다.  
  
 배경 목적으로 다음 표는 호환성 수준을 요약하지만 각 수준에서 제공하는 것을 이해하기 위해 세부 항목을 검토해야 합니다.  
  
||||  
|-|-|-|  
|테이블 형식|1200|SQL Server 2016|  
|테이블 형식|1103|SQL Server 2014|  
|테이블 형식|1100|SQL Server 2012|  
|다차원|1100|SQL Server 2012 이상|  
|다차원|1050|SQL Server 2005, 2008, 2008 R2|  
  
 자세한 내용은 [다차원 데이터베이스의 호환성 수준&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md) 및 [Analysis Services에서 테이블 형식 모델에 대한 호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)을 참조하세요.  
  
## <a name="tabular-model-upgrade-to-1200-compatibility-level"></a>1200 호환성 수준으로 테이블 형식 모델 업그레이드  
 테이블 형식 모델 및 데이터베이스는 SQL Server 2016에서 많은 정보를 활용합니다. 이 릴리스는 혼합 모드의 제거, 디자인 타임 시 데이터의 하위 집합을 검색하기 위한 쿼리 문의 추가 및 백 엔드 데이터베이스에서 행 권한 대신 DAX를 통한 행 수준 보안으로 단순화된 호환성 수준 1200에서 수정된 DirectQuery 모드를 제공합니다.  
  
 업그레이드하는 두 번째 이유는 모델 내부의 새 테이블 형식 메타데이터 생성입니다. 해당 레벨에서 만들어졌거나 해당 레벨로 업그레이드된 새로운 호환성 수준 1200에서 테이블 형식 모델은 해당 주요 요소를 설명하기 위해 모델, 테이블, 관계 및 열과 같은 개체 정의에 대한 기본 용어를 사용합니다.  
  
 테이블 형식 모델을 업그레이드하려면 이 릴리스에 대한 [SSDT(SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx) 작성 버전을 사용하여 **호환성 수준** 속성을 **SQL Server 2016 RTM(1200)**으로 변경합니다.  
  
 **CompatibilityLevel**을(를) 변경하기 위해 SSMS, 코드 또는 스크립트를 사용하지 마십시오. 자체적으로 속성 변경은 아무 작업도 수행하지 않습니다. 프로젝트를 다시 연 후 속성 업데이트에 대한 응답으로 SSDT에서 메타데이터 변환이 발생합니다.  
  
 늘 그렇듯이 업그레이드 전 버전으로 되돌려야 할 경우 업그레이드 전에 모델의 백업을 저장해야 합니다.  
  
1.  SSDT > 솔루션 탐색기에서 **model.bim**을 마우스 오른쪽 단추로 클릭하고 모델이 닫히고 새 창(코드 창)에서 다시 열리는 **코드 보기** 승인을 선택합니다.  
  
2.  모델은 XMLA 문서로 열립니다. 비교 목적으로 변환 이후 내용을 다른 파일에 복사합니다.(SSDT에서 새 XML 파일을 열 수 있습니다.)  
  
3.  **model.bim** 을 마우스 오른쪽 단추로 클릭하고 **디자이너 보기**로 다시 변경합니다.  
  
4.  **CompatibilityLevel** 을  **SQL Server 2016 RTM(1200)**으로 설정합니다.  
  
5.  이 단계를 되돌릴 수 없으므로 해당 작업을 확인하라는 메시지가 나타납니다. 계속하려면 **예** 를 클릭합니다. 프로젝트가 새로 고쳐집니다.  
  
6.  **model.bim** 을 마우스 오른쪽 단추로 클릭하고 **코드 보기**로 다시 변경합니다.  
  
     이제 테이블 형식 메타데이터를 사용하는 모델 정의는 JSON에 있습니다.  
  
 **메타데이터 변환**  
  
 변환 전 후 메타데이터 비교로 메타데이터가 JSON으로 변환되고 중복 정의로 잘린 것을 알 수 있습니다.  
  
 모델은 모든 기능을 유지합니다. 데이터 바인딩, 파티션 조각, 식, 개체 식별자, 개체 이름, 설명, 캡션, 번역 및 주석은 그대로 유지됩니다. 하지만 특정 개체를 참조하는 코드 또는 스크립트가 있는 경우 코드 재작성의 일부는 더 이상 존재하지 않는 개체에 대한 참조 제거를 포함합니다. 예를 들어 1050 또는 1103 모델은 큐브 외부에 있는 차원에 대한 섹션을 갖는 반면 1200 모델은 단일 개체로 테이블을 정의합니다.  
  
> [!NOTE]  
>  1050 및 1103의 이전 테이블 형식 호환성 수준은 지원되지만 사용되지 않습니다. SQL Server의 몇 가지 후속 릴리스에서 다차원 개체로 캐스팅하는 테이블 형식 모델은 더 이상 지원되지 않습니다. 발표는 [Deprecated Analysis Services Features in SQL Server 2016](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md) 을(를) 참조하세요.  
  
## <a name="post-upgrade-for-tabular-models-at-1200-compatibilitylevel"></a>1200 CompatibilityLevel에서 테이블 형식 모델에 대한 업그레이드 후  
 모델이 변환된 후 XMLA 대신 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)를 사용하여 데이터베이스 작업을 스크립팅합니다. TMSL은 모델이 1200일 때 SSMS에서 자동으로 생성됩니다. 테이블 형식 1200 데이터베이스를 대상으로 하는 사용자 지정 코드는 Microsoft.AnalysisServces.Tabular 네임스페이스에서 정의된 API를 사용해야 합니다. 처음부터 스크립트 및 코드를 작성해야 합니다. 기본 제공 변환에 대한 메커니즘이 없습니다. 자세한 내용은 [Analysis Services 개발자 설명서](../../analysis-services/analysis-services-developer-documentation.md) 를 참조하세요.  
  
 또한 테이블 형식 모델에 호환성 수준 1200에서만 지원되는 다음 기능을 추가할 수 있습니다.  
  
-   모델링 목적 및 단순한 구성을 위해 모델의 DAX를 통한 행 수준 보안, 더 많은 데이터 원본, 데이터 하위 집합을 지원하는 DirectQuery 구현.  
  
-   계산 열  
  
-   표시 폴더  
  
## <a name="upgrade-tabular-models-in-directquery-mode"></a>DirectQuery 모드에서 테이블 형식 모델 업그레이드  
 DirectQuery에 대해 구성된 기존 테이블 형식 모델의 내부 업그레이드를 수행할 수 없습니다. DirectQuery의 새 구현에는 작은 구성 사용 공간이 있으며 모든 설정을 이식할 수 없습니다.  
  
1.  SSDT에서 모델이 메모리 내 저장소를 사용하도록 **DirectQuery** 모드를 해제합니다. 자세한 내용은 [DirectQuery 디자인 모드를 사용하도록 설정(SSAS 테이블 형식)](https://msdn.microsoft.com/library/hh270245.aspx) 을 참조하세요.  
  
2.  **CompatibilityLevel** 을 SQL Server 2016(RTM) 1200으로 설정합니다.  
  
3.  모델을 저장하고 다시 작성하거나 배포합니다.  
  
4.  **DirectQuery** 을(를) 다시 켭니다. 자세한 지침은 [DirectQuery for Tabular 1200 models](http://msdn.microsoft.com/library/4227977e-7368-4d45-b78f-24076882e7a8) 을(를) 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [DirectQuery 모드&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Analysis Services의 새로운 기능](../../analysis-services/what-s-new-in-analysis-services.md)   
 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)   
 [SharePoint용 파워 피벗 업그레이드](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [다차원 및 데이터 마이닝 모드에서 Analysis Services 설치](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [설치 마법사를 사용하여 SQL Server 2016으로 업그레이드&#40;설치 프로그램&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  

