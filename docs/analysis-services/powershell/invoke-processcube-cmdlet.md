---
title: "Invoke-ProcessCube cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: b10ba7c1-8f10-4e72-9626-f9285e4341fd
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Invoke-ProcessCube cmdlet
  특정 처리 유형 변수를 사용하여 큐브를 처리합니다.  
  
## 구문  
 `Invoke-ProcessCube [-Name] <System.String> [-Database] <System.String> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
 `Invoke-ProcessCube –DatabaseCube <Microsoft.AnalysisServices.Cube> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
## Description  
 Invoke-ProcessCube cmdlet은 사용자가 지정한 수준으로 큐브를 처리합니다. 예를 들어 ProcessFull은 기존 데이터를 모두 새로운 데이터로 덮어씁니다. 큐브를 처리할 때는 처리 유형을 지정해야 합니다. 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
## 매개 변수  
  
### -Name \<string>  
 처리할 큐브를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -Database \<string>  
 큐브가 속한 데이터베이스를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|1.|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -ProcessType \<Microsoft.AnalysisServices.ProcessType>  
 ProcessFull, ProcessAdd, ProcessUpdate, ProcessIndexes, ProcessData, ProcessDefault, ProcessClear, ProcessStructure, ProcessCelarStructureOnly, ProcessScriptCache, ProcessRecalc 등 처리 유형을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|2|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -DatabaseCube \<Microsoft.AnalysisSevices.Cube>  
 처리할 Microsoft.AnalysisServices.Cube 개체를 지정합니다. 파이프라인을 통해 큐브 이름에 전달하려는 경우 이 매개 변수를 사용합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|True(ByPropertyName)|  
|와일드카드 문자 허용|false|  
  
### \<CommonParameters>  
 이 cmdlet은 공통 매개 변수 -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer 및 -OutVariable을 지원합니다. 자세한 내용은 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## 입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|InclusionThresholdSetting|  
|출력|InclusionThresholdSetting|  
  
## 예제 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works > Get-Item .| Invoke-ProcessCube–ProcessType:ProcessDefault`  
  
 이 명령은 처리할 큐브의 ID를 파이프합니다.  
  
## 예제 2  
 `PS SQL SERVER:\sqlas\locahost\default > Invoke-ProcessCube “Adventure Works” –database AWTEST –ProcessType:ProcessDefault`  
  
 이 명령은 AWTEST 데이터베이스에서 Adventure Works 큐브를 처리합니다.  
  
## 관련 항목:  
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [PowerShell을 사용하여 테이블 형식 모델 관리](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  