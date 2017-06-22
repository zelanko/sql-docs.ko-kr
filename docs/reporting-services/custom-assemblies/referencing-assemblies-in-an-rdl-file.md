---
title: "RDL 파일에서 어셈블리 참조 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
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
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
caps.latest.revision: 36
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 87609ab5b118eaa696f7152b25cf7e984e7f6e7f
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="referencing-assemblies-in-an-rdl-file"></a>RDL 파일에서 어셈블리 참조
  보고서 정의 파일에서 사용자 지정 코드 어셈블리의 사용을 지원 하려면 두 개의 언어 RDL (Report Definition) 요소가 RDL 사양에 포함 된다는:는 **CodeModules** 요소 및 **클래스** 요소입니다.  
  
 **CodeModules** 요소를 사용 하면 보고서 식에서 관리 코드 어셈블리를 참조할 수 있습니다. **CodeModules** 는 특수화 된 함수를 호출 하 여 보고서 정의 파일에서 사용 하는 어셈블리에 대 한 참조를 포함 하는 최상위 요소입니다. 사용자 지정 어셈블리 사용을 지원하는 보고서 정의 항목은 다음과 같습니다.  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 호출 하는 대신 <xref:System.Reflection.Assembly.Load%2A> 사용자 지정 코드에서 수동으로 추가 하거나 사용자 지정 어셈블리를 등록 **CodeModule** RDL 파일을 사용 하거나 사용 하 여 요소는 **참조** 탭은 **보고서 속성** 대화 상자. 자세한 내용은 [보고서 디자이너의 식에 포함된 사용자 지정 코드 및 어셈블리 참조&#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)를 참조하세요.  
  
 **클래스** 요소가 보고서 정의의 인스턴스 멤버 사용을 지원 합니다. **클래스** 클래스 이름 및 인스턴스 이름에 대 한 참조를 포함 하는 요소는 최상위 요소입니다. 인스턴스 멤버 사용을 지원하는 보고서 정의 항목은 다음과 같습니다.  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 자세한 내용은 참조 [액세스 Custom Assemblies Through Expressions](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서에 사용자 지정 어셈블리 사용](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
