---
title: SQL Server 백업 및 복원 Windows azure Blob Storage 서비스 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 52f1bdf9e748625e1310210c98beeb4401a5dd81
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62920698"
---
# <a name="sql-server-backup-and-restore-with-windows-azure-blob-storage-service"></a>Windows Azure Blob Storage 서비스로 SQL Server 백업 및 복원
  이 항목에서는 소개 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 및 복원에서 합니다 [Windows Azure Blob 저장소 서비스](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)합니다. Microsoft Azure Blob service를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업을 저장할 경우의 이점에 대해서도 간략하게 설명합니다.  
  
 SQL Server는 다음과 같은 방식으로 Windows Azure Blob 저장소 서비스에 백업을 저장하는 것을 지원합니다.  
  
-   **Windows Azure에 대 한 백업 관리:** 디스크와 테이프에 백업하는 데 사용되는 동일한 방법을 사용하여, 이제 URL을 백업 대상으로 지정함으로써 Windows Azure 저장소에 백업할 수 있습니다.  이 기능을 사용하여 로컬 스토리지나 다른 오프사이트 옵션의 경우처럼 수동으로 백업하거나 자체 백업 전략을 구성할 수 있습니다. 이 기능을 **URL에 대한 SQL Server 백업**이라고도 합니다. 자세한 내용은 [SQL Server Backup to URL](sql-server-backup-to-url.md)을 참조하세요. 이 기능은 SQL Server 2012 SP1 CU2 이상에서 사용할 수 있습니다.  
  
    > [!NOTE]  
    >  SQL Server 2014 이전의 SQL Server 버전의 경우 추가 기능인 Microsoft Azure에 대한 SQL Server 백업 도구를 사용하여 빠르고 쉽게 Microsoft Azure Storage에 백업을 만들 수 있습니다. 자세한 내용은 [다운로드 센터](https://go.microsoft.com/fwlink/?LinkID=324399)를 참조하십시오.  
  
-   **Windows Azure에 SQL Server 관리 백업을 사용 수 있습니다.** 백업 전략을 관리하고 단일 데이터베이스나 여러 데이터베이스에 대한 백업을 예약하도록 SQL Server를 구성하거나 인스턴스 수준에서 기본값을 설정합니다. 이 기능 이라고 **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]** 합니다. 자세한 내용은 참조 [SQL Server Managed Backup to Windows Azure](sql-server-managed-backup-to-microsoft-azure.md)합니다. 이 기능은 SQL Server 2014 이상에서 사용할 수 있습니다.  
  
## <a name="benefits-of-using-the-windows-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업에 Microsoft Azure Blob service를 사용할 경우의 이점  
  
-   유연하고 안정적인 무제한 오프사이트 저장소: Microsoft Azure Blob service에 백업 저장은 편리하고 유연하며 쉽게 액세스할 수 있는 오프사이트 옵션입니다. 기존 스크립트/작업을 수정하는 것처럼 쉽게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업에 사용할 오프사이트 스토리지를 만들 수 있습니다. 오프사이트 스토리지는 대개 오프사이트 및 프로덕션 데이터베이스 위치 모두에 영향을 줄 수 있는 재해 방지를 위해 프로덕션 데이터베이스 위치로부터 충분히 멀리 있어야 합니다. Blob 스토리지 지리적 복제를 선택하여 전체 지역에 영향을 줄 수 있는 재해 발생에 대비한 추가 보호막을 만듭니다. 또한 언제 어디서나 백업을 사용할 수 있으며 복원을 위해 백업에 쉽게 액세스할 수 있습니다.  
  
-   백업 보관: Microsoft Azure Blob Storage는 백업 보관에 자주 사용하는 테이프 옵션보다 더 효율적입니다. 테이프 스토리지를 사용하려면 오프사이트 시설로 물리적 이동과 미디어 보호 조치가 필요합니다. Microsoft Azure Blob Storage에 백업을 저장하면 빠르고 지속적이며 항상 사용 가능한 보관 옵션을 사용할 수 있습니다.  
  
-   Windows Azure 서비스를 사용하면 하드웨어 관리에 따른 오버헤드가 없습니다. Windows Azure 서비스는 하드웨어를 관리하며 하드웨어 오류에 대비한 중복과 보호를 위해 지리적 복제를 제공합니다.  
  
-   현재 Windows Azure 가상 컴퓨터를 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 경우 연결된 디스크를 만들어서 Windows Azure Blob 저장소 서비스로 백업할 수 있습니다. 그러나 Windows Azure 가상 컴퓨터에 연결할 수 있는 디스크 수에 제한이 있습니다. 초대형 인스턴스의 경우 16개이며, 그보다 작은 인스턴스의 경우 더 적습니다. Microsoft Azure Blob Storage에 직접 백업하면 16개의 디스크 제한을 무시할 수 있습니다.  
  
     또한 데이터베이스를 연결하고 분리하거나 VHD를 다운로드하고 연결할 필요 없이 온-프레미스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]나 Windows Azure 가상 컴퓨터에서 실행 중인 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 Windows Azure Blob 저장소 서비스에 저장되는 백업 파일을 바로 사용할 수 있습니다  
  
-   비용상의 이점: 사용되는 서비스에 대한 비용만 지불합니다. 오프사이트 및 백업 보관 옵션만큼 비용 효율적일 수 있습니다. 참조 된 [Windows Azure 청구 고려 사항](#Billing) 자세한 내용 및 링크에 대 한 섹션입니다.  
  
##  <a name="Billing"></a> Windows Azure 청구 고려 사항:  
 Windows Azure 저장소 비용을 이해하면 Windows Azure에서 백업을 만들고 저장하는 데 드는 비용을 예측할 수 있습니다.  
  
 합니다 [Windows Azure 가격 계산기](https://go.microsoft.com/fwlink/?LinkId=277060) 비용 예상 하는 데 도움이 됩니다.  
  
 **스토리지:** 요금은 사용 공간을 기준으로 하며 단계적 등급과 중복 수준에 따라 계산됩니다. 자세한 내용과 최선 정보는 **가격 정보** 문서의 [데이터 관리](https://go.microsoft.com/fwlink/?LinkId=277059) 섹션을 참조하세요.  
  
 **데이터 전송:** Windows Azure로의 인바운드 데이터 전송은 무료입니다. 아웃바운드 전송의 경우 대역폭 사용 요금이 부과되며 단계적 지역별 등급을 기준으로 계산됩니다. 자세한 내용은 가격 정보 문서의 [데이터 전송](https://go.microsoft.com/fwlink/?LinkId=277061) 섹션을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [URL에 대한 SQL Server 백업 - 최상의 방법 및 문제 해결](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [자습서: Windows Azure Blob Storage Service로 SQL Server 백업 및 복원](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)   
 [URL에 대한 SQL Server 백업](sql-server-backup-to-url.md)  
  
  
