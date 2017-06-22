---
title: "포함된 데이터베이스 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- contained database
- database_uncontained_usage event
- partially contained database
- contained database, understanding
ms.assetid: 36af59d7-ce96-4a02-8598-ffdd78cdc948
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 40dc720b7c0e74efbd1602d29af26da6320f66c1
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="contained-databases"></a>포함된 데이터베이스
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  *포함된 데이터베이스* 는 다른 데이터베이스 및 해당 데이터베이스를 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 격리된 데이터베이스입니다.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 인스턴스에서 데이터베이스를 격리하는 방법은 네 가지가 있습니다.  
  
-   데이터베이스를 설명하는 메타데이터는 대부분 데이터베이스에 유지됩니다. 메타데이터는 master 데이터베이스 대신 해당 데이터베이스에 유지되거나 두 데이터베이스 모두에 유지됩니다.  
  
-   모든 메타데이터는 동일한 데이터 정렬을 사용하여 정의됩니다.  
  
-   데이터베이스를 통해 사용자 인증을 수행하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 로그인에 대한 데이터베이스 종속성을 줄일 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경은 포함 정보를 보고하며 그에 따라 조치를 취할 수 있습니다.  
  
 메타데이터를 데이터베이스에 저장하는 등의 부분적으로 포함된 데이터베이스의 일부 기능은 모든 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스에 적용됩니다. 데이터베이스 수준 인증 및 카탈로그 데이터 정렬 등의 부분적으로 포함된 데이터베이스의 일부 이점은 먼저 사용하도록 설정해야만 사용할 수 있습니다. **CREATE DATABASE** 및 **ALTER DATABASE** 문을 사용하거나 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 부분 포함을 사용하도록 설정할 수 있습니다. 부분 데이터베이스 포함을 사용하도록 설정하는 방법은 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)을 참조하십시오.  
  
##  <a name="Concepts"></a> 부분적으로 포함된 데이터베이스 개념  
 전체적으로 포함된 데이터베이스는 데이터베이스를 정의하는 데 필요한 모든 설정과 메타데이터를 포함하며 데이터베이스가 설치된 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스와 어떠한 구성 종속 관계도 가지고 있지 않습니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 분리하는 작업은 시간이 많이 걸릴 수 있으며 이 작업을 위해서는 데이터베이스와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 간 관계를 자세히 알고 있어야 합니다. 부분적으로 포함된 데이터베이스를 사용하면 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 다른 데이터베이스와 쉽게 분리할 수 있습니다.  
  
 포함된 데이터베이스는 포함과 관련된 기능을 고려합니다. 데이터베이스에 있는 기능에만 의존하는 사용자 정의 엔터티는 완전히 포함된 것으로 간주됩니다. 데이터베이스 외부의 기능에 의존하는 사용자 정의 엔터티는 포함되지 않은 것으로 간주됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [포함](#containment) 섹션을 참조하세요.  
  
 다음 용어는 포함된 데이터베이스 모델에 적용됩니다.  
  
 데이터베이스 경계  
 데이터베이스와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 사이의 경계입니다. 데이터베이스와 다른 데이터베이스 사이의 경계입니다.  
  
 포함됨  
 데이터베이스 경계 내에 전체가 포함되는 요소입니다.  
  
 포함되지 않음  
 데이터베이스 경계를 넘는 요소입니다.  
  
 포함되지 않은 데이터베이스  
 포함이 **NONE**으로 설정된 데이터베이스입니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이전 버전의 모든 데이터베이스는 포함되지 않은 데이터베이스입니다. 기본적으로 모든 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상 데이터베이스는 포함이 **NONE**으로 설정되어 있습니다.  
  
 부분적으로 포함된 데이터베이스  
 부분적으로 포함된 데이터베이스는 데이터베이스 경계를 넘는 일부 기능을 허용할 수 있는 포함된 데이터베이스입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 포함 경계가 교차할 때 확인할 수 있는 기능이 있습니다.  
  
 포함된 사용자  
 포함된 데이터베이스에는 두 가지 유형의 사용자가 있습니다.  
  
-   **암호가 있는 포함된 데이터베이스 사용자**  
  
     암호가 있는 포함된 데이터베이스 사용자는 데이터베이스에 의해 인증됩니다. 자세한 내용은 [포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기](../../relational-databases/security/contained-database-users-making-your-database-portable.md)를 참조하세요.  
  
-   **Windows 보안 주체**  
  
     권한이 있는 Windows 사용자 및 권한이 있는 Windows 그룹의 멤버는 데이터베이스에 직접 연결할 수 있으며 **master** 데이터베이스의 로그인이 필요하지 않습니다. 데이터베이스는 Windows에 의한 인증을 신뢰합니다.  
  
 **master** 데이터베이스의 로그인을 기반으로 하는 사용자는 포함된 데이터베이스에 대한 액세스 권한을 부여받을 수 있지만 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 종속성이 생깁니다. 따라서 로그인을 기반으로 하는 사용자를 만드는 경우 부분적으로 포함된 데이터베이스에 대한 설명을 참조하십시오.  
  
> [!IMPORTANT]  
>  부분적으로 포함된 데이터베이스를 사용하도록 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 액세스 제어 권한이 데이터베이스 소유자에게 위임됩니다. 자세한 내용은 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)를 참조하세요.  
  
 데이터베이스 경계  
 부분적으로 포함된 데이터베이스는 인스턴스의 기능에서 데이터베이스 기능을 분리하므로 이 두 요소 사이에 *데이터베이스 경계*라는 명확히 정의된 선이 있습니다.  
  
 데이터베이스 경계 내부에는 *데이터베이스 모델*이 있으며 여기에서 데이터베이스가 개발되고 관리됩니다. 데이터베이스 내부에 있는 엔터티에는 **sys.tables**와 같은 시스템 테이블, 암호가 있는 포함된 데이터베이스 사용자, 두 부분으로 구성된 이름으로 참조되는 현재 데이터베이스의 사용자 테이블 등이 있습니다.  
  
 데이터베이스 경계의 외부에는 *관리 모델*이 있으며 이 모델은 인스턴스 수준 기능 및 관리와 관련되어 있습니다. 데이터베이스 경계 외부에 있는 엔터티에는 **sys.endpoints**와 같은 시스템 테이블, 로그인에 매핑된 사용자, 세 부분으로 구성된 이름으로 참조되는 다른 데이터베이스의 사용자 테이블 등이 있습니다.  
  
##  <a name="containment"></a> 포함  
 전적으로 데이터베이스 내부에 있는 사용자 엔터티는 *포함된*것으로 간주됩니다. 데이터베이스 외부에 있거나 데이터베이스 외부 기능과의 상호 작용에 의존하는 사용자 엔터티는 *포함되지 않은*것으로 간주됩니다.  
  
 일반적으로 사용자 엔터티는 다음과 같은 포함 범주로 분류됩니다.  
  
-   sys.indexes와 같이 데이터베이스 경계를 넘지 않는, 완전히 포함된 사용자 엔터티. 이러한 기능을 사용하는 모든 코드 또는 이러한 엔터티만 참조하는 모든 개체도 완전히 포함된 것으로 간주됩니다.  
  
-   sys.server_principals 또는 서버 보안 주체(로그인)와 같이 데이터베이스 경계를 넘는, 포함되지 않은 사용자 엔터티. 이러한 엔터티를 사용하는 모든 코드 또는 이러한 엔터티를 참조하는 모든 기능은 포함되지 않은 것으로 간주됩니다.  
  
###  <a name="partial"></a> Partially Contained Database  
 포함된 데이터베이스 기능은 현재 부분적으로 포함된 상태에서만 사용할 수 있습니다. 부분적으로 포함된 데이터베이스는 포함되지 않은 기능을 사용하도록 허용하는 포함된 데이터베이스입니다.  
  
 포함되지 않은 개체 또는 기능에 대한 정보를 반환하려면 [sys.dm_db_uncontained_entities](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md) 및 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) 뷰를 사용하세요. 데이터베이스 요소의 포함 상태를 파악함으로써 포함 상태를 승격시키려면 어떤 개체 또는 기능을 바꾸거나 변경해야 하는지 확인할 수 있습니다.  
  
> [!IMPORTANT]  
>  일부 개체는 기본 포함 설정이 **NONE**이므로 이 뷰는 거짓 긍정을 반환할 수 있습니다.  
  
 부분적으로 포함된 데이터베이스의 동작은 포함되지 않은 데이터베이스의 동작과 데이터 정렬의 측면에서 가장 많이 다릅니다. 데이터 정렬 문제에 대한 자세한 내용은 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)을 참조하십시오.  
  
##  <a name="benefits"></a> 부분적으로 포함된 데이터베이스 사용의 이점  
 부분적으로 포함된 데이터베이스를 사용하면 포함되지 않은 데이터베이스와 관련된 일부 문제 및 복잡성을 해결할 수 있습니다.  
  
### <a name="database-movement"></a>데이터베이스 이동  
 데이터베이스를 이동할 때 발생하는 문제 중 하나는 인스턴스 간에 데이터베이스를 이동하면 일부 중요한 정보를 사용할 수 없게 된다는 점입니다. 예를 들어 로그인 정보가 데이터베이스 대신 인스턴스 내에 저장되어 있는 경우, 포함되지 않은 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 한 인스턴스에서 다른 인스턴스로 이동하면 이러한 정보는 남겨집니다. 그러면 누락된 데이터를 식별하여 데이터베이스와 함께 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 이동해야 합니다. 이 프로세스는 시간이 많이 걸리며 어려울 수 있습니다.  
  
 부분적으로 포함된 데이터베이스는 중요 정보를 데이터베이스에 저장할 수 있으므로 데이터베이스를 이동한 후에도 데이터베이스에 정보가 그대로 있습니다.  
  
> [!NOTE]  
>  부분적으로 포함된 데이터베이스는 인스턴스에서 분리할 수 없는 데이터베이스에서 사용하는 기능을 설명하는 설명서를 제공합니다. 여기에는 서로 관련된 다른 데이터베이스 목록, 데이터베이스에 필요하지만 포함할 수 없는 시스템 설정 등이 포함됩니다.  
  
### <a name="benefit-of-contained-database-users-with-always-on"></a>Always On을 사용하는 포함된 데이터베이스 사용자의 이점  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스와의 관련성을 줄이면 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]을 사용할 때 장애 조치 중에 부분적으로 포함된 데이터베이스가 유용할 수 있습니다.  
  
 포함된 사용자를 만들면 사용자가 포함된 데이터베이스에 직접 연결할 수 있습니다. 이 기능은 Always On 솔루션과 같은 고가용성 및 재해 복구 시나리오에서 매우 중요한 기능입니다. 사용자가 포함된 사용자인 경우 장애 조치(failover) 시 보조 복제본을 호스팅하는 인스턴스에 대한 로그인을 만들지 않고도 보조 복제본에 연결할 수 있습니다. 이는 즉각적인 이점을 제공합니다. 자세한 내용은 [Always On 가용성 그룹 개요(SQL Server)](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) 및 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항(SQL Server)](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)을 참조하세요.  
  
