---
title: WQL을 사용 하 여 및 스크립팅 언어를 WMI 공급자 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 18
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ed3b0c63486e00ab4af97895193de8110befd3a8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider"></a>WQL을 사용 하 여 및 스크립팅 언어를 WMI 공급자
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  관리 응용 프로그램에서는 다음과 같은 두 가지 방법으로 구성 관리용 WMI(Windows Management Instrumentation) 공급자 개체를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 네트워크 설정에 액세스합니다.  
  
-   WQL 편집기 또는 WBEMTest.exe 같은 쿼리 도구를 사용하여 WQL(Windows Management Instrumentation Language)로 설정된 개체를 쿼리합니다.  
  
-   VBScript 같은 스크립트 언어를 사용합니다.  
  
 또는 SMO에서 WMI 관리되는 개체를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 네트워크 설정을 프로그래밍 방식으로 관리할 수도 있습니다. WMI를 프로그래밍 하는 방법에 대 한 자세한 내용은 관리 되는 개체를 참조 [서비스 관리 및 WMI 공급자를 사용 하 여 네트워크 설정을](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)합니다.  
  
 구성 관리용 WMI 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 관리 콘솔을 사용하여 액세스할 수 있습니다. 사용자 인터페이스에서 WMI 공급자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [서비스 관리 방법 도움말 항목 &#40;SQL Server 구성 관리자&#41;](http://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [WQL을 사용 하 여 구성 관리용 WMI 공급자 액세스](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-wql.md)   
 [VBScript를 사용 하는 SQL Server 서비스 고급 속성 수정](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
  
