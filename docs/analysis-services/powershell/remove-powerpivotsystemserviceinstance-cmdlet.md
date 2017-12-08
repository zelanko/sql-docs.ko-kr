---
title: Remove-powerpivotsystemserviceinstance cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: bc46094a-5584-47ba-8883-77dc79373a5d
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 91075034a552805dd9540a87597d5956c457ada5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="remove-powerpivotsystemserviceinstance-cmdlet"></a>Remove-PowerPivotSystemServiceInstance cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 인스턴스를 팜에서 제거합니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
 **적용 대상:** SharePoint 2010 및 SharePoint 2013  
  
## <a name="syntax"></a>구문  
  
```  
Remove-PowerPivotSystemServiceInstance [-Confirm <switch>] [-DeleteLocal <switch>] [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Remove-PowerPivotSystemServiceInstance cmdlet은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스에 대한 인스턴스 정보를 팜에서 제거합니다. 프로그램 파일은 제거하지 않습니다. 프로그램 파일을 영구히 제거하려면 프로그램을 제거해야 합니다.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스를 제거하려는 경우 Remove-PowerPivotEngineServiceInstance도 실행하여 관련 Analysis Services 인스턴스를 제거한 다음 Remove-PowerPivotServiceApplication을 실행하여 PowerPivot 서비스 응용 프로그램을 삭제해야 합니다. 서비스가 제거되면 서비스 응용 프로그램이 더 이상 실행되지 않습니다.  
  
 이 변경을 되돌리려면 New-PowerPivotSystemServiceInstance -Provision:$true를 실행하여 인스턴스 정보를 다시 사용하도록 설정하면 됩니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-identity-powerpivotmidtierserviceinstancepipebind"></a>Id \<PowerPivotMidTierServiceInstancePipeBind >  
 제거할 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 인스턴스의 GUID를 지정합니다. SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 이 설치된 각 응용 프로그램 서버에는 서비스 인스턴스가 하나씩 있습니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|true|  
|와일드카드 문자 허용|false|  
  
### <a name="-deletelocal-switch"></a>-DeleteLocal \<전환 >  
 로컬 컴퓨터에 설치된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 인스턴스를 삭제하여 개체 ID를 지정하지 않고도 인스턴스를 제거할 수 있도록 합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-confirm-switch"></a>-확인 \<전환 >  
 명령을 실행하기 전 확인 메시지를 표시합니다. 이 값은 기본적으로 설정되어 있습니다. 명령에서 확인 응답을 무시하려면 명령에 Confirm:$false를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="commonparameters"></a>\<일반 매개 변수 >  
 이 cmdlet은 공통 매개 변수 Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer 및 OutVariable을 지원합니다. 자세한 내용은 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## <a name="inputs-and-outputs"></a>입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|없음|  
|출력|없음|  
  
## <a name="example-1"></a>예제 1  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -deletelocal  
```  
  
 이 예에서는 로컬 응용 프로그램 서버에서 실행되는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 인스턴스를 제거하는 방법을 보여 줍니다.  
  
## <a name="example-2"></a>예제 2  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -identity 1234567-890a-bcde-fghijklmn  
```  
  
 이 예에서는 ID를 기준으로 특정 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스를 삭제하는 방법을 보여 줍니다.  
  
  
