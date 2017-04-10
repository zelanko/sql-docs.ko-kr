---
title: "Get-PowerPivotSystemServiceInstance cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 56027a8e-1949-4349-b616-68c8b1d2963c
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Get-PowerPivotSystemServiceInstance cmdlet
  팜의 응용 프로그램 서버에서 실행 중인 하나 이상의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 인스턴스를 반환합니다.  
  
 **적용 대상:** SharePoint 2010 및 SharePoint 2013  
  
## 구문  
  
```  
Get-PowerPivotSystemServiceInstance [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## Description  
 Get-PowerPivotSystemServiceInstance cmdlet은 팜에서 실행 중인 하나 이상의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 인스턴스의 속성을 반환합니다. 이 cmdlet은 응용 프로그램 유형, 상태(온라인 또는 오프라인) 및 ID를 보고합니다. 특정 인스턴스의 추가 속성을 보려면 이 cmdlet에 Identity 매개 변수와 format-list 옵션을 추가합니다.  
  
## 매개 변수  
  
### -Identity \<PowerPivotMidTierServiceInstancePipeBind>  
 가져올 서비스 인스턴스를 지정합니다. 팜에서 개체를 고유하게 식별하는 유효한 GUID 값을 지정해야 합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|true|  
|와일드카드 문자 허용|false|  
  
### \<CommonParameters>  
 이 cmdlet은 공통 매개 변수 Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer 및 OutVariable을 지원합니다. 자세한 내용은 [About_commonparameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## 입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|없음|  
|출력|없음|  
  
## 예제 1  
  
```  
C:\PS>Get-PowerPivotSystemServiceInstance -Identity 1234567-890a-bcde-fghijklm | format-list| format-list  
```  
  
 이 예에서는 서버 이름, 버전 및 업그레이드 상태를 포함하여 지정한 인스턴스의 추가 속성을 반환합니다.  
  
  