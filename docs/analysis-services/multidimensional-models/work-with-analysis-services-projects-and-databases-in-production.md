---
title: 작업할 Analysis Services 프로젝트 및 프로덕션 환경에서 데이터베이스 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f90af41c397da20fb26c73bebc6723b9a3cf6270
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62743239"
---
# <a name="work-with-analysis-services-projects-and-databases-in-production"></a>작업할 Analysis Services 프로젝트 및 프로덕션 환경에서 데이터베이스
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 개발하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스로 배포한 다음에는 배포된 데이터베이스의 개체 변경 방법을 결정해야 합니다. 보안 역할, 분할 및 스토리지 설정과 관련된 변경 내용 등 특정 설정은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]를 사용하여 변경할 수 있습니다. 특성 추가나 사용자 정의 계층과 같은 기타 설정은 프로젝트 모드나 온라인 모드의 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서만 변경할 수 있습니다.  
  
 온라인 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 배포된 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 데이터베이스를 변경하면 배포에 사용된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트는 이제 최신이 아닙니다. 개발자가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 내에서 변경 작업을 수행하고 수정된 프로젝트를 배포하려고 하면 전체 데이터베이스를 덮어쓸 것인지 묻는 메시지가 표시됩니다. 개발자가 전체 데이터베이스를 덮어쓰면 해당 데이터베이스도 처리해야 합니다. 프로덕션 직원이 배포된 데이터베이스를 직접 변경한 사항이 개발 팀에 전달되지 않은 경우 해당 변경 내용이 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 표시되지 않는 이유를 이해하지 못하기 때문에 문제가 복잡해집니다.  
  
 SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 도구를 사용하여 이런 경우의 문제를 방지할 수 있는 방법에는 여러 가지가 있습니다.  
  
-   방법 1: 프로덕션 버전으로 변경 될 때마다를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 사용 하 여 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 새 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 수정된 된 버전을 기반으로 하는 프로젝트는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스입니다. 이 새 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 프로젝트의 마스터 복사본으로 원본 제어 시스템에 체크 인할 수 있습니다. 이 방법은 온라인 모드의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 데이터베이스를 변경했는지에 관계없이 작동합니다.  
  
-   방법 2: 프로덕션 버전으로 변경 된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 사용 하 여 데이터베이스 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 프로젝트 모드에서. 이 방법을 사용하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사의 옵션을 사용하여 보안 역할 및 스토리지 설정과 같은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 변경 내용을 유지할 수 있습니다. 이렇게 하면 디자인 관련 설정이 프로젝트 파일에 유지되고(스토리지 설정과 보안 역할은 무시될 수 있음) 온라인 서버가 보안 역할 및 스토리지 설정에 사용됩니다.  
  
-   방법 3: 프로덕션 버전으로 변경 프로그램 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 사용 하 여 데이터베이스 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 온라인 모드로 합니다. 두 도구는 같은 온라인 서버에서만 작동하기 때문에 다른 버전이 동기화되지 않을 가능성이 없습니다.  
  
  
