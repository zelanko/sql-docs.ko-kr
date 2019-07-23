---
title: 프로그래밍 방식으로 패키지 역할 관리(SSIS 서비스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5833ff25bc698b94e1798aa77e3fc776d5955a1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028507"
---
# <a name="managing-package-roles-programmatically-ssis-service"></a>프로그래밍 방식으로 패키지 역할 관리(SSIS 서비스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 프로그래밍 방식으로 사용할 때 패키지에 적용할 수 있는 역할을 확인하거나 개별 패키지에 적용된 역할을 확인 또는 설정할 수 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.Application> 네임스페이스의 <xref:Microsoft.SqlServer.Dts.Runtime> 클래스는 이 요구 사항을 충족하기 위한 다양한 메서드를 제공합니다.  
  
 역할은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** 데이터베이스에 저장된 패키지에만 적용됩니다. 패키지 역할에 대한 자세한 내용은 [Integration Services 역할&#40;SSIS Service&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)을 참조하세요.  
  
 이 항목에서 설명하는 모든 방법은 **Microsoft.SqlServer.ManagedDTS** 어셈블리에 대한 참조가 필요합니다. 새 프로젝트에 참조를 추가한 후 **using** 또는 **Imports** 문을 사용하여 <xref:Microsoft.SqlServer.Dts.Runtime> 네임스페이스를 가져옵니다.  
  
> [!IMPORTANT]  
>  SSIS 패키지 저장소를 사용하기 위한 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스의 메서드는 ".", localhost 또는 로컬 서버의 서버 이름만 지원합니다. "(local)"은 사용할 수 없습니다.  
  
## <a name="determining-which-roles-are-available"></a>사용 가능한 역할 확인  
 특정 서버에 저장된 패키지에 사용할 수 있는 역할을 확인하려면 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> 클래스의 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 메서드를 호출합니다.  
  
## <a name="determining-which-roles-are-assigned"></a>할당된 역할 확인  
 특정 패키지에 이미 할당된 역할을 확인하려면 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A> 메서드를 호출합니다. 패키지에 역할을 할당하려면 <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A> 메서드를 호출합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 역할&#40;SSIS 서비스&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  
