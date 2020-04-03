---
title: RDL 파일에서 어셈블리 참조 | Microsoft Docs
description: RDL(Report Definition Language) 파일에서, 특히 CodeModules 요소와 Classes 요소에서 어셈블리를 참조하는 방법을 알아봅니다.
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
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
ms.openlocfilehash: d310ec6895f1e8d027378fca71df36331dfbf5a8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80217022"
---
# <a name="referencing-assemblies-in-an-rdl-file"></a>RDL 파일에서 어셈블리 참조
  보고서 정의 파일에서 사용자 지정 코드 어셈블리를 사용할 수 있도록 지원하기 위해 두 가지 RDL(Report Definition Language) 요소인 **CodeModules** 요소와 **Classes** 요소가 RDL 사양에 포함되었습니다.  
  
 **CodeModules** 요소를 통해 보고서 식에서 관리 코드 어셈블리를 참조할 수 있습니다. **CodeModules**는 보고서 정의 파일에서 특수화된 함수를 호출하는 데 사용하는 어셈블리에 대한 참조가 포함된 최상위 요소입니다. 사용자 지정 어셈블리 사용을 지원하는 보고서 정의 항목은 다음과 같습니다.  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 사용자 지정 코드에서 <xref:System.Reflection.Assembly.Load%2A>를 호출하는 대신 **CodeModule** 요소를 RDL 파일에 수동으로 추가하거나 **보고서 속성** 대화 상자의 **참조** 탭을 사용하여 사용자 지정 어셈블리를 등록합니다. 자세한 내용은 [보고서 디자이너의 식에 포함된 사용자 지정 코드 및 어셈블리 참조&#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)를 나타냅니다.  
  
 **Classes** 요소는 보고서 정의에서 인스턴스 멤버 사용을 지원합니다. **Classes**는 클래스 이름 및 인스턴스 이름에 대한 참조를 포함하는 최상위 요소입니다. 인스턴스 멤버 사용을 지원하는 보고서 정의 항목은 다음과 같습니다.  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 자세한 내용은 [식을 통해 사용자 지정 어셈블리 액세스](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [보고서에서 사용자 지정 어셈블리 사용](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