### <a name="initial-database-development"></a>초기 데이터베이스 개발  
 개발자는 새 데이터베이스가 배포될 위치를 알지 못할 수 있으므로 데이터베이스에 대한 배포 환경의 영향을 제한하면 개발자의 작업이 더 쉬워질 수 있습니다. 포함되지 않은 모델에서 개발자는 새 데이터베이스 및 프로그램에 대해 가능한 환경적 영향을 고려해야 합니다. 하지만 개발자는 부분적으로 포함된 데이터베이스를 사용하여 데이터베이스에 대한 인스턴스 수준의 영향과 인스턴스 수준에서 개발자가 고려해야 할 요소를 검색할 수 있습니다.  
  
### <a name="database-administration"></a>데이터베이스 관리  
 데이터베이스 설정을 master 데이터베이스 대신 데이터베이스에 유지하면 데이터베이스 소유자에게 **sysadmin** 권한을 제공할 필요 없이 각 데이터베이스 소유자가 해당 데이터베이스를 더 세밀하게 제어할 수 있습니다.  
  
##  <a name="Limitations"></a> 제한 사항  
 부분적으로 포함된 데이터베이스는 다음 기능을 허용하지 않습니다.  
  
-   부분적으로 포함된 데이터베이스는 복제, 변경 데이터 캡처 또는 변경 내용 추적 기능을 사용할 수 없습니다.  
  
-   번호를 매긴 프로시저  
  
-   데이터 정렬이 변경된 기본 제공 기능에 종속된 스키마 바운드 개체  
  
-   개체, 열, 기호 또는 유형에 대한 참조를 비롯하여 데이터 정렬 변경의 결과로 발생하는 바인딩 변경  
  
-   복제, 변경 데이터 캡처 및 변경 내용 추적  
  
> [!WARNING]  
>  임시 저장 프로시저는 현재 허용되지만, 포함 조건을 위반하므로 이후 버전의 포함된 데이터베이스에서는 지원되지 않을 것입니다.  
  
##  <a name="Identifying"></a> 데이터베이스 포함 식별  
 데이터베이스의 포함 상태를 식별할 수 있는 도구가 두 가지 있습니다. [sys.dm_db_uncontained_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md)는 데이터베이스에서 포함되지 않은 엔터티일 가능성이 있는 엔터티를 모두 표시하는 뷰입니다. 런타임 시 실제로 포함되지 않은 엔터티가 식별될 때 database_uncontained_usage 이벤트가 발생합니다.  
  
### <a name="sysdmdbuncontainedentities"></a>sys.dm_db_uncontained_entities  
 이 뷰는 데이터베이스 경계를 넘는 엔터티와 같이 포함되지 않은 엔터티가 될 가능성이 있는 데이터베이스의 엔터티를 보여 줍니다. 여기에는 데이터베이스 모델 외부 개체를 사용할 수 있는 사용자 엔터티가 포함됩니다. 그러나 런타임이 될 때까지 일부 엔터티(예: 동적 SQL을 사용하는 엔터티)의 포함을 확인할 수 없기 때문에 이 뷰에서 실제로는 포함되지 않은 엔터티가 아닌 일부 엔터티를 보여 줄 수 있습니다. 자세한 내용은 [sys.dm_db_uncontained_entities&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md)를 참조하세요.  
  
### <a name="databaseuncontainedusage-event"></a>database_uncontained_usage 이벤트  
 XEvent는 런타임 시 포함되지 않은 엔터티가 식별될 때마다 발생합니다. 여기에는 클라이언트 코드에서 시작된 엔터티가 포함됩니다. 이 XEvent는 실제로 포함되지 않은 엔터티에 대해서만 발생합니다. 그러나 이벤트는 런타임에만 발생합니다. 따라서 실행하지 않은, 포함되지 않은 모든 사용자 엔터티는 이 XEvent에서 식별되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [수정된 기능&#40;포함된 데이터베이스&#41;](../../relational-databases/databases/modified-features-contained-database.md)   
 [Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)   
 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)   
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [포함된 데이터베이스 사용자 - 이식 가능한 데이터베이스 만들기](../../relational-databases/security/contained-database-users-making-your-database-portable.md)  
  
  

