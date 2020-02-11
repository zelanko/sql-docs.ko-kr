---
title: Integration Services 서비스 구성 (SSIS 서비스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- configuration files [Integration Services]
- service [Integration Services], configuring
- default configuration files
ms.assetid: 36d78393-a54c-44b0-8709-7f003f44c27f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 600858e3d7b2ea29a30541c559aa764b4085f7cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66060494"
---
# <a name="configuring-the-integration-services-service-ssis-service"></a>Integration Services 서비스 구성(SSIS 서비스)
    
> [!IMPORTANT]  
>  이 항목에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 관리하는 Windows 서비스인 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 대해 설명합니다. 
  [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 는 이전 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]버전과의 호환성을 위한 서비스를 지원합니다. 
  [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]부터는 Integration Services 서버의 패키지와 같은 개체를 관리할 수 있습니다.  
  
 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스는 구성 파일을 사용하여 해당 설정을 구성합니다. 기본적으로이 구성 파일의 이름은 MsDtsSrvr. .ini .xml이 고 파일 은%ProgramFiles%\Microsoft SQL Server\120\dts\binn입니다. 폴더에 있습니다.  
  
 일반적으로 이 구성 파일이나 이 구성 파일의 위치는 변경하지 않아도 되지만 패키지가 명명된 인스턴스, [!INCLUDE[ssDE](../includes/ssde-md.md)]의 원격 인스턴스 또는 여러 [!INCLUDE[ssDE](../includes/ssde-md.md)]인스턴스에 저장되는 경우에는 이 구성 파일을 수정해야 합니다. 또한 이 구성 파일을 기본 위치 이외의 다른 위치로 이동할 경우 파일 위치를 지정하는 레지스트리 키도 수정해야 합니다.  
  
## <a name="configuration-file-contents"></a>파일 내용 구성  
 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]를 설치할 때 설치 프로세스는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 대한 구성 파일을 만들고 설치합니다. 이 구성 파일에는 다음과 같은 설정이 들어 있습니다.  
  
-   서비스가 중지되면 패키지에 중지 명령이 전송됩니다.  
  
-   
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 의 개체 탐색기에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에 대해 표시할 루트 폴더는 MSDB와 파일 시스템 폴더입니다.  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에서 관리 하는 파일 시스템의 패키지 는%ProgramFiles%\Microsoft SQL Server\120\DTS\Packages.에 있습니다.  
  
 이 구성 파일은 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에서 관리할 패키지가 들어 있는 msdb 데이터베이스도 지정합니다. 기본적으로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssDE](../includes/ssde-md.md)]와 동시에 설치되는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 인스턴스의 msdb 데이터베이스에 있는 패키지를 관리하도록 구성됩니다. 
  [!INCLUDE[ssDE](../includes/ssde-md.md)] 인스턴스가 동시에 설치되지 않는 경우 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스는 [!INCLUDE[ssDE](../includes/ssde-md.md)]의 로컬 기본 인스턴스에 있는 msdb 데이터베이스에 저장된 패키지를 관리하도록 구성됩니다.  
  
### <a name="default-configuration-file-example"></a>기본 구성 파일 예  
 다음 예에서는 아래의 설정을 지정하는 기본 구성 파일을 보여 줍니다.  
  
-   
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스가 중지되면 패키지 실행도 중지됩니다.  
  
-   
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 의 패키지 스토리지에 대한 루트 폴더는 MSDB와 파일 시스템입니다.  
  
-   서비스에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 로컬 기본 인스턴스에 있는 msdb 데이터베이스에 저장된 패키지를 관리합니다.  
  
-   서비스에서 파일 시스템의 패키지 폴더에 저장된 패키지를 관리합니다.  
  
 **기본 구성 파일의 예**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>.</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## <a name="modification-of-the-configuration-file"></a>구성 파일 수정  
 구성 파일을 수정하여 서비스가 중지되어도 패키지가 계속 실행되게 하거나 개체 탐색기에 추가 루트 폴더를 표시하거나 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에서 관리할 파일 시스템의 다른 폴더 또는 추가 폴더를 지정할 수 있습니다. 예를 들어 `SqlServerFolder` 유형의 추가 루트 폴더를 만들어 추가 [!INCLUDE[ssDE](../includes/ssde-md.md)] 인스턴스의 msdb 데이터베이스에 저장된 패키지를 관리할 수 있습니다.  
  
