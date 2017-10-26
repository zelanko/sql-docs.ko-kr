---
title: "서비스 관리를 위한 보안 요구 사항 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent service, security
- services [SQL Server], security
- SQL Server services, security
- WMI Providers [SQL Server]
- server configuration [SQL Server]
- security [SQL Server], services
- services [SQL Server], WMI
ms.assetid: 1874a317-ddb2-425d-98d9-b53e1be6fc6a
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cf5902f634cb69689388cadf26c0c53fed607519
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="security-requirements-for-managing-services"></a>서비스 관리를 위한 보안 요구 사항
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 관리하려면 SQL Server 구성 관리자 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용합니다. 클러스터 관리자를 사용하여 클러스터형 서버에서 서비스를 관리합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 관리하고 서버 구성 옵션을 설정하려면 **serveradmin** 고정 서버 역할이나 **sysadmin** 고정 서버 역할의 멤버여야 합니다. Windows **Administrators** 그룹의 멤버는 서비스를 시작하거나 중지하고 Windows에서 제공하는 서버 옵션을 구성할 수 있습니다.  
  
> [!NOTE]  
>  정상적으로 작동하려면 서비스에 사용되는 계정은 올바른 도메인, 파일 시스템 및 레지스트리 권한으로 구성해야 합니다. 필요한 사용 권한에 대한 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.  
  
## <a name="windows-management-instrumentation"></a>Windows Management Instrumentation  
 SQL Server 구성 관리자와 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 WMI(Windows Management Instrumentation)를 사용하여 일부 서버 속성을 표시하고 수정합니다. 서비스를 관리하고 서비스 상태를 파악하려면 WMI 개체에 액세스할 권한이 있어야 합니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 다음 서버 속성 페이지에 WMI를 사용합니다.  
  
-   자동 시작 서비스  
  
-   시작 매개 변수  
  
-   보안  
  
-   기타 서버 설정  
  
## <a name="related-tasks"></a>관련 태스크  
 [WMI를 구성하여 SQL Server 도구에 서버 상태 표시](http://msdn.microsoft.com/library/7e97197b-ed4d-40d1-9a52-9ab1d92401d7)  
  
## <a name="related-content"></a>관련 내용  
 [구성 관리용 WMI 공급자 개념](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md)  
  
  

