---
title: 데이터베이스 백업 (SQL Server Management Studio) 복원 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.locatebackupfileazure.f1
- sql12.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
caps.latest.revision: 73
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fa6388416e41fac400d6b77ad603a305fad50e21
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089338"
---
# <a name="restore-a-database-backup-sql-server-management-studio"></a>데이터베이스 백업 복원(SQL Server Management Studio)
  이 항목에서는 전체 데이터베이스 백업을 복원하는 방법에 대해 설명합니다.  
  
> [!IMPORTANT]  
>  전체 복구 모델 또는 대량 로그 복구 모델의 경우 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 데이터베이스를 복원하려면 먼저 활성 트랜잭션 로그(비상 로그라고도 함)를 백업해야 합니다. 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)데이터베이스를 새 위치로 복원하고 선택적으로 데이터베이스 이름을 바꾸는 방법을 설명합니다. 암호화된 데이터베이스를 복원하려면 데이터베이스를 암호화하는 데 사용된 인증서 또는 비대칭 키에 대한 액세스 권한이 있어야 합니다. 인증서 또는 비대칭 키가 없으면 데이터베이스를 복원할 수 없습니다. 따라서 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서는 백업이 필요한 동안에는 유지되어야 합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상의 데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 복원하면 데이터베이스가 자동으로 업그레이드됩니다. 일반적으로 데이터베이스는 즉시 사용할 수 있습니다. 그러나 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스에 전체 텍스트 인덱스가 있는 경우 업그레이드 프로세스는 **전체 텍스트 업그레이드 옵션** 서버 속성의 설정에 따라 인덱스를 가져오거나, 다시 설정하거나, 다시 작성합니다. 업그레이드 옵션이 **가져오기** 또는 **다시 작성**으로 설정되어 있는 경우 업그레이드하는 동안 전체 텍스트 인덱스를 사용할 수 없습니다. 인덱싱되는 데이터 양에 따라 가져오기 작업은 몇 시간씩 걸릴 수 있으며 다시 작성 작업은 10배 정도 더 걸릴 수 있습니다. 업그레이드 옵션이 **가져오기**로 설정되어 있으면 전체 텍스트 카탈로그를 사용할 수 없는 경우 관련된 전체 텍스트 인덱스가 다시 작성됩니다. **전체 텍스트 업그레이드 옵션** 속성 설정을 보거나 변경하는 방법은 [서버 인스턴스의 전체 텍스트 검색 관리 및 모니터링](../search/manage-and-monitor-full-text-search-for-a-server-instance.md)을 참조하세요.  
  
### <a name="to-restore-a-full-database-backup"></a>전체 데이터베이스 백업을 복원하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장합니다. 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스**를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  가리키는 데이터베이스를 마우스 오른쪽 단추로 **작업**, 가리킨 **복원**, 클릭 하 고 **데이터베이스**, 열립니다는 **데이터베이스 복원** 대화 상자입니다.  
  
