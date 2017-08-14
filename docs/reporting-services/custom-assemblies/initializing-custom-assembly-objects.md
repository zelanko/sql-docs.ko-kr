---
title: "사용자 지정 어셈블리 개체 초기화 | Microsoft Docs"
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
- initializing custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], initializing
- OnInit method
ms.assetid: 26fd74dc-d02f-40f7-aeb3-50ce05e9e6b9
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: ab05efc7baba58a34180faa038cb58c7f57f4af2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/12/2017

---
# <a name="initializing-custom-assembly-objects"></a>사용자 지정 어셈블리 개체 초기화
  사용자 지정 어셈블리 클래스를 인스턴스화할 때 속성 및 필드 값을 초기화해야 하는 경우가 있습니다. 대개 보고서의 전역 개체 컬렉션에서 제공되는 값으로 사용자 지정 클래스를 초기화해야 합니다. 재정의 하 여이 작업을 수행는 **OnInit** 의 메서드는 **코드** 보고서의 개체입니다. 에 액세스 하려면 **OnInit**를 사용 하 여는 **코드** 보고서 정의의 요소입니다. 보고서에 사용 하려는 사용자 지정 어셈블리의 클래스의 정적 속성 또는 필드 값을 초기화 하는 두 가지 방법은: 선언 하 고 사용 하 여 클래스의 새 인스턴스를 만들거나 **OnInit**, 하거나 사용 하 여 공개적으로 사용할 수 있는 메서드를 호출할 수 있습니다 **OnInit**합니다.  
  
## <a name="global-object-collections-and-initialization"></a>전역 개체 컬렉션 및 초기화  
 사용자 지정 클래스 변수를 초기화하는 데 사용할 수 있는 컬렉션이 다수 있으며, 사용할 수는 **Globals** 및 **사용자** 컬렉션입니다. **매개 변수**, **필드** 및 **ReportItems** 컬렉션 지점 보고서 수명 주기에서 사용할 수 없는 경우는 **OnInit** 메서드가 호출 됩니다. 공유 컬렉션 사용 기준 **Globals** 또는 **사용자**를 포함 해야는 **보고서** 개체 참조입니다. 예를 들어 사용자 지정 클래스를 초기화 하는 보고서를 액세스 하는 사용자의 현재 언어에 따라 프로그램 **코드** 요소는 다음과 같을 수 있습니다.  
  
```  
<Code>  
   Dim m_myClass As MyClass  
  
   Protected Overrides Sub OnInit()  
      m_myClass = new MyClass(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 위에 제시한 대로 클래스의 속성 및 필드 값을 초기화하는 한 가지 방법은 다시 정의된 생성자를 호출하여 클래스를 선언하고 이 클래스의 새 인스턴스를 만드는 것입니다.  
  
 사용자 지정 어셈블리의 클래스의 속성 및 필드 값을 초기화 하는 다른 방법은에서 정의 하는 공개적으로 사용할 수 있는 메서드를 호출 하는 것은 **OnInit** 메서드. 먼저 보고서 정의 파일에서 클래스에 대한 인스턴스 이름을 추가해야 합니다. 올바른 어셈블리 참조 및 인스턴스 이름을 추가하고 나면 초기화 메서드를 호출하여 클래스에 대한 속성 및 필드 값을 초기화할 수 있습니다. 프로그램 **OnInit** 메서드는 다음과 같을 수 있습니다.  
  
```  
<Code>  
   Protected Overrides Sub OnInit()  
      m_myClass.MyInitializationMethod(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 사용자 지정 클래스에 대 한 어셈블리 참조 및 인스턴스 이름을 추가 하는 방법에 대 한 자세한 내용은 참조 [보고서 &#40;에 대 한 어셈블리 참조를 추가 합니다. Ssrs&#41; ](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md).  
  
 전역 개체 컬렉션에 대 한 자세한 내용은 참조 하세요. [식 &#40;의 기본 제공 컬렉션 보고서 작성기 및 SSRS &#41; ](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
## <a name="see-also"></a>관련 항목:  
 [보고서에서 사용자 지정 어셈블리 사용](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
