---
title: "Get-PowerPivotServiceApplication cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 99e4faa1-2f87-43c6-b7ec-a97d4112c5ac
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Get-PowerPivotServiceApplication cmdlet
  하나 이상의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 반환합니다.  
  
 **적용 대상:** SharePoint 2010 및 SharePoint 2013  
  
## 구문  
  
```  
Get-PowerPivotServiceApplication [[-Identity] <SPGeminiServiceApplicationPipeBind>] [<CommonParameters>]  
```  
  
## Description  
 Get-PowerPivotServiceApplication cmdlet은 Identity 매개 변수로 지정된 서비스 응용 프로그램을 반환합니다. 매개 변수를 지정하지 않으면 팜에 있는 모든 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 반환합니다. 각 응용 프로그램은 응용 프로그램의 표시 이름, 응용 프로그램 유형 및 GUID로 식별됩니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램의 추가 속성을 보려면 이 cmdlet에 format-list 옵션을 추가합니다.  
  
## 매개 변수  
  
### -Identity \<SPGeminiServiceApplicationPipeBind>  
 가져올 서비스 응용 프로그램을 지정합니다. 팜에서 개체를 고유하게 식별하는 유효한 GUID 값을 지정해야 합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|true|  
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
C:\PS>Get-PowerPivotServiceApplication  
```  
  
 이 예에서는 팜에 있는 하나 이상의 서비스 응용 프로그램을 반환합니다.  
  
## 예제 2  
  
```  
C:\PS>Get-PowerPivotServiceApplication | format-list  
```  
  
 이 예에서는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램의 모든 속성을 반환합니다.  
  
## 예 3  
  
```  
C:\PS>get-PowerPivotServiceApplication -Identity 1234567-890a-bcde-fghijklm  
```  
  
 이 예에서는 표시 이름, 응용 프로그램 유형 및 응용 프로그램 GUID와 함께 단일 서비스 응용 프로그램을 반환합니다. 표시 이름이 긴 경우 잘립니다. 전체 이름을 보려면 format-list 옵션을 사용합니다.  
  
  