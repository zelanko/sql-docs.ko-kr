---
title: 사용자 지정 Foreach 열거자 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom foreach enumerators [Integration Services], creating
ms.assetid: 050e8455-2ed0-4b6d-b3ea-4e80e6c28487
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 49455bf9a5138d539a13ed241a24ab5d720c7f43
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58393981"
---
# <a name="creating-a-custom-foreach-enumerator"></a>사용자 지정 Foreach 열거자 만들기
  사용자 지정 foreach 열거자를 만드는 단계는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]의 다른 사용자 지정 개체를 만드는 단계와 비슷합니다.  
  
-   기본 클래스에서 상속되는 새 클래스를 만듭니다. foreach 열거자의 경우 기본 클래스는 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>입니다.  
  
-   개체 유형을 식별하는 특성을 클래스에 적용합니다. foreach 열거자의 경우 이 특성은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>입니다.  
  
-   기본 클래스의 메서드 및 속성 구현을 재정의합니다. foreach 열거자의 경우 가장 중요한 항목은 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 메서드입니다.  
  
-   필요한 경우 사용자 지정 사용자 인터페이스를 개발합니다. foreach 열거자의 경우 사용자 지정 사용자 인터페이스를 개발하려면 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSForEachEnumeratorUI> 인터페이스를 구현하는 클래스가 필요합니다.  
  
 사용자 지정 열거자는 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 컨테이너에 의해 호스팅됩니다. 런타임에 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> 컨테이너는 사용자 지정 열거자의 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 메서드를 호출합니다. 사용자 지정 열거자는 `IEnumerable`와 같이 `ArrayList` 인터페이스를 구현하는 개체를 반환합니다. 그런 다음 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>는 컬렉션의 각 요소를 반복하고, 사용자 정의 변수를 통해 현재 요소의 값을 제어 흐름에 제공하고, 컨테이너에서 제어 흐름을 실행합니다.  
  
## <a name="getting-started-with-a-custom-foreach-enumerator"></a>사용자 지정 ForEach 열거자 시작  
  
### <a name="creating-projects-and-classes"></a>프로젝트 및 클래스 만들기  
 관리되는 foreach 열거자는 모두 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator> 기본 클래스에서 파생되므로 사용자 지정 foreach 열거자를 만들려면 먼저 관리되는 프로그래밍 언어로 클래스 라이브러리 프로젝트를 만들고 기본 클래스에서 상속되는 클래스를 만들어야 합니다. 이 파생 클래스에서 기본 클래스의 메서드 및 속성을 재정의하여 사용자 지정 기능을 구현합니다.  
  
 동일한 솔루션에서 사용자 지정 사용자 인터페이스에 대한 두 번째 클래스 라이브러리 프로젝트를 만듭니다. 배포를 쉽게 하려면 사용자 인터페이스에 대한 별도의 어셈블리를 만드는 것이 좋습니다. 이렇게 하면 foreach 열거자 또는 해당 사용자 인터페이스를 독립적으로 업데이트하거나 다시 배포할 수 있기 때문입니다.  
  
 강력한 이름 키 파일을 사용하여 빌드 시 생성될 어셈블리에 서명하도록 두 프로젝트를 구성합니다.  
  
### <a name="applying-the-dtsforeachenumerator-attribute"></a>DtsForEachEnumerator 특성 적용  
 앞에서 만든 클래스에 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> 특성을 적용하여 해당 클래스를 foreach 열거자로 식별합니다. 이 특성은 foreach 열거자의 이름 및 설명 같은 디자인 타임 정보를 제공합니다. `Name` 속성에서 사용 가능한 열거자의 드롭다운 목록에 표시 됩니다는 **컬렉션** 탭의 **Foreach 루프 편집기** 대화 상자.  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute.UITypeName%2A> 속성을 사용하여 foreach 열거자를 사용자 지정 사용자 인터페이스에 연결합니다. 이 속성에 필요한 공개 키 토큰을 가져오려면 **sn.exe -t**를 사용하여 사용자 인터페이스 어셈블리 서명에 사용할 키 쌍(.snk) 파일의 공개 키 토큰을 표시할 수 있습니다.  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Namespace Microsoft.Samples.SqlServer.Dts  
    <DtsForEachEnumerator(DisplayName = "MyEnumerator", Description="A sample custom enumerator", UITypeName="FullyQualifiedTypeName,AssemblyName,Version=1.00.000.00,Culture=Neutral,PublicKeyToken=<publickeytoken>")> _   
    Public Class MyEnumerator  
     Inherits ForEachEnumerator  
        'Insert code here.  
    End Class  
End Namespace  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsForEachEnumerator( DisplayName = "MyEnumerator", Description="A sample custom enumerator", UITypeName="FullyQualifiedTypeName,AssemblyName,Version=1.00.000.00,Culture=Neutral,PublicKeyToken=<publickeytoken>")]  
    public class MyEnumerator : ForEachEnumerator  
    {  
        //Insert code here.  
    }  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-enumerator"></a>사용자 지정 열거자 빌드, 배포 및 디버깅  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 사용자 지정 foreach 열거자의 빌드, 배포 및 디버깅 단계는 다른 형식의 사용자 지정 개체에 대해 필요한 단계와 매우 비슷합니다. 자세한 내용은 [사용자 지정 개체 빌드, 배포 및 디버그](../building-deploying-and-debugging-custom-objects.md)를 참조하세요.  
  
![Integration Services 아이콘 (작은)](../../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 Foreach 열거자 코딩](coding-a-custom-foreach-enumerator.md)   
 [사용자 지정 ForEach 열거자의 사용자 인터페이스 개발](developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
  
  
