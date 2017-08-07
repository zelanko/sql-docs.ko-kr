---
title: "복제 관리 개체 개념 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
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
- replication [SQL Server], RMO
- programming interfaces [SQL Server replication]
- replication [SQL Server], how-to topics
- RMO [SQL Server]
- Replication Management Objects
- programming [SQL Server replication], RMO
ms.assetid: 37476d50-fb47-49e3-9504-3b163ac381d8
caps.latest.revision: 61
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e940ba8880aa2d1c4e4677c779b6984b2e6d4dde
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="replication-management-objects-concepts"></a>Replication Management Objects Concepts
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  RMO(복제 관리 개체)는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 복제 기능을 캡슐화하는 관리 코드 어셈블리로, <xref:Microsoft.SqlServer.Replication> 네임스페이스를 통해 구현됩니다.  
  
 다음 섹션의 항목에서는 RMO를 사용하여 복제 태스크를 프로그래밍 방식으로 제어하는 방법에 대해 설명합니다.  
  
 [배포 구성](../../../relational-databases/replication/configure-distribution.md)  
 이 섹션의 항목에서는 RMO를 사용하여 게시 및 배포를 구성하는 방법을 보여 줍니다.  
  
 [게시 및 아티클 만들기, 수정 및 삭제&#40;복제&#41;](../../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md)  
 이 섹션의 항목에서는 RMO를 사용하여 게시 및 아티클을 작성, 삭제 및 수정하는 방법을 보여 줍니다.  
  
 [게시 구독](../../../relational-databases/replication/subscribe-to-publications.md)  
 이 섹션의 항목에서는 RMO를 사용하여 구독을 작성, 삭제 및 수정하는 방법을 보여 줍니다.  
  
 [복제 토폴로지 보안 설정](../../../relational-databases/replication/security/secure-a-replication-topology.md)  
 이 섹션의 항목에서는 RMO를 사용하여 보안 설정을 보고 수정하는 방법을 보여 줍니다.  
  
 [구독 동기화&#40;복제&#41;](../../../relational-databases/replication/synchronize-subscriptions-replication.md)  
 이 섹션의 항목에서는 구독을 동기화하는 방법을 보여 줍니다.  
  
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
 이 섹션의 항목에서는 프로그래밍 방식으로 복제 토폴로지를 모니터링하는 방법을 보여 줍니다.  
  
## <a name="introduction-to-rmo-programming"></a>RMO 프로그래밍 소개  
 RMO는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제의 모든 측면을 프로그래밍하기 위해 디자인되었습니다. RMO 네임스페이스는 <xref:Microsoft.SqlServer.Replication>이며 이 네임스페이스는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 어셈블리인 Microsoft.SqlServer.Rmo.dll을 통해 구현됩니다. <xref:Microsoft.SqlServer.Replication> 네임스페이스에 속하는 Microsoft.SqlServer.Replication.dll 어셈블리는 다양한 복제 에이전트(스냅숏 에이전트, 배포 에이전트 및 병합 에이전트)를 프로그래밍하는 데 필요한 관리되는 코드 인터페이스를 구현합니다. 이 어셈블리의 클래스는 RMO에서 액세스하여 구독을 동기화하는 데 사용될 수 있습니다. Microsoft.SqlServer.Replication.BusinessLogicSupport.dll 어셈블리를 통해 구현되는 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 네임스페이스의 클래스는 병합 복제에 대한 사용자 지정 비즈니스 논리를 만드는 데 사용됩니다. 이 어셈블리는 RMO에 종속되지 않습니다.  
  
## <a name="deploying-applications-based-on-rmo"></a>RMO를 기초로 응용 프로그램 배포  
 RMO는 SQL Server Compact를 제외한 모든 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 포함된 복제 구성 요소와 클라이언트 연결 구성 요소를 필요로 하기 때문에 RMO를 기초로 응용 프로그램을 배포하려면 복제 구성 요소와 클라이언트 연결 구성 요소가 포함된 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전을 응용 프로그램을 실행할 컴퓨터에 설치해야 합니다.  
  
## <a name="getting-started-with-rmo"></a>RMO 시작  
 이 섹션에서는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio를 사용하여 간단한 RMO 프로젝트를 시작하는 방법에 대해 설명합니다.  
  
#### <a name="to-create-a-new-microsoft-visual-c-project"></a>새 Microsoft Visual C# 프로젝트를 만들려면  
  
1.  Visual Studio를 시작합니다.  
  
2.  **파일** 메뉴에서 **새 프로젝트**를 클릭합니다. **새 프로젝트** 대화 상자가 나타납니다.  
  
3.  **프로젝트 형식** 대화 상자에서 **Visual C# 프로젝트**를 선택합니다. **템플릿** 창에서 **Windows 응용 프로그램**을 선택합니다.  
  
4.  (옵션) **이름**에 새 응용 프로그램의 이름을 입력합니다.  
  
5.  **확인**을 클릭하여 Visual C# Windows 템플릿을 로드합니다.  
  
6.  **프로젝트** 메뉴에서 **참조 추가** 항목을 선택합니다. **참조 추가** 대화 상자가 나타납니다.  
  
7.  **.NET** 탭의 목록에서 다음과 같은 어셈블리를 선택한 후 **확인**을 클릭합니다.  
  
    -   Microsoft.SqlServer.Replication .NET Programming Interface  
  
    -   Microsoft.SqlServer.ConnectionInfo  
  
    -   Replication Agent Library  
  
    > [!NOTE]  
    >  둘 이상의 파일을 선택하려면 Ctrl 키를 사용합니다.  
  
8.  (옵션) 6단계를 반복합니다. **찾아보기** 탭을 클릭하고 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM으로 이동한 다음 Microsoft.SqlServer.Replication.BusinessLogicSupport.dll을 선택하고 **확인**을 클릭합니다.  
  
9. **보기** 메뉴에서 **코드**를 클릭합니다.  
  
10. 코드에서 RMO 네임스페이스의 형식을 한정하기 위해 네임스페이스 문 앞에 다음 **using** 문을 입력합니다.  
  
    ```  
    // These namespaces are required.  
    using Microsoft.SqlServer.Replication;  
    using Microsoft.SqlServer.Management.Common;  
    // This namespace is only used when creating custom business  
    // logic for merge replication.  
    using Microsoft.SqlServer.Replication.BusinessLogicSupport;   
    ```  
  
#### <a name="to-create-a-new-microsoft-visual-basic-net-project"></a>새 Microsoft Visual Basic .NET 프로젝트를 만들려면  
  
1.  Visual Studio를 시작합니다.  
  
2.  **파일** 메뉴에서 **새 프로젝트**를 선택합니다. **새 프로젝트** 대화 상자가 나타납니다.  
  
3.  프로젝트 형식 창에서 **Visual Basic**을 선택합니다. 템플릿 창에서 **Windows 응용 프로그램**을 선택합니다.  
  
4.  (옵션) **이름** 상자에 새 응용 프로그램의 이름을 입력합니다.  
  
5.  **확인**을 클릭하여 Visual Basic Windows 템플릿을 로드합니다.  
  
6.  **프로젝트** 메뉴에서 **참조 추가**를 선택합니다. **참조 추가** 대화 상자가 나타납니다.  
  
7.  **.NET** 탭의 목록에서 다음과 같은 어셈블리를 선택한 후 **확인**을 클릭합니다.  
  
    -   Microsoft.SqlServer.Replication .NET Programming Interface  
  
    -   Microsoft.SqlServer.ConnectionInfo  
  
    -   Replication Agent Library  
  
    > [!NOTE]  
    >  둘 이상의 파일을 선택하려면 Ctrl 키를 사용합니다.  
  
8.  (옵션) 6단계를 반복합니다. **찾아보기** 탭을 클릭하고 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM으로 이동한 다음 Microsoft.SqlServer.Replication.BusinessLogicSupport.dll을 선택하고 **확인**을 클릭합니다.  
  
9. **보기** 메뉴에서 **코드**를 클릭합니다.  
  
10. 코드에서 다른 모든 선언 앞에 다음 **Imports** 문을 입력하여 RMO 네임스페이스의 형식을 한정합니다.  
  
    ```  
    ' These namespaces are required.  
    Imports Microsoft.SqlServer.Replication  
    Imports Microsoft.SqlServer.Management.Common  
    ' This namespace is only used when creating custom business  
    ' logic for merge replication.  
    Imports Microsoft.SqlServer.Replication.BusinessLogicSupport   
    ```  
  
## <a name="connecting-to-a-replication-server"></a>복제 서버에 연결  
 RMO 프로그래밍 개체의 경우 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스의 인스턴스를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 인스턴스에 연결해야 합니다. 이 서버 연결은 RMO 프로그래밍 개체와는 독립적으로 이루어집니다. 그런 다음에는 인스턴스 생성 중에 또는 개체의 `P:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContex`t 속성을 할당하여 연결을 RMO 개체로 전달합니다. 이런 식으로 RMO 프로그래밍 개체와 연결 개체 인스턴스를 별도로 만들고 관리할 수 있으며 여러 RMO 프로그래밍 개체에서 단일 연결 개체를 다시 사용할 수 있습니다. 복제 서버에 대한 연결에는 다음 규칙이 적용됩니다.  
  
-   지정된 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체에 대해 모든 연결 속성을 정의합니다.  
  
-   각 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결에 고유한 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체가 있어야 합니다.  
  
-   <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체는 서버에서 생성되거나 액세스되는 RMO 프로그래밍 개체의 `P:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext` 속성에 할당합니다.  
  
-   <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> 메서드는 서버에 대한 연결을 엽니다. 이 메서드는 서버에 액세스하는 다른 모든 메서드를 호출하기 전에 해당 연결을 사용하는 RMO 프로그래밍 개체에 대해 호출해야 합니다.  
  
-   RMO 및 SMO([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects) 모두 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 연결하기 때문에 RMO와 SMO 개체 모두가 동일한 연결을 사용할 수 있습니다. 자세한 내용은 [SQL Server 인스턴스에 연결](../../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)을 참조하세요.  
  
-   서버에 연결하고 성공적으로 로그인하기 위해 모든 인증 정보를 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체에 제공합니다.  
  
-   Windows 인증이 기본값입니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인증을 사용하려면 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.LoginSecure%2A>를 **false**로 설정하고 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Login%2A> 및 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Password%2A>를 유효한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그온 및 암호로 설정해야 합니다. 보안 자격 증명은 항상 안전하게 저장 및 처리되어야 하고 가능하면 런타임에 제공해야 합니다.  
  
-   다중 스레드 응용 프로그램의 경우 각 스레드에서 별도의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 사용해야 합니다.  
  
 RMO 개체에서 사용하는 활성 서버 연결을 닫으려면 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> 개체에 대해 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 메서드를 호출합니다.  
  
## <a name="setting-rmo-properties"></a>RMO 속성 설정  
 RMO 프로그래밍 개체의 속성은 서버에 있는 이러한 복제 개체의 속성을 나타냅니다. 서버에서 새 복제 개체를 만들 경우 이러한 개체는 RMO 속성을 사용하여 정의됩니다. 기존 개체의 경우 RMO 속성은 기존 개체의 속성을 나타내며, 이러한 속성은 쓰기 또는 설정 가능한 속성에 한해서만 수정할 수 있습니다. 새 개체나 기존 개체에 대해 속성을 설정할 수 있습니다.  
  
### <a name="setting-properties-for-new-replication-objects"></a>새 복제 개체의 속성 설정  
 서버에서 새 복제 개체를 만들 경우 개체의 **Create** 메서드를 호출하기 전에 모든 필수 속성을 지정해야 합니다. 새 복제 개체의 속성을 설정하는 방법은 [게시 및 배포 구성](../../../relational-databases/replication/configure-publishing-and-distribution.md)을 참조하세요.  
  
### <a name="setting-properties-for-existing-replication-objects"></a>기존 복제 개체의 속성 설정  
 서버에 있는 기존 복제 개체의 경우 개체에 따라 RMO에서 해당 개체의 속성 전체 또는 일부의 변경을 지원하는지 여부가 달라집니다. 쓰기 또는 설정 가능한 속성만 변경 가능합니다. 속성을 변경하려면 먼저 **Load** 또는 `M:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties` 메서드를 호출하여 서버에서 현재 속성을 가져와야 합니다. 이러한 메서드 호출은 기존 개체가 수정됨을 나타냅니다.  
  
 기본적으로 RMO는 개체 속성을 변경할 때 현재 사용 중인 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>의 실행 모드에 따라 변경 내용을 서버에 커밋합니다. `P:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject` 메서드를 사용하면 개체의 속성을 검색하거나 변경하기 전에 해당 개체가 서버에 있는지 여부를 확인할 수 있습니다. 복제 개체의 속성을 변경하는 방법은 [배포자 및 게시자 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
> [!NOTE]  
>  여러 RMO 클라이언트 또는 RMO 프로그래밍 개체의 여러 인스턴스가 서버에 있는 동일한 복제 개체에 액세스할 경우 RMO 개체의 **Refresh** 메서드를 호출하면 서버에 있는 개체의 현재 상태에 따라 속성을 업데이트할 수 있습니다.  
  
### <a name="caching-property-changes"></a>속성 변경 내용 캐시  
 <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> 속성을 <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes.CaptureSql>로 설정하면 RMO에서 생성한 모든 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문이 캡처됩니다. 이 경우 실행 메서드 중 하나를 사용하여 하나의 일괄 처리에서 문을 수동으로 실행할 수 있습니다. RMO를 사용하면 속성 변경 내용을 캐시한 후 개체의 `M:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges` 메서드를 사용하여 하나의 일괄 처리에서 한 번에 커밋할 수 있습니다. 속성 변경 내용을 캐시하려면 개체의 `P:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges` 속성을 **true**로 설정해야 합니다. RMO의 속성 변경 내용을 캐시하는 경우에도 변경 내용이 서버에 전송되는 시점은 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체에 의해 제어됩니다. 복제 개체의 속성 변경 내용을 캐시하는 방법은 [배포자 및 게시자 속성 보기 및 수정](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  속성을 설정할 때 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 트랜잭션을 명시적으로 선언할 수 있지만 이러한 트랜잭션은 내부 복제 트랜잭션을 방해하여 예기치 않은 결과를 초래할 수 있기 때문에 RMO와 함께 사용하지 않는 것이 좋습니다.  
  
## <a name="example"></a>예제  
 이 예에서는 속성 변경 내용을 캐시하는 방법을 보여 줍니다. 여기서 트랜잭션 게시의 특성에 대한 변경 내용은 서버에 명시적으로 전송되기 전까지 캐시됩니다.  
  
 [!code-cs[HowTo#rmo_ChangeTranPub_cached](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changetranpub_cached)]  
  
## <a name="see-also"></a>참고 항목  
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [복제 프로그래밍 개념](../../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  
  
