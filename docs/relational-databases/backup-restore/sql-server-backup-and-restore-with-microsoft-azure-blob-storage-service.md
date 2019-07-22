---
title: Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원 | Microsoft 문서
ms.custom: ''
ms.date: 03/25/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 169e437c141d379401b7a3294f0ae852d756374f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041373"
---
# <a name="sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service"></a>Microsoft Azure Blob Storage Service로 SQL Server 백업 및 복원
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  ![Azure Blob에 백업 그래픽](../../relational-databases/backup-restore/media/backup-to-azure-blob-graphic.png "Backup to Azure blob graphic")  
  
 이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 [Microsoft Azure Blob Storage 서비스](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)로 백업하고 반대로 복원하는 방법에 대해 설명합니다. 또한 Microsoft Azure Blob 서비스를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업을 저장할 경우의 이점에 대해서도 간략하게 설명합니다.  
  
 SQL Server에서는 다음과 같은 방식으로 Microsoft Azure Blob Storage 서비스에 백업할 수 있습니다.  
  
-   **Microsoft Azure에 대한 백업 관리:** 디스크와 테이프에 백업하는 데 사용되는 동일한 방법을 사용하여, 이제 URL을 백업 대상으로 지정함으로써 Microsoft Azure 스토리지에 백업할 수 있습니다. 이 기능을 사용하여 로컬 스토리지나 다른 오프사이트 옵션의 경우처럼 수동으로 백업하거나 자체 백업 전략을 구성할 수 있습니다. 이 기능을 **URL에 대한 SQL Server 백업**이라고도 합니다. 자세한 내용은 [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)을 참조하세요. 이 기능은 SQL Server 2012 SP1 CU2 이상에서 사용할 수 있습니다. 이 기능은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 에서 블록 Blob, 공유 액세스 서명, 스트라이프를 사용하면서 성능과 기능이 더욱 향상되었습니다.  
  
    > [!NOTE]  
    >  SQL Server 2012 SP1 CU2 이전의 SQL Server 버전의 경우 Microsoft Azure 도구의 추가 기능인 SQL Server 백업을 사용하여 Microsoft Azure Storage에 백업을 쉽고 빠르게 만들 수 있습니다. 자세한 내용은 [다운로드 센터](https://go.microsoft.com/fwlink/?LinkID=324399)를 참조하십시오.  
  
-   **Azure Blob Storage의 데이터베이스 파일에 대한 파일-스냅샷 백업** : Azure 스냅샷을 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 파일-스냅샷 백업은 Azure Blob Storage 서비스를 사용하여 저장된 데이터베이스 파일에 대해 거의 즉각적인 백업 및 복원을 제공합니다. 이 기능으로 백업 및 복원 정책을 간소화할 수 있으며 특정 시점 복원을 지원합니다. 자세한 내용은 [Azure의 데이터베이스 파일에 대한 파일-스냅샷 백업](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요. 이 기능은 SQL Server 2016 이상에서 사용할 수 있습니다.  
  
-   **SQL Server에서 Microsoft Azure에 대한 백업을 관리하도록 구성:** 백업 전략을 관리하고 단일 데이터베이스나 여러 데이터베이스에 대한 백업을 예약하도록 SQL Server를 구성하거나 인스턴스 수준에서 기본값을 설정합니다. 이 기능을 **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]** 이라고 합니다. 자세한 내용은 [Microsoft Azure에 대한 SQL Server Managed Backup](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)을 참조하세요. 이 기능은 SQL Server 2014 이상에서 사용할 수 있습니다.  
  
## <a name="benefits-of-using-the-microsoft-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업에 Microsoft Azure Blob 서비스를 사용할 경우의 이점  
  
-   유연하고 안정적인 무제한 오프사이트 스토리지: Microsoft Azure Blob service에 백업 저장은 편리하고 유연하며 쉽게 액세스할 수 있는 오프사이트 옵션입니다. 기존 스크립트/작업을 수정하는 것처럼 쉽게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업에 사용할 오프사이트 스토리지를 만들 수 있습니다. 오프사이트 스토리지는 대개 오프사이트 및 프로덕션 데이터베이스 위치 모두에 영향을 줄 수 있는 재해 방지를 위해 프로덕션 데이터베이스 위치로부터 충분히 멀리 있어야 합니다. Blob 스토리지 지리적 복제를 선택하여 전체 지역에 영향을 줄 수 있는 재해 발생에 대비한 추가 보호막을 만듭니다. 또한 언제 어디서나 백업을 사용할 수 있으며 복원을 위해 백업에 쉽게 액세스할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 블록 blob을 사용하면 백업 세트를 스트라이프하여 최대 12.8TB의 백업 파일 크기를 지원할 수 있습니다.  
  
-   백업 보관: Microsoft Azure Blob Storage 서비스는 백업 보관에 자주 사용하는 테이프 옵션보다 더 효율적입니다. 테이프 스토리지를 사용하려면 오프사이트 시설로 물리적 이동과 미디어 보호 조치가 필요합니다. Microsoft Azure Blob Storage에 백업을 저장하면 즉각적이고 견고하며 가용성이 높은 보관이 가능합니다.  
  
-   하드웨어 관리 오버헤드 없음: Microsoft Azure 서비스를 사용하면 하드웨어 관리에 따른 오버헤드가 없습니다. Microsoft Azure 서비스는 하드웨어를 관리하며 하드웨어 오류에 대비한 중복과 보호를 위해 지리적 복제를 제공합니다.  
  
-   현재 Microsoft Azure 가상 머신에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 경우 연결된 디스크를 만들어 Microsoft Azure Blob Storage 서비스로 백업할 수 있습니다. 그러나 Microsoft Azure 가상 머신에 연결할 수 있는 디스크 수에 제한이 있습니다. 초대형 인스턴스의 경우 16개이며, 그보다 작은 인스턴스의 경우 더 적습니다. Microsoft Azure Blob Storage에 직접 백업하면 16개의 디스크 제한을 무시할 수 있습니다.  
  
     또한, 데이터베이스를 연결하고 분리하거나 VHD를 다운로드하고 연결할 필요 없이 온-프레미스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](이)나 Microsoft Azure 가상 머신에서 실행 중인 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 Microsoft Azure Blob Storage 서비스에 저장되는 백업 파일을 바로 사용할 수 있습니다.  
  
