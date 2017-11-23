---
title: Get-powerpivotsystemserviceinstance cmdlet | Microsoft Docs
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
ms.assetid: 56027a8e-1949-4349-b616-68c8b1d2963c
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 744292be0abd645347570c6d63a6e8239001197f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="get-powerpivotsystemserviceinstance-cmdlet"></a>Get-PowerPivotSystemServiceInstance cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  팜의 응용 프로그램 서버에서 실행 중인 하나 이상의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 인스턴스를 반환합니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
 **적용 대상:** SharePoint 2010 및 SharePoint 2013  
  
## <a name="syntax"></a>구문  
  
```  
Get-PowerPivotSystemServiceInstance [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Get-PowerPivotSystemServiceInstance cmdlet은 팜에서 실행 중인 하나 이상의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 인스턴스의 속성을 반환합니다. 이 cmdlet은 응용 프로그램 유형, 상태(온라인 또는 오프라인) 및 ID를 보고합니다. 특정 인스턴스의 추가 속성을 보려면 이 cmdlet에 Identity 매개 변수와 format-list 옵션을 추가합니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-identity-powerpivotmidtierserviceinstancepipebind"></a>Id \<PowerPivotMidTierServiceInstancePipeBind >  
 가져올 서비스 인스턴스를 지정합니다. 팜에서 개체를 고유하게 식별하는 유효한 GUID 값을 지정해야 합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|true|  
|와일드카드 문자 허용|false|  
  
### <a name="commonparameters"></a>\<일반 매개 변수 >  
 이 cmdlet은 공통 매개 변수 Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer 및 OutVariable을 지원합니다. 자세한 내용은 [About_commonparameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## <a name="inputs-and-outputs"></a>입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|없음|  
|출력|없음|  
  
## <a name="example-1"></a>예제 1  
  
```  
C:\PS>Get-PowerPivotSystemServiceInstance -Identity 1234567-890a-bcde-fghijklm | format-list| format-list  
```  
  
 이 예에서는 서버 이름, 버전 및 업그레이드 상태를 포함하여 지정한 인스턴스의 추가 속성을 반환합니다.  
  
  
