---
title: 프로그래밍 방식으로 패키지 실행 관리 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: run-manage-packages-programmatically
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- packages [Integration Services], managing
- running packages [Integration Services]
ms.assetid: 0e91f4ac-6f29-40d7-8c28-9b82e4802c35
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e87373afb607c598d3cc5095bd15dc855f4908e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="managing-running-packages-programmatically"></a>프로그래밍 방식으로 실행 중인 패키지 관리
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 프로그래밍 방식으로 사용할 때 현재 실행 중인 패키지를 확인할 수 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.Application> 네임스페이스의 <xref:Microsoft.SqlServer.Dts.Runtime> 클래스는 이 요구 사항을 충족하기 위한 메서드와 클래스를 제공합니다.  
  
 패키지 모니터링에 대한 자세한 내용은 [패키지 관리&#40;SSIS 서비스&#41;](../../integration-services/service/package-management-ssis-service.md)를 참조하세요.  
  
 이 항목에서 설명하는 모든 방법은 **Microsoft.SqlServer.ManagedDTS** 어셈블리에 대한 참조가 필요합니다. 새 프로젝트에 참조를 추가한 후 **using** 또는 **Imports** 문을 사용하여 <xref:Microsoft.SqlServer.Dts.Runtime> 네임스페이스를 가져옵니다.  
  
> [!IMPORTANT]  
>  SSIS 패키지 저장소를 사용하기 위한 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 클래스의 메서드는 ".", localhost 또는 로컬 서버의 서버 이름만 지원합니다. "(local)"은 사용할 수 없습니다.  
  
## <a name="determining-which-packages-are-currently-running"></a>현재 실행 중인 패키지 확인  
 지정한 서버에서 현재 실행 중인 패키지를 확인하려면 <xref:Microsoft.SqlServer.Dts.Runtime.Application.GetRunningPackages%2A> 메서드를 호출합니다. 이 메서드는 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> 개체의 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> 컬렉션을 반환합니다.  
  
> [!NOTE]  
>  관리자는 컴퓨터에서 현재 실행 중인 모든 패키지를 볼 수 있고 다른 사용자는 자신이 실행한 패키지만 볼 수 있습니다.  
  
## <a name="working-with-running-packages"></a>실행 중인 패키지 작업  
 현재 실행 중인 패키지를 확인한 후에는 패키지에 대한 정보를 가져오고 패키지를 중지하도록 요청할 수 있습니다.  
  
### <a name="getting-information-about-a-running-package"></a>실행 중인 패키지에 대한 정보 얻기  
 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackages> 컬렉션을 반복할 때 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> 개체의 속성을 사용하여 패키지를 찾거나 실행 중인 패키지에 대한 추가 정보를 얻을 수 있습니다.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionDuration%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.ExecutionStartTime%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.InstanceID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageDescription%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageID%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.PackageName%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.UserName%2A>  
  
### <a name="stopping-a-running-package"></a>실행 중인 패키지 중지  
 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage.Stop%2A> 개체의 <xref:Microsoft.SqlServer.Dts.Runtime.RunningPackage> 메서드를 호출하여 패키지를 중지하도록 요청할 수 있습니다. 중지 요청이 실행된 시간과 패키지가 실제로 중지되는 시간 사이에는 지연이 있을 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [패키지 관리&#40;SSIS 서비스&#41;](../../integration-services/service/package-management-ssis-service.md)   
 [프로그래밍 방식으로 사용 가능 패키지 열거](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  
