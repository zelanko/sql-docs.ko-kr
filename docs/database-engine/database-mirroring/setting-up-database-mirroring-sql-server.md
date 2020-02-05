---
title: 데이터베이스 미러링 설정(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
ms.assetid: da45efed-55eb-4c71-be34-ac2589dfce8d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 43c964db4c0231d15101f58b7af088bc239fe152
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68048092"
---
# <a name="setting-up-database-mirroring-sql-server"></a>데이터베이스 미러링 설정(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 섹션에서는 데이터베이스 미러링을 설정하기 위한 사전 요구 사항, 권장 사항 및 단계에 대해 설명합니다. 데이터베이스 미러링에 대한 소개는 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  구성이 성능에 영향을 줄 수 있으므로 사용률이 낮은 시간에 데이터베이스 미러링을 구성하는 것이 좋습니다.  
  
  
##  <a name="PrepareInstances"></a> 미러 서버를 호스팅하도록 서버 인스턴스 준비  
 각 데이터베이스 미러링 세션에 대해 다음을 준비합니다.  
  
1.  주 서버, 미러 서버 및 미러링 모니터 서버(있는 경우)는 별도의 호스트 시스템에 있는 개별 서버 인스턴스로 호스팅되어야 합니다. 각 서버 인스턴스에는 데이터베이스 미러링 엔드포인트가 필요합니다. 데이터베이스 미러링 엔드포인트를 만들어야 할 경우 다른 서버 인스턴스에 액세스할 수 있는지 확인합니다.  
  
     서버 인스턴스에서 데이터베이스 미러링에 사용하는 인증 형식은 데이터베이스 미러링 엔드포인트의 속성입니다. 데이터베이스 미러링에서 사용할 수 있는 두 가지 전송 보안 유형으로 Windows 인증과 인증서 기반 인증이 있습니다. 자세한 내용은 [데이터베이스 미러링 및 Always On 가용성 그룹에 대한 전송 보안&#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)을 참조하세요.  
  
     네트워크 액세스에 대한 요구 사항은 다음과 같은 인증 형태에 따라 달라집니다.  
  
    -   **Windows 인증을 사용하는 경우**  
  
         서버 인스턴스가 여러 도메인 사용자 계정으로 실행되는 경우 각 인스턴스는 다른 인스턴스의 **master** 데이터베이스에서 로그인을 필요로 합니다. 따라서 로그인이 없으면 만들어야 합니다. 자세한 내용은 [Windows 인증을 사용하여 데이터베이스 미러링 엔드포인트에 대한 네트워크 액세스 허용&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)을 참조하세요.  
  
    -   **인증서를 사용하는 경우**  
  
         지정된 서버 인스턴스에서 데이터베이스 미러링에 인증서 인증을 사용하려면 시스템 관리자가 아웃바운드 및 인바운드 연결 모두에 인증서를 사용하도록 각 서버 인스턴스를 구성해야 합니다. 이 경우 아웃바운드 연결을 먼저 구성해야 합니다. 자세한 내용은 [데이터베이스 미러링 엔드포인트에 대한 인증서 사용&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)을 참조하세요.  
  
2.  미러 서버에 모든 데이터베이스 사용자에 대한 로그인이 있는지 확인하십시오. 자세한 내용은 [데이터베이스 미러링 또는 Always On 가용성 그룹에 대한 로그인 계정 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)을 참조하세요.  
  
3.  미러 데이터베이스를 호스팅하는 서버 인스턴스에서 미러링된 데이터베이스에 필요한 환경의 남은 부분을 설정합니다. 자세한 내용은 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)을 참조하세요.  
  
##  <a name="EstablishUsingWinAuthentication"></a> 개요: 데이터베이스 미러링 세션 설정  
 미러링 세션을 설정하는 기본 단계는 다음과 같습니다.  
  
1.  모든 복원 작업에서 RESTORE WITH NORECOVERY를 사용하여 다음 백업을 복원해서 미러 데이터베이스를 만듭니다.  
  
    1.  백업을 수행할 때 주 데이터베이스가 이미 전체 복구 모델을 사용 중이었는지 확인한 후 주 데이터베이스의 최근 전체 데이터베이스 백업을 복원합니다. 미러 데이터베이스는 주 데이터베이스와 이름이 동일해야 합니다.  
  
    2.  복원된 전체 백업 이후 데이터베이스에 대해 차등 백업을 수행한 경우 가장 최근의 차등 백업을 복원합니다.  
  
    3.  전체 또는 차등 데이터베이스 백업 이후 수행된 모든 로그 백업을 복원합니다.  
  
     자세한 내용은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)을 사용합니다.  
  
    > [!IMPORTANT]  
    >  주 데이터베이스의 백업을 수행한 다음 가능한 빨리 남은 설정 단계를 완료하십시오. 파트너에서 미러링을 시작할 수 있으려면 먼저 원래 데이터베이스에서 현재 로그 백업을 만든 다음 후속 미러 데이터베이스로 복원해야 합니다.  
  
2.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 데이터베이스 미러링 마법사를 사용하여 미러링을 설정할 수 있습니다. 자세한 내용은 다음 중 하나를 참조하십시오.  
  
    -   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
  
    -   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
