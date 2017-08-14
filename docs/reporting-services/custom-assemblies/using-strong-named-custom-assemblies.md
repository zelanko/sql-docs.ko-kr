---
title: "강력한 이름의 사용자 지정 어셈블리를 사용 하 여 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- AllowPartiallyTrustedCallersAttribute attribute
- strong-named custom assemblies [Reporting Services]
- strong names [Reporting Services]
- assemblies [Reporting Services], strong names
- custom assemblies [Reporting Services], strong-named
ms.assetid: ca9f19d7-6e86-46f2-b9ad-9bf807eaa52e
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: cf8ee5462bd75ab82ea4296a5b71136cb2eb9ee9
ms.contentlocale: ko-kr
ms.lasthandoff: 08/12/2017

---
# <a name="using-strong-named-custom-assemblies"></a>강력한 이름의 사용자 지정 어셈블리 사용
  강력한 이름은 어셈블리를 식별하며 어셈블리의 텍스트 이름, 네 부분으로 구성된 버전 번호, 문화권 정보(제공된 경우), 공개 키, 어셈블리의 매니페스트에 저장된 디지털 서명 등을 포함합니다. 강력한 이름은 CLR(공용 언어 런타임)에 대해 어셈블리를 고유하게 식별하고 이진 무결성을 보장합니다.  
  
## <a name="using-allowpartiallytrustedcallersattribute"></a>AllowPartiallyTrustedCallersAttribute 사용  
 강력한 이름의 어셈블리를 보고서와 함께 사용 하려면 강력한 이름의 어셈블리는 어셈블리를 사용 하 여 부분적으로 신뢰할 수 있는 코드에서 호출할 수를 허용 해야 **AllowPartiallyTrustedCallers** 특성입니다. 사용할 수 있습니다 **AllowPartiallyTrustedCallersAttribute** 강력한 이름의 어셈블리를 보고서 디자이너 또는 보고서 식에서 보고서 서버에서 호출할 수 있도록 합니다. 부분적으로 신뢰할 수 있는 코드로 강력한 이름의 어셈블리를 호출할 수 있도록 하려면 다음 어셈블리 수준 특성을 어셈블리 특성 파일에 추가합니다.  
  
```vb  
<assembly:AllowPartiallyTrustedCallers>  
```  
  
```csharp  
[assembly:AllowPartiallyTrustedCallers]  
```  
  
 **AllowPartiallyTrustedCallersAttribute** 어셈블리 수준에서 강력한 이름의 어셈블리에 의해 적용 하는 경우에 적용 됩니다. 어셈블리 수준에서 특성을 적용 하는 방법에 대 한 자세한 내용은 "특성 적용"을 참조는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK 설명서입니다.  
  
> [!CAUTION]  
>  때 **AllowPartiallyTrustedCallersAttribute** 가 있으면 기본 **FullTrustLinkDemand** 보안 검사가, 신뢰할 수 있는 어셈블리는 어셈블리를 부분적으로 호출할 수 있는 다른 하도록 합니다. 클래스 수준 또는 메서드 수준의 선언적 보안 특성을 포함한 모든 보안 검사는 명시적으로 지정되어야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서에서 사용자 지정 어셈블리 사용](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
