---
title: "New-PowerPivotSystemServiceInstance cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 7ea94113-c0f1-4cca-9228-f1a034fba5db
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# New-PowerPivotSystemServiceInstance cmdlet
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스의 새 인스턴스를 응용 프로그램 서버에 추가합니다.  
  
 **적용 대상:** SharePoint 2010 및 SharePoint 2013  
  
## 구문  
  
```  
New-PowerPivotSystemServiceInstance [[-ParentService] <PowerPivotMidTierServicePipeBind>] [-SystemServiceInstanceName <string>] [-Provision] [<CommonParameters>]  
```  
  
## Description  
 New-PowerPivotSystemServiceInstance cmdlet은 SQL Server 설치 프로그램을 사용하여 로컬 응용 프로그램 서버에 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]이 설치된 후 팜 수준의 새 PowerPivotSystemService 개체를 프로비전합니다. 각 응용 프로그램 서버에 서비스 인스턴스를 하나만 제공할 수 있습니다.  서비스가 이미 프로비전된 경우 이 cmdlet을 실행할 수 없습니다.  
  
## 매개 변수  
  
### -ParentService \<PowerPivotMidTierServicePipeBind>  
 팜에 있는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 부모 개체의 GUID를 지정합니다. 이 릴리스에서는 부모 개체가 하나만 허용됩니다. 서비스 개체나 개체의 GUID를 반환하려면 Get-PowerPivotSystemService를 사용합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|true|  
|와일드카드 문자 허용|false|  
  
### -SystemServiceInstanceName \<string>  
 이 개체를 식별하는 이름을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|1.|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### Provision [\<SwitchParameter>]  
 SharePoint에서 서비스를 사용할 수 있게 설정합니다. 유효한 값은 $true 또는 $false입니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### \<CommonParameters>  
 이 cmdlet은 공통 매개 변수 Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer 및 OutVariable을 지원합니다. 자세한 내용은 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## 입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|없음|  
|출력|없음|  
  
## 예제 1  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -Provision:$true  
```  
  
 이 예에서는 cmdlet의 가장 일반적인 형태를 보여 줍니다. 이 예에서는 로컬 응용 프로그램 서버의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스를 팜에 등록합니다.  
  
## 예제 2  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -SystemServiceInstanceName "MyPSSInstance" -provision:$false  
```  
  
 이 예에서는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 인스턴스를 프로비전하지 않고 이름만 지정합니다. 이름을 지정하지 않으면 기본 이름인 SQL Server Analysis Services 시스템 서비스 인스턴스가 대신 사용됩니다. 필요한 경우 서비스에 대해 사용자 지정 이름을 만들 수 있습니다. 테스트 시나리오를 지원하려는 경우에 또는 이후 단계에서 인스턴스를 제공하는 스크립트나 사용자 지정 도구가 있는 경우에 서비스 이름을 지정할 수 있습니다.  
  
  