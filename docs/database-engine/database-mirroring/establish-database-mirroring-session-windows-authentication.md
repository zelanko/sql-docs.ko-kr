---
title: 데이터베이스 미러링 세션 설정 - Windows 인증 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], sessions
ms.assetid: 7cb418d6-dce1-4a0d-830e-9c5ccfe3bd72
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a33e5f09ee0bda2bb1967b90902e47663f1846be
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52522318"
---
# <a name="establish-database-mirroring-session---windows-authentication"></a>데이터베이스 미러링 세션 설정 - Windows 인증
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]을 대신 사용합니다.  
  
 데이터베이스 미러링 세션을 설정하고 데이터베이스에 대한 데이터베이스 미러링 속성을 수정하려면 **데이터베이스 속성** 대화 상자의 **미러링** 페이지를 사용합니다. **미러링** 페이지를 사용하여 데이터베이스 미러링을 구성하기 전에 다음 요구 사항이 충족되었는지 확인합니다.  
  
-   주 서버 인스턴스 및 미러 서버 인스턴스에서는 같은 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](Standard 또는 Enterprise)를 실행해야 합니다. 또한 서버 인스턴스는 동일한 작업을 처리할 수 있는 동등한 시스템에서 실행하는 것이 좋습니다.  
  
    > [!NOTE]  
    >  미러링 모니터 서버 인스턴스는 일부 버전의 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서만 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
-   최신 상태의 미러 데이터베이스가 있어야 합니다.  
  
     미러 데이터베이스를 만들려면 WITH NORECOVERY를 사용하여 미러 서버 인스턴스에서 주 데이터베이스의 최근 백업을 복원해야 합니다. 또한 전체 백업 후에 로그 백업을 하나 이상 만들고 WITH NORECOVERY를 사용하여 순서대로 미러 데이터베이스에 복원해야 합니다. 자세한 내용은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)에서만 사용할 수 있습니다.  
  
-   서버 인스턴스가 여러 도메인 사용자 계정으로 실행되는 경우 각 계정의 로그인이 다른 계정의 **master** 데이터베이스에 있어야 합니다. 로그인이 없으면 미러링을 구성하기 전에 만들어야 합니다. 자세한 내용은 [Windows 인증을 사용하여 데이터베이스 미러링 엔드포인트에 대한 네트워크 액세스 허용&amp;#40;SQL Server&amp;#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)을 참조하세요.  
  
### <a name="to-configure-database-mirroring"></a>데이터베이스 미러링을 구성하려면  
  
1.  주 서버 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 미러링할 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 선택한 다음 **미러**를 클릭합니다. **데이터베이스 속성** 대화 상자의 **미러링** 페이지가 열립니다.  
  
4.  미러링 구성을 시작하려면 **보안 구성** 을 클릭하여 데이터베이스 미러링 보안 구성 마법사를 시작합니다.  
  
    > [!NOTE]  
    >  데이터베이스 미러링 세션 중에 미러링 모니터 서버 인스턴스를 추가하거나 변경하기 위한 용도로만 이 마법사를 사용할 수 있습니다.  
  
5.  데이터베이스 미러링 보안 구성 마법사를 사용하면 자동으로 각 서버 인스턴스에 데이터베이스 미러링 엔드포인트가 생성되고(없는 경우) 서버 인스턴스의 역할(**주 서버**, **미러 서버**또는 **미러링 모니터 서버**)에 해당하는 필드에 서버 네트워크 주소가 입력됩니다.  
  
    > [!IMPORTANT]  
    >  엔드포인트를 만드는 경우 데이터베이스 미러링 보안 구성 마법사에서 항상 Windows 인증을 사용합니다. 마법사에서 인증서 기반 인증을 사용하려면 각 서버 인스턴스의 인증서를 사용하도록 미러링 엔드포인트가 구성되어 있어야 합니다. 또한 마법사의 **서비스 계정** 대화 상자에 있는 모든 필드가 비어 있어야 합니다. 인증서를 사용할 데이터베이스 미러링 엔드포인트를 만드는 방법은 [CREATE ENDPOINT&amp;#40;Transact-SQL&amp;#41;](../../t-sql/statements/create-endpoint-transact-sql.md)를 참조하세요.  
  
6.  선택적으로 운영 모드를 변경합니다. 특정 운영 모드의 가용성은 미러링 모니터에 TCP 주소를 지정했는지 여부에 따라 다릅니다. 다음과 같은 옵션이 있습니다.  
  
    |옵션|미러링 모니터 여부|설명|  
    |------------|--------------|-----------------|  
    |**성능 우선(비동기)**|Null(있어도 사용되지 않지만 세션에 쿼럼이 필요함)|성능을 최대화하기 위해 미러 데이터베이스는 항상 주 데이터베이스와 시간 간격을 두며 앞서가지 않습니다. 그러나 두 데이터베이스의 시간 간격은 일반적으로 크지 않습니다. 파트너가 손실되면 다음과 같은 결과가 나타납니다.<br /><br /> 미러 서버 인스턴스를 사용할 수 없는 경우 주 서버 인스턴스가 계속합니다.<br /><br /> 주 서버 인스턴스를 사용할 수 없는 경우 미러 서버 인스턴스가 중지되지만 세션에 권장된 미러링 모니터 서버가 없거나 미러링 모니터 서버가 미러 서버에 연결되어 있으면 웜 대기로 미러 서버에 액세스할 수 있습니다. 데이터베이스 소유자는 미러 서버 인스턴스에 서비스를 강제 적용할 수 있으며 이 경우 데이터가 손실될 수 있습니다.<br /><br /> <br /><br /> 자세한 내용은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)에서만 사용할 수 있습니다.|  
    |**자동 장애 조치(Failover)가 없는 보호 우선(동기)**|아니오|커밋된 모든 트랜잭션이 미러 서버의 디스크에 기록됩니다.<br /><br /> 파트너가 서로 연결되어 있으며 데이터베이스가 동기화된 경우 수동 장애 조치를 사용할 수 있습니다.<br /><br /> 파트너가 손실되면 다음과 같은 결과가 나타납니다.<br /><br /> 미러 서버 인스턴스를 사용할 수 없는 경우 주 서버 인스턴스가 계속합니다.<br /><br /> 주 서버 인스턴스를 사용할 수 없는 경우 미러 서버 인스턴스가 중지되지만 웜 대기로 액세스할 수 있습니다. 데이터베이스 소유자는 미러 서버 인스턴스에 서비스를 강제 적용할 수 있으며 이 경우 데이터가 손실될 수 있습니다.<br /><br /> <br /><br /> 자세한 내용은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)에서만 사용할 수 있습니다.|  
    |**자동 장애 조치(Failover)가 있는 보호 우선(동기)**|예(필수)|커밋된 모든 트랜잭션이 미러 서버의 디스크에 기록됩니다.<br /><br /> 자동 장애 조치를 지원하도록 미러링 모니터 서버 인스턴스를 포함하여 가용성을 최대화합니다. 미러링 모니터 서버 주소를 먼저 지정한 경우에만 **자동 장애 조치(failover)가 있는 보호 우선(동기)** 옵션을 선택할 수 있습니다.<br /><br /> 파트너가 서로 연결되어 있으며 데이터베이스가 동기화된 경우 수동 장애 조치를 사용할 수 있습니다.<br /><br /> 미러링 모니터 서버가 있을 경우 파트너가 손실되면 다음과 같은 결과가 나타납니다.<br /><br /> 주 서버 인스턴스를 사용할 수 없는 경우 자동 장애 조치가 수행됩니다. 미러 서버 인스턴스가 주 서버 인스턴스의 역할로 전환하여 해당 데이터베이스를 주 데이터베이스로 제공합니다.<br /><br /> 미러 서버 인스턴스를 사용할 수 없는 경우 주 서버 인스턴스가 계속합니다.<br /><br /> <br /><br /> 자세한 내용은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)에서만 사용할 수 있습니다.<br /><br /> **&#42;&#42; 중요 &#42;&#42;** 미러링 모니터 서버의 연결이 끊어지면 파트너가 서로 연결되어 있어야만 데이터베이스를 사용할 수 있습니다. 자세한 내용은 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.|  
  
