---
title: 호환성 수준 (SSAS 테이블 형식 SP1) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: 8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d4c04690906d9b5f3fd38ddf444d6c3f99e917a9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299003"
---
# <a name="compatibility-level-ssas-tabular-sp1"></a>호환성 수준(SSAS 테이블 형식 SP1)
  지정할 수 있습니다 *호환성 수준* 테이블 형식 모델 데이터베이스에 배포 된 기존를 업그레이드할 때 기존 테이블 형식 모델 프로젝트를 업그레이드 하는 경우 새 테이블 형식 모델 프로젝트를 만들 때 또는 PowerPivot 통합 문서를 가져올 때입니다.  
  
## <a name="compatibility-level"></a>호환성 수준  
 일반적으로 새 버전과 서비스 팩은 프로덕션 컴퓨터에 설치하기 전에 개발 및 테스트 컴퓨터에 먼저 설치합니다. 이 경우 두 새 테이블 형식 모델 프로젝트에 대한 호환성 수준과 프로덕션 환경에 이미 배포된 기존 프로젝트에 대한 호환성 수준을 설정하는 방법을 알아야 합니다.  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Analysis Services 인스턴스는 다음 호환성 수준(데이터베이스 버전)을 지원합니다.  
  
-   SQL Server 2012 (1100)  
  
-   SQL Server 2012 SP1(1103)  
  
-   SQL Server 2014 (1103)  
  
### <a name="set-compatibility-level-when-creating-a-new-tabular-model-project"></a>새 테이블 형식 모델 프로젝트를 만들 때 호환성 수준 설정  
 SQL Server 데이터 도구 (SSDT)에서 새 테이블 형식 모델 프로젝트를 만들 때 합니다 **새 테이블 형식 프로젝트 옵션** 대화 호환성 수준을 지정할 수 있습니다. 새 프로젝트를 만들 때 해당 프로젝트를 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 이상의 Analysis Services 인스턴스에 배포할지 또는 SQL Server 2012 Analysis Services 인스턴스(서비스 팩 1 없음)에 배포할지를 선택할 수 있습니다.  
  
 또한 **이 메시지를 다시 표시 안 함** 옵션을 선택하여 기본 호환성 수준을 지정할 수도 있습니다. 모든 후속 프로젝트는 지정된 호환성 수준을 사용합니다. SSDT의 옵션에서 기본 호환성 수준을 변경할 수 있습니다.  
  
### <a name="upgrade-an-existing-tabular-model-project-to-1103-compatibility-level"></a>기존 테이블 형식 모델 프로젝트를 1103 호환성 수준으로 업그레이드  
 설치 하기 전에 SSDT에서 만든 테이블 형식 모델 프로젝트를 업그레이드할 수 있습니다 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 또는 나중에 사용 하 여 데이터베이스 버전 1103 호환 되어야 합니다 **호환성 수준** 모델의 속성 **속성**창. 테이블 형식 모델 프로젝트를 업그레이드하려면 SSDT가 설치된 컴퓨터에 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 이상을 설치해야 하며 작업 영역 데이터베이스가 상주하는 Analysis Services 인스턴스에도 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 이상을 설치해야 합니다. 이전 버전으로 다운그레이드할 수 없습니다.  
  
### <a name="upgrade-a-deployed-tabular-model-database-to-1103-compatibility-level"></a>배포된 테이블 형식 모델 데이터베이스를 1103 호환성 수준으로 업그레이드  
 사용 하 여 기존 배포 된 테이블 형식 모델 데이터베이스 버전 1103 SQL Server Management Studio (SSMS)과 호환 되도록 업그레이드할 수 있습니다 합니다 **호환성 수준** 속성에서 **데이터베이스 속성**. 업그레이드하려면 SQL Server Analysis Services 인스턴스가 설치된 컴퓨터에 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 이상을 설치해야 합니다. 배포된 테이블 형식 모델 데이터베이스를 이전 버전으로 다운그레이드할 수 없습니다.  
  
### <a name="import-from-powerpivot"></a>PowerPivot에서 가져오기  
 PowerPivot에서 가져오는 방식으로 새 테이블 형식 모델 프로젝트를 만들 때는 호환성 수준을 기본 호환성 수준(이전에 SSDT에서 구성한 경우)으로 업그레이드할지 아니면 PowerPivot 통합 문서에 이미 지정된 호환성 수준을 그대로 사용할지를 지정할 수 있습니다.  
  
### <a name="check-compatibility-level-for-a-tabular-model-database-in-ssms"></a>SSMS에서 테이블 형식 모델 데이터베이스에 대한 호환성 수준 확인  
 SSMS에서 테이블 형식 모델 데이터베이스의 호환성 수준을 확인 하 여 확인할 수 있습니다 합니다 **호환성 수준** 속성 (의 새로운 기능 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)])에서 **데이터베이스 속성**합니다.  
  
### <a name="check-supported-compatibility-level-for-an-analysis-services-instance-in-ssms"></a>SSMS에서 Analysis Services 인스턴스에 대해 지원되는 호환성 수준 확인  
 SSMS에서 지원 되는 호환성 수준을 확인 하 여 확인할 수 있습니다는 **지원 되는 호환성 수준** 속성에는 **정보** 페이지 (의 새로운 기능 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)])에서 **분석 서비스 속성**합니다. 지원되는 호환성 수준 1103은 SQL Server SP1 이상이 설치되어 있음을 나타냅니다. 지원되는 호환성 수준은 변경할 수 없습니다.  
  
  
