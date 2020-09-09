---
title: 구성 관리용 WMI 공급자 개념
description: Microsoft Management Console 및 Microsoft SQL Server Configuration Manager에서 SQL Server 구성 관리자 사용 되는 WMI 공급자에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management
- SQL Server WMI Provider
- configuration management [WMI]
- WMI Provider for Configuration Management, about WMI Provider for Configuration Management
ms.assetid: 7e41db24-b915-4eb8-a1d6-e6948ee915b7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8a93cebef339d72a80139d079f5f14fffaa119f7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545215"
---
# <a name="wmi-provider-for-configuration-management"></a>구성 관리용 WMI 공급자
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  WMI 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] MMC (Management Console) 및 Configuration Manager에 대 한 Configuration Manager 스냅인과 함께 사용 되는 게시 된 계층입니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 이 계층은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 요청하는 레지스트리 작업을 관리하는 통합 API 호출 상호 작용 방법과 선택한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 대한 향상된 제어 및 조작을 제공합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에 의해 자동으로 컴파일되는 DLL 및 MOF 파일입니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 공급자에는 다음과 같은 방법으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 제어하는 데 사용되는 개체 클래스 집합이 포함되어 있습니다.  
  
-   WQL(Windows 쿼리 언어)을 포함할 수 있는 VBScript, [!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)] 또는 Perl과 같은 스크립트 언어  
  
-   SMO 관리 코드 프로그램의 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 개체  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 공급자 스냅인이 포함된 MMC  
  
## <a name="using-a-script-language"></a>스크립트 언어 사용  
 스크립트 언어를 사용하면 다음과 같은 이점이 있습니다.  
  
-   개발 환경이 필요 없습니다.  
  
-   스크립트 언어를 지원하는 파일을 구하기 쉽습니다.  
  
 스크립트는 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 공급자 외에 다른 WMI 공급자에서도 사용할 수 있습니다. 도메인 관리자는 스크립트를 사용하여 네트워크의 여러 컴퓨터에서 서비스, 네트워크 설정 및 별칭 설정을 지정할 수 있습니다.  
  
 이 섹션에서는 스크립트에서 구성 관리용 WMI 공급자에 액세스하는 방법을 자세히 설명합니다.  
  
## <a name="using-the-smo-managedcomputer-object"></a>SMO ManagedComputer 개체 사용  
 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 개체는 구성 관리용 WMI 공급자에 대한 액세스를 제공하는 관리되는 SMO 개체입니다. SMO 프로그램을 사용하면 <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> 개체를 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스, 네트워크 설정 및 별칭 설정을 보고 수정할 수 있습니다. 자세한 내용은 [WMI 공급자를 사용 하 여 서비스 및 네트워크 설정 관리](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)를 참조 하세요.  
  
## <a name="using-the-microsoft-management-console-or-sql-server-configuration-manager"></a>MMC 또는 SQL Server 구성 관리자 사용  
 MMC(Microsoft Management Console)는 스크립팅 언어나 관리 코드 프로그램과는 달리 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 관리하기 위한 인터페이스를 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 MMC 스냅인을 사용하여 서비스를 중지 및 시작하고 서비스 계정을 변경할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스, 클라이언트 프로토콜, 서버 프로토콜 및 서버 별칭을 관리하는 데도 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [구성 관리용 WMI 공급자 이해](../../relational-databases/wmi-provider-configuration/understanding-the-wmi-provider-for-configuration-management.md)   
 [구성 관리용 WMI 공급자 작업](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [구성 관리용 WMI 공급자에 WQL 및 스크립트 언어 사용](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
