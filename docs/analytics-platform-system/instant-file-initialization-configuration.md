---
title: Analytics Platform System 인스턴트 파일 초기화-구성 | Microsoft Docs
description: Analytics Platform System에 인스턴트 파일 초기화를 구성 합니다. 즉시 파일 초기화는 더 빠르게 실행 하기 위해 데이터 파일 작업을 허용 하는 SQL Server 기능입니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 959d219565de6577e31d9548f5daea0fe0d2419e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298130"
---
# <a name="instant-file-initialization-configuration"></a>즉시 파일 초기화 구성
즉시 파일 초기화는 더 빠르게 실행 하기 위해 데이터 파일 작업을 허용 하는 SQL Server 기능입니다. 즉시 파일 초기화를 켜려면 확인란을 선택 하면 SQL Server PDW의 성능이 향상 됩니다. 그러나이 보안 위험이 제기 하기 비즈니스를 하는 경우 다음 확인란의 선택을 취소 합니다.  
  
> [!IMPORTANT]  
> SQL Server는 인스턴트 파일 초기화를 사용 하는 경우에 0을 사용 하 여 삭제 된 비트 덮어쓰지 않습니다.  이 동작은 권한이 없는 사용자가 삭제 된 데이터에 액세스할 경우 보안 취약점을 만들 수 있습니다. SQL Server PDW; SQL Server 인스턴스에 SQL Server 데이터베이스 및 백업 파일 항상 연결 되어 있는지 확인 하 여이 위험을 완화 하는 반면 SQL Server 서비스 계정 및 로컬 관리자는 SQL Server PDW에서 삭제 된 데이터를 액세스할 수 있습니다.  
  
TDE를 사용하도록 설정되어 있으면 즉시 파일 초기화를 사용할 수 없습니다.  
  
## <a name="add-permission-for-the-backup-account"></a>백업 계정에 권한을 추가 합니다.  
백업 프로세스는 백업 저장소 위치에 액세스할 수는 네트워크 자격 증명 (Windows 사용자 계정)에 필요 합니다. PDW를 사용 하 여 계정을 사용 하도록 권한을 부여 합니다 [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 프로시저입니다. 참조 [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md) 전체 백업 프로세스에 대 한 합니다. 즉시 파일 초기화를 사용 하려면 백업 계정에 부여 해야 합니다 `Perform volume maintenance tasks` 권한.  
  
1.  백업 서버에서 엽니다는 **로컬 보안 정책** 응용 프로그램 (`secpol.msc`).  
  
2.  왼쪽 창에서 **로컬 정책**을 확장한 다음 **사용자 권한 할당**을 클릭합니다.  
  
3.  오른쪽 창에서 **볼륨 유지 관리 작업 수행**을 두 번 클릭합니다.  
  
4.  **사용자 또는 그룹 추가** 를 클릭하고 백업에 사용되는 사용자 계정을 추가합니다.  
  
5.  **적용**을 클릭한 다음 모든 **로컬 보안 정책** 대화 상자를 닫습니다.  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>즉시 파일 초기화를 켜거나 끄려면를  
  
1.  구성 관리자를 시작 합니다. 자세한 내용은 [구성 관리자 시작 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)합니다.  
  
2.  구성 관리자의 왼쪽된 창에서 클릭 **인스턴트 파일 초기화**합니다.  
  
3.  즉시 파일 초기화를 활성화 하려면 선택 상자 옆 **모든 노드에서 즉시 파일 초기화를 사용 하도록 설정**합니다. 즉시 파일 초기화를 해제 하려면 확인란의 선택을 취소 합니다 옆 **모든 노드에서 즉시 파일 초기화를 사용 하도록 설정**합니다.  
  
    > [!WARNING]  
    > 즉시 파일 초기화를 해제 하면 기능에 대해 위에서 설명한 보안 고려 사항 인스턴트 파일 초기화를 사용 하는 동안 삭제 된 파일에 계속 적용 될 수 있습니다.  
  
4.  **적용**을 클릭합니다. 변경 내용을 어플라이언스 서비스를 다시 시작한 다음에 SQL Server PDW에서 SQL Server 인스턴스를 통해 전파 됩니다. 어플라이언스 서비스를 지금 다시 시작을 참조 하세요 [PDW 서비스 상태 &#40;Analytics Platform System&#41;](pdw-services-status.md)합니다.  
  
5.  위에 설명 된 대로 단계를 반복 하는 것이 좋습니다 **백업 계정에 대 한 권한 추가** 제거할 합니다 **볼륨 유지 관리 작업 수행** 권한.  
  
![DWConfig 어플라이언스 PDW 인스턴트 파일 초기화](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
즉시 파일 초기화에 대 한 자세한 내용은 참조 하세요. [인스턴트 파일 초기화](https://technet.microsoft.com/library/ms175935(v=SQL.105).aspx)합니다.  
  