> [!NOTE]  
>  일부 문자는 폴더 이름에 적합하지 않습니다. 폴더 이름에 적합한 문자는 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 클래스 **System.IO.Path** 와 **GetInvalidFilenameChars** 필드에 의해 결정됩니다. 
  **GetInvalidFilenameChars** 필드는 **Path** 클래스의 멤버에 전달된 경로 문자열 인수에 지정할 수 없는 플랫폼별 문자 배열을 제공합니다. 잘못된 문자 집합은 파일 시스템에 따라 달라질 수 있습니다. 일반적으로 따옴표("), 보다 작음(<) 문자 및 파이프(|) 문자가 잘못된 문자입니다.  
  
 그러나 [!INCLUDE[ssDE](../includes/ssde-md.md)]의 명명된 인스턴스나 원격 인스턴스에 저장된 패키지를 관리하려면 구성 파일을 수정해야 합니다. 구성 파일을 업데이트하지 않으면 **의** 개체 탐색기 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 사용하여 명명된 인스턴스나 원격 인스턴스의 msdb 데이터베이스에 저장된 패키지를 볼 수 있습니다. 
  **개체 탐색기** 를 사용하여 이러한 패키지를 보려고 하면 다음과 같은 오류 메시지가 나타납니다.  
  
 `Failed to retrieve data for this request. (Microsoft.SqlServer.SmoEnum)`  
  
 `The SQL Server specified in Integration Services service configuration is not present or is not available. This might occur when there is no default instance of SQL Server on the computer. For more information, see the topic "Configuring the Integration Services Service" in SQL Server 2008 Books Online.`  
  
 `Login Timeout Expired`  
  
 `An error has occurred while establishing a connection to the server. When connecting to SQL Server 2008, this failure may be caused by the fact that under the default settings SQL Server does not allow remote connections.`  
  
 `Named Pipes Provider: Could not open a connection to SQL Server [2]. (MsDtsSvr).`  
  
 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스의 구성 파일을 수정하려면 텍스트 편집기를 사용합니다.  
  
> [!IMPORTANT]  
>  서비스 구성 파일을 수정한 후 업데이트된 서비스 구성을 사용하려면 서비스를 다시 시작해야 합니다.  
  
### <a name="modified-configuration-file-example"></a>수정된 구성 파일 예  
 다음 예에서는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 수정된 구성 파일을 보여 줍니다. 이 파일은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 서버의 `InstanceName` 이라는 `ServerName`의 명명된 인스턴스에 사용됩니다.  
  
 **SQL Server의 명명 된 인스턴스에 대 한 수정 된 구성 파일의 예**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>ServerName\InstanceName</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## <a name="modification-of-the-configuration-file-location"></a>구성 파일 위치 수정  
레지스트리 키 **HKEY_LOCAL_MACHINE \SOFTWARE\MICROSOFT\MICROSOFT SQL Server\120\SSIS\ServiceConfigFile** 는 서비스에서 사용 하는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 구성 파일의 위치와 이름을 지정 합니다. 레지스트리 키의 기본값은 **C:\Program FILES\MICROSOFT SQL Server\120\DTS\Binn\MsDtsSrvr.ini.xml**입니다. 이 레지스트리의 값을 업데이트하여 구성 파일의 이름과 위치를 변경할 수 있습니다. 경로의 버전 번호 (SQL Server [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]의 경우 120)는 SQL Server 버전에 따라 달라 집니다. 
  
  
> [!CAUTION]  
>  레지스트리 키를 잘못 편집하면 운영 체제를 다시 설치해야 하는 심각한 문제가 발생할 수 있습니다. 
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 는 레지스트리를 잘못 편집하여 발생하는 문제에 대한 해결을 보증하지 않습니다. 레지스트리를 편집하기 전에 중요한 데이터를 백업하십시오. 레지스트리를 백업, 복원 및 편집하는 방법은 [!INCLUDE[msCoName](../includes/msconame-md.md)] 기술 자료 문서 [Microsoft Windows 레지스트리 설명](https://support.microsoft.com/kb/256986)을 참조하십시오.  
  
 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스는 시작될 때 구성 파일을 로드하므로 레지스트리 항목의 변경 내용을 적용하려면 서비스를 다시 시작해야 합니다.  
  
  