7.  다음 조건을 모두 만족하면 **미러링 시작** 을 클릭하여 미러링을 시작합니다.  
  
    -   현재 주 서버 인스턴스에 연결되어 있습니다.  
  
    -   보안이 올바로 구성되었습니다.  
  
    -   **서버 네트워크 주소** 섹션에 주 서버 및 미러 서버 인스턴스의 정규화된 TCP 주소가 지정되어 있습니다.  
  
    -   운영 모드가 **자동 장애 조치(failover)가 있는 보호 우선(동기)** 으로 설정되어 있는 경우 미러링 모니터 서버 인스턴스의 정규화된 TCP 주소도 지정됩니다.  
  
8.  미러링이 시작된 후 운영 모드를 변경하고 **확인**을 클릭하여 변경 사항을 저장할 수 있습니다. 미러링 모니터 서버 주소를 먼저 지정한 경우에만 자동 장애 조치(Failover)가 있는 보호 우선 모드로 전환할 수 있습니다.  
  
    > [!NOTE]  
    >  미러링 모니터 서버를 제거하려면 **미러링 모니터 서버** 필드에서 서버 네트워크 주소를 삭제합니다. 자동 장애 조치(failover)가 있는 보호 우선 모드에서 성능 우선 모드로 전환하면 **미러링 모니터 서버** 필드가 자동으로 지워집니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)   
 [데이터베이스 속성&#40;미러링 페이지&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [데이터베이스 미러링 세션 일시 중지 또는 재개&#40;SQL Server&#41;](../../database-engine/database-mirroring/pause-or-resume-a-database-mirroring-session-sql-server.md)   
 [Trustworthy 속성을 사용하도록 미러 데이터베이스 설정&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)   
 [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-database-mirroring-sql-server.md)   
 [역할 전환 후 로그인 및 작업 관리&#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)   
 [데이터베이스 미러링 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [데이터베이스 미러링 모니터 서버 추가 또는 바꾸기&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
  
