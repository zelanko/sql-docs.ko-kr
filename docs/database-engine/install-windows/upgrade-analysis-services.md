---
title: Analysis Services 업그레이드 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
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
author: Minewiskan
ms.author: owend
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: erikre
ms.openlocfilehash: dbf87499f1bc5c23ae272daa393ef981a97e66d5
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892563"
---
# <a name="upgrade-analysis-services"></a>Analysis Services 업그레이드

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  Analysis Services 인스턴스는 [Analysis Services의 새로운 기능](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)에서 설명한 대로 현재 릴리스에 도입된 기능을 활용하기 위해 동일한 서버 모드의 SQL Server 버전으로 업그레이드할 수 있습니다.  
  
 동일한 하드웨어에서 실행 중인 다른 인스턴스와 독립적으로 각 인스턴스 내부를 업그레이드할 수 있습니다. 그러나 대부분의 관리자는 프로덕션 작업을 새 서버로 전송하기 전에 애플리케이션 테스트에 대한 새 버전의 새 인스턴스를 설치하도록 선택합니다. 하지만 개발 또는 테스트 서버의 경우 내부 업그레이드가 더 편리할 수 있습니다.  
  
## <a name="server-upgrade"></a>서버 업그레이드  
 서버 및 데이터베이스를 업그레이드하기 위한 두 가지 기본 방법은 다음과 같습니다.  
  
> [!NOTE]
> 수동으로 변경하지 않는 한 지정된 서버에 연결되어 있는 데이터베이스의 호환성 수준은 동일하게 유지됩니다.
   
  
### <a name="in-place-upgrade"></a>내부 업그레이드  
 업그레이드 프로세스는 기존 데이터베이스를 이전 인스턴스에서 새 인스턴스로 자동으로 마이그레이션합니다. 메타데이터와 이진 데이터는 두 버전 간에 호환되므로 업그레이드 후 이 데이터를 보존하면 수동으로 마이그레이션할 필요가 없습니다.  
  
 기존 인스턴스를 업그레이드하려면 설치 프로그램을 실행하고 기존 인스턴스의 이름을 새 인스턴스의 이름으로 지정합니다.  
  
### <a name="side-by-side-upgrade"></a>병렬 업그레이드  
  
-   모든 데이터베이스를 백업하고 각각 복원할 수 있는지 확인합니다. 자세한 내용은 [Analysis Services 데이터베이스 백업 및 복원](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)을 참조하세요.  
  
-   보고서의 하위 집합, 스프레드시트 또는 대시보드 스냅샷을 식별하여 업그레이드 후 서버 작업 확인에 대한 기준으로 나중에 사용합니다. 가능한 경우 업그레이드된 서버의 동일한 작업에 대한 비교를 실행할 수 있도록 성능 측정값을 수집합니다.  
  
-   교체하려고 하는 서버와 동일한 서버 모드(테이블 형식 또는 다차원)를 선택하는 Analysis Services의 새 인스턴스를 설치합니다. 
  
     포트 구성 및 서버 관리자 추가를 위해 설치 후 작업을 수행합니다. 자세한 내용은 [설치 후 구성&#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/instances/post-install-configuration-analysis-services)을 참조하세요.  
  
-   각 데이터베이스를 연결 또는 복원합니다.  
  
-   DBCC를 실행하여 데이터베이스 무결성을 확인합니다. 모델 계층 구조 전체에서 분리된 개체에 대한 테스트를 사용하여 테이블 형식 모델은 보다 철저한 검사를 수행합니다. 다차원 모델의 경우 파티션 인덱스만 검사됩니다. 자세한 내용은 [Analysis Services의 테이블 형식 및 다차원 데이터베이스에 대한 DBCC&#40;데이터베이스 일관성 검사기&#41;](https://docs.microsoft.com/analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services)를 참조하세요.  
  
-   보고서, 스프레드시트 대시보드를 테스트하여 동작 또는 계산에 부정적인 변경 내용이 없는지 확인합니다. 다차원 및 테이블 형식 작업에 대한 성능 향상이 표시됩니다.  
  
-   모든 로그인 또는 사용 권한 문제를 수정하는 처리 작업을 테스트합니다. 연결에 기본 서비스 계정을 사용하는 경우 새 서비스는 다른 계정으로 실행됩니다. 자세한 내용은 [서비스 계정 구성&#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/instances/configure-service-accounts-analysis-services)을 참조하세요.  
  
-   새 서버 이름을 사용하도록 스크립트를 조정하는 업그레이드된 서버에 대한 백업 및 복원 작업을 테스트합니다.  
  
## <a name="database-upgrade"></a>데이터베이스 업그레이드  
 이전 버전에서 작성된 데이터베이스는 원래 호환성 수준 설정을 사용하여 업그레이드된 서버에서 실행됩니다. 일반적으로 새로운 기능에 대한 액세스 권한을 얻기 위해 높은 호환성 수준에서 작동하도록 데이터베이스 또는 모델을 업그레이드할 수 있지만 이렇게 하면 특정 서버 버전으로 바인딩됩니다.  
  
 데이터베이스를 업그레이드하려면 일반적으로 SSDT(SQL Server Data Tools)에서 모델을 업그레이드한 다음 업그레이드된 서버 인스턴스에 솔루션을 배포합니다.
  
 테이블 형식 및 다차원 데이터베이스는 서로 다른 버전 경로를 따릅니다. 다차원 및 테이블 형식 모델 모두에 비슷한 숫자의 호환성 수준이 있는 것은 우연의 일치입니다.  기능 변경 내용이 둘 중 하나에만 영향을 주는 경우 모드는 서로 다른 속도로 진행됩니다.  
  
 배경 지식을 제공할 목적으로 다음 표에 호환성 수준이 요약되어 있지만, 각 수준에서 제공하는 내용을 정확하게 이해하려면 세부 문서를 검토해야 합니다.  
  
||||  
|-|-|-|  
|테이블 형식|1400|SQL Server 2017|
|테이블 형식|1200|SQL Server 2016|  
|테이블 형식|1103|SQL Server 2014|  
|테이블 형식|1100|SQL Server 2012|  
|다차원|1100|SQL Server 2012 이상|  
|다차원|1050|SQL Server 2005, 2008, 2008 R2|  
  
 자세한 내용은 [다차원 데이터베이스의 호환성 수준&#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services) 및 [Analysis Services 테이블 형식 모델에 대한 호환성 수준](https://docs.microsoft.com/analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 설치 계획](../../sql-server/install/planning-a-sql-server-installation.md)   
 [PowerPivot for SharePoint 업그레이드](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
  
  
