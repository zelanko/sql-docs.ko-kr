---
title: VBScript를 사용 하는 SQL Server 서비스 고급 속성 수정 | Microsoft Docs
ms.custom: ''
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
ms.openlocfilehash: 90632548114577475735a6dfca9244c84c09ab2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139443"
---
# <a name="access-wmi-provider-for-configuration-management-using-vbscript"></a>VBScript를 사용하여 구성 관리용 WMI 공급자 액세스
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  이 섹션에서는 설치 된 인스턴스의 버전을 나열 하는 VBScript 프로그램을 만드는 방법 설명 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 실행 되는 합니다.  
  
 이 코드 예제에서는 컴퓨터에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스와 해당 버전을 나열합니다.  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>SQL Server의 설치된 인스턴스 이름 및 버전 나열  
  
1.  텍스트 편집기(예: [!INCLUDE[msCoName](../../includes/msconame-md.md)] 메모장)에서 새 파일을 엽니다. 이 절차 다음에 나오는 코드를 복사하여 확장명이 .vbs인 파일로 저장합니다. 이 예제의 경우 test.vbs입니다.  
  
2.  VBScript `GetObject` 함수를 사용하여 컴퓨터 관리용 WMI 공급자의 인스턴스에 연결합니다. 이 예제에서는 mpc라는 원격 컴퓨터에 연결하지만 로컬 컴퓨터에 연결하는 경우에는 winmgmts:root\Microsoft\SqlServer\ComputerManagement와 같이 컴퓨터 이름을 생략합니다. `GetObject` 함수에 대한 자세한 내용은 VBScript를 참조하십시오.  
  
3.  `InstancesOf` 메서드를 사용하여 서비스 목록을 열거합니다. `ExecQuery` 메서드 대신 간단한 WQL 쿼리와 `InstancesOf` 메서드를 사용하여 서비스를 열거할 수도 있습니다.  
  
4.  `ExecQuery` 메서드와 WQL 쿼리를 사용하여 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름과 버전을 검색합니다.  
  
5.  파일을 저장합니다.  
  
6.  입력 하 여 스크립트 실행 **cscript test.vbs** 명령 프롬프트에서.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="example"></a>예제  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  
