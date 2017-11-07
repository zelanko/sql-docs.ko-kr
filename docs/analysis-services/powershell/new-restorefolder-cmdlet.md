---
title: "새 RestoreFolder cmdlet | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 5938b3a9-6412-45fc-86f8-264651d01598
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4ee3a6068f376ff4f08af4cae67aa00d157d1f86
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="new-restorefolder-cmdlet"></a>New-RestoreFolder cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  원래 폴더를 새 폴더에 복원합니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
## <a name="syntax"></a>구문  
 `New-RestoreFolder [-OriginalFolder] <String> [-NewFolder] <String> [-AsTemplate] [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 `New-RestoreFolder [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 –Verbose, -Debug, 오류 및 경고 매개 변수, -Whatif 및 –Confirm과 같은 공통 매개 변수는 Windows PowerShell 참조에 설명되어 있습니다. 자세한 내용은 [about_CommonParameters](http://technet.microsoft.com/library/dd315352.aspx)를 참조하세요.  
  
## <a name="description"></a>Description  
 New-RestoreFolder cmdlet은 원래 폴더의 이름을 기준으로 새 폴더를 만드는 데 사용됩니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-originalfolder-string"></a>-OriginalFolder \<문자열 >  
 원래 폴더 위치를 가져옵니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|true|  
|와일드카드 문자 허용|false|  
  
### <a name="-newfolder-string"></a>-NewFolder \<문자열 >  
 새 폴더 위치를 설정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|1.|  
|기본값||  
|파이프라인 입력 허용|true|  
|와일드카드 문자 허용|false|  
  
### <a name="-astemplate-switchparameter"></a>-AsTemplate \<SwitchParameter >  
 개체를 메모리에 만들어 반환해야 하는지 여부를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-server-string"></a>-서버 \<문자열 >  
 cmdlet이 연결하고 실행할 Analysis Services 인스턴스를 지정합니다. 서버 이름을 제공하지 않으면 localhost에 연결됩니다. 기본 인스턴스의 경우에는 서버 이름만 지정합니다. 명명된 인스턴스의 경우에는 servername\instancename 형식을 사용합니다. HTTP 연결의 경우 http[s]://server[:port]/virtualdirectory/msmdpump.dll 형식을 사용합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값|localhost|  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 이 매개 변수는 HTTP 액세스를 사용하도록 구성한 Analysis Service 인스턴스에 대해 HTTP 연결을 사용할 때 사용자 이름 및 암호를 전달하는 데 사용됩니다. 자세한 내용은 참조 [HTTP 액세스 구성 Analysis Services 인터넷 정보 서비스 &#40; IIS &#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md) HTTP 연결에 대 한 합니다.  
  
 이 매개 변수를 지정하면 사용자 이름 및 암호를 사용하여 지정된 Analysis Server 인스턴스에 연결합니다. 자격 증명을 지정하지 않으면 도구를 실행 중인 사용자의 기본 Windows 계정이 사용됩니다.  
  
 이 매개 변수를 사용하려면 먼저 Get-Credential을 사용하여 PSCredential 개체를 만들어 사용자 이름 및 암호를 지정합니다(예: `$Cred=Get-Credential “adventure-works\bobh”`). 그런 다음 이 개체를 –Credential 매개 변수에 파이프할 수 있습니다 `(-Credential:$Cred`).  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|True(ByValue)|  
|와일드카드 문자 허용|false|  
  
## <a name="inputs-and-outputs"></a>입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력||  
|출력|없음|  
  

