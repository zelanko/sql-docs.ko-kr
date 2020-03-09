---
title: SQL Server의 데이터베이스 미러링
description: 데이터베이스 미러링 기능에 대해 설명합니다.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: c7ace2feb39bcc3f5f257c0ac2c7360649cfc33c
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2020
ms.locfileid: "78897004"
---
# <a name="database-mirroring-in-sql-server"></a>SQL Server의 데이터베이스 미러링

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server의 데이터베이스 미러링을 사용하면 대기 서버에서 SQL Server 데이터베이스의 복사본, 즉 미러를 유지할 수 있습니다. 미러링을 사용하면 별도의 데이터 복사본 두 개가 항상 존재하여 높은 가용성과 완전한 데이터 중복성을 보장합니다. Microsoft SqlClient Provider for SQL Server에서는 데이터베이스 미러링을 암시적으로 지원하므로 SQL Server 데이터베이스에 대해 미러링이 구성되고 나면 개발자는 별도로 작업을 수행하거나 코드를 작성할 필요가 없습니다. 또한 <xref:Microsoft.Data.SqlClient.SqlConnection> 개체는 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>에서의 장애 조치(failover) 파트너 서버 이름 제공을 지원합니다.  
  
미러링용으로 구성된 데이터베이스를 대상으로 하는 <xref:Microsoft.Data.SqlClient.SqlConnection> 개체에 대하여 다음과 같은 간단한 이벤트 시퀀스가 발생합니다.  
  
1. 클라이언트 애플리케이션이 주 데이터베이스에 성공적으로 연결되고 서버에서 파트너 서버의 이름을 다시 보냅니다(클라이언트에 캐시됨).  
  
2. 주 데이터베이스가 포함된 서버가 실패하거나 연결이 중단되면 연결 및 트랜잭션 상태가 손실됩니다. 클라이언트 애플리케이션은 주 데이터베이스에 대한 연결을 다시 설정하려고 시도하고 실패합니다.  
  
3. 그런 다음 클라이언트 애플리케이션은 파트너 서버에서 미러 데이터베이스에 대한 연결을 투명하게 시도합니다. 성공하면 연결이 미러 데이터베이스로 리디렉션되고, 그러면 새로운 주 데이터베이스가 됩니다.  
  
## <a name="specifying-the-failover-partner-in-the-connection-string"></a>연결 문자열에 장애 조치(failover) 파트너 지정  
연결 문자열에 장애 조치(failover) 파트너 서버 이름을 제공하는 경우에는 클라이언트 애플리케이션이 처음 연결될 때 주 데이터베이스를 사용할 수 없다면 클라이언트는 장애 조치(failover) 파트너와의 연결을 투명하게 시도합니다.  
  
```csharp
";Failover Partner=PartnerServerName"  
```  
  
장애 조치(failover) 파트너 서버의 이름을 생략하고 클라이언트 애플리케이션이 처음 연결될 때 주 데이터베이스를 사용할 수 없다면 <xref:Microsoft.Data.SqlClient.SqlException>이 발생합니다.  
  
<xref:Microsoft.Data.SqlClient.SqlConnection>이 성공적으로 열리면 서버에서 장애 조치(failover) 파트너의 이름이 반환되어 연결 문자열에 제공된 모든 값을 대체합니다.  
  
> [!NOTE]
>  데이터베이스 미러링 시나리오의 경우 연결 문자열에 초기 카탈로그 또는 데이터베이스 이름을 명시적으로 지정해야 합니다. 클라이언트에서 명시적으로 지정된 초기 카탈로그 또는 데이터베이스가 없는 연결에 대한 장애 조치 정보를 받으면 장애 조치 정보가 캐시되지 않고 주 서버가 실패해도 애플리케이션에서 장애 조치를 시도하지 않습니다. 연결 문자열에 장애 조치(failover) 파트너에 대한 값은 있지만 초기 카탈로그 또는 데이터베이스에 대한 값이 없는 경우에는 `InvalidArgumentException`이 발생합니다.  
  
## <a name="retrieving-the-current-server-name"></a>현재 서버 이름 검색  
장애 조치(failover) 시 <xref:Microsoft.Data.SqlClient.SqlConnection> 개체의 <xref:Microsoft.Data.SqlClient.SqlConnection.DataSource%2A> 속성을 사용하여 현재 연결이 실제로 연결된 서버의 이름을 검색할 수 있습니다. 다음 코드 조각은 연결 변수가 열린 <xref:Microsoft.Data.SqlClient.SqlConnection>을 참조한다고 가정하여 활성 서버의 이름을 검색합니다.  
  
장애 조치 이벤트가 발생하고 연결이 미러 서버로 전환되면 **DataSource** 속성이 업데이트되며 미러 이름을 반영합니다.  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## <a name="sqlclient-mirroring-behavior"></a>SqlClient 미러링 동작  
클라이언트는 항상 현재 주 서버에 연결을 시도합니다. 실패하면 장애 조치(failover) 파트너로 연결을 시도합니다. 미러 데이터베이스가 파트너 서버의 주 역할로 이미 전환된 경우에는 연결이 성공하고 새로운 주-미러 매핑이 클라이언트로 전송되며 호출 <xref:System.AppDomain>의 수명 동안 캐시됩니다. 이 매핑은 영구 스토리지에 저장되지 않으므로 다른 **AppDomain** 또는 프로세스의 후속 연결에는 사용할 수 없습니다. 그러나 동일한 **AppDomain** 내에서의 후속 연결에는 사용할 수 있습니다. 같거나 다른 컴퓨터에서 실행되는 다른 **AppDomain** 또는 프로세스에는 항상 연결 풀이 있으며 이러한 연결은 다시 설정되지 않습니다. 이 경우 주 데이터베이스가 다운되면 각 프로세스 또는 **AppDomain**이 실패하고 나서 풀이 자동으로 지워집니다.  
  
> [!NOTE]
>  서버에서의 미러링 지원은 데이터베이스별로 구성됩니다. 다중 파트 이름을 사용하거나 현재 데이터베이스를 변경하는 방식으로 주/미러 집합에 포함되지 않은 다른 데이터베이스에 대해 데이터 조작 작업이 실행되는 경우, 이러한 다른 데이터베이스에 대한 변경 내용은 실패 시 전파되지 않습니다. 미러되지 않은 데이터베이스에서 데이터가 수정되는 경우에는 오류가 발생하지 않습니다. 개발자는 이러한 작업이 미칠 수 있는 영향을 평가해야 합니다.  
  
## <a name="next-steps"></a>다음 단계
### <a name="database-mirroring-resources"></a>데이터베이스 미러링 리소스  
미러링 구성, 배포 및 관리에 대한 개념 설명서 및 정보를 보려면 SQL Server 설명서에서 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[데이터베이스 미러링](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)|SQL Server에서 미러링을 설정 및 구성하는 방법을 설명합니다.|  
