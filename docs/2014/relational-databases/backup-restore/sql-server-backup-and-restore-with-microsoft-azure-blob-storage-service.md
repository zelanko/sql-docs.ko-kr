---
title: Azure Blob Storage 서비스를 사용 하 여 백업 및 복원 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4ba066136493c2a429b1193d9846f4183f781846
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84956483"
---
# <a name="sql-server-backup-and-restore-with-azure-blob-storage-service"></a>Azure Blob Storage Service로 SQL Server 백업 및 복원
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Azure Blob 저장소 서비스](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)에 대 한 백업 및 복원에 대해 소개 합니다. 또한 Azure Blob service를 사용 하 여 백업을 저장 하는 이점에 대 한 요약을 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
 SQL Server는 다음과 같은 방법으로 Azure Blob storage 서비스에 백업을 저장 하도록 지원 합니다.  
  
-   **Azure에 대 한 백업 관리:** 이제 디스크 및 테이프에 백업 하는 데 사용 되는 것과 동일한 방법을 사용 하 여 URL을 백업 대상으로 지정 하 여 Azure storage에 백업할 수 있습니다.  이 기능을 사용하여 로컬 스토리지나 다른 오프사이트 옵션의 경우처럼 수동으로 백업하거나 자체 백업 전략을 구성할 수 있습니다. 이 기능을 **URL에 대한 SQL Server 백업**이라고도 합니다. 자세한 내용은 [URL에 대한 SQL Server Backup](sql-server-backup-to-url.md)을 참조하세요. 이 기능은 SQL Server 2012 SP1 CU2 이상에서 사용할 수 있습니다.  
  
    > [!NOTE]  
    >  2014 SQL Server 이전 SQL Server 버전의 경우 추가 기능 SQL Server Azure에 백업 도구를 사용 하 여 Azure storage에 백업을 쉽고 빠르게 만들 수 있습니다. 자세한 내용은 [다운로드 센터](https://go.microsoft.com/fwlink/?LinkID=324399)를 참조하십시오.  
  
-   **Azure에 대 한 백업을 SQL Server 관리할 수 있습니다.** 단일 데이터베이스 또는 여러 데이터베이스에 대해 백업 전략을 관리 하 고 백업을 예약 하거나 인스턴스 수준에서 기본값을 설정 하도록 SQL Server를 구성 합니다. 이 기능을 라고 **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]** 합니다. 자세한 내용은 [Azure에 대 한 관리 되는 백업 SQL Server를](sql-server-managed-backup-to-microsoft-azure.md)참조 하세요. 이 기능은 SQL Server 2014 이상에서 사용할 수 있습니다.  
  
## <a name="benefits-of-using-the-azure-blob-service-for-ssnoversion-backups"></a>백업에 Azure Blob Service를 사용할 경우의 이점 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   유연 하 고 안정적 이며 무제한 오프 사이트 저장소: Azure Blob service에 백업을 저장 하면 편리 하 고 유연 하며 쉽게 액세스할 수 있는 오프 사이트 옵션입니다. 기존 스크립트/작업을 수정하는 것처럼 쉽게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업에 사용할 오프사이트 스토리지를 만들 수 있습니다. 오프사이트와 프로덕션 데이터베이스 위치 둘 다에 영향을 줄 수 있는 단일 재해를 방지하려면 오프사이트 스토리지는 일반적으로 프로덕션 데이터베이스 위치와 충분히 멀리 떨어져 있어야 합니다. Blob 스토리지 지리적 복제를 선택하여 전체 지역에 영향을 줄 수 있는 재해 발생에 대비한 추가 보호막을 만듭니다. 또한 언제 어디서나 백업을 사용할 수 있으며 복원을 위해 백업에 쉽게 액세스할 수 있습니다.  
  
-   백업 보관: Azure Blob Storage 서비스는 백업 보관에 자주 사용 하는 테이프 옵션 보다 더 나은 대안을 제공 합니다. 테이프 스토리지를 사용하려면 미디어를 보호하기 위해 오프사이트 시설 및 수단까지 테이프를 물리적으로 운반해야 할 수 있습니다. Azure Blob Storage에 백업 저장은 즉각적이고 내구성 있는 고가용성 보관 옵션을 제공합니다.  
  
-   하드웨어 관리 오버 헤드 없음: Azure 서비스를 사용한 하드웨어 관리 오버 헤드가 없습니다. Azure 서비스에서 하드웨어를 관리하며 하드웨어 오류 방지와 중복을 위해 지역에서 복제 옵션을 제공합니다.  
  
-   현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure 가상 머신에서 실행 중인 인스턴스의 경우 연결 된 디스크를 만들어 Azure Blob 저장소 서비스로 백업할 수 있습니다. 그러나 Azure 가상 컴퓨터에 연결할 수 있는 디스크 수에는 제한이 있습니다. 초대형 인스턴스의 경우 16개이며, 그보다 작은 인스턴스의 경우 더 적습니다. Azure Blob Storage에 대 한 직접 백업을 사용 하도록 설정 하면 16 개의 디스크 제한을 무시할 수 있습니다.  
  
     또한 Azure Blob storage 서비스에 저장 된 백업 파일은 온-프레미스 또는 Azure 가상 컴퓨터에서 실행 되는 다른 데이터베이스에서 직접 사용할 수 있습니다 .이 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 연결/분리, VHD 다운로드 및 연결이 필요 하지 않습니다.  
  
-   비용 이점: 사용한 서비스에 대한 비용만 지불합니다. 오프사이트 및 백업 보관 옵션만큼 비용 효율적일 수 있습니다. 자세한 내용 및 링크는 [Azure 청구 고려 사항](#Billing) 섹션을 참조 하세요.  
  
##  <a name="azure-billing-considerations"></a><a name="Billing"></a>Azure 청구 고려 사항:  
 Azure 저장소 비용을 이해 하면 Azure에서 백업을 만들고 저장 하는 비용을 예측할 수 있습니다.  
  
 [Azure 가격 계산기](https://go.microsoft.com/fwlink/?LinkId=277060) 를 통해 비용을 추정할 수 있습니다.  
  
 **스토리지:** 요금은 사용 공간을 기준으로 하며 단계적 등급과 중복 수준에 따라 계산됩니다. 자세한 내용과 최선 정보는 **가격 정보** 문서의 [데이터 관리](https://go.microsoft.com/fwlink/?LinkId=277059) 섹션을 참조하세요.  
  
 **데이터 전송:** Azure에 대 한 인바운드 데이터 전송은 무료입니다. 아웃바운드 전송의 경우 대역폭 사용 요금이 부과되며 단계적 지역별 등급을 기준으로 계산됩니다. 자세한 내용은 가격 정보 문서의 [데이터 전송](https://go.microsoft.com/fwlink/?LinkId=277061) 섹션을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [URL에 대한 SQL Server 백업 - 최상의 방법 및 문제 해결](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [자습서: Azure Blob Storage 서비스로 백업 및 복원 SQL Server](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)   
 [URL에 대한 SQL Server 백업](sql-server-backup-to-url.md)  
  
