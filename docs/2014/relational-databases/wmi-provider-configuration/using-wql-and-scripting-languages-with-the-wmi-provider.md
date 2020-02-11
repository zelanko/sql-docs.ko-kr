---
title: 구성 관리용 WMI 공급자에 WQL 및 스크립트 언어 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: cc9994d4429e82f2bdd4f40797df1c5f628c6500
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68195830"
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider-for-configuration-management"></a>구성 관리용 WMI 공급자에 WQL 및 스크립트 언어 사용
  관리 애플리케이션에서는 다음과 같은 두 가지 방법으로 구성 관리용 WMI(Windows Management Instrumentation) 공급자 개체를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 네트워크 설정에 액세스합니다.  
  
-   WQL 편집기 또는 WBEMTest.exe 같은 쿼리 도구를 사용하여 WQL(Windows Management Instrumentation Language)로 설정된 개체를 쿼리합니다.  
  
-   VBScript 같은 스크립트 언어를 사용합니다.  
  
 또는 SMO에서 WMI 관리되는 개체를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 네트워크 설정을 프로그래밍 방식으로 관리할 수도 있습니다. WMI 관리 개체를 프로그래밍 하는 방법에 대 한 자세한 내용은 [Wmi 공급자를 사용 하 여 서비스 및 네트워크 설정 관리](../server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)를 참조 하세요.  
  
 구성 관리용 WMI 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 및 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 관리 콘솔을 사용하여 액세스할 수 있습니다. 사용자 인터페이스에서 WMI 공급자에 액세스 하는 방법에 대 한 자세한 내용은 [서비스 관리 방법 도움말 항목 &#40;SQL Server 구성 관리자&#41;](../../database-engine/managing-services-how-to-topics-sql-server-configuration-manager.md)을 참조 하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [WQL을 사용 하 여 구성 관리용 WMI 공급자 액세스](access-wmi-provider-for-configuration-management-using-wql.md)   
 [VBScript를 사용하여 SQL Server 서비스 고급 속성 수정](access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
  
