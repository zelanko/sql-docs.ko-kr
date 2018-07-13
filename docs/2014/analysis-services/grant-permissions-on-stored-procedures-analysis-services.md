---
title: 저장된 프로시저 (Analysis Services)에 대 한 권한 부여 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 01793166-a3e5-4856-8302-21b82d494e69
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7b90318de4420df1776c01e5e881740d9d44ea20
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278759"
---
# <a name="grant-permissions-on-stored-procedures-analysis-services"></a>저장 프로시저 관련 사용 권한 부여(Analysis Services)
  저장 프로시저 또는 어셈블리 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 로 작성 된 외부 루틴이 며를 [!INCLUDE[msCoName](../includes/msconame-md.md)] 의 기능을 확장 하는.NET 프로그래밍 언어로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]합니다. 개발자는 어셈블리를 사용하여 언어 간 통합, 예외 처리, 버전 관리 지원, 배포 지원 및 디버깅 지원을 이용할 수 있습니다.  
  
 어셈블리를 등록하려면 서버 관리자여야 합니다. 참조 [서버 관리자 권한 부여 &#40;Analysis Services&#41;](instances/grant-server-admin-rights-to-an-analysis-services-instance.md)합니다.  
  
## <a name="security-context-for-stored-procedure-execution"></a>저장 프로시저 실행을 위한 보안 컨텍스트  
 모든 사용자가 저장 프로시저를 호출할 수 있습니다. 저장 프로시저 구성에 따라 프로시저를 호출하는 사용자 또는 익명 사용자의 컨텍스트에서 프로시저가 실행될 수 있습니다. 익명 사용자에게는 보안 컨텍스트가 없으므로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 구성에 이 기능을 사용하여 익명 액세스를 허용합니다.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 저장 프로시저를 실행하기 전에 사용자가 해당 저장 프로시저를 호출하면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서 저장 프로시저 내의 동작을 평가합니다. 이 경우 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에서는 사용자에 부여된 사용 권한과 프로시저 실행에 사용되는 권한 집합의 공통 요소를 기준으로 저장 프로시저의 작업을 평가합니다. 사용자의 데이터베이스 역할로는 수행할 수 없는 동작이 저장 프로시저에 있는 경우 해당 작업은 수행되지 않습니다.  
  
 다음은 저장 프로시저 실행에 사용되는 권한 집합입니다.  
  
-   **안전한** 안전 권한 집합을 저장된 프로시저의 보호 된 리소스에 액세스할 수 없습니다는 [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework입니다. 이 권한 집합에서는 계산만 허용됩니다. 정보가 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 외부로 누출되지 않고 사용 권한을 승격할 수 없으며 데이터 훼손 공격의 위험이 최소화된다는 점에서 가장 안전한 권한 집합입니다.  
  
-   **외부 액세스** 외부 액세스 권한 집합을 사용하면 저장 프로시저에서 관리 코드를 사용하여 외부 리소스에 액세스할 수 있습니다. 저장 프로시저를 이 권한 집합으로 설정하면 서버 불안정을 일으키는 프로그래밍 오류가 발생하지 않습니다. 그러나 서버 외부로 정보가 누출되거나 권한 승격 및 데이터 훼손 공격의 가능성이 있습니다.  
  
-   **제한 없음** 제한 없음 권한 집합을 사용하면 저장 프로시저에서 아무 코드나 사용하여 외부 리소스에 액세스할 수 있습니다. 저장 프로시저를 이 권한 집합으로 설정하면 저장 프로시저의 보안이나 안정성이 보장되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [다차원 모델 어셈블리 관리](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
