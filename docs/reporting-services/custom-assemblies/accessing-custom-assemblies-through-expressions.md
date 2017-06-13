---
title: "식을 통해 사용자 지정 어셈블리 액세스 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
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
- expressions [Reporting Services], custom assemblies
- static member calls
- instance member calls [Reporting Services]
- calling class members
- custom assemblies [Reporting Services], expressions
ms.assetid: 917c4d47-1a95-4f54-98b1-e8cb2165d90f
caps.latest.revision: 32
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 70ff488827e5289d401bf62b67a82a08ecc25f70
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="accessing-custom-assemblies-through-expressions"></a>식을 통해 사용자 지정 어셈블리 액세스
  사용자 지정 어셈블리를 만들어 보고서 디자이너 또는 보고서 서버에서 사용할 수 있도록 했으며, 적절한 보안 정책을 추가하고, 보고서 정의에서 사용자 지정 어셈블리에 대한 참조를 추가했으면 보고서 식을 사용하여 어셈블리의 클래스 멤버에 액세스할 수 있습니다. 식의 사용자 지정 코드를 참조하려면 어셈블리 내에서 클래스의 멤버를 호출해야 합니다. 이 방법은 메서드가 정적인지 아니면 인스턴스 기반인지에 따라 달라집니다.  
  
## <a name="calling-static-members-from-a-report-definition-file"></a>보고서 정의 파일에서 정적 멤버 호출  
 정적 멤버는 인스턴스화된 개체가 아닌 클래스 또는 형식 자체에 속합니다. 이러한 멤버는 클래스에서 직접 호출하여 액세스할 수 있습니다. 정적 멤버가 기능을 가장 잘 수행하므로 보고서에서 사용자 지정 함수를 호출하려면 가능하면 항상 정적 멤버를 사용해야 합니다. 형식을 사용 하는 식으로 참조 해야 정적 멤버를 호출 하려면 =*Namespace.Class.Method*합니다.  
  
#### <a name="to-call-static-members"></a>정적 멤버를 호출하려면  
  
-   정적 멤버를 호출하려면 네임스페이스, 클래스 이름 및 멤버 이름이 포함된 멤버의 정규화된 이름과 동일하게 식을 설정합니다. 다음 예제에서는 **ToGBP** 을 변환 하는 메서드는 **StandardCost** 필드 값을 달러에서 파운드로 변환 하는 보고서에 표시 됩니다:  
  
    ```  
    =CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
    ```  
  
### <a name="important-information-regarding-static-fields-and-properties"></a>정적 필드 및 속성 관련 중요 정보  
 현재 모든 보고서는 동일한 응용 프로그램 도메인에서 실행됩니다. 이것은 사용자별 정적 데이터가 있는 보고서에서 동일한 보고서의 다른 인스턴스에 이 데이터를 공개한다는 의미입니다. 이에 따라 특정 보고서를 현재 실행하고 있는 모든 사용자가 한 사용자의 정적 데이터를 사용할 수 있게 됩니다. 이러한 이유로 것이 좋습니다 사용 하는 정적 필드 또는 속성을 사용자 지정 어셈블리 또는 **코드** 요소로 대신 보고서에서 인스턴스 필드나 속성을 사용 합니다. 정적 메서드는 상태나 데이터를 저장하지 않으므로 계속 사용할 수 있습니다.  
  
## <a name="calling-instance-members-from-a-report-definition-file"></a>보고서 정의 파일에서 인스턴스 멤버 호출  
 액세스해야 할 보고서 정의 내 인스턴스 멤버가 사용자 지정 어셈블리에 포함되어 있는 경우 클래스에 대한 인스턴스 이름을 보고서에 추가해야 합니다. 사용 하 여 클래스에 대 한 인스턴스 이름을 추가할 수는 **코드** 탭은 **보고서 속성** 대화 상자. 클래스의 인스턴스를 보고서에 추가 하는 방법에 대 한 자세한 내용은 참조 [사용자 지정 코드 및 보고서 디자이너 &#40;의 식에서 어셈블리 참조 Ssrs&#41; ](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 형식을 사용 하는 식으로 참조 해야 정적 멤버를 호출 하려면 = Code*합니다. InstanceName.Method*합니다.  
  
#### <a name="to-call-instance-members"></a>인스턴스 멤버를 호출하려면  
  
-   사용자 지정 어셈블리의 인스턴스 멤버를 호출 하려면를 참조 해야 합니다는 **코드** 키워드 인스턴스 이름 및 메서드가 뒤에 추가 합니다. 다음 예제에서는 인스턴스 메서드를 호출 **ToEUR** 으로 변환 하는 **StandardCost** 필드 값을 달러에서 유로로을 보고서에 표시 됩니다.  
  
    ```  
    =Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
    ```  
  
## <a name="see-also"></a>관련 항목:  
 [보고서에 사용자 지정 어셈블리 사용](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
