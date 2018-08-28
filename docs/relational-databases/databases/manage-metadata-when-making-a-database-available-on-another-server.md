---
title: 다른 서버에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리 | Microsoft 문서
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cross-database queries [SQL Server]
- logins [SQL Server], recreating on another server instance
- triggers [SQL Server], DLL
- user-defined error messages [SQL Server]
- permissions [SQL Server], metadata access
- Full-Text Engine [SQL Server]
- metadata [SQL Server], databases available to other instances
- jobs [SQL Server Agent], recreating on another server instance
- failover [SQL Server], managing metadata
- event notifications [SQL Server], metadata
- database mirroring [SQL Server], metadata
- startup options [SQL Server]
- restoring [SQL Server], onto another server instance
- linked servers [SQL Server], metadata
- WMI Provider for Server Events, metadata
- attaching databases [SQL Server]
- log shipping [SQL Server], metadata
- encryption [SQL Server], metadata
- server configuration [SQL Server]
- distributed queries [SQL Server], metadata
- extended stored procedures [SQL Server], metadata
- credentials [SQL Server], metadata
- copying databases
ms.assetid: 5d98cf2a-9fc2-4610-be72-b422b8682681
caps.latest.revision: 84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 610c566e97a700ee47f48aedd99874c9ac719064
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40405697"
---
# <a name="manage-metadata-when-making-a-database-available-on-another-server"></a>다른 서버에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 아티클에는 다음과 같은 상황과 관련된 내용이 포함되어 있습니다.  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 가용성 그룹의 가용성 복제본을 구성하는 경우  
  
-   데이터베이스에 대해 데이터베이스 미러링을 설정하는 경우  
  
-   로그 전달 구성에서 주 서버와 보조 서버 간에 역할 변경을 준비하는 경우  
  
-   데이터베이스를 다른 서버 인스턴스로 복원하는 경우  
  
-   다른 서버 인스턴스에서 데이터베이스 복사본을 연결하는 경우  
  
 일부 응용 프로그램은 단일 사용자 데이터베이스 범위 밖에 있는 정보, 엔터티 및/또는 개체에 따라 달라집니다. 일반적으로 응용 프로그램은 **master** 및 **msdb** 데이터베이스뿐만 아니라 사용자 데이터베이스에 따라 달라집니다. 사용자 데이터베이스의 올바른 작동을 위해 해당 데이터베이스 외부에 저장되어 있는 모든 요소는 대상 서버 인스턴스에서 사용할 수 있어야 합니다. 예를 들어 응용 프로그램에 대한 로그인은 **master** 데이터베이스에서 메타데이터로 저장되어 있으며 대상 서버에서 다시 생성되어야 합니다. 메타데이터가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스에 저장되어 있는** 에이전트 작업에 따라 응용 프로그램이나 데이터베이스 유지 관리 계획이 달라지는 경우 대상 서버 인스턴스에서 이러한 작업을 다시 만들어야 합니다. 마찬가지로 서버 수준 트리거에 대한 메타데이터는 **master**에 저장되어 있습니다.  
  
 응용 프로그램에 대한 데이터베이스를 다른 서버 인스턴스로 이동할 경우 대상 서버 인스턴스의 **master** 및 **msdb** 에서 종속 개체와 엔터티의 모든 메타데이터를 다시 만들어야 합니다. 예를 들어 데이터베이스 응용 프로그램이 서비스 수준 트리거를 사용하는 경우 단순히 새 시스템에서 데이터베이스를 연결하거나 복원하는 것만으로 충분하지 않습니다. **master** 데이터베이스에서 이러한 트리거에 대한 모든 메타데이터를 수동으로 다시 만들지 않으면 데이터베이스가 예상대로 작동하지 않습니다.  
  
##  <a name="information_entities_and_objects"></a> 사용자 데이터베이스의 외부에 저장된 정보, 엔터티 및 개체  
 이 아티클의 나머지에서는 다른 서버 인스턴스에서 사용되는 데이터베이스에 영향을 줄 수 있는 발생 가능한 문제에 대해 요약합니다. 다음 목록에 나열된 하나 또는 그 이상의 정보, 엔터티 또는 개체 유형을 다시 만들어야 할 수 있습니다. 요약을 보려면 항목의 링크를 클릭합니다.  
  
