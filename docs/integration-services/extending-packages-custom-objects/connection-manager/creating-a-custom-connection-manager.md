---
title: 사용자 지정 연결 관리자 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom connection managers [Integration Services], creating
ms.assetid: e83f8e02-ace4-42e0-b979-2f6be1460985
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e6015aa5f7d9271c71a534fab6126cba9a8dcbf
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297281"
---
# <a name="creating-a-custom-connection-manager"></a>사용자 지정 연결 관리자 만들기

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  사용자 지정 연결 관리자를 만들 때 수행해야 하는 단계는 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]의 다른 사용자 지정 개체를 만들 때의 단계와 비슷합니다.  
  
-   기본 클래스에서 상속되는 새 클래스를 만듭니다. 연결 관리자의 경우 기본 클래스는 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>입니다.  
  
-   개체 유형을 식별하는 특성을 클래스에 적용합니다. 연결 관리자의 경우 이 특성은 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>입니다.  
  
-   기본 클래스의 메서드 및 속성 구현을 재정의합니다. 연결 관리자의 경우 이러한 구현에는 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> 속성과 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A> 메서드가 포함됩니다.  
  
-   필요한 경우 사용자 지정 사용자 인터페이스를 개발합니다. 연결 관리자의 경우 사용자 지정 사용자 인터페이스를 개발하려면 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI> 인터페이스를 구현하는 클래스가 필요합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에 기본 제공된 대부분의 태스크, 원본 및 대상은 특정 유형의 기본 제공 연결 관리자와만 사용할 수 있습니다. 따라서 이러한 예제를 기본 제공 태스크 및 구성 요소와 함께 테스트할 수 없습니다.  
  
## <a name="getting-started-with-a-custom-connection-manager"></a>사용자 지정 연결 관리자 시작  
  
### <a name="creating-projects-and-classes"></a>프로젝트 및 클래스 만들기  
 관리되는 연결 관리자는 모두 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase> 기본 클래스에서 파생되므로 사용자 지정 연결 관리자를 만들려면 먼저 관리되는 프로그래밍 언어로 클래스 라이브러리 프로젝트를 만들고 기본 클래스에서 상속되는 클래스를 만들어야 합니다. 이 파생 클래스에서 기본 클래스의 메서드 및 속성을 재정의하여 사용자 지정 기능을 구현합니다.  
  
 동일한 솔루션에서 사용자 지정 사용자 인터페이스에 대한 두 번째 클래스 라이브러리 프로젝트를 만듭니다. 배포를 쉽게 하려면 사용자 인터페이스에 대한 별도의 어셈블리를 만드는 것이 좋습니다. 이렇게 하면 연결 관리자 또는 해당 사용자 인터페이스를 독립적으로 업데이트하거나 다시 배포할 수 있기 때문입니다.  
  
 강력한 이름 키 파일을 사용하여 빌드 시 생성될 어셈블리에 서명하도록 두 프로젝트를 구성합니다.  
  
### <a name="applying-the-dtsconnection-attribute"></a>DtsConnection 특성 적용  
 앞에서 만든 클래스에 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> 특성을 적용하여 해당 클래스를 연결 관리자로 식별합니다. 이 특성은 연결 관리자의 이름, 설명 및 연결 유형 같은 디자인 타임 정보를 제공합니다. <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute.ConnectionType%2A> 및 **Description** 속성은 **에서 패키지에 대한 연결을 구성할 때** SSIS 연결 관리자 추가**대화 상자에 표시되는**유형**및**설명[!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 열에 해당합니다.  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute.UITypeName%2A> 속성을 사용하여 연결 관리자를 사용자 지정 사용자 인터페이스에 연결합니다. 이 속성에 필요한 공개 키 토큰을 가져오려면 **sn.exe -t**를 사용하여 사용자 인터페이스 어셈블리 서명에 사용할 키 쌍(.snk) 파일의 공개 키 토큰을 표시할 수 있습니다.  
  
```vb  
<DtsConnection(ConnectionType:="SQLVB", _  
  DisplayName:="SqlConnectionManager (VB)", _  
  Description:="Connection manager for Sql Server", _  
  UITypeName:="SqlConnMgrUIVB.SqlConnMgrUIVB,SqlConnMgrUIVB,Version=1.0.0.0,Culture=neutral,PublicKeyToken=<insert public key token here>")> _  
Public Class SqlConnMgrVB  
  Inherits ConnectionManagerBase  
  . . .  
End Class  
```  
  
```csharp  
[DtsConnection(ConnectionType = "SQLCS",  
  DisplayName = "SqlConnectionManager (CS)",  
  Description = "Connection manager for Sql Server",  
  UITypeName = "SqlConnMgrUICS.SqlConnMgrUICS,SqlConnMgrUICS,Version=1.0.0.0,Culture=neutral,PublicKeyToken=<insert public key token here>")]  
public class SqlConnMgrCS :  
ConnectionManagerBase  
{  
  . . .  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-connection-manager"></a>사용자 지정 연결 관리자 빌드, 배포 및 디버깅  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 사용자 지정 연결 관리자의 빌드, 배포 및 디버깅 단계는 다른 형식의 사용자 지정 개체에 대한 단계와 비슷합니다. 자세한 내용은 [사용자 지정 개체 빌드, 배포 및 디버그](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)를 참조하세요.    
  
## <a name="see-also"></a>참고 항목  
 [사용자 지정 연결 관리자 코딩](../../../integration-services/extending-packages-custom-objects/connection-manager/coding-a-custom-connection-manager.md)   
 [사용자 지정 연결 관리자의 사용자 인터페이스 개발](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-user-interface-for-a-custom-connection-manager.md)  
  
  
