---
title: "프로그래밍 방식으로 실행 중인 패키지 관리 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 34f2c773e89c0162df5d13a16d27f01eb5d8f4df
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="managing-running-packages-programmatically"></a>프로그래밍 방식으로 실행 중인 패키지 관리
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 프로그래밍 방식으로 사용할 때 현재 실행 중인 패키지를 확인할 수 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.Application> 네임스페이스의 <xref:Microsoft.SqlServer.Dts.Runtime> 클래스는 이 요구 사항을 충족하기 위한 메서드와 클래스를 제공합니다.  
  
 패키지를 모니터링 하는 방법에 대 한 자세한 내용은 참조 [패키지 관리 &#40; SSIS 서비스 &#41; ](../../integration-services/service/package-management-ssis-service.md).  
  
 이 항목에서 설명한 모든 메서드에 필요한에 대 한 참조는 **Microsoft.SqlServer.ManagedDTS** 어셈블리입니다. 새 프로젝트에 대 한 참조를 추가한 후에 가져올는 <xref:Microsoft.SqlServer.Dts.Runtime> 포함 된 네임 스페이스는 **를 사용 하 여** 또는 **Imports** 문.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [패키지 관리 &#40; SSIS 서비스 &#41;](../../integration-services/service/package-management-ssis-service.md)   
 [프로그래밍 방식으로 사용 가능한 패키지 열거](../../integration-services/run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
  
  