-   [서버 구성 설정](#server_configuration_settings)  
  
-   [자격 증명](#credentials)  
  
-   [데이터베이스 간 쿼리](#cross_database_queries)  
  
-   [데이터베이스 소유권](#database_ownership)  
  
-   [분산 쿼리/연결된 서버](#distributed_queries_and_linked_servers)  
  
-   [암호화된 데이터](#encrypted_data)  
  
-   [사용자 정의 오류 메시지](#user_defined_error_messages)  
  
-   [이벤트 알림 및 WMI(Windows Management Instrumentation) 이벤트(서버 수준)](#event_notif_and_wmi_events)  
  
-   [확장 저장 프로시저](#extended_stored_procedures)  
  
-   [SQL Server용 전체 텍스트 엔진 속성](#ifts_service_properties)  
  
-   [작업](#jobs)  
  
-   [로그인](#logins)  
  
-   [사용 권한](#permissions)  
  
-   [복제 설정](#replication_settings)  
  
-   [Service Broker 응용 프로그램](#sb_applications)  
  
-   [시작 프로시저](#startup_procedures)  
  
-   [트리거(서버 수준)](#triggers)  
  
##  <a name="server_configuration_settings"></a> Server Configuration Settings  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서는 키 서비스 및 기능을 필요에 따라 설치하고 시작합니다. 이를 통해 시스템이 공격 받을 수 있는 노출 영역을 줄일 수 있습니다. 새 설치의 기본 구성에서는 많은 기능이 활성화되지 않습니다. 데이터베이스가 기본적으로 해제된 서비스나 기능을 사용하는 경우 대상 서버 인스턴스에서 이 서비스나 기능을 설정해야 합니다.  
  
 이러한 설정에 대한 자세한 내용과 설정을 지정하거나 해제하는 방법은 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)을 참조하세요.  
  
  
##  <a name="credentials"></a> 자격 증명  
 자격 증명은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]외부의 리소스에 연결하는 데 필요한 인증 정보가 포함된 레코드입니다. 대부분의 자격 증명은 Windows 로그인 및 암호로 구성됩니다.  
  
 이 기능에 대한 자세한 내용은 [자격 증명&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)을 참조하세요.  
  
> **참고:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정은 자격 증명을 사용합니다. 프록시 계정의 자격 증명 ID를 확인하려면 [sysproxies](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md) 시스템 테이블을 사용하십시오.  
  
  
##  <a name="cross_database_queries"></a> Cross-Database Queries  
 DB_CHAINING 및 TRUSTWORTHY 데이터베이스 옵션은 기본적으로 OFF입니다. 원래 데이터베이스에 대해 이러한 옵션 중 하나가 ON으로 설정되어 있으면 대상 서버 인스턴스의 데이터베이스에서 해당 옵션을 설정해야 할 수도 있습니다. 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
 연결 및 분리 작업을 수행하면 해당 데이터베이스의 데이터베이스 간 소유권 체인을 사용할 수 없게 됩니다. 체인을 사용하도록 설정하는 방법은 [cross db ownership chaining 서버 구성 옵션](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)을 참조하세요.  
  
 자세한 내용은 [Trustworthy 속성을 사용하도록 미러 데이터베이스 설정&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)을 참조하세요.  
  
  
##  <a name="database_ownership"></a> 데이터베이스 소유권  
 데이터베이스를 다른 컴퓨터에서 복원하는 경우 복원 작업을 시작한 Windows 사용자 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 자동으로 새 데이터베이스 소유자가 됩니다. 데이터베이스를 복원할 때 시스템 관리자나 새 데이터베이스 소유자는 데이터베이스 소유권을 변경할 수 있습니다.  
  
##  <a name="distributed_queries_and_linked_servers"></a> 분산 쿼리 및 연결된 서버  
 분산 쿼리와 연결된 서버는 OLE DB 응용 프로그램에 대해 지원됩니다. 분산 쿼리는 같은 컴퓨터나 다른 컴퓨터에 있는 유형이 다른 여러 데이터 원본의 데이터에 액세스합니다. 연결된 서버를 구성하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 원격 서버에 있는 OLE DB 데이터 원본에 대해 명령을 실행할 수 있습니다. 이러한 기능에 대한 자세한 내용은 [연결된 서버&#40;데이터베이스 엔진&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)를 참조하세요.  
  
  
##  <a name="encrypted_data"></a> 암호화된 데이터  
 다른 서버 인스턴스에서 사용할 수 있도록 할 데이터베이스에 암호화된 데이터가 있으며 데이터베이스 마스터 키가 원래 서버의 서비스 마스터 키로 보호되는 경우 서비스 마스터 키 암호화를 다시 만들어야 할 수도 있습니다. *데이터베이스 마스터 키* 는 암호화된 데이터베이스에 있는 인증서의 개인 키와 비대칭 키를 보호하는 데 사용되는 대칭 키입니다. 데이터베이스 마스터 키는 생성 시에 Triple DES 알고리즘 및 사용자 제공 암호를 사용하여 암호화됩니다.  
  
 서버 인스턴스에서 데이터베이스 마스터 키의 자동 암호 해독을 설정하기 위해 서비스 마스터 키를 사용하여 이 키의 복사본을 암호화합니다. 이 암호화된 복사본은 해당 데이터베이스와 **master**에 모두 저장됩니다. 일반적으로 **master** 에 저장된 복사본은 마스터 키가 변경될 때마다 자동으로 업데이트됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 먼저 인스턴스의 서비스 마스터 키로 데이터베이스 마스터 키의 암호를 해독하려고 시도합니다. 암호 해독에 실패하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 마스터 키가 필요한 데이터베이스와 패밀리 GUID가 동일한 마스터 키 자격 증명을 자격 증명 저장소에서 검색합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 암호 해독이 성공하거나 남은 자격 증명이 없을 때까지 일치하는 각 자격 증명을 사용하여 데이터베이스 마스터 키의 암호화를 해독하려고 시도합니다. 서비스 마스터 키를 사용하여 암호화되지 않은 마스터 키는 OPEN MASTER KEY 문과 암호를 사용하여 열어야 합니다.  
  
 암호화된 데이터베이스를 복사 또는 복원하거나 새로운 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결할 때는 서비스 마스터 키로 암호화된 데이터베이스 마스터 키의 복사본이 대상 서버 인스턴스의 **master** 에 저장되지 않습니다. 대상 서버 인스턴스에서 해당 데이터베이스의 마스터 키를 열어야 합니다. 마스터 키를 열려면 OPEN MASTER KEY DECRYPTION BY PASSWORD **='***password***'** 문을 실행합니다. 그런 다음 ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY 문을 실행하여 데이터베이스 마스터 키의 자동 암호 해독을 설정하는 것이 좋습니다. 이 ALTER MASTER KEY 문은 서비스 마스터 키로 암호화된 데이터베이스 마스터 키의 복사본을 서버 인스턴스에 제공합니다. 자세한 내용은 [OPEN MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md) 및 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)를 참조하세요.  
  
 미러 데이터베이스의 데이터베이스 마스터 키 자동 암호 해독을 설정하는 방법은 [암호화된 미러 데이터베이스 설정](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)을 참조하세요.  
  
 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
-   [암호화된 미러 데이터베이스 설정](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)  
  
-   [두 서버에서 동일한 대칭 키 만들기](../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  
##  <a name="user_defined_error_messages"></a> User-defined Error Messages  
 사용자 정의 오류 메시지는 [sys.messages](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md) 카탈로그 뷰에 있습니다. 이 카탈로그 뷰는 **master**에 저장됩니다. 데이터베이스 응용 프로그램이 사용자 정의 오류 메시지를 사용하며 다른 서버 인스턴스에서 데이터베이스를 사용할 수 있는 경우 [sp_addmessage](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md) 를 사용하여 대상 서버 인스턴스에서 이러한 사용자 정의 메시지를 추가합니다.  

  
##  <a name="event_notif_and_wmi_events"></a> Event Notifications and Windows Management Instrumentation (WMI) Events (at Server Level)  
  
### <a name="server-level-event-notifications"></a>서버 수준 이벤트 알림  
 서버 수준 이벤트 알림은 **msdb**에 저장됩니다. 그러므로 데이터베이스 응용 프로그램이 서버 수준 이벤트 알림을 사용하는 경우 대상 서버 인스턴스에서 해당 이벤트 알림을 다시 만들어야 합니다. 서버 인스턴스의 이벤트 알림을 보려면 [sys.server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md) 카탈로그 뷰를 사용합니다. 자세한 내용은 [Event Notifications](../../relational-databases/service-broker/event-notifications.md)을 참조하세요.  
  
 또한 이벤트 알림은 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 사용하여 배달됩니다. 들어오는 메시지에 대한 경로는 서비스가 포함된 데이터베이스에 포함되지 않습니다. 대신 명시적인 경로는 **msdb**에 저장됩니다. 서비스가 **msdb** 데이터베이스에서 명시적인 경로를 사용하여 들어오는 메시지를 서비스에 라우팅하는 경우 다른 인스턴스에서 데이터베이스를 연결할 때 이 경로를 다시 만들어야 합니다.  
  
### <a name="windows-management-instrumentation-wmi-events"></a>WMI(Windows Management Instrumentation) 이벤트  
 서버 이벤트용 WMI 공급자는 WMI(Windows Management Instrumentation)를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이벤트를 모니터링할 수 있도록 합니다. 데이터베이스가 사용하는 WMI 공급자를 통해 표시된 서버 수준 이벤트를 사용하는 응용 프로그램은 대상 서버 인스턴스의 컴퓨터에서 정의해야 합니다. WMI 이벤트 공급자는 **msdb**에서 정의한 대상 서비스로 이벤트 알림을 만듭니다.  
  
> **참고:** 자세한 내용은 [서버 이벤트용 WMI 공급자 개념](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)을 참조하세요.  
  
 **SQL Server Management Studio를 사용하여 WMI 경고를 만들려면**  
  
-   [WMI 이벤트 경고 만들기](../../ssms/agent/create-a-wmi-event-alert.md)  
  
### <a name="how-event-notifications-work-for-a-mirrored-database"></a>미러된 데이터베이스에 대한 이벤트 알림의 작동 방식  
 미러된 데이터베이스를 포함하는 이벤트 알림의 데이터베이스 간 배달은 미러된 데이터베이스가 장애 조치(Failover)될 수 있으므로 정의상 원격일 수밖에 없습니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 는 *미러된 경로*의 형태로 미러된 데이터베이스에 대해 특별한 지원을 제공합니다. 미러된 경로에는 두 개의 주소가 있습니다. 하나는 주 서버 인스턴스에 대한 주소이며 다른 하나는 미러 서버 인스턴스에 대한 주소입니다.  
  
 미러된 경로를 설정하여 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 라우팅에서 데이터베이스 미러링을 인식하도록 지정할 수 있습니다. 미러된 경로를 사용하여 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 에서 현재 주 서버 인스턴스에 대화를 투명하게 리디렉션할 수 있습니다. 예를 들어 미러된 데이터베이스인 Database_A가 Service_A라는 서비스를 호스팅하는데 이 Service_A와 대화를 하기 위해 Database_B가 호스팅하는 Service_B라는 다른 서비스가 필요한 경우 이 대화를 가능하게 하려면 Database_B에 Service_A에 대해 미러된 경로가 포함되어야 합니다. 또한 Database_A에 로컬 경로와는 달리 장애 조치 후에 유효한 상태로 남아 있는 Service_B에 대한 미러되지 않은 TCP 전송 경로가 포함되어야 합니다. 이러한 경로로 인해 ACK가 장애 조치 후에 원래 상태로 돌아옵니다. 보낸 사람의 서비스는 항상 동일한 방식으로 명명되므로 경로는 Broker 인스턴스를 지정해야 합니다.  
  
 미러된 경로에 대한 요구 사항은 미러된 데이터베이스의 서비스가 시작자 서비스인지 대상 서비스인지에 관계없이 적용합니다.  
  
-   대상 서비스가 미러된 데이터베이스에 있으면 시작자 서비스는 미러된 경로를 대상으로 되돌려야 합니다. 그러나 대상이 정규 경로를 시작자로 되돌릴 수 있습니다.  
  
-   시작자 서비스가 미러된 데이터베이스에 있으면 대상 서비스는 승인 및 응답을 배달하기 위해 미러된 경로를 시작자로 되돌려야 합니다. 그러나 시작자가 정규 경로를 대상으로 되돌릴 수 있습니다.  
  
  
##  <a name="extended_stored_procedures"></a> Extended Stored Procedures  
  
> **중요!** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 [CLR 통합](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) 을 사용하세요.  
  
 확장 저장 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장 저장 프로시저 API를 사용하여 프로그래밍합니다. **sysadmin** 고정 서버 역할의 멤버는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 확장 저장 프로시저를 등록하고 사용자에게 이 프로시저를 실행할 권한을 부여할 수 있습니다. **master** 데이터베이스에만 확장 저장 프로시저를 추가할 수 있습니다.  
  
 확장 저장 프로시저는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 주소 공간에서 직접 실행되며 메모리 손실 및 서버의 성능과 안정성을 저하시키는 다른 문제를 유발할 수 있습니다. 참조되는 데이터가 들어 있는 인스턴스와는 별도의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 확장 저장 프로시저를 저장해야 합니다. 또한 분산 쿼리를 사용하여 데이터베이스에 액세스해야 합니다.  
  
  > [!IMPORTANT]
  > 시스템 관리자는 확장 저장 프로시저를 서버에 추가하고 다른 사용자에게 EXECUTE 권한을 부여하기 전에 각 확장 저장 프로시저를 철저히 검토하여 유해한 악성 코드가 포함되지는 않았는지를 확인해야 합니다.  
  
 자세한 내용은 [GRANT 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md), [DENY 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md) 및 [REVOKE 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)을 참조하세요.  
  
  
##  <a name="ifts_service_properties"></a> SQL Server용 전체 텍스트 엔진 속성  
 속성은 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)에 의해 전체 텍스트 엔진에 설정됩니다. 대상 서버 인스턴스에 해당 속성에 필요한 설정이 있는지 확인합니다. 이러한 속성에 대한 자세한 내용은 [FULLTEXTSERVICEPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)를 참조하세요.  
  
 또한 원래 서버 인스턴스와 대상 서버 인스턴스에 있는 [단어 분리기 및 형태소 분석기](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) 구성 요소 또는 [전체 텍스트 검색 필터](../../relational-databases/search/configure-and-manage-filters-for-search.md) 구성 요소의 버전이 서로 다르면 전체 텍스트 인덱스 및 쿼리가 다르게 동작할 수 있습니다. 또한 [동의어 사전](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md) 은 인스턴스별 파일에 저장됩니다. 이러한 파일의 복사본을 대상 서버 인스턴스의 해당 위치로 전송하거나 새 인스턴스에서 다시 만들어야 합니다.  
  
> **참고:** [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서버 인스턴스에 전체 텍스트 카탈로그 파일이 포함된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스를 연결할 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서와 같이 다른 데이터베이스 파일과 함께 이전 위치에서 카탈로그 파일이 연결됩니다. 자세한 내용은 [전체 텍스트 검색 업그레이드](../../relational-databases/search/upgrade-full-text-search.md)를 참조하세요.  
  
 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [전체 텍스트 카탈로그와 인덱스 백업 및 복원](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
-   [데이터베이스 미러링 및 전체 텍스트 카탈로그&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-full-text-catalogs-sql-server.md)  

  
##  <a name="jobs"></a> 작업  
 데이터베이스에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 사용하는 경우 대상 서버 인스턴스에서 해당 작업을 다시 만들어야 합니다. 작업은 해당 환경에 따라 달라집니다. 대상 서버 인스턴스에서 기존 작업을 다시 만드는 경우 원래 서버 인스턴스의 작업 환경과 일치하도록 대상 서버 인스턴스를 수정해야 할 수도 있습니다. 중요한 환경 요소는 다음과 같습니다.  
  
-   작업에 사용되는 로그인  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 만들거나 실행하려면 먼저 작업에 필요한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 대상 서버 인스턴스에 추가해야 합니다. 자세한 내용은 [SQL Server 에이전트 작업을 만들고 관리하도록 사용자 구성](../../ssms/agent/configure-a-user-to-create-and-manage-sql-server-agent-jobs.md)을 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 시작 계정  
  
     서비스 시작 계정은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에이전트를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 계정과 해당 네트워크 사용 권한을 정의합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 지정된 사용자 계정으로 실행됩니다. 에이전트 서비스의 컨텍스트는 작업과 실행 환경에 대한 설정에 영향을 줍니다. 계정이 작업에 필요한 네트워크 공유 등의 리소스에 액세스할 수 있어야 합니다. 서비스 시작 계정을 선택하고 수정하는 방법은 [SQL Server 에이전트 서비스의 계정 선택](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)을 참조하세요.  
  
     서비스 시작 계정이 올바르게 작동하려면 올바른 도메인, 파일 시스템 및 레지스트리 권한을 구성해야 합니다. 서비스 계정에 대해 구성해야 하는 공유 네트워크 리소스가 작업에 필요할 수도 있습니다. 자세한 내용은 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)을 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트 서비스에는 자체 레지스트리 하이브가 있으며 일반적으로 해당 작업은 이 레지스트리 하이브의 하나 또는 그 이상의 설정에 종속되어 있습니다. 작업이 의도한 대로 동작하려면 이러한 레지스트리 설정이 필요합니다. 스크립트를 사용하여 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에서 작업을 다시 만들면 해당 작업에 대한 레지스트리 설정이 올바르지 않을 수 있습니다. 다시 만든 작업이 대상 서버 인스턴스에서 올바르게 동작하려면 원래 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스와 대상 SQL Server 에이전트 서비스의 레지스트리 설정이 같아야 합니다.  
  
    > [!CAUTION]  
    >  현재 설정이 다른 작업에 필요한 경우 다시 만든 작업을 처리하기 위해 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스의 레지스트리 설정을 변경하는 것이 문제가 될 수 있습니다. 또한 레지스트리를 올바르게 편집하지 않으면 시스템에 심각한 손상을 줄 수 있습니다. 따라서 레지스트리를 변경하기 전에 컴퓨터의 중요한 데이터는 백업해 두는 것이 좋습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시는 지정된 작업 단계의 보안 컨텍스트를 정의합니다. 작업이 대상 서버 인스턴스에서 실행되려면 해당 인스턴스에서 수동으로 필요한 모든 프록시를 다시 만들어야 합니다. 자세한 내용은 [SQL Server 에이전트 프록시 만들기](../../ssms/agent/create-a-sql-server-agent-proxy.md) 및 [프록시를 사용하는 다중 서버 작업 문제 해결](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)을 참조하세요.  
  
 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [작업 구현](../../ssms/agent/implement-jobs.md)  
  
-   [역할 전환 후 로그인 및 작업 관리&#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)(데이터베이스 미러링의 경우)  
  
-   [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 설치하는 경우)  
  
-   [SQL Server 에이전트 구성](../../ssms/agent/configure-sql-server-agent.md) ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 설치하는 경우)  
  
-   [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)  
  
 **기존 작업과 해당 속성을 보려면**  
  
-   [작업 활동 모니터링](../../ssms/agent/monitor-job-activity.md)  
  
-   [sp_help_job&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)  
  
-   [작업 단계 정보 보기](../../ssms/agent/view-job-step-information.md)  
  
-   [dbo.sysjobs&#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)  
  
 **작업을 만들려면**  
  
-   [작업 만들기](../../ssms/agent/create-a-job.md)  
  
-   [작업 만들기](../../ssms/agent/create-a-job.md)  
  
#### <a name="best-practices-for-using-a-script-to-re-create-a-job"></a>스크립트를 사용하여 작업을 다시 만드는 최상의 방법  
 먼저 간단한 작업을 스크립팅하고 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에서 작업을 다시 만든 다음 작업을 실행하여 의도한 대로 작동하는지 확인하는 것이 좋습니다. 이렇게 하면 비호환성을 확인하고 해결할 수 있습니다. 스크립팅한 작업이 새 환경에서 의도한 대로 작동하지 않을 경우 이와 동등하면서 해당 환경에서 올바르게 작동하는 작업을 만드는 것이 좋습니다.  
  

##  <a name="logins"></a> 로그인  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 로그인하려면 올바른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 필요합니다. 이 로그인은 보안 주체가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결할 수 있는지 여부를 확인하는 인증 프로세스에서 사용됩니다. 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 서버 인스턴스에서 정의되지 않았거나 잘못 정의되어 있는 데이터베이스 사용자는 이 인스턴스에 로그인할 수 없습니다. 이러한 사용자는 해당 서버 인스턴스에 있는 데이터베이스의 *분리된 사용자* 라고 합니다. 데이터베이스가 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 복원, 연결 또는 복사된 후에도 데이터베이스 사용자가 분리될 수 있습니다.  
  
 데이터베이스의 원래 복사본에 있는 일부 또는 모든 개체에 대해 스크립트를 생성하려면 스크립트 생성 마법사를 사용하고 **스크립트 옵션 선택** 대화 상자에서 **로그인 스크립팅** 옵션을 **True**로 설정합니다.  
  
> **참고:** 미러된 데이터베이스에 대한 로그인을 설정하는 방법은 [데이터베이스 미러링 또는 Always On 가용성 그룹에 대한 로그인 계정 설정(SQL Server)](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md) 및 [역할 전환 후 로그인 및 작업 관리&#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)를 참조하세요.  
  
  
##  <a name="permissions"></a> 사용 권한  
 데이터베이스를 다른 서버 인스턴스에서 사용할 수 있을 때 다음의 사용 권한 유형이 영향을 받을 수 있습니다.  
  
-   시스템 개체에 대한 GRANT, REVOKE 또는 DENY 권한  
  
-   서버 인스턴스에 대한 GRANT, REVOKE 또는 DENY 권한(*서버 수준 사용 권한*)  
  
### <a name="grant-revoke-and-deny-permissions-on-system-objects"></a>시스템 개체에 대한 GRANT, REVOKE 또는 DENY 권한  
 저장 프로시저, 확장 저장 프로시저, 함수 및 뷰와 같은 시스템 개체에 대한 사용 권한은 **master** 데이터베이스에 저장되며 대상 서버 인스턴스에서 구성해야 합니다.  
  
 데이터베이스의 원래 복사본에 있는 일부 또는 모든 개체에 대해 스크립트를 생성하려면 스크립트 생성 마법사를 사용하고 **스크립트 옵션 선택** 대화 상자에서 **개체 수준 사용 권한 스크립팅** 옵션을 **True**로 설정합니다.  
  
   > [!IMPORTANT]
   > 로그인을 스크립팅하는 경우 암호는 스크립팅되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 로그인이 있으면 대상에서 스크립트를 수정해야 합니다.  
  
 시스템 개체는 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) 카탈로그 뷰에 표시됩니다. 시스템 개체에 대한 사용 권한은 **master** 데이터베이스의 [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) 카탈로그 뷰에 표시됩니다. 이러한 카탈로그 뷰를 쿼리하고 시스템 개체 사용 권한을 부여하는 방법은 [GRANT 시스템 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)을 참조하세요. 자세한 내용은 [REVOKE 시스템 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md) 및 [DENY 시스템 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)을 참조하세요.  
  
### <a name="grant-revoke-and-deny-permissions-on-a-server-instance"></a>서버 인스턴스에 대한 GRANT, REVOKE 또는 DENY 권한  
 서버 범위의 사용 권한은 **master** 데이터베이스에 저장되며 대상 서버 인스턴스에서 구성해야 합니다. 서버 인스턴스의 서버 사용 권한에 대한 자세한 내용을 보려면 [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) 카탈로그 뷰를 쿼리하세요. 서버 보안 주체에 대한 자세한 내용을 보려면 [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) 카탈로그 뷰를 쿼리하세요. 서버 역할의 멤버 자격에 대한 자세한 내용을 보려면 [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) 카탈로그 뷰를 쿼리하세요.  
  
 자세한 내용은 [GRANT 서버 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md), [REVOKE 서버 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md) 및 [DENY 서버 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)을 참조하세요.  
  
#### <a name="server-level-permissions-for-a-certificate-or-asymmetric-key"></a>인증서 또는 비대칭 키에 대한 서버 수준 사용 권한  
 인증서 또는 비대칭 키에 직접 서버 수준 사용 권한을 부여할 수는 없습니다. 대신 서버 수준 사용 권한은 특정 인증서나 비대칭 키 전용으로 만든 매핑된 로그인에 부여됩니다. 그러므로 서버 수준 사용 권한이 필요한 각 인증서 또는 비대칭 키에 해당 *인증서 매핑 로그인* 이나 *비대칭 키 매핑 로그인*이 필요합니다. 인증서나 비대칭 키에 서버 수준 사용 권한을 부여하려면 해당 매핑된 로그인에 사용 권한을 부여합니다.  
  
> **참고:** 매핑된 로그인은 해당 인증서나 비대칭 키로 서명된 코드의 권한 부여를 위해서만 사용됩니다. 매핑된 로그인은 인증에 사용할 수 없습니다.  
  
 매핑된 로그인과 해당 사용 권한은 모두 **master**에 있습니다. 인증서나 비대칭 키가 **master**이외의 데이터베이스에 있을 경우 **master** 에서 다시 만들어 로그인에 매핑해야 합니다. 데이터베이스를 다른 서버 인스턴스로 이동, 복사 또는 복원하는 경우 대상 서버 인스턴스의 **master** 데이터베이스에서 해당 인증서나 비대칭 키를 다시 만들어 로그인에 매핑한 다음 필요한 서버 수준 사용 권한을 로그인에 부여해야 합니다.  
  
 **인증서나 비대칭 키를 만들려면**  
  
-   [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
  
 **인증서나 비대칭 키를 로그인에 매핑하려면**  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
 **매핑된 로그인에 사용 권한을 할당하려면**  
  
-   [GRANT 서버 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)  
  
 인증서 및 비대칭 키에 대한 자세한 내용은 [Encryption Hierarchy](../../relational-databases/security/encryption/encryption-hierarchy.md)을 참조하십시오.  
  
## <a name="trustworthy-property"></a>Trustworthy 속성
TRUSTWORHTY 데이터베이스 속성은 SQL Server 인스턴스가 데이터베이스 및 그 내용을 트러스트하는지 여부를 나타내는 데 사용됩니다. 데이터베이스가 연결된 경우 원래 서버에 이 옵션이 ON으로 설정된 경우에도 기본적으로 보안을 위해 이 옵션이 OFF로 설정됩니다. 이 속성에 대한 자세한 내용은 [TRUSTWORTHY 데이터베이스 속성](../security/trustworthy-database-property.md)을 참조하세요. 이 옵션을 ON으로 설정하는 방법에 대한 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  


##  <a name="replication_settings"></a> Replication Settings  
 복제된 데이터베이스의 백업을 다른 서버 또는 데이터베이스로 복원할 경우 복제 설정은 유지되지 않습니다. 이 경우 백업 복원 후 모든 게시 및 구독을 다시 만들어야 합니다. 이 프로세스를 간단하게 하려면 현재 복제 설정과 복제 설정 및 해제에 대한 스크립트를 만듭니다. 편리하게 복제 설정을 다시 만들려면 이러한 스크립트를 복사하고 대상 서버 인스턴스에서 작동하도록 서버 이름 참조를 변경합니다.  
  
 자세한 내용은 [복제된 데이터베이스 백업 및 복원](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md), [데이터베이스 미러링 및 복제&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md), [로그 전달 및 복제&#40;SQL Server&#41;](../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)를 참조하세요.  
  
  
##  <a name="sb_applications"></a> Service Broker 응용 프로그램  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 응용 프로그램의 많은 부분이 데이터베이스와 함께 이동됩니다. 그러나 응용 프로그램의 일부분은 새 위치에서 다시 만들거나 다시 구성해야 합니다.  다른 서버에서 데이터베이스가 연결된 경우 기본적으로 보안을 위해 *is_broker_enabled* 및 *is_honoor_broker_priority_on* 옵션이 OFF로 설정됩니다. 이러한 옵션을 ON으로 설정하는 방법에 대한 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
  
##  <a name="startup_procedures"></a> Startup Procedures  
 시작 프로시저는 자동 실행되도록 표시되었으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시작될 때마다 실행되는 저장 프로시저입니다. 데이터베이스가 시작 프로시저에 따라 달라지는 경우 대상 서버 인스턴스에서 해당 프로시저를 정의하고 시작 시 자동으로 실행되도록 구성해야 합니다.  

  
##  <a name="triggers"></a> Triggers (at Server Level)  
 DDL 트리거는 다양한 DDL(데이터 정의 언어) 이벤트에 대한 응답으로 저장 프로시저를 실행합니다. 이러한 이벤트는 주로 CREATE, ALTER 및 DROP 키워드로 시작하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 해당합니다. DDL과 같은 작업을 수행하는 특정 시스템 저장 프로시저에서 DDL 트리거가 발생할 수도 있습니다.  
  
 이 기능에 대한 자세한 내용은 [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md)를 참조하십시오.  
  
  
## <a name="see-also"></a>참고 항목  
 [포함된 데이터베이스](../../relational-databases/databases/contained-databases.md)   
 [데이터베이스를 다른 서버로 복사](../../relational-databases/databases/copy-databases-to-other-servers.md)   
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [로그 전달 보조 데이터베이스로 장애 조치(failover)&#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)   
 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [암호화된 미러 데이터베이스 설정](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)   
 [분리된 사용자 문제 해결&#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)  
  
  
