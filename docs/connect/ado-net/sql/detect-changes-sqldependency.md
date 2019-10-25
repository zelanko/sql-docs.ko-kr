---
title: SqlDependency로 변경 내용 감지
description: 쿼리 결과가 원래 수신 된 결과와 다를 때를 검색 하는 방법을 보여 줍니다.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: e6a58316-f005-4477-92e1-45cc2eb8c5b4
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 2d2c4c48a9085fa83d6104233be5f2e1c6b11318
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452241"
---
# <a name="detecting-changes-with-sqldependency"></a>SqlDependency로 변경 내용 감지

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

쿼리 결과가 원래 검색 된 결과와 다를 때를 감지 하기 위해 <xref:Microsoft.Data.SqlClient.SqlDependency> 개체를 <xref:Microsoft.Data.SqlClient.SqlCommand>에 연결할 수 있습니다. 연결 된 명령의 결과가 변경 될 때 발생 하는 `OnChange` 이벤트에 대리자를 할당할 수도 있습니다. 명령을 실행 하기 전에 <xref:Microsoft.Data.SqlClient.SqlDependency>를 명령과 연결 해야 합니다. @No__t_1의 `HasChanges` 속성을 사용 하 여 데이터를 처음 검색 한 이후 쿼리 결과가 변경 되었는지 여부를 확인할 수도 있습니다.

## <a name="security-considerations"></a>보안 고려 사항

종속성 인프라는 지정 된 명령에 대 한 기본 데이터가 변경 되었다는 알림을 받기 위해 <xref:Microsoft.Data.SqlClient.SqlDependency.Start%2A> 호출 될 때 열리는 <xref:Microsoft.Data.SqlClient.SqlConnection>에 의존 합니다. 클라이언트에서 `SqlDependency.Start`에 대 한 호출을 시작 하는 기능은 <xref:Microsoft.Data.SqlClient.SqlClientPermission> 및 코드 액세스 보안 특성을 사용 하 여 제어 됩니다. 자세한 내용은 [쿼리 알림 사용](enable-query-notifications.md)을 참조 하세요.

### <a name="example"></a>예제

다음 단계에서는 종속성을 선언 하 고, 명령을 실행 하 고, 결과 집합이 변경 될 때 알림을 수신 하는 방법을 보여 줍니다.

1. 서버에 대한 `SqlDependency` 연결을 개시합니다.

2. 서버에 연결 하 고 Transact-sql 문을 정의 하는 <xref:Microsoft.Data.SqlClient.SqlConnection> 및 <xref:Microsoft.Data.SqlClient.SqlCommand> 개체를 만듭니다.

3. 새 `SqlDependency` 개체를 만들거나 기존 개체를 사용 하 여 `SqlCommand` 개체에 바인딩합니다. 내부적으로는 <xref:Microsoft.Data.Sql.SqlNotificationRequest> 개체를 만들고 필요에 따라 명령 개체에 바인딩합니다. 이 알림 요청에는이 `SqlDependency` 개체를 고유 하 게 식별 하는 내부 식별자가 포함 됩니다. 또한 아직 활성 상태가 아닌 경우 클라이언트 수신기를 시작 합니다.

4. @No__t_1 개체의 `OnChange` 이벤트에 이벤트 처리기를 구독 합니다.

5. @No__t_1 개체의 `Execute` 메서드 중 하나를 사용 하 여 명령을 실행 합니다. 명령이 알림 개체에 바인딩되기 때문에 서버에서는 알림을 생성해야 하는 것으로 인식하며 큐 정보는 종속성 큐를 가리킵니다.

6. 서버에 대 한 `SqlDependency` 연결을 중지 합니다.

이후에 사용자가 기본 데이터를 변경 하는 경우 Microsoft SQL Server는 이러한 변경에 대해 보류 중인 알림이 있음을 감지 하 고,에서 생성 된 기본 `SqlConnection`를 통해 처리 되어 클라이언트에 전달 되는 알림을 게시 합니다. `SqlDependency.Start`를 호출 합니다. 클라이언트 수신기는 무효화 메시지를 수신 합니다. 그런 다음 클라이언트 수신기는 연결 된 `SqlDependency` 개체를 찾고 `OnChange` 이벤트를 발생 시킵니다.

다음 코드 조각에서는 샘플 응용 프로그램을 만드는 데 사용 하는 디자인 패턴을 보여 줍니다.

```csharp
void Initialization()
{
    // Create a dependency connection.
    SqlDependency.Start(connectionString, queueName);
}

void SomeMethod()
{
    // Assume connection is an open SqlConnection.

    // Create a new SqlCommand object.
    using (SqlCommand command=new SqlCommand(
        "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers",
        connection))
    {

        // Create a dependency and associate it with the SqlCommand.
        SqlDependency dependency=new SqlDependency(command);
        // Maintain the reference in a class member.

        // Subscribe to the SqlDependency event.
        dependency.OnChange+=new
           OnChangeEventHandler(OnDependencyChange);

        // Execute the command.
        using (SqlDataReader reader = command.ExecuteReader())
        {
            // Process the DataReader.
        }
    }
}

// Handler method
void OnDependencyChange(object sender,
   SqlNotificationEventArgs e )
{
  // Handle the event (for example, invalidate this cache entry).
}

void Termination()
{
    // Release the dependency.
    SqlDependency.Stop(connectionString, queueName);
}
```

## <a name="next-steps"></a>다음 단계
- [SQL Server의 쿼리 알림](query-notifications-sql-server.md)