3.  기본적으로 세션은 전체 트랜잭션 보안으로 설정되므로(SAFETY가 FULL로 설정됨) 자동 장애 조치를 지원하지 않는 동기 보호 우선 모드로 세션이 시작됩니다. 이러한 세션을 다음과 같이 자동 장애 조치(Failover)가 있는 보호 우선 모드나 비동기 성능 우선 모드에서 실행되도록 다시 구성할 수 있습니다.  
  
    -   **자동 장애 조치 있는 보호 우선 모드**  
  
         자동 장애 조치(Failover)가 있는 보호 우선 모드로 세션을 실행하려면 미러링 모니터 서버 인스턴스를 추가합니다.  
  
         **미러링 모니터 서버를 추가하려면**  
  
        -   [Windows 인증을 사용하여 데이터베이스 미러링 모니터 추가&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
        -   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
        > [!NOTE]  
        >  데이터베이스 소유자는 언제든지 데이터베이스의 미러링 모니터를 해제할 수 있습니다. 미러링 모니터를 해제하면 미러링 모니터가 없는 것과 마찬가지로 자동 장애 조치가 실행되지 않습니다.  
  
    -   **성능 우선 모드**  
  
         자동 장애 조치 기능을 지원하지 않고 가용성보다 성능을 우선하려면 트랜잭션 보안을 해제합니다. 자세한 내용은 [데이터베이스 미러링 세션에서 트랜잭션 보안 변경&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)을 참조하세요.  
  
        > [!NOTE]  
        >  성능 우선 모드에서는 WITNESS를 OFF로 설정해야 합니다. 자세한 내용은 [쿼럼: 미러링 모니터 서버가 데이터베이스 가용성에 미치는 영향&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)을 참조하세요.  
  
> [!NOTE]  
>  Microsoft Windows 인증을 사용하여 데이터베이스 미러링을 설정하기 위해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하는 예제는 [예제: Windows 인증을 사용하여 데이터베이스 미러링 설정&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-windows-authentication-transact-sql.md)을 참조하세요.  
>   
>  Microsoft Windows 인증을 사용하여 데이터베이스 미러링을 설정하기 위해 [!INCLUDE[tsql](../../includes/tsql-md.md)] 을 사용하는 예제는 [예: 인증서를 사용하여 데이터베이스 미러링 설정&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)을 참조하세요.  
  
  
##  <a name="InThisSection"></a> 섹션 내용  
 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
 일시 중단된 세션을 재개하기 전에 미러 데이터베이스를 만들거나 준비하는 단계를 요약합니다. 또한 방법 도움말 항목에 대한 링크를 제공합니다.  
  
 [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
 서버 네트워크 주소의 구문, 주소로 서버 인스턴스의 데이터베이스 미러링 엔드포인트를 식별하는 방법 및 시스템의 정규화된 도메인 이름을 찾는 방법에 대해 설명합니다.  
  
 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
 데이터베이스 미러링 보안 구성 마법사를 사용하여 데이터베이스에서 데이터베이스 미러링을 시작하는 방법에 대해 설명합니다.  
  
 [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
 데이터베이스 미러링을 설정하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 단계에 대해 설명합니다.  
  
 [예제: Windows 인증을 사용하여 데이터베이스 미러링 설정&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-windows-authentication-transact-sql.md)  
 Windows 인증을 사용하여 미러링 모니터 서버가 있는 데이터베이스 미러링 세션을 만드는 데 필요한 모든 단계의 예를 포함합니다.  
  
 [예제: 인증서를 사용하여 데이터베이스 미러링 설정&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
 인증서 기반 인증을 사용하여 미러링 모니터 서버가 있는 데이터베이스 미러링 세션을 만드는 데 필요한 모든 단계의 예를 포함합니다.  
  
 [데이터베이스 미러링 또는 Always On 가용성 그룹에 대한 로그인 계정 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/set-up-login-accounts-database-mirroring-always-on-availability.md)  
 로컬 서버 인스턴스가 아닌 다른 계정을 사용하는 원격 서버 인스턴스의 로그인을 만드는 방법에 대해 설명합니다.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
 **SQL Server Management Studio**  
  
-   [데이터베이스 미러링 보안 구성 마법사 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
 **Transact-SQL**  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 엔드포인트에 대한 네트워크 액세스 허용&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)  
  
-   [데이터베이스 미러링 엔드포인트의 아웃바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
-   [데이터베이스 미러링 엔드포인트의 인바운드 연결에 대한 인증서 사용 허용&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Windows 인증에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 모니터 추가&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
-   [Trustworthy 속성을 사용하도록 미러 데이터베이스 설정&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)  
  
 **Transact-SQL/SQL Server Management Studio**  
  
-   [Upgrading Mirrored Instances](../../database-engine/database-mirroring/upgrading-mirrored-instances.md)  
  
-   [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [데이터베이스 미러링 구성 문제 해결&#40;SQL Server&#41;](../../database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링: 상호 운용성 및 공존성&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-interoperability-and-coexistence-sql-server.md)   
 [데이터베이스 미러링 및 Always On 가용성 그룹에 대한 전송 보안&#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [서버 네트워크 주소 지정&#40;데이터베이스 미러링&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
  
