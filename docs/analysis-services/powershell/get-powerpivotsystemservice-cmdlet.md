---
title: Get-powerpivotsystemservice cmdlet | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c2a955a9d9b91521adc6abfcdd5af4109958fa8f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34037487"
---
# <a name="get-powerpivotsystemservice-cmdlet"></a>Get-PowerPivotSystemService cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  팜에 있는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 개체의 전역 속성을 반환합니다. 

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
 **적용 대상:** SharePoint 2010 및 SharePoint 2013  
  
## <a name="syntax"></a>구문  
  
```  
Get-PowerPivotSystemService [-Identity <PowerPivotMidTierServicePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Get-PowerPivotSystemService cmdlet은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 개체의 전역 속성을 반환합니다. 부모 개체는 팜마다 하나씩이지만 팜의 개별 응용 프로그램 서버에서 실행되는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 인스턴스는 여러 개 있을 수 있습니다. 부모 개체는 인스턴스별로 달라지지 않는 팜 수준 설정을 보여 줍니다. 팜에 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치가 여러 개 있는 경우 팜의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 인스턴스 수를 나타내는 쉼표로 구분된 인스턴스 목록이 제공됩니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-identity-powerpivotmidtierservicepipebind"></a>-Identity \<PowerPivotMidTierServicePipeBind>  
 가져올 부모 개체를 지정합니다. 팜에서 개체를 고유하게 식별하는 유효한 GUID 값을 지정해야 합니다.  
  
|||  
|-|-|  
|필수 여부|false|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|true|  
|와일드카드 문자 허용|false|  
  
### <a name="commonparameters"></a>\<CommonParameters>  
 이 cmdlet은 공통 매개 변수 Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer 및 OutVariable을 지원합니다. 자세한 내용은 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## <a name="inputs-and-outputs"></a>입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|없음|  
|출력|없음|  
  
## <a name="example-1"></a>예제 1  
  
```  
C:\PS>Get-PowerPivotSystemService  
```  
  
 이 예에서는 팜의 모든 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 시스템 서비스 인스턴스가 공유하는 속성을 보여 주는 부모 개체의 전역 속성을 반환합니다.  
  
  
