---
title: "변수를 사용 하 여 스크립트 구성 요소에서 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bac1e6d96e872be0355282c3e12fc81054ca41cd
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="using-variables-in-the-script-component"></a>스크립트 구성 요소에서 변수 사용
  변수에는 패키지와 해당 컨테이너, 태스크 및 이벤트 처리기에서 런타임에 사용할 수 있는 값이 저장됩니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../../integration-services/integration-services-ssis-variables.md)를 참조하세요.  
  
 기존 변수를 사용할 수 있는 읽기 전용으로 설정 하거나 읽기/쓰기 권한으로 사용자 지정 스크립트에서 변수의 쉼표로 구분 된 목록을 입력 하 여는 **ReadOnlyVariables** 및 **ReadWriteVariables** 필드에 **스크립트** 의 페이지는 **스크립트 변환 편집기**합니다. 변수 이름은 대/소문자를 구분합니다. 사용 하 여는 **값** 개별 변수를 읽고 속성입니다. 스크립트 구성 요소에서는 스크립트를 통해 런타임에 변수가 조작될 때 필요한 모든 잠금을 백그라운드에서 처리합니다.  
  
> [!IMPORTANT]  
>  컬렉션 **ReadWriteVariables** 는 에서만 사용할 수는 **PostExecute** 메서드 성능을 최대화 하 고 잠금 충돌의 위험을 최소화 합니다. 따라서 각 데이터 행을 처리할 때 패키지 변수의 값을 직접 증분시킬 수 없습니다. 대신 지역 변수의 값이 증가 하 고 패키지 변수의 값에 있는 지역 변수의 값으로 설정 된 **PostExecute** 메서드 후 모든 데이터를 처리 합니다. 이 항목의 뒷부분에 설명된 대로 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 속성을 사용하여 이 제한을 해결할 수도 있습니다. 그러나 각 행이 처리될 때 패키지 변수에 직접 값을 쓰면 성능이 저하되고 잠금 충돌의 위험이 높아집니다.  
  
 에 대 한 자세한 내용은 **스크립트** 의 페이지는 **스크립트 변환 편집기**, 참조 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) 및 [스크립트 변환 편집기 &#40; 스크립트 페이지 &#41; ](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
 스크립트 구성 요소를 만듭니다는 **변수** 의 컬렉션 클래스는 **ComponentWrapper** 속성 변수 자체와 동일한 이름에 있는 미리 구성 된 각 변수의 값에 대 한 강력한 형식의 접근자 속성을 가진 프로젝트 항목입니다. 이 컬렉션을 통해 노출 되는 **변수** 의 속성은 **ScriptMain** 클래스. 접근자 속성은 변수 값에 대한 읽기 전용 또는 읽기/쓰기 권한을 적절하게 제공합니다. 예를 들어, 라는 정수 변수를 추가한 경우 `MyIntegerVariable` 에 **ReadOnlyVariables** 목록에서 있습니다 수 해당 값을 검색 스크립트에 다음 코드를 사용 하 여:  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 `Me.VariableDispenser`를 호출하여 액세스할 수 있는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 속성을 사용하여 스크립트 구성 요소에서 변수를 사용할 수도 있습니다. 이 경우 변수에 대한 형식화되고 명명된 접근자 속성을 사용하지 않고 변수에 직접 액세스합니다. <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>를 사용하는 경우 개발자가 자신의 고유 코드에서 잠금 의미 체계와 변수 값에 대한 데이터 형식 캐스팅을 모두 처리해야 합니다. 디자인 타임에는 사용할 수 없지만 런타임에 프로그래밍 방식으로 만들어지는 변수를 사용하려면 명명되고 형식화된 접근자 속성 대신 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 속성을 사용해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services &#40; Ssis&#41; 변수](../../../integration-services/integration-services-ssis-variables.md)   
 [패키지에서 변수 사용](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  

