---
title: 구성 관리용 WMI 공급자 이해 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 459bb3bb7843a0f962d9747ac702da23909ca9fc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184894"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>구성 관리용 WMI 공급자 이해
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리용 WMI 공급자를 제공합니다. 구성 관리용 WMI 공급자는 WMI(Windows Management Instrumentation)를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트/서버 네트워크 설정 및 서버 별칭을 관리할 수 있도록 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스, 네트워크 설정 및 별칭 root\Microsoft\SqlServer\ComputerManagement에 있는 WMI 개체로 표시 됩니다*nn* 컴퓨터의 네임 스페이스입니다. 지정된 컴퓨터에서 WMI 공급자를 사용하여 연결이 설정된 후에는 WQL이나 스크립팅 언어를 사용하여 서비스, 네트워크 설정 및 별칭을 쿼리할 수 있습니다.  
  
 WMI 공급자는 인스턴스 공급자로서 인스턴스를 제공 된 [WMI 클래스](../wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md) 하 고 다음과 같은 비동기 작업을 지원 합니다.  
  
 인스턴스 검색  
 특정 클래스 유형 인스턴스를 검색합니다.  
  
 열거형  
 모든 클래스 유형 인스턴스를 열거합니다.  
  
 수정  
 특정 클래스 유형 인스턴스를 수정합니다.  
  
 클래스에는 해당 속성을 수정할 수 있는 메서드가 있습니다.  
  
 삭제  
 특정 클래스 유형 인스턴스를 제거합니다.  
  
 쿼리 처리  
 필터를 기반으로 클래스 유형 인스턴스를 열거합니다.  
  
 구성 관리용 WMI 공급자를 사용 하 여 관리 응용 프로그램의 예 참조 [WQL 및 스크립트 언어 구성 관리용 WMI 공급자](using-wql-and-scripting-languages-with-the-wmi-provider.md)합니다.  
  
 WMI 공급자를 사용 하 여 관리 응용 프로그램을 프로그래밍 하는 방법에 대 한 자세한 내용은에 있는 WMI 설명서를 참조 하십시오.는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework SDK입니다.  
  
## <a name="see-also"></a>관련 항목  
 [구성 관리용 WMI 공급자 작업](working-with-the-wmi-provider-for-configuration-management.md)   
 [구성 관리용 WMI 공급자에 WQL 및 스크립트 언어 사용](using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  