---
title: VBScript를 사용 하 여 WMI 공급자 액세스
description: 컴퓨터에서 실행 중인 설치 된 SQL Server 인스턴스의 버전을 나열 하는 VBScript 프로그램을 만드는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- VBScript [WMI]
- modifying SQL Server Service properties
- WMI Provider for Configuration Management, VBScript
ms.assetid: f3c5d981-eaa3-4d34-9b91-37e42636aa81
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fd1633699f6035d03066bcbd38f6ce3882b9cb68
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784678"
---
# <a name="access-wmi-provider-for-configuration-management-using-vbscript"></a>VBScript를 사용하여 구성 관리용 WMI 공급자 액세스
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]
  이 섹션에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 컴퓨터에서 실행 중인 설치 된 인스턴스의 버전을 나열 하는 VBScript 프로그램을 만드는 방법을 설명 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 이 코드 예제에서는 컴퓨터에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스와 해당 버전을 나열합니다.  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>SQL Server의 설치된 인스턴스 이름 및 버전 나열  
  
1.  텍스트 편집기(예: [!INCLUDE[msCoName](../../includes/msconame-md.md)] 메모장)에서 새 파일을 엽니다. 이 절차 다음에 나오는 코드를 복사하여 확장명이 .vbs인 파일로 저장합니다. 이 예제의 경우 test.vbs입니다.  
  
2.  VBScript `GetObject` 함수를 사용하여 컴퓨터 관리용 WMI 공급자의 인스턴스에 연결합니다. 이 예제에서는 mpc라는 원격 컴퓨터에 연결하지만 로컬 컴퓨터에 연결하는 경우에는 winmgmts:root\Microsoft\SqlServer\ComputerManagement와 같이 컴퓨터 이름을 생략합니다. `GetObject` 함수에 대한 자세한 내용은 VBScript를 참조하십시오.  
  
3.  `InstancesOf` 메서드를 사용하여 서비스 목록을 열거합니다. `ExecQuery` 메서드 대신 간단한 WQL 쿼리와 `InstancesOf` 메서드를 사용하여 서비스를 열거할 수도 있습니다.  
  
4.  `ExecQuery` 메서드와 WQL 쿼리를 사용하여 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름과 버전을 검색합니다.  
  
5.  파일을 저장합니다.  
  
6.  명령 프롬프트에서 **cscript** 를 입력 하 여 스크립트를 실행 합니다.  

## <a name="example"></a>예제  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  
