---
title: "New-RestoreLocation cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 5ca13d8c-1c5d-4f02-869c-72e0defce6d7
caps.latest.revision: 11
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 11
---
# New-RestoreLocation cmdlet
  데이터베이스를 복원하는 데 사용되는 정보를 지정합니다.  
  
## 구문  
 `New-RestoreLocation [-File <String>] [-DataSourceId <String>] [-ConnectionString <String>] [-DataSourceType <RestoreDataSourceType>] [-Folders <RestoreFolder[]>] [-AsTemplate] [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 `New-RestoreLocation [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 –Verbose, -Debug, 오류 및 경고 매개 변수, -Whatif 및 –Confirm과 같은 공통 매개 변수는 Windows PowerShell 참조에 설명되어 있습니다. 자세한 내용은 [about_CommonParameters](http://technet.microsoft.com/library/dd315352.aspx)를 참조하세요.  
  
## Description  
 New-RestoreLocation cmdlet은 서버 및 데이터베이스의 연결 문자열, 데이터 원본 속성, 복원되는 데이터베이스와 연결된 파일 및 폴더를 비롯하여 데이터베이스 복원에 사용되는 정보를 포함합니다.  
  
## 매개 변수  
  
### -File \<string>  
 복원하는 백업 파일의 이름을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -DataSourceId \<string>  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -ConnectionString \<string>  
 원격 Analysis Services 인스턴스의 연결 문자열을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -DataSourceType \<AS.RestoreDataSourceType>  
 파티션의 위치를 기준으로 데이터 원본이 원격인지 로컬인지 여부를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -Folders \<AS.RestoreFolder>  
 로컬 또는 원격 인스턴스의 파티션 폴더를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -AsTemplate \<SwitchParameter>  
 개체를 메모리에 만들어 반환해야 하는지 여부를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -Server \<string>  
 cmdlet이 연결하고 실행할 Analysis Services 인스턴스를 지정합니다. 서버 이름을 제공하지 않으면 localhost에 연결됩니다. 기본 인스턴스의 경우에는 서버 이름만 지정합니다. 명명된 인스턴스의 경우에는 servername\instancename 형식을 사용합니다. HTTP 연결의 경우 http[s]://server[:port]/virtualdirectory/msmdpump.dll 형식을 사용합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|localhost|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### -Credential \<PSCredential>  
 이 매개 변수는 HTTP 액세스를 사용하도록 구성한 Analysis Service 인스턴스에 대해 HTTP 연결을 사용할 때 사용자 이름 및 암호를 전달하는 데 사용됩니다. 자세한 내용은 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md) 및 HTTP 연결에 대한 [Analysis Services의 PowerShell 스크립팅](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)을 참조하세요.  
  
 이 매개 변수를 지정하면 사용자 이름 및 암호를 사용하여 지정된 Analysis Server 인스턴스에 연결합니다. 자격 증명을 지정하지 않으면 도구를 실행 중인 사용자의 기본 Windows 계정이 사용됩니다.  
  
 이 매개 변수를 사용하려면 먼저 Get-Credential을 사용하여 PSCredential 개체를 만들어 사용자 이름 및 암호를 지정합니다(예: `$Cred=Get-Credential “adventure-works\bobh”`). 그런 다음 이 개체를 –Credential 매개 변수에 파이프할 수 있습니다`(-Credential:$Cred`).  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|True(ByValue)|  
|와일드카드 문자 허용|false|  
  
## 입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|InclusionThresholdSetting|  
|출력|InclusionThresholdSetting|  
  
## 예  
  
## 관련 항목:  
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [PowerShell을 사용하여 테이블 형식 모델 관리](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  