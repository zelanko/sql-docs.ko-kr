---
title: XEvents 개요 - SQL Server
description: SQL Server 확장 이벤트 아키텍처를 사용하면 성능 문제를 확인하고 해결하는 데 필요한 데이터를 수집할 수 있습니다. SQL Server 확장 이벤트 아키텍처는 구성 가능하고 확장성이 있습니다.
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: overview
helpviewer_keywords:
- extended events [SQL Server]
- xe
- XEvents
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c837902edb7baa43d7fa07cfefc8ec335dc4183e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465534"
---
# <a name="extended-events-overview"></a>확장 이벤트 개요

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장 이벤트 아키텍처를 사용하여 성능 문제를 해결하거나 파악하는 데 필요한 만큼의 데이터만 수집할 수 있습니다. 확장 이벤트는 구성 가능하며 확장성이 매우 높습니다.

확장 이벤트에 대한 자세한 내용은 [빠른 시작: SQL Server의 확장 이벤트](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)를 참조하세요.

## <a name="benefits-of-ssnoversion-extended-events"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장 이벤트의 이점  

확장 이벤트는 최소한의 성능 리소스를 사용하는 간단한 성능 모니터링 시스템입니다. 확장 이벤트에서는 두 가지 그래픽 사용자 인터페이스가 제공되므로 세션 데이터를 작성, 수정, 표시 및 분석할 수 있습니다. 이러한 인터페이스의 이름은 다음과 같습니다.

- 새 세션 마법사
- 새 세션

## <a name="extended-events-concepts"></a>확장 이벤트 개념  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장 이벤트는 이벤트나 이벤트 소비자와 같은 기존 개념을 바탕으로 하고 Windows용 이벤트 추적의 개념을 사용하며 여기에 새로운 개념을 도입했습니다.  
  
 다음 표는 확장 이벤트의 개념에 대해 설명합니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[SQL Server 확장 이벤트 패키지](../../relational-databases/extended-events/sql-server-extended-events-packages.md)|개체를 포함하는 확장 이벤트 패키지에 대해 설명합니다. 이러한 개체는 확장 이벤트 세션이 실행 중일 때 데이터를 가져오고 처리하는 데 사용됩니다.|  
|[SQL Server 확장 이벤트 대상](/previous-versions/sql/sql-server-2016/bb630339(v=sql.130))|이벤트 세션이 지속되는 동안 데이터를 수신할 수 있는 이벤트 소비자에 대해 설명합니다.|  
|[SQL Server 확장 이벤트 엔진](../../relational-databases/extended-events/sql-server-extended-events-engine.md)|확장 이벤트 세션을 구현 및 관리하는 엔진에 대해 설명합니다.|  
|[SQL Server 확장 이벤트 세션](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)|확장 이벤트 세션에 대해 설명합니다.|  
| &nbsp; | &nbsp; |
  
## <a name="extended-events-architecture"></a>확장 이벤트 아키텍처  

확장 이벤트는 서버 시스템을 위한 일반적인 이벤트 처리 시스템을 지칭하는 이름입니다. 확장 이벤트 인프라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터와의 연계가 가능하고 특정 조건에서는 운영 체제 및 데이터베이스 애플리케이션 데이터와 연계해서 사용할 수 있는 기능도 지원합니다. 운영 체제의 경우 확장 이벤트 출력이 ETW(Windows용 이벤트 추적)로 전달되어야 합니다. ETW는 이벤트 데이터와 Windows 운영 체제 또는 애플리케이션 이벤트 데이터의 상관 관계를 파악할 수 있습니다.  

모든 애플리케이션에는 애플리케이션 내부 및 외부 모두에서 유용한 실행 지점이 있습니다. 애플리케이션 내부에서는 태스크의 초기 실행 중에 수집된 정보를 사용하여 비동기 처리를 큐에 넣을 수 있습니다. 애플리케이션 외부에서 실행 지점은 정보와 함께 모니터링 유틸리티를 제공합니다. 이 정보는 모니터링되는 애플리케이션의 동작 및 성능 특성에 대한 정보입니다.  

 확장 이벤트는 프로세스 외부에서의 이벤트 데이터 사용을 지원하며 이러한 데이터는 일반적으로 다음에서 사용됩니다.  
  
-   SQL 추적 및 시스템 모니터와 같은 추적 도구  
  
-   Windows 이벤트 로그 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그 등의 로깅 도구  
  
-   제품을 관리하거나 제품의 애플리케이션을 개발하는 사용자  
  
 확장 이벤트는 다음과 같은 주요 요소를 고려하여 디자인되었습니다.  
  
-   확장 이벤트 엔진은 이벤트 중립적입니다. 이 엔진은 이벤트 내용에 따른 제한이 없으므로 모든 이벤트를 모든 대상에 바인딩할 수 있습니다. 확장 이벤트 엔진에 대한 자세한 내용은 [SQL Server Extended Events Engine](../../relational-databases/extended-events/sql-server-extended-events-engine.md)을 참조하십시오.  
  
-   이벤트는 확장 이벤트의 *대상* 이라고 하는 이벤트 소비자와 분리됩니다. 따라서 모든 대상이 모든 이벤트를 수신할 수 있습니다. 또한 발생한 모든 이벤트는 대상에서 자동으로 사용되므로 추가 이벤트 컨텍스트가 기록되거나 제공될 수 있습니다. 자세한 내용은 [SQL Server Extended Events Targets](/previous-versions/sql/sql-server-2016/bb630339(v=sql.130))을 참조하세요.  
  
-   이벤트는 이벤트가 발생할 때 실행되는 동작과는 별개입니다. 따라서 모든 이벤트에 모든 동작을 연결할 수 있습니다.  
  
-   조건자를 사용하면 이벤트 데이터를 캡처해야 할 때를 동적으로 필터링할 수 있으므로 동적 필터링을 통해 확장 이벤트 인프라의 유연성이 높아집니다. 자세한 내용은 [SQL Server Extended Events Packages](../../relational-databases/extended-events/sql-server-extended-events-packages.md)을 참조하세요.  
  
 확장 이벤트는 이벤트 데이터를 동기적으로 생성하고 데이터를 비동기적으로 처리하여 유연한 이벤트 처리 솔루션을 제공합니다. 또한 확장 이벤트는 다음 기능도 지원합니다.  
  
-   사용자가 문제 해결을 위해 특정 이벤트를 격리할 수 있도록 허용하면서 서버 시스템 전체에서 일관된 이벤트 처리 방식  
  
-   기존 ETW 도구 통합 및 지원  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]을 기반으로 하는 완전히 구성 가능한 이벤트 처리 메커니즘  
  
-   활성 프로세스에 거의 영향을 주지 않고 동적으로 이를 모니터링할 수 있는 기능  
  
-   성능에 크게 영향을 주지 않고 실행되는 기본 시스템 상태 세션. 이 세션은 성능 문제를 해결하는 데 사용할 수 있는 시스템 데이터를 수집합니다. 자세한 내용은 [system_health 세션 사용](../../relational-databases/extended-events/use-the-system-health-session.md)을 참조하세요.  
  
## <a name="extended-events-tasks"></a>확장 이벤트 태스크  

[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL(데이터 정의 언어) 문, 동적 관리 뷰와 함수 또는 카탈로그 뷰를 실행하면 사용 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경에 맞는 간단하거나 복잡한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장 이벤트 문제 해결 솔루션을 만들 수 있습니다.  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|**개체 탐색기** 를 사용하여 이벤트 세션을 관리합니다.|[개체 탐색기에서 이벤트 세션 관리](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)|  
|확장 이벤트 세션을 만드는 방법에 대해 설명합니다.|[확장 이벤트 세션 만들기](/previous-versions/sql/sql-server-2016/hh213147(v=sql.130))|  
|대상 데이터를 보고 새로 고치는 방법에 대해 설명합니다.| [SQL Server 확장 이벤트의 대상 데이터 고급 보기](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)|  
|확장 이벤트 도구를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장 이벤트 세션을 만들고 관리하는 방법에 대해 설명합니다.|[확장 이벤트 도구](../../relational-databases/extended-events/extended-events-tools.md)|  
|확장 이벤트 세션을 변경하는 방법에 대해 설명합니다.|[확장 이벤트 세션 변경](../../relational-databases/extended-events/alter-an-extended-events-session.md)|  
|이벤트와 관련된 필드에 대한 정보를 가져오는 방법에 대해 설명합니다.|[모든 이벤트에 대한 필드 가져오기](/previous-versions/sql/sql-server-2016/bb677249(v=sql.130))|  
|등록된 패키지에서 사용할 수 있는 이벤트를 확인하는 방법에 대해 설명합니다.|[등록된 패키지에 대한 이벤트 보기](./selects-and-joins-from-system-views-for-extended-events-in-sql-server.md)|  
|등록된 패키지에서 사용할 수 있는 확장 이벤트 대상을 확인하는 방법에 대해 설명합니다.|[등록된 패키지의 확장 이벤트 대상 보기](/previous-versions/sql/sql-server-2016/bb677247(v=sql.130))|  
|각 SQL 추적 이벤트 및 관련 열에 해당하는 확장 이벤트의 이벤트 및 동작을 확인하는 방법에 대해 설명합니다.|[SQL 추적 이벤트 클래스에 해당하는 확장 이벤트 항목 확인](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|CREATE EVENT SESSION 또는 ALTER EVENT SESSION에 ADD TARGET 인수를 사용할 경우에 설정할 수 있는 매개 변수를 확인하는 방법에 대해 설명합니다.|[ADD TARGET 인수에 대한 구성 가능한 매개 변수 가져오기](/previous-versions/sql/sql-server-2016/bb677176(v=sql.130))|  
|기존 SQL 추적 스크립트를 확장 이벤트 세션으로 변환하는 방법에 대해 설명합니다.|[기존 SQL 추적 스크립트를 확장 이벤트 세션으로 변환](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|잠금을 보유 중인 쿼리, 쿼리 계획 및 잠긴 시점의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스택을 확인하는 방법에 대해 설명합니다.|[잠금을 보유한 쿼리 파악](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)|  
|데이터베이스 성능을 저하시키는 잠금의 원인을 파악하는 방법에 대해 설명합니다.|[가장 많은 잠금이 발생한 개체 찾기](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|확장 이벤트를 Windows용 이벤트 추적과 함께 사용하여 시스템 작업을 모니터링하는 방법에 대해 설명합니다.|[확장 이벤트를 사용하여 시스템 작업 모니터링](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)|  
|확장 이벤트 대해 카탈로그 뷰 및 DMV(동적 관리 뷰) 사용 | [SQL Server 확장 이벤트에 대한 시스템 뷰의 SELECT 및 JOIN](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) |
| &nbsp; | &nbsp; |

다음 Transact-SQL(T-SQL) 쿼리를 사용하여 가능한 모든 확장 이벤트와 해당 설명을 나열합니다.

```sql
SELECT
     obj1.name as [XEvent-name],
     col2.name as [XEvent-column],
     obj1.description as [Descr-name],
     col2.description as [Descr-column]
  FROM
               sys.dm_xe_objects        as obj1
      JOIN sys.dm_xe_object_columns as col2 on col2.object_name = obj1.name
  ORDER BY
    obj1.name,
    col2.name
```


## <a name="code-examples-can-differ-for-azure-sql-database"></a>코드 예제는 Azure SQL Database와 다를 수 있음

[!INCLUDE[sql-on-premises-vs-azure-similar-sys-views-include.](../../includes/paragraph-content/sql-on-premises-vs-azure-similar-sys-views-include.md)]

## <a name="see-also"></a>참고 항목

[데이터 계층 애플리케이션](../../relational-databases/data-tier-applications/data-tier-applications.md)  
[SQL Server 개체 및 버전에 대한 DAC 지원](/previous-versions/sql/sql-server-2012/ee210549(v=sql.110))  
[데이터 계층 애플리케이션 배포](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)  
[데이터 계층 애플리케이션 모니터링](../../relational-databases/data-tier-applications/monitor-data-tier-applications.md)  
&nbsp;  
[확장 이벤트 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)  
[확장 이벤트 카탈로그 뷰(Transact-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)  
&nbsp;  
[XELite: XEL 파일 또는 라이브 SQL 스트림에서 XEvents를 읽을 수 있는 플랫폼 간 라이브러리](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite/), 2019년 5월에 릴리스됨.  
[Read-SQLXEvent PowerShell cmdlet](https://www.powershellgallery.com/packages/SqlServer.XEvent) 2019년 6월 릴리스.  
[SQL Mysteries: XEvent 세션의 인과 관계 추적 및 이벤트 순서(블로그 게시일 2019년 4월 1일)](https://bobsql.com/sql-mysteries-causality-tracking-vs-event-sequence-for-xevent-sessions/)