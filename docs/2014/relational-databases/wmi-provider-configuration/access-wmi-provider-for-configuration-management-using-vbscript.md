---
title: VBScript를 사용 하 여 SQL Server 서비스 고급 속성 수정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: f3a380f80b4ecc7540e29605543722edd55e226d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62705060"
---
# <a name="modify-sql-server-service-advanced-properties-using-vbscript"></a>VBScript를 사용하여 SQL Server 서비스 고급 속성 수정
  이 섹션에서는 컴퓨터에서 실행 중인 설치 된 인스턴스의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 나열 하는 VBScript 프로그램을 만드는 방법을 설명 합니다.  
  
 이 코드 예제에서는 컴퓨터에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스와 해당 버전을 나열합니다.  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>SQL Server의 설치된 인스턴스 이름 및 버전 나열  
  
1.  텍스트 편집기(예: [!INCLUDE[msCoName](../../includes/msconame-md.md)] 메모장)에서 새 파일을 엽니다. 이 절차 다음에 나오는 코드를 복사하여 확장명이 .vbs인 파일로 저장합니다. 이 예제의 경우 test.vbs입니다.  
  
2.  VBScript `GetObject` 함수를 사용하여 컴퓨터 관리용 WMI 공급자의 인스턴스에 연결합니다. 이 예제에서는 mpc라는 원격 컴퓨터에 연결하지만 로컬 컴퓨터에 연결하는 경우에는 winmgmts:root\Microsoft\SqlServer\ComputerManagement와 같이 컴퓨터 이름을 생략합니다. `GetObject` 함수에 대한 자세한 내용은 VBScript를 참조하십시오.  
  
3.  `InstancesOf` 메서드를 사용하여 서비스 목록을 열거합니다. `ExecQuery` 메서드 대신 간단한 WQL 쿼리와 `InstancesOf` 메서드를 사용하여 서비스를 열거할 수도 있습니다.  
  
4.  `ExecQuery` 메서드와 WQL 쿼리를 사용하여 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름과 버전을 검색합니다.  
  
5.  파일을 저장합니다.  
  
6.  명령 프롬프트에서를 입력 `cscript test.vbs` 하 여 스크립트를 실행 합니다.  
  
## <a name="example"></a>예제  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  
