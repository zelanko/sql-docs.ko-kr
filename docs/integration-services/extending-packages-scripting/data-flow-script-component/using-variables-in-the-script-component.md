---
title: 스크립트 구성 요소에서 변수 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c267518f15bb87dddfd1139e80c3c7922bdf37c1
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58278062"
---
# <a name="using-variables-in-the-script-component"></a>스크립트 구성 요소에서 변수 사용
  변수에는 패키지와 해당 컨테이너, 태스크 및 이벤트 처리기에서 런타임에 사용할 수 있는 값이 저장됩니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../../integration-services/integration-services-ssis-variables.md)을 참조하세요.  
  
 **스크립트 변환 편집기**의 **스크립트** 페이지에 있는 **ReadOnlyVariables** 및 **ReadWriteVariables** 필드에 쉼표로 구분된 변수 목록을 입력하여 사용자 지정 스크립트에서 기존 변수를 읽기 전용 또는 읽기/쓰기 권한으로 액세스할 수 있게 할 수 있습니다. 변수 이름은 대/소문자를 구분합니다. 개별 변수를 읽고 쓰는 데는 **Value** 속성을 사용합니다. 스크립트 구성 요소에서는 스크립트를 통해 런타임에 변수가 조작될 때 필요한 모든 잠금을 백그라운드에서 처리합니다.  
  
> [!IMPORTANT]  
>  **ReadWriteVariables**의 컬렉션은 **PostExecute** 메서드에서 성능을 최대화하고 잠금 충돌의 위험을 최소화하는 데만 사용할 수 있습니다. 따라서 각 데이터 행을 처리할 때 패키지 변수의 값을 직접 증분시킬 수 없습니다. 대신 지역 변수의 값을 증분시키고 모든 데이터가 처리된 후에 **PostExecute** 메서드에서 패키지 변수의 값을 지역 변수 값으로 설정합니다. 이 항목의 뒷부분에 설명된 대로 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 속성을 사용하여 이 제한을 해결할 수도 있습니다. 그러나 각 행이 처리될 때 패키지 변수에 직접 값을 쓰면 성능이 저하되고 잠금 충돌의 위험이 높아집니다.  
  
 **스크립트 변환 편집기**의 **스크립트** 페이지에 대한 자세한 내용은 [스크립트 구성 요소 편집기에서 스크립트 구성 요소 구성](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) 및 [스크립트 변환 편집기&#40;스크립트 페이지&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md)를 참조하세요.  
  
 스크립트 구성 요소에서는 미리 구성된 각 변수의 값에 대한 강력한 형식의 접근자 속성이 있는 **Variables** 컬렉션 클래스를 **ComponentWrapper** 프로젝트 항목에 만듭니다. 이때 접근자 속성 이름은 변수 이름과 동일합니다. 이 컬렉션은 **ScriptMain** 클래스의 **Variables** 속성을 통해 제공됩니다. 접근자 속성은 변수 값에 대한 읽기 전용 또는 읽기/쓰기 권한을 적절하게 제공합니다. 예를 들어 **ReadOnlyVariables** 목록에 `MyIntegerVariable`이라는 정수 변수를 추가한 경우 스크립트에서 다음 코드를 사용하여 해당 값을 검색할 수 있습니다.  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 `Me.VariableDispenser`를 호출하여 액세스할 수 있는 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 속성을 사용하여 스크립트 구성 요소에서 변수를 사용할 수도 있습니다. 이 경우 변수에 대한 형식화되고 명명된 접근자 속성을 사용하지 않고 변수에 직접 액세스합니다. <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>를 사용하는 경우 개발자가 자신의 고유 코드에서 잠금 의미 체계와 변수 값에 대한 데이터 형식 캐스팅을 모두 처리해야 합니다. 디자인 타임에는 사용할 수 없지만 런타임에 프로그래밍 방식으로 만들어지는 변수를 사용하려면 명명되고 형식화된 접근자 속성 대신 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> 속성을 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 변수](../../../integration-services/integration-services-ssis-variables.md)   
 [패키지에서 변수 사용](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
