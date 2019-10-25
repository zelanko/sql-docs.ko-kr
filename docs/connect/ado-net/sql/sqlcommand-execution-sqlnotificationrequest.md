---
title: SqlNotificationRequest를 사용한 SqlCommand 실행
description: 쿼리 알림과 함께 작동 하도록 SqlCommand 개체를 구성 하는 방법을 보여 줍니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 1776f48f-9bea-41f6-83a4-c990c7a2c991
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 892f11e2d81e3a0733a1f0747c0b72c72ebc79fc
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451941"
---
# <a name="sqlcommand-execution-with-a-sqlnotificationrequest"></a>SqlNotificationRequest를 사용한 SqlCommand 실행

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

서버에서 데이터를 가져온 후 데이터가 변경 될 때 알림을 생성 하도록 <xref:Microsoft.Data.SqlClient.SqlCommand>를 구성 하 고, 쿼리를 다시 실행 하는 경우 결과 집합을 다르게 구성할 수 있습니다. 이 기능은 서버에서 사용자 지정 알림 큐를 사용 하려는 경우 또는 라이브 개체를 유지 관리 하지 않으려는 경우에 유용 합니다.

## <a name="creating-the-notification-request"></a>알림 요청 만들기

@No__t_0 개체를 사용 하 여 `SqlCommand` 개체에 바인딩하여 알림 요청을 만들 수 있습니다. 요청이 만들어지면 `SqlNotificationRequest` 개체가 더 이상 필요 하지 않습니다. 모든 알림에 대해 큐를 쿼리 하 고 적절 하 게 응답할 수 있습니다. 응용 프로그램이 종료 된 후 다시 시작 되는 경우에도 알림이 발생할 수 있습니다.

연결된 알림에 대한 명령이 실행될 때 원래 결과 집합에 대한 변경 사항이 있으면 알림 요청에 구성되어 있는 SQL Server 큐로 메시지를 보내는 작업이 트리거됩니다.

SQL Server 큐를 폴링하고 메시지를 해석하는 방법은 애플리케이션에 따라 다릅니다. 애플리케이션에서는 큐를 폴링하고 메시지의 내용에 따라 반응하는 작업을 수행합니다.

> [!NOTE]
> @No__t_0에서 SQL Server 알림 요청을 사용 하는 경우 기본 서비스 이름을 사용 하는 대신 고유한 큐 이름을 만듭니다.

@No__t_0에 대 한 새로운 클라이언트 쪽 보안 요소는 없습니다. 이는 주로 서버 기능이 며 서버는 사용자가 알림을 요청 하는 데 필요한 특별 한 권한을 만들었습니다.

### <a name="example"></a>예제

다음 코드 조각에서는 <xref:Microsoft.Data.Sql.SqlNotificationRequest>을 만들고 <xref:Microsoft.Data.SqlClient.SqlCommand>에 연결 하는 방법을 보여 줍니다.

```csharp
// Assume connection is an open SqlConnection.
// Create a new SqlCommand object.
SqlCommand command=new SqlCommand(
 "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection);

// Create a SqlNotificationRequest object.
SqlNotificationRequest notificationRequest=new SqlNotificationRequest();
notificationRequest.id="NotificationID";
notificationRequest.Service="mySSBQueue";

// Associate the notification request with the command.
command.Notification=notificationRequest;
// Execute the command.
command.ExecuteReader();
// Process the DataReader.
// You can use Transact-SQL syntax to periodically poll the
// SQL Server queue to see if you have a new message.
```

## <a name="next-steps"></a>다음 단계
- [SQL Server의 쿼리 알림](query-notifications-sql-server.md)
