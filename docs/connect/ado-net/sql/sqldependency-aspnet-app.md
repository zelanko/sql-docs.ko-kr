---
title: ASP.NET 애플리케이션의 SqlDependency
description: ASP.NET 응용 프로그램에서 쿼리 알림을 사용 하는 방법을 보여 줍니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 2115d087d837118b99ee3ffded9cae0003b6d4e0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451968"
---
# <a name="sqldependency-in-an-aspnet-application"></a>ASP.NET 애플리케이션의 SqlDependency

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

이 단원의 예제에서는 ASP.NET <xref:System.Web.Caching.SqlCacheDependency> 개체를 활용 하 여 <xref:Microsoft.Data.SqlClient.SqlDependency>를 간접적으로 사용 하는 방법을 보여 줍니다. @No__t_0 개체는 <xref:Microsoft.Data.SqlClient.SqlDependency>를 사용 하 여 알림을 수신 하 고 캐시를 올바르게 업데이트 합니다.  
  
> [!NOTE]
>  이 샘플 코드에서는 [쿼리 알림을 사용 하도록 설정](enable-query-notifications.md)하는 스크립트를 실행 하 여 쿼리 알림을 사용 하도록 설정 했다고 가정 합니다.  
  
## <a name="about-the-sample-application"></a>예제 응용 프로그램 정보  
애플리케이션 예제에서는 단일 ASP.NET 웹 페이지를 사용하여 **AdventureWorks** SQL Server 데이터베이스의 제품 정보를 <xref:System.Web.UI.WebControls.GridView> 컨트롤에 표시합니다. 페이지가 로드 되 면 코드는 <xref:System.Web.UI.WebControls.Label> 컨트롤에 현재 시간을 씁니다. 그런 다음 <xref:System.Web.Caching.SqlCacheDependency> 개체를 정의하고 최대 3분 동안 캐시 데이터를 저장하도록 <xref:System.Web.Caching.Cache> 개체의 속성을 설정합니다. 그런 다음 코드는 데이터베이스에 연결 하 고 데이터를 검색 합니다. 페이지가 로드 되 고 응용 프로그램이 실행 되는 경우 ASP.NET는 캐시에서 데이터를 검색 하며,이는 페이지의 시간이 변경 되지 않는다는 것을 확인 하 여 확인할 수 있습니다. 모니터링 되는 데이터가 변경 되 면 ASP.NET은 캐시를 무효화 하 고 `GridView` 컨트롤을 새 데이터로 다시 채우기 `Label` 컨트롤에 표시 되는 시간을 업데이트 합니다.  
  
## <a name="creating-the-sample-application"></a>애플리케이션 예제 만들기  
예제 응용 프로그램을 만들고 실행 하려면 다음 단계를 수행 합니다.  
  
1. 새 ASP.NET 웹 사이트 만들기  
  
2. Default.aspx 페이지에 <xref:System.Web.UI.WebControls.Label> 및 <xref:System.Web.UI.WebControls.GridView> 컨트롤을 추가 합니다.  
  
3. 페이지의 클래스 모듈을 열고 다음 지시문을 추가 합니다.  
  
    ```csharp  
    using Microsoft.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4. 페이지의 `Page_Load` 이벤트에 다음 코드를 추가 합니다.  
  
    [!code-csharp[DataWorks SqlDependency_Start#1](~/../sqlclient/doc/samples/SqlDependency_Start.cs#1)]
  
5. @No__t_0 및 `GetSQL` 라는 두 개의 도우미 메서드를 추가 합니다. 정의된 연결 문자열은 통합 보안을 사용합니다. 사용 중인 계정에 필요한 데이터베이스 권한이 있는지, 그리고 **AdventureWorks** 샘플 데이터베이스에서 알림을 사용했는지를 확인해야 합니다.
  
    [!code-csharp[DataWorks SqlDependency_Start#2](~/../sqlclient/doc/samples/SqlDependency_Start.cs#2)]
  
### <a name="testing-the-application"></a>애플리케이션 테스트  
응용 프로그램은 Web form에 표시 된 데이터를 캐시 하 고 활동이 없으면 3 분 마다 새로 고칩니다. 데이터베이스가 변경되면 즉시 캐시를 새로 고칩니다. Visual Studio에서 응용 프로그램을 실행 합니다. 그러면 페이지가 브라우저에 로드 됩니다. 표시 된 캐시 새로 고침 시간은 캐시를 마지막으로 새로 고친 시간을 나타냅니다. 3 분 기다렸다가 페이지를 새로 고쳐 다시 게시 이벤트를 발생 시킵니다. 페이지에 표시 된 시간이 변경 되었습니다. 3 분 이내에 페이지를 새로 고치면 페이지에 표시 되는 시간이 동일 하 게 유지 됩니다.  
  
이제 Transact-sql UPDATE 명령을 사용 하 여 데이터베이스의 데이터를 업데이트 하 고 페이지를 새로 고칩니다. 이제 표시 된 시간은 캐시가 데이터베이스의 새 데이터로 새로 고쳐진 것을 나타냅니다. 캐시를 업데이트 하는 경우에도 페이지에 표시 되는 시간은 포스트백 이벤트가 발생할 때까지 변경 되지 않습니다.  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server의 쿼리 알림](query-notifications-sql-server.md)
