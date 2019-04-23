---
title: RDL 파일에서 어셈블리 참조 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bc52419f382ea44fc718a47e99bbd0981275d240
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60153750"
---
# <a name="referencing-assemblies-in-an-rdl-file"></a>RDL 파일에서 어셈블리 참조
  보고서 정의 파일에서 사용자 지정 코드 어셈블리를 사용할 수 있도록 지원하기 위해 두 가지 RDL(Report Definition Language) 요소인 **CodeModules** 요소와 **Classes** 요소가 RDL 사양에 포함되었습니다.  
  
 **CodeModules** 요소를 통해 보고서 식에서 관리 코드 어셈블리를 참조할 수 있습니다. **CodeModules**는 보고서 정의 파일에서 특수화된 함수를 호출하는 데 사용하는 어셈블리에 대한 참조가 포함된 최상위 요소입니다. 사용자 지정 어셈블리 사용을 지원하는 보고서 정의 항목은 다음과 같습니다.  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 사용자 지정 코드에서 <xref:System.Reflection.Assembly.Load%2A>를 호출하는 대신 **CodeModule** 요소를 RDL 파일에 수동으로 추가하거나 **보고서 속성** 대화 상자의 **참조** 탭을 사용하여 사용자 지정 어셈블리를 등록합니다. 자세한 내용은 [보고서 디자이너의 식에 포함된 사용자 지정 코드 및 어셈블리 참조&#40;SSRS&#41;](../report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)를 참조하세요.  
  
 **Classes** 요소는 보고서 정의에서 인스턴스 멤버 사용을 지원합니다. **Classes**는 클래스 이름 및 인스턴스 이름에 대한 참조를 포함하는 최상위 요소입니다. 인스턴스 멤버 사용을 지원하는 보고서 정의 항목은 다음과 같습니다.  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 자세한 내용은 [식을 통해 사용자 지정 어셈블리 액세스](accessing-custom-assemblies-through-expressions.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [보고서에서 사용자 지정 어셈블리 사용](using-custom-assemblies-with-reports.md)  
  
  
