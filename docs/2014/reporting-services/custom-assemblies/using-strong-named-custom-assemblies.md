---
title: 강력한 이름의 사용자 지정 어셈블리 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- AllowPartiallyTrustedCallersAttribute attribute
- strong-named custom assemblies [Reporting Services]
- strong names [Reporting Services]
- assemblies [Reporting Services], strong names
- custom assemblies [Reporting Services], strong-named
ms.assetid: ca9f19d7-6e86-46f2-b9ad-9bf807eaa52e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5e685ecda39e0487eb4b469920820fa6e4a10daa
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60153914"
---
# <a name="using-strong-named-custom-assemblies"></a>강력한 이름의 사용자 지정 어셈블리 사용
  강력한 이름은 어셈블리를 식별하며 어셈블리의 텍스트 이름, 네 부분으로 구성된 버전 번호, 문화권 정보(제공된 경우), 공개 키, 어셈블리의 매니페스트에 저장된 디지털 서명 등을 포함합니다. 강력한 이름은 CLR(공용 언어 런타임)에 대해 어셈블리를 고유하게 식별하고 이진 무결성을 보장합니다.  
  
## <a name="using-allowpartiallytrustedcallersattribute"></a>AllowPartiallyTrustedCallersAttribute 사용  
 보고서에서 강력한 이름의 어셈블리를 사용하려면 어셈블리의 **AllowPartiallyTrustedCallers** 특성을 사용하여 부분적으로 신뢰할 수 있는 코드를 통해 강력한 이름의 어셈블리가 호출되도록 해야 합니다. **AllowPartiallyTrustedCallersAttribute**를 사용하여 강력한 이름의 어셈블리가 보고서 식에서 보고서 디자이너 또는 보고서 서버에 의해 호출되도록 할 수 있습니다. 부분적으로 신뢰할 수 있는 코드로 강력한 이름의 어셈블리를 호출할 수 있도록 하려면 다음 어셈블리 수준 특성을 어셈블리 특성 파일에 추가합니다.  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 **AllowPartiallyTrustedCallersAttribute**는 어셈블리 수준에서 강력한 이름의 어셈블리에 의해 적용될 때만 유효합니다. 어셈블리 수준에서 특성을 적용하는 방법은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 설명서의 "특성 적용"을 참조하세요.  
  
> [!CAUTION]  
>  **AllowPartiallyTrustedCallersAttribute**가 있는 경우에는 기본 **FullTrustLinkDemand** 보안 검사가 수행되지 않아 부분적으로 신뢰할 수 있는 다른 어셈블리에서 어셈블리를 호출할 수 있게 됩니다. 클래스 수준 또는 메서드 수준의 선언적 보안 특성을 포함한 모든 보안 검사는 명시적으로 지정되어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서에서 사용자 지정 어셈블리 사용](using-custom-assemblies-with-reports.md)  
  
  
