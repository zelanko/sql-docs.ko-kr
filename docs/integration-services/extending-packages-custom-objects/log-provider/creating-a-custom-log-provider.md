---
title: "사용자 지정 로그 공급자를 만드는 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom log providers [Integration Services], creating
ms.assetid: fc20af96-9eb8-4195-8d3f-8a4d7c753f24
caps.latest.revision: 58
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4e98f1b5a032353c27ffa1438eb7d01bd517892a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-custom-log-provider"></a>사용자 지정 로그 공급자 만들기
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 런타임 환경에는 광범위한 로깅 기능이 있습니다. 로그를 사용하면 패키지를 실행하는 동안 발생하는 이벤트를 캡처할 수 있습니다. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에는 XML, 텍스트, 데이터베이스, Windows 이벤트 로그 등의 다양한 형식으로 로그를 만들고 저장하는 데 사용할 수 있는 다양한 로그 공급자가 포함되어 있습니다. 이러한 공급자 또는 출력 형식이 요구 사항에 맞지 않을 경우에는 사용자 지정 로그 공급자를 만들 수 있습니다.  
  
 사용자 지정 로그 공급자를 만드는 단계는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]의 다른 사용자 지정 개체를 만드는 단계와 비슷합니다.  
  
-   기본 클래스에서 상속되는 새 클래스를 만듭니다. 로그 공급자의 경우 기본 클래스는 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>입니다.  
  
-   개체 유형을 식별하는 특성을 클래스에 적용합니다. 로그 공급자의 경우 이 특성은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>입니다.  
  
-   기본 클래스의 메서드 및 속성 구현을 재정의합니다. 로그 공급자의 경우 이러한 구현에는 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 속성과 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A> 메서드가 포함됩니다.  
  
-   사용자 지정 로그 공급자에 대 한 사용자 지정 사용자 인터페이스에서 구현 되지 않습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]합니다.  
  
## <a name="getting-started-with-a-custom-log-provider"></a>사용자 지정 로그 공급자 시작  
  
### <a name="creating-projects-and-classes"></a>프로젝트 및 클래스 만들기  
 관리되는 로그 공급자는 모두 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase> 기본 클래스에서 파생되므로 사용자 지정 로그 공급자를 만들려면 먼저 관리되는 프로그래밍 언어로 클래스 라이브러리 프로젝트를 만든 다음 기본 클래스에서 상속되는 클래스를 만들어야 합니다. 이 파생 클래스에서 기본 클래스의 메서드 및 속성을 재정의하여 사용자 지정 기능을 구현합니다.  
  
 생성할 어셈블리를 강력한 이름 키 파일을 사용하여 서명하도록 프로젝트를 구성합니다.  
  
> [!NOTE]  
>  많은 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 로그 공급자가 구현 하는 사용자 지정 사용자 인터페이스 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> 하 고 대체는 **구성** 텍스트 상자에 **SSIS 로그 구성** 사용 가능한 연결 관리자의 필터링 된 드롭다운 목록 사용 하 여 대화 상자. 그러나 사용자 지정 로그 공급자의 사용자 지정 사용자 인터페이스는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에 구현되어 있지 않습니다.  
  
### <a name="applying-the-dtslogprovider-attribute"></a>DtsLogProvider 특성 적용  
 앞에서 만든 클래스에 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 특성을 적용하여 해당 클래스를 로그 공급자로 식별합니다. 이 특성은 로그 공급자의 이름 및 설명 같은 디자인 타임 정보를 제공합니다. **DisplayName** 및 **설명** 특성의 속성에 해당 하는 **이름** 및 **설명** 에 표시 된 열은 **SSIS 로그 구성** 편집기에서 패키지에 대 한 로깅을 구성할 때 표시 되는 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]합니다.  
  
> [!IMPORTANT]  
>  이 특성의 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.LogProviderType%2A> 속성은 사용되지 않습니다. 그러나 이 속성을 설정하지 않으면 사용 가능한 로그 공급자 목록에 해당 사용자 지정 로그 공급자가 표시되지 않으므로 이 속성 값을 반드시 입력해야 합니다.  
  
> [!NOTE]  
>  사용자 지정 로그 공급자의 사용자 지정 사용자 인터페이스는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에 구현되어 있지 않으므로 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A>의 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 속성에 값을 지정해도 아무 영향이 없습니다.  
  
```vb  
<DtsLogProvider(DisplayName:="MyLogProvider", Description:="A simple log provider.", LogProviderType:="Custom")> _  
Public Class MyLogProvider  
     Inherits LogProviderBase  
    ' TODO: Override the base class methods.  
End Class  
```  
  
```csharp  
[DtsLogProvider(DisplayName="MyLogProvider", Description="A simple log provider.", LogProviderType="Custom")]  
public class MyLogProvider : LogProviderBase  
{  
    // TODO: Override the base class methods.  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-log-provider"></a>사용자 지정 로그 공급자 빌드, 배포 및 디버깅  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 사용자 지정 로그 공급자의 빌드, 배포 및 디버깅 단계는 다른 형식의 사용자 지정 개체에 대해 필요한 단계와 매우 비슷합니다. 자세한 내용은 참조 [건물, Deploying, and Debugging Custom Objects](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [사용자 지정 로그 공급자 코딩](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)   
 [사용자 지정 로그 공급자에 대 한 사용자 인터페이스 개발](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-user-interface-for-a-custom-log-provider.md)  
  
  

