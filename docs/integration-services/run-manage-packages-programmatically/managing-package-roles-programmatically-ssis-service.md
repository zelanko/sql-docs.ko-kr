---
title: "패키지 역할 프로그래밍 방식으로 관리 (SSIS 서비스) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: run-manage-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services packages, roles
- roles [Integration Services]
- packages [Integration Services], roles
ms.assetid: 2e0ca0d5-d4f5-421d-b17d-a48b37b923e5
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 7a7fb000389756caf0c2f2ea00cd0b80e75557d8
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="managing-package-roles-programmatically-ssis-service"></a>프로그래밍 방식으로 패키지 역할 관리(SSIS 서비스)
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 프로그래밍 방식으로 사용할 때 패키지에 적용할 수 있는 역할을 확인하거나 개별 패키지에 적용된 역할을 확인 또는 설정할 수 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.Application> 네임스페이스의 <xref:Microsoft.SqlServer.Dts.Runtime> 클래스는 이 요구 사항을 충족하기 위한 다양한 메서드를 제공합니다.  
  
 역할에 저장 된 패키지에만 적용 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **msdb** 데이터베이스입니다. 패키지 역할에 대 한 자세한 내용은 참조 하십시오. [Integration Services 역할 &#40; SSIS 서비스 &#41; ](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
 이 항목에서 설명한 모든 메서드에 필요한에 대 한 참조는 **Microsoft.SqlServer.ManagedDTS** 어셈블리입니다. 새 프로젝트에 대 한 참조를 추가한 후에 가져올는 <xref:Microsoft.SqlServer.Dts.Runtime> 를 사용 하 여 네임 스페이스는 **를 사용 하 여** 또는 **Imports** 문.  
  
> [!IMPORTANT]  
>  SSIS 패키지 저장소를 사용하기 위한 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스의 메서드는 ".", localhost 또는 로컬 서버의 서버 이름만 지원합니다. "(local)"은 사용할 수 없습니다.  
  
## <a name="determining-which-roles-are-available"></a>사용 가능한 역할 확인  
 특정 서버에 저장된 패키지에 사용할 수 있는 역할을 확인하려면 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetDtsServerRoles%2A> 클래스의 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 메서드를 호출합니다.  
  
## <a name="determining-which-roles-are-assigned"></a>할당된 역할 확인  
 특정 패키지에 이미 할당된 역할을 확인하려면 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetPackageRoles%2A> 메서드를 호출합니다. 패키지에 역할을 할당하려면 <xref:Microsoft.SqlServer.Dts.Runtime.Application.SetPackageRoles%2A> 메서드를 호출합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 역할 &#40; SSIS 서비스 &#41;](../../integration-services/security/integration-services-roles-ssis-service.md)  
  
  

