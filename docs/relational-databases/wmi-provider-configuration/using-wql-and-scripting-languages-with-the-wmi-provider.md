---
title: WQL 및 스크립팅을 사용 하 여 WMI 공급자 액세스
description: WQL 편집기나 쿼리 도구나 스크립트 언어를 사용 하 여 WMI 공급자를 사용 하 여 SQL Server 서비스 및 네트워크 설정에 액세스 하는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- scripts [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
- WMI Provider for Configuration Management, scripts
ms.assetid: c1e64905-3c2b-4974-88f4-abf17cf7e289
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f96e814f14ba3e5de82ac633a757a8027f87296d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729983"
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider"></a>WMI 공급자에 WQL 및 스크립트 언어 사용
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]
  관리 애플리케이션에서는 다음과 같은 두 가지 방법으로 구성 관리용 WMI(Windows Management Instrumentation) 공급자 개체를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 네트워크 설정에 액세스합니다.  
  
-   WQL 편집기 또는 WBEMTest.exe 같은 쿼리 도구를 사용하여 WQL(Windows Management Instrumentation Language)로 설정된 개체를 쿼리합니다.  
  
-   VBScript 같은 스크립트 언어를 사용합니다.  
  
 또는 SMO에서 WMI 관리되는 개체를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 네트워크 설정을 프로그래밍 방식으로 관리할 수도 있습니다. WMI 관리 개체를 프로그래밍 하는 방법에 대 한 자세한 내용은 [Wmi 공급자를 사용 하 여 서비스 및 네트워크 설정 관리](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)를 참조 하세요.  
  
 구성 관리용 WMI 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 관리 콘솔을 사용하여 액세스할 수 있습니다. 사용자 인터페이스에서 WMI 공급자에 액세스 하는 방법에 대 한 자세한 내용은 [서비스 관리 방법 도움말 항목 &#40;SQL Server 구성 관리자&#41;](https://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)을 참조 하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [WQL을 사용 하 여 구성 관리용 WMI 공급자 액세스](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-wql.md)   
 [VBScript를 사용 하 여 WMI 공급자 액세스](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
  
