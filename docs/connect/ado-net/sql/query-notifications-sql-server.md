---
title: SQL Server의 쿼리 알림
description: .NET 응용 프로그램에서 데이터가 변경 될 때 SQL Server에서 알림을 요청 하는 방법을 설명 합니다.
ms.date: 08/15/2019
ms.assetid: 0f0ba1a1-3180-4af8-87f7-c795dc8f8f55
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d47241e3656e3ca7b4f5ea0eebe9f2cc8b571bf6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452075"
---
# <a name="query-notifications-in-sql-server"></a>SQL Server의 쿼리 알림

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Service Broker 인프라를 기반으로 구축된 쿼리 알림을 통해 애플리케이션은 데이터 변경 시 알림을 받을 수 있습니다. 이 기능은 데이터베이스의 정보 캐시를 제공하며 원본 데이터 변경 시 알림을 받아야 하는 애플리케이션(예: 웹 애플리케이션)에 특히 유용합니다.  
  
ADO.NET를 사용 하 여 쿼리 알림을 구현 하는 방법에는 세 가지가 있습니다.  
  
- 하위 수준 구현은 서버 쪽 기능을 노출 하는 `SqlNotificationRequest` 클래스에서 제공 하므로 알림 요청을 사용 하 여 명령을 실행할 수 있습니다.  
  
- 개략적인 구현은 소스 응용 프로그램과 SQL Server 간의 알림 기능에 대 한 높은 수준의 추상화를 제공 하는 클래스인 `SqlDependency` 클래스에서 제공 하므로 종속성을 사용 하 여 서버의 변경 내용을 검색할 수 있습니다. 일반적으로 관리형 클라이언트 애플리케이션에서 Microsoft SqlClient Data Provider for SQL Server를 사용하여 SQL Server 알림 기능을 가장 간단하고 효과적으로 활용하는 방법입니다.  
  
- 또한 ASP.NET 2.0 이상을 사용하여 작성된 웹 애플리케이션에서는 `SqlCacheDependency` 도우미 클래스를 사용할 수 있습니다.  
  
쿼리 알림은 기본 데이터의 변경 내용에 대 한 응답으로 표시 또는 캐시를 새로 고쳐야 하는 응용 프로그램에 사용 됩니다. .NET 애플리케이션에서 Microsoft SQL Server를 사용하여 SQL Server에 명령을 보낼 수 있을 뿐 아니라 동일한 명령을 실행했을 때 처음 검색한 것과 다른 결과 집합이 나오면 알림을 생성하도록 요청할 수도 있습니다. 서버에서 생성된 알림은 나중에 처리하기 위해 큐를 통해 전송됩니다.  
  
SELECT 및 EXECUTE 문에 대 한 알림을 설정할 수 있습니다. EXECUTE 문을 사용 하는 경우 EXECUTE 문 자체가 아니라 실행 된 명령에 대 한 알림을 SQL Server 등록 합니다. 명령은 SELECT 문의 요구 사항과 제한 사항을 따라야 합니다. 알림을 등록하는 명령에 하나 이상의 문이 포함된 경우 데이터베이스 엔진은 일괄 처리에 있는 각 문에 대한 알림을 만듭니다.  
  
데이터가 변경될 때 신뢰할 수 있는 하위 보조 알림이 필요한 애플리케이션을 개발하려는 경우 SQL Server 온라인 설명서의 [알림 계획 항목](https://go.microsoft.com/fwlink/?LinkId=211984)에 있는 **효율적인 쿼리 알림 방법 계획** 및 **쿼리 알림 대체 방법** 단원을 참조하세요. 쿼리 알림 및 SQL Server Service Broker에 대 한 자세한 내용은 SQL Server 온라인 설명서의 항목에 대 한 다음 링크를 참조 하십시오.  
  
**SQL Server 설명서**  
  
- [쿼리 알림 사용](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms175110(v=sql.105))  
  
- [알림에 대한 쿼리 만들기](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms181122(v=sql.105))  
  
- [개발(Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522889(v=sql.105))  
  
- [Service Broker 개발자 정보 센터](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms166100(v=sql.105))  
  
- [개발자 가이드(Service Broker)](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb522908(v=sql.105))  
  
## <a name="in-this-section"></a>섹션 내용  
[쿼리 알림 사용](enable-query-notifications.md)  
쿼리 알림을 사용 하도록 설정 하 고 사용 하기 위한 요구 사항을 포함 하 여 쿼리 알림을 사용 하는 방법을 설명 합니다.  
  
[ASP.NET 애플리케이션의 SqlDependency](sqldependency-aspnet-app.md)  
ASP.NET 응용 프로그램에서 쿼리 알림을 사용 하는 방법을 보여 줍니다.  
  
[SqlDependency로 변경 내용 감지](detect-changes-sqldependency.md)  
쿼리 결과가 원래 수신 된 결과와 다를 때를 검색 하는 방법을 보여 줍니다.  
  
[SqlNotificationRequest를 사용한 SqlCommand 실행](sqlcommand-execution-sqlnotificationrequest.md)  
쿼리 알림과 함께 작동 하도록 <xref:Microsoft.Data.SqlClient.SqlCommand> 개체를 구성 하는 방법을 보여 줍니다.  
  
## <a name="reference"></a>참조  
<xref:Microsoft.Data.Sql.SqlNotificationRequest>  
@No__t_0 클래스와 모든 해당 멤버에 대해 설명 합니다.  
  
<xref:Microsoft.Data.SqlClient.SqlDependency>  
@No__t_0 클래스와 모든 해당 멤버에 대해 설명 합니다.  
  
<xref:System.Web.Caching.SqlCacheDependency>  
@No__t_0 클래스와 모든 해당 멤버에 대해 설명 합니다.  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 및 ADO.NET](index.md)
