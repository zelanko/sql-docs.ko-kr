---
title: 구성 관리용 WMI 공급자
description: 구성 관리용 WMI 공급자가 WMI를 사용 하 여 SQL Server에서 서비스, 서버 별칭 및 클라이언트/서버 네트워크 설정을 관리 하는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 643cfdcca57bc6427cf92f2ca96f1c9e4716ced9
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888224"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>구성 관리용 WMI 공급자 이해
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]구성 관리용 WMI 공급자를 제공 합니다. 구성 관리용 WMI 공급자는 WMI(Windows Management Instrumentation)를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트/서버 네트워크 설정 및 서버 별칭을 관리할 수 있도록 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]서비스, 네트워크 설정 및 별칭은 컴퓨터의 root\Microsoft\SqlServer\ComputerManagement*nn* 네임 스페이스에 있는 WMI 개체로 표시 됩니다. 지정된 컴퓨터에서 WMI 공급자를 사용하여 연결이 설정된 후에는 WQL이나 스크립팅 언어를 사용하여 서비스, 네트워크 설정 및 별칭을 쿼리할 수 있습니다.  
  
 WMI 공급자는 인스턴스 공급자로서 [WMI 클래스](../../relational-databases/wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md) 의 인스턴스를 제공 하 고 다음과 같은 비동기 작업을 지원 합니다.  
  
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
  
 구성 관리용 WMI 공급자를 사용 하는 관리 응용 프로그램의 예는 [구성 관리용 Wmi 공급자에 WQL 및 스크립트 언어 사용](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)을 참조 하세요.  
  
 WMI 공급자를 사용 하 여 관리 응용 프로그램을 프로그래밍 하는 방법에 대 한 자세한 내용은 .NET Framework SDK의 WMI 설명서를 참조 하십시오 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>참고 항목  
 [구성 관리용 WMI 공급자 작업](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [구성 관리용 WMI 공급자에 WQL 및 스크립트 언어 사용](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
