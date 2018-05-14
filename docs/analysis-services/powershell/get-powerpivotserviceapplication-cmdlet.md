---
title: Get-powerpivotserviceapplication cmdlet | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2a5ccd05b8c5e947972218a22c0abbc358731ee5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="get-powerpivotserviceapplication-cmdlet"></a>Get-PowerPivotServiceApplication cmdlet
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  하나 이상의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 반환합니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
 **적용 대상:** SharePoint 2010 및 SharePoint 2013  
  
## <a name="syntax"></a>구문  
  
```  
Get-PowerPivotServiceApplication [[-Identity] <SPGeminiServiceApplicationPipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 Get-PowerPivotServiceApplication cmdlet은 Identity 매개 변수로 지정된 서비스 응용 프로그램을 반환합니다. 매개 변수를 지정하지 않으면 팜에 있는 모든 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램을 반환합니다. 각 응용 프로그램은 응용 프로그램의 표시 이름, 응용 프로그램 유형 및 GUID로 식별됩니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램의 추가 속성을 보려면 이 cmdlet에 format-list 옵션을 추가합니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>Id \<SPGeminiServiceApplicationPipeBind >  
 가져올 서비스 응용 프로그램을 지정합니다. 팜에서 개체를 고유하게 식별하는 유효한 GUID 값을 지정해야 합니다.  
  
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
C:\PS>Get-PowerPivotServiceApplication  
```  
  
 이 예에서는 팜에 있는 하나 이상의 서비스 응용 프로그램을 반환합니다.  
  
## <a name="example-2"></a>예제 2  
  
```  
C:\PS>Get-PowerPivotServiceApplication | format-list  
```  
  
 이 예에서는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서비스 응용 프로그램의 모든 속성을 반환합니다.  
  
## <a name="example-3"></a>예 3  
  
```  
C:\PS>get-PowerPivotServiceApplication -Identity 1234567-890a-bcde-fghijklm  
```  
  
 이 예에서는 표시 이름, 응용 프로그램 유형 및 응용 프로그램 GUID와 함께 단일 서비스 응용 프로그램을 반환합니다. 표시 이름이 긴 경우 잘립니다. 전체 이름을 보려면 format-list 옵션을 사용합니다.  
  
  
