---
title: 사용자 지정 어셈블리 배포 | Microsoft Docs
description: SQL Server Reporting Services에서 사용자 지정 어셈블리를 배포하는 방법을 알아봅니다. 실행 권한 이상의 사용자 지정 어셈블리 권한을 부여하는 방법도 알아봅니다.
ms.date: 11/23/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- deploying custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], deploying
- custom assemblies [Reporting Services], updating
- updating custom assemblies
ms.assetid: c6674cd8-0de7-4a5a-9e7c-12ffa49f6fd2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2c68562c1be1817d8f7457f680b4f45169de4a1f
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96166886"
---
# <a name="deploying-a-custom-assembly"></a>사용자 지정 어셈블리 배포
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 사용자 지정 어셈블리를 배포하려면 어셈블리를 보고서 디자이너 및 보고서 서버의 애플리케이션 폴더에 둡니다. 기본적으로 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 사용자 지정 어셈블리에는 **Execution** 권한이 부여됩니다. 사용자 지정 어셈블리에 실행 권한 이상의 권한을 부여하려면 보고서 서버에 대한 rssrvpolicy.config 구성 파일 및 보고서 디자이너 미리 보기 창에 대한 rspreviewpolicy.config 구성 파일을 편집해야 합니다. 또는 GAC(전역 어셈블리 캐시)에 사용자 지정 어셈블리를 설치할 수도 있습니다.  
  
> [!NOTE]  
>  보고서 디자이너에는 보고서 프로젝트를 **DebugLocal** 모드에서 시작할 때 실행되는 팝업 미리 보기 창과 미리 보기 탭이라는 두 개의 미리 보기 모드가 있습니다. 미리 보기 탭에서는 **FullTrust** 권한 집합을 사용하여 모든 보고서 식을 실행하며 보안 정책 설정을 적용하지 않습니다. 팝업 미리 보기 창은 보고서 서버 기능을 시뮬레이션하기 위한 것이므로 보고서 디자이너에서 사용자 지정 어셈블리를 사용하기 위해 작업자나 관리자가 수정해야 하는 정책 구성 파일을 포함합니다. 또한 이 팝업 미리 보기는 사용자 지정 어셈블리를 잠급니다. 따라서 사용자 지정 어셈블리 코드를 수정하거나 업데이트하려면 미리 보기 창을 닫아야 합니다.  
  
## <a name="to-deploy-a-custom-assembly-in-reporting-services"></a>Reporting Services에서 사용자 지정 어셈블리를 배포하려면  
  
1.  사용자 지정 어셈블리를 빌드 위치에서 보고서 서버 bin 폴더 또는 보고서 디자이너 폴더에 복사합니다. 

     사용자 지정 어셈블리를 보고서 서버 bin 폴더에 저장하면 이 사용자 지정 어셈블리를 참조하는 보고서를 게시할 수 있습니다. 보고서 서버에 대한 bin 폴더의 기본 위치는 다음과 같습니다.

     Reporting Services 2016
     ```
     %ProgramFiles%\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin
     ```
     Reporting Services 2017 이상
     ```
     %ProgramFiles%\Microsoft SQL Server Reporting Services\SSRS\ReportServer\bin
     ```
     사용자 지정 어셈블리를 보고서 디자이너 폴더에 저장하면 보고서 디자이너에 있는 이 사용자 지정 어셈블리를 참조하는 보고서를 실행 및 디버깅할 수 있습니다. 보고서 디자이너의 기본 위치는 다음과 같습니다.

     Visual Studio 2012
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies
     ```
     Visual Studio 2013
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies
     ```
     Visual Studio 2015
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies
     ```
     Visual Studio 2017
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS
     ```
     Visual Studio 2019
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS
     ```  
2.  해당하는 구성 파일을 엽니다. 보고서 서버에 대한 rssrvpolicy.config의 기본 위치는 다음과 같습니다.

     Reporting Services 2016
     ```
     %ProgramFiles%\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer
     ```
     Reporting Services 2017 이상
     ```
     %ProgramFiles%\Microsoft SQL Server Reporting Services\SSRS\ReportServer
     ```
     보고서 디자이너에 대해 업데이트할 파일은 다음과 같습니다.

     Visual Studio 2012
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE\PrivateAssemblies\RSReportHost11.exe.config
     ```
     Visual Studio 2013
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio 12.0\Common7\IDE\PrivateAssemblies\RSReportHost.exe.config
     ```
     Visual Studio 2015
     ```
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\PrivateAssemblies\RSReportHost.exe.config
     ```
     Visual Studio 2017
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSReportHost.exe.config
     ```
     Visual Studio 2019
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\PreviewProcessingService.exe.config
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSPreviewPolicy.config
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSReportDesigner.config
     C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\CommonExtensions\Microsoft\SSRS\RSReportHost.exe.config
     ```    
3.  사용자 지정 어셈블리에 대한 코드 그룹을 추가합니다. 자세한 내용은 [보안 개발&#40;Reporting Services&#41;](../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)을 참조하세요.  
  
## <a name="updating-custom-assemblies"></a>사용자 지정 어셈블리 업데이트  
 게시된 다수의 보고서에서 현재 참조하고 있는 사용자 지정 어셈블리의 버전을 어느 시점에 업데이트해야 할 수 있습니다. 해당하는 어셈블리가 보고서 서버의 bin 디렉터리나 보고서 디자이너에 이미 있으며 어셈블리의 버전 번호가 높아지거나 어떤 식으로든 변경되는 경우 현재 게시된 보고서는 더 이상 올바르게 작동하지 않습니다. 보고서 정의의 **CodeModules** 요소에서 참조되는 어셈블리의 버전을 업데이트하고 보고서를 다시 게시해야 합니다. 사용자 지정 어셈블리를 자주 업데이트할 예정이며 현재 게시된 보고서에서 새 어셈블리를 참조해야 하는 경우에는 특정 어셈블리의 모든 업데이트에서 동일한 버전 사용을 고려해야 할 수도 있습니다.  
  
 현재 게시된 보고서에서 새 버전의 어셈블리를 참조할 필요가 없는 경우 사용자 지정 어셈블리를 전역 어셈블리 캐시에 배포할 수 있습니다. 전역 어셈블리 캐시에서는 동일한 어셈블리의 여러 버전을 유지 관리할 수 있으므로 현재 보고서에서 이전 버전의 어셈블리를 참조하고 새로 게시된 보고서에서 업데이트된 어셈블리를 참조할 수 있습니다. 또 다른 방법은 이전 어셈블리에 대한 모든 요청이 새 어셈블리로 리디렉션되도록 보고서 서버의 바인딩 리디렉션을 설정하는 것입니다. 이 경우 보고서 서버 Web.config 파일 및 보고서 서버 ReportingServicesService.exe.config 파일을 수정해야 합니다. 항목은 다음과 같습니다.  
  
```  
<configuration>  
   <runtime>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
         <dependentAssembly>  
            <assemblyIdentity name="myAssembly"  
                              publicKeyToken="32ab4ba45e0a69a1"  
                              culture="neutral" />  
            <bindingRedirect oldVersion="1.0.0.0"  
                             newVersion="2.0.0.0"/>  
         </dependentAssembly>  
      </assemblyBinding>  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목  
 [보고서에서 사용자 지정 어셈블리 사용](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [어셈블리 및 전역 어셈블리 캐시 사용](https://go.microsoft.com/fwlink/?LinkId=63912)  
  
  