4.  **일반** 페이지에서 **원본** 섹션을 사용하여 복원할 백업 집합의 원본과 위치를 지정합니다. 다음 옵션 중 하나를 선택합니다.  
  
    -   **데이터베이스 백업**  
  
         복원할 데이터베이스를 드롭다운 목록에서 선택합니다. 목록에는 **msdb** 백업 기록에 따라 백업된 데이터베이스만 포함되어 있습니다.  
  
    > [!NOTE]  
    >  백업을 다른 서버에서 가져온 경우 대상 서버에 지정한 데이터베이스에 대한 백업 기록 정보가 없습니다. 이 경우 **장치** 를 선택하여 복원할 파일이나 장치를 수동으로 지정합니다.  
  
    -   **장치**  
  
         찾아보기(**...**) 단추를 클릭하여 **백업 장치 선택** 대화 상자를 엽니다. **백업 미디어 유형** 상자에서 나열된 장치 유형 중 하나를 선택합니다. **백업 미디어** 상자에 대해 하나 이상의 장치를 선택하려면 **추가**를 클릭합니다.  
  
         원하는 장치를 **백업 미디어** 목록 상자에 추가한 후 **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.  
  
         **원본: 장치: 데이터베이스** 목록 상자에서 복원할 데이터베이스의 이름을 선택합니다.  
  
        > [!NOTE]  
        >  이 목록은 **장치** 를 선택한 경우에만 사용할 수 있습니다. 선택한 장치에 백업이 있는 데이터베이스만 사용할 수 있습니다.  
  
         **백업 미디어**  
         복원 작업에 사용할 미디어: **파일**, **테이프**, **URL**또는 **백업 장치**합니다. **테이프** 옵션은 컴퓨터에 테이프 드라이브가 탑재된 경우에만 나타나고 **백업 장치** 옵션은 적어도 하나의 백업 장치가 있는 경우에만 나타납니다.  
  
         **백업 위치**  
         복원 작업에 사용할 미디어를 표시하거나 추가하거나 제거합니다. 목록에는 파일, 테이프 또는 백업 장치가 64개까지 포함될 수 있습니다.  
  
         **추가**  
         백업 장치를 위치 추가 **백업 위치** 목록입니다. **백업 미디어** 필드에서 선택한 미디어 유형에 따라 **추가** 를 클릭하면 다음 대화 상자 중 하나가 열립니다.  
  
        |미디어 유형|대화 상자|Description|  
        |----------------|----------------|-----------------|  
        |**최근에 사용한 파일**|**백업 파일 찾기**|이 대화 상자에서는 트리에서 로컬 파일을 선택하거나 정규화된 UNC(Universal Naming Convention) 이름을 사용하여 원격 파일을 지정할 수 있습니다. 자세한 내용은 [백업 장치&#40;SQL Server&#41;](backup-devices-sql-server.md)인스턴스에서 가져온 경우에 필요합니다.|  
        |**장치**|**백업 장치 선택**|이 대화 상자에서는 서버 인스턴스에 정의된 논리적 백업 장치의 목록에서 장치를 선택할 수 있습니다.|  
        |**테이프**|**백업 테이프 선택**|이 대화 상자에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 실행하는 컴퓨터에 물리적으로 연결된 테이프 드라이브의 목록에서 백업 테이프를 선택할 수 있습니다.|  
        |**URL**|이는 두 대화 상자를 다음 순서로 시작합니다.<br /><br /> 1) **Windows 연결할 Azure 저장소**<br /><br /> 2) **Windows Azure에서 백업 파일 찾기**|**Windows Azure 저장소에 연결**  대화 상자에서 Windows Azure 저장소 계정 이름 및 액세스 키 정보를 저장하는 기존 SQL 자격 증명을 선택하거나 저장소 계정 이름 및 저장소 액세스 키 정보를 지정하여 새 SQL 자격 증명을 만듭니다. 자세한 내용은 참조 [Windows Azure 저장소에 연결 &#40;복원&#41;](connect-to-microsoft-azure-storage-restore.md)합니다.<br /><br /> **백업 파일 찾기** 대화 상자에서는 왼쪽 프레임에 표시된 컨테이너 목록에서 파일을 선택할 수 있습니다.|  
  
         목록이 꽉 차면 **추가** 단추를 사용할 수 없습니다.  
  
         **제거**  
         선택한 파일, 테이프 또는 논리적 백업 장치를 하나 이상 제거합니다.  
  
         **내용**  
         선택한 파일, 테이프 또는 논리적 백업 장치의 미디어 내용을 표시합니다.  
  
5.  **대상** 섹션의 **데이터베이스** 상자에는 복원할 데이터베이스의 이름이 자동으로 채워집니다. 데이터베이스의 이름을 변경하려면 **데이터베이스** 상자에 새 이름을 입력합니다.  
  
6.  **복원 위치** 상자에서 기본값인 **마지막으로 수행된 백업으로** 를 그대로 적용하거나 **시간대** 를 클릭하여 **백업 시간대** 대화 상자에 액세스한 후 복구 동작을 중지할 지정 시간을 직접 선택합니다. 특정 지정 시간을 지정하는 방법은 [Backup Timeline](backup-timeline.md)를 참조하십시오.  
  
7.  **복원에 사용할 백업 세트** 표에서 복원할 백업을 선택합니다. 이 표는 지정한 위치에서 사용 가능한 백업을 표시합니다. 기본적으로 복구 계획이 제안됩니다. 제안된 복구 계획을 재정의하려면 표에서 선택 항목을 변경합니다. 이전 백업의 선택이 취소되면 이전 백업 복원에 기반하는 백업도 자동으로 선택이 취소됩니다. **복원에 사용할 백업 세트** 표의 열에 대한 자세한 내용은 [데이터베이스 복원&#40;일반 페이지&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)을 참조하세요.  
  
8.  필요에 따라 **페이지 선택** 창에서 **파일** 을 클릭하여 **파일** 대화 상자에 액세스합니다. 여기서 **데이터베이스 파일을 다음으로 복원** 표의 각 파일에 대해 새 복원 대상을 지정하여 데이터베이스를 새 위치에 복원할 수 있습니다. 이 표에 대한 자세한 내용은 [데이터베이스 복원&#40;파일 페이지&#41;](restore-database-files-page.md)을 참조하세요.  
  
9. 고급 옵션을 보거나 선택하려면 상황에 따라 **옵션** 페이지의 **복원 옵션** 패널에서 다음 옵션 중 하나를 선택할 수 있습니다.  
  
    1.  `WITH` 옵션 (필요 없음):  
  
        -   **기존 데이터베이스 덮어쓰기(WITH REPLACE)**  
  
        -   **복제 설정 유지(WITH KEEP_REPLICATION)**  
  
        -   **복원된 데이터베이스에 대한 액세스 제한(WITH RESTRICTED_USER)**  
  
    2.  **복구 상태** 상자에 대한 옵션을 선택합니다. 이 상자에서 복원 작업 후 데이터베이스의 상태를 확인합니다.  
  
        -   **RESTORE WITH RECOVERY** 는 커밋되지 않은 트랜잭션을 롤백하여 데이터베이스를 사용 준비가 된 상태로 유지하는 기본 동작입니다. 추가 트랜잭션 로그를 복원할 수 없습니다. 필요한 모든 백업을 지금 복원하는 경우 이 옵션을 선택합니다.  
  
        -   **RESTORE WITH NORECOVERY** 는 데이터베이스를 비작동 상태로 유지하고 커밋되지 않은 트랜잭션을 롤백하지 않습니다. 추가 트랜잭션 로그를 복원할 수 데이터베이스는 복구할 때까지 사용할 수 없습니다.  
  
        -   **RESTORE WITH STANDBY** 는 읽기 전용 모드로 데이터베이스를 유지합니다. 이 옵션은 커밋되지 않은 트랜잭션의 실행을 취소하지만, 복구 결과를 되돌릴 수 있도록 실행 취소 동작을 대기 파일에 저장합니다.  
  
    3.  **복원 전 비상 로그 백업 수행** 은 선택한 지정 시간에 필요한 경우에 선택됩니다. 이 설정을 수정할 필요는 없지만 필요하지 않은 경우에도 비상 로그를 백업할 수 있습니다. 여기에 파일 이름? **일반** 페이지의 첫 번째 백업 세트가 Windows Azure에 있으면 비상 로그도 동일한 저장소 컨테이너에 백업됩니다.  
  
    4.  데이터베이스에 대한 활성 연결이 있으면 복원 작업이 실패할 수 있습니다. **기존 연결 닫기** 옵션을 선택하여 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 와 데이터베이스 간의 모든 활성 연결을 닫습니다. 이 확인란을 선택하면 복원 작업을 수행하기 전에 데이터베이스가 단일 사용자 모드로 설정되고 복원 작업이 완료될 때 데이터베이스가 다중 사용자 모드로 설정됩니다.  
  
    5.  각 복원 작업 사이에 확인 메시지를 표시하려면 **각 백업 복원 전에 확인** 을 선택합니다. 데이터베이스가 크고 복원 작업의 상태를 모니터링하려는 경우가 아니면 이 옵션은 일반적으로 필요하지 않습니다.  
  
     이러한 복원 옵션에 대한 자세한 내용은 [데이터베이스 복원&#40;옵션 페이지&#41;](restore-database-options-page.md)라고도 함)를 백업해야 할 수 있습니다.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)   
 [데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)   
 [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [데이터베이스 복원&#40;옵션 페이지&#41;](restore-database-options-page.md)   
 [데이터베이스 복원&#40;일반 페이지&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  
