---
title: 즉시 파일 초기화 구성
description: 분석 플랫폼 시스템에서 즉시 파일 초기화를 구성 합니다. 즉시 파일 초기화는 데이터 파일 작업을 보다 신속 하 게 실행할 수 있는 SQL Server 기능입니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 62b76b616786c593d395ee8720bba4c012390290
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766892"
---
# <a name="instant-file-initialization-configuration"></a>즉시 파일 초기화 구성
즉시 파일 초기화는 데이터 파일 작업을 보다 신속 하 게 실행할 수 있는 SQL Server 기능입니다. 즉시 파일 초기화를 설정 하는 확인란을 선택 하면 SQL Server PDW 성능이 향상 됩니다. 그러나이로 인해 비즈니스에 보안 위험이 발생 하는 경우에는 확인란을 선택 하지 않은 상태로 둡니다.  
  
> [!IMPORTANT]  
> 인스턴트 파일 초기화를 사용 하도록 설정 하면 SQL Server는 삭제 된 비트를 0으로 덮어쓰지 않습니다.  이 동작은 권한 없는 사용자가 삭제 된 데이터에 대 한 액세스 권한을 얻는 경우 보안 취약점을 만들 수 있습니다. 그러나 SQL Server PDW SQL Server 데이터베이스와 백업 파일이 항상 SQL Server 인스턴스에 연결 되도록 하 여이 위험을 완화 합니다. SQL Server 서비스 계정 및 로컬 관리자만 SQL Server PDW에서 삭제 된 데이터에 액세스할 수 있습니다.  
  
TDE를 사용하도록 설정되어 있으면 즉시 파일 초기화를 사용할 수 없습니다.  
  
## <a name="add-permission-for-the-backup-account"></a>백업 계정에 대 한 권한 추가  
백업 프로세스에는 백업 저장소 위치에 액세스할 수 있는 네트워크 자격 증명 (Windows 사용자 계정)이 필요 합니다. [Sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 절차를 사용 하 여 PDW가 계정을 사용할 수 있도록 권한을 부여 합니다. 전체 백업 프로세스는 [데이터베이스 백업](../t-sql/statements/backup-transact-sql.md?view=sql-server-ver15) 을 참조 하세요. 즉시 파일 초기화를 사용 하려면 백업 계정에 권한을 부여 해야 합니다 `Perform volume maintenance tasks` .  
  
1.  Backup 서버에서 **로컬 보안 정책** 응용 프로그램 ()을 엽니다 `secpol.msc` .  
  
2.  왼쪽 창에서 **로컬 정책**을 확장한 다음 **사용자 권한 할당**을 클릭합니다.  
  
3.  오른쪽 창에서 **볼륨 유지 관리 작업 수행**을 두 번 클릭합니다.  
  
4.  **사용자 또는 그룹 추가** 를 클릭하고 백업에 사용되는 사용자 계정을 추가합니다.  
  
5.  **적용**을 클릭한 다음 모든 **로컬 보안 정책** 대화 상자를 닫습니다.  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>즉시 파일 초기화를 설정 하거나 해제 하려면  
  
1.  Configuration Manager를 시작 합니다. 자세한 내용은 [Configuration Manager &#40;Analytics Platform System&#41;시작 ](launch-the-configuration-manager.md)을 참조 하세요.  
  
2.  Configuration Manager의 왼쪽 창에서 **즉시 파일 초기화**를 클릭 합니다.  
  
3.  즉시 파일 초기화를 켜려면 **모든 노드에서 즉시 파일 초기화 사용**옆의 상자를 선택 합니다. 즉시 파일 초기화를 해제 하려면 **모든 노드에서 인스턴트 파일 초기화 사용**옆에 있는 확인란의 선택을 취소 합니다.  
  
    > [!WARNING]  
    > 즉시 파일 초기화를 해제 하면 즉시 파일 초기화를 사용 하는 동안 삭제 된 파일에도 해당 기능에 대해 위에서 설명한 보안 고려 사항이 적용 될 수 있습니다.  
  
4.  **적용**을 클릭합니다. 변경 내용은 다음에 어플라이언스 서비스를 다시 시작할 때 SQL Server PDW의 SQL Server 인스턴스를 통해 전파 됩니다. 지금 어플라이언스 서비스를 다시 시작 하려면 [PDW 서비스 상태 &#40;분석 플랫폼 시스템&#41;](pdw-services-status.md)을 참조 하세요.  
  
5.  위에 설명 된 단계를 **백업 계정에 대 한 추가 권한** 으로 반복 하 여 **볼륨 유지 관리 작업 수행** 권한을 제거할 수 있습니다.  
  
![DWConfig 어플라이언스 PDW 즉시 파일 초기화](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
즉시 파일 초기화에 대 한 자세한 내용은 [인스턴트 파일 초기화](/previous-versions/sql/sql-server-2008-r2/ms175935(v=sql.105))를 참조 하세요.  
