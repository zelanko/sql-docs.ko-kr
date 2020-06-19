---
title: VSTA로 스크립트 마이그레이션 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SSIS Script task, converting scripts
- Script component [Integration Services], converting scripts
- Script task [Integration Services], converting scripts
- SSIS Script component, converting scripts
ms.assetid: d685098b-86a1-46bf-939a-63d56951e009
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 041b46383232f3784c1c817f8feb726f382e1ec5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054715"
---
# <a name="migrate-scripts-to-vsta"></a>VSTA로 스크립트 마이그레이션
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]패키지를로 업그레이드 하 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 경우는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 스크립트 태스크 또는 스크립트 구성 요소의 스크립트를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA (Tools for Applications)로 마이그레이션합니다. VSTA는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 사용하는 스크립팅 환경입니다. 에서의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 스크립트 환경은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSA (for Applications)입니다.  
  
 스크립트 태스크나 스크립트 구성 요소의 스크립트에서 인터페이스를 참조하는 경우에는 패키지를 업그레이드하기 전에 해당 참조를 수정해야 합니다. 그렇지 않으면 사용하는 업그레이드 방법에 따라 패키지 업그레이드가 실패하거나 스크립트의 유효성 검사가 실패하게 됩니다. 이러한 참조를 수정 하려면 IDTS*xxx*90 인터페이스에 대 한 참조를 해당 idts*xxx*100 인터페이스에 대 한 참조로 바꿉니다.  
  
 스크립트를 마이그레이션하고 패키지를 업그레이드 하는 방법에 대 한 자세한 내용은 [Integration Services 패키지 업그레이드](../../integration-services/install-windows/upgrade-integration-services-packages.md)를 참조 하세요.  
  
## <a name="understanding-migration-failures"></a>마이그레이션 오류 이해  
 스크립트를 마이그레이션할 때 다음과 같은 이유로 마이그레이션이 실패할 수 있습니다.  
  
-   VSA 스크립트의 진입점 이름이 바뀐 경우  
  
     진입점은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 런타임이 VSTA 프로젝트의 `ScriptMain` 클래스에서 스크립트 태스크 코드에 대한 진입점으로 호출하는 메서드를 지정합니다. `ScriptMain` 클래스는 스크립트 템플릿이 생성하는 기본 클래스입니다.  
  
-   VSA 스크립트에 진입점이 없거나 여러 개 있는 경우  
  
-   어셈블리 참조를 추가할 수 없는 경우  
  
-   `ScriptMain` 클래스는 `ScriptObjectModelSSIS` 클래스뿐만 아니라 다른 클래스에서도 상속되도록 수정되었습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]는 다중 상속을 지원 하지 않습니다.  
  
 에서 사용 하는 VSA 스크립트를에서 사용 하는 VSTA 스크립트로 변환할 수 없습니다 [!INCLUDE[vbprvblong](../../includes/vbprvblong-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)] . 그러나를 사용 하는 새 VSTA 스크립트를 만들 수 있습니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csharp_orcas_long](../../includes/csharp-orcas-long-md.md)] . 자세한 내용은은 [스크립트 태스크 코딩 및 디버깅](../../integration-services/control-flow/script-task.md) 및 [스크립트 구성 요소 코딩 및 디버깅](../../integration-services/data-flow/transformations/script-component.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [스크립팅을 사용한 패키지 확장](../../relational-databases/server-management-objects-smo/tasks/scripting.md)  
  
  
