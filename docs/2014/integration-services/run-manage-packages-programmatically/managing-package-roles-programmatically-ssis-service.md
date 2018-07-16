---
title: 프로그래밍 방식으로 패키지 역할 관리(SSIS 서비스) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bd0ffb7426ddcf3a816fbad8a414c7c156c72aee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37311983"
---
# <a name="managing-package-roles-programmatically-ssis-service"></a>프로그래밍 방식으로 패키지 역할 관리(SSIS 서비스)
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 프로그래밍 방식으로 사용할 때 패키지에 적용할 수 있는 역할을 확인하거나 개별 패키지에 적용된 역할을 확인 또는 설정할 수 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.Application> 네임스페이스의 <xref:Microsoft.SqlServer.Dts.Runtime> 클래스는 이 요구 사항을 충족하기 위한 다양한 메서드를 제공합니다.  
  
 역할은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** 데이터베이스에 저장된 패키지에만 적용됩니다. 패키지 역할에 대한 자세한 내용은 [Integration Services 역할&#40;SSIS Service&#41;](../security/integration-services-roles-ssis-service.md)을 참조하세요.  
  
 이 항목에서 설명한 모든 메서드에는 `Microsoft.SqlServer.ManagedDTS` 어셈블리에 대한 참조가 있어야 합니다. 새 프로젝트에 참조를 추가한 후 `using` 또는 `Imports` 문을 사용하여 <xref:Microsoft.SqlServer.Dts.Runtime> 네임스페이스를 가져오십시오.  
  
> [!IMPORTANT]  
>  SSIS 패키지 저장소를 사용하기 위한 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스의 메서드는 ".", localhost 또는 로컬 서버의 서버 이름만 지원합니다. "(local)"은 사용할 수 없습니다.  
  
## <a name="determining-which-roles-are-available"></a>사용 가능한 역할 확인  
 특정 서버에 저장된 패키지에 사용할 수 있는 역할을 확인하려면 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> 클래스의 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 메서드를 호출합니다.  
  
## <a name="determining-which-roles-are-assigned"></a>할당된 역할 확인  
 특정 패키지에 이미 할당된 역할을 확인하려면 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A> 메서드를 호출합니다. 패키지에 역할을 할당하려면 <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A> 메서드를 호출합니다.  
  
![Integration Services 아이콘 (작은)](../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정  **<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 역할&#40;SSIS 서비스&#41;](../security/integration-services-roles-ssis-service.md)  
  
  