-   비용상의 이점: 사용되는 서비스에 대한 비용만 지불합니다. 오프사이트 및 백업 보관 옵션만큼 비용 효율적일 수 있습니다. 자세한 내용과 링크는 [Microsoft Azure 청구 고려 사항](#Billing) 섹션을 참조하십시오.  
  
##  <a name="Billing"></a> Microsoft Azure 청구 고려 사항:  
 Microsoft Azure Storage 비용을 이해하면 Microsoft Azure에서 백업을 만들고 스토리지하는 데 드는 비용을 예측할 수 있습니다.  
  
 [Microsoft Azure 가격 계산기](https://go.microsoft.com/fwlink/?LinkId=277060) 로 예상 비용을 계산할 수 있습니다.  
  
 **스토리지:** 요금은 사용 공간을 기준으로 하며 단계적 등급과 중복 수준에 따라 계산됩니다. 자세한 내용과 최선 정보는 **가격 정보** 문서의 [데이터 관리](https://go.microsoft.com/fwlink/?LinkId=277059) 섹션을 참조하세요.  
  
 **데이터 전송:** Microsoft Azure에 대한 인바운드 데이터 전송은 무료입니다. 아웃바운드 전송의 경우 대역폭 사용 요금이 부과되며 단계적 지역별 등급을 기준으로 계산됩니다. 자세한 내용은 가격 정보 문서의 [데이터 전송](https://go.microsoft.com/fwlink/?LinkId=277061) 섹션을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  

[URL에 대한 SQL Server 백업 - 최상의 방법 및 문제 해결](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)   

[시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   

[자습서: SQL Server 2016 데이터베이스와 함께 Microsoft Azure Blob 스토리지 서비스 사용](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)

[URL에 대한 SQL Server 백업](../../relational-databases/backup-restore/sql-server-backup-to-url.md)  
  
  
