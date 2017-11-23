---
title: "즉시 파일 초기화 (분석 플랫폼 시스템) 구성"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58be8982-4d2e-4aa3-bcdd-874a062d2f9d
caps.latest.revision: "20"
ms.openlocfilehash: af18d7da04c84f9cbc74b9b2974ef568098963ba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="instant-file-initialization-configuration"></a>즉시 파일 초기화 구성
즉시 파일 초기화는 보다 빠르게 실행 하는 데이터 파일 작업을 허용 하는 SQL Server 기능입니다. 즉시 파일 초기화를 설정 하려면 확인란을 선택 하면 SQL Server PDW의 성능이 향상 됩니다. 그러나이 작업은 보안상 위험 하기에 대 한 비즈니스, 하는 경우 다음 상자를 둡니다 선택 취소 되어 있음.  
  
> [!IMPORTANT]  
> SQL Server는 즉시 파일 초기화를 사용 하는 경우 0이 삭제 된 비트 덮어쓰지 않습니다.  이 동작 권한이 없는 사용자가 삭제 된 데이터에 액세스할 경우 보안 취약점을 만들 수 있습니다. SQL Server PDW에 SQL Server; 인스턴스에 SQL Server 데이터베이스 및 백업 파일 항상 연결 되어 있는지 확인 하 여 이러한 위험을 완화 하는 반면 SQL Server 서비스 계정 및 로컬 관리자는 SQL Server PDW에서 삭제 된 데이터를 액세스할 수 있습니다.  
  
TDE를 사용하도록 설정되어 있으면 즉시 파일 초기화를 사용할 수 없습니다.  
  
## <a name="add-permission-for-the-backup-account"></a>백업 계정에 대 한 사용 권한 추가  
백업 프로세스는 백업 저장소 위치에 액세스할 수 있는 네트워크 자격 증명 (Windows 사용자 계정) 필요 합니다. PDW 계정을 사용 하 여 사용할 수 있는 권한이 부여 된 [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) 프로시저입니다. 참조 [백업 데이터베이스](../t-sql/statements/backup-database-parallel-data-warehouse.md) 전체 백업 프로세스에 대 한 합니다. 즉시 파일 초기화를 사용 하려면 백업 계정에 부여 해야는 `Perform volume maintenance tasks` 권한.  
  
1.  백업 서버에서 열고는 **로컬 보안 정책** 응용 프로그램 (`secpol.msc`).  
  
2.  왼쪽 창에서 **로컬 정책**을 확장한 다음 **사용자 권한 할당**을 클릭합니다.  
  
3.  오른쪽 창에서 **볼륨 유지 관리 작업 수행**을 두 번 클릭합니다.  
  
4.  **사용자 또는 그룹 추가** 를 클릭하고 백업에 사용되는 사용자 계정을 추가합니다.  
  
5.  **적용**을 클릭한 다음 모든 **로컬 보안 정책** 대화 상자를 닫습니다.  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>즉시 파일 초기화 켜기 / 끄기를  
  
1.  구성 관리자를 시작 합니다. 자세한 내용은 참조 [구성 관리자 &#40; 시작 분석 플랫폼 시스템 &#41; ](launch-the-configuration-manager.md).  
  
2.  구성 관리자의 왼쪽된 창에서 클릭 **즉시 파일 초기화**합니다.  
  
3.  즉시 파일 초기화를 설정 하려면 상자를 옆에 선택 **모든 노드에서 즉시 파일 초기화를 사용 하도록 설정**합니다. 즉시 파일 초기화를 해제 하려면 확인란의 선택을 취소 옆에 **모든 노드에서 즉시 파일 초기화를 사용 하도록 설정**합니다.  
  
    > [!WARNING]  
    > 즉시 파일 초기화 해제 하면 기능에 대해 위에서 설명한 보안 고려 사항 여전히 즉시 파일 초기화를 사용 하는 동안 삭제 된 파일에 적용할 수 있습니다.  
  
4.  **적용**을 클릭합니다. 변경 내용을 다음 기기 서비스를 다시 시작할 때 SQL Server PDW에서 SQL Server 인스턴스를 통해 전파 됩니다. 어플라이언스 서비스를 지금 다시 시작 하려면 참조 [PDW 서비스 상태 &#40; 분석 플랫폼 시스템 &#41; ](pdw-services-status.md).  
  
5.  위에 설명 된 대로 단계를 반복 하는 것이 좋습니다 **백업 계정에 대 한 권한 추가** 제거 하는 **볼륨 유지 관리 작업 수행** 권한.  
  
![DWConfig 어플라이언스 PDW 인스턴트 파일 초기화](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
즉시 파일 초기화에 대 한 자세한 내용은 참조 [즉시 파일 초기화](http://technet.microsoft.com/en-us/library/ms175935(v=SQL.105).aspx)합니다.  
  
