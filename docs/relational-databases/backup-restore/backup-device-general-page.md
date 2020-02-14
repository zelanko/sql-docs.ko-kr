---
title: 백업 디바이스(일반 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.backupdevice.general.f1
ms.assetid: c557e37d-319e-4adb-a0c1-94189b15d2ac
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0d37918c0ca2be62c2e620faa8034548df2b4592
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67940820"
---
# <a name="backup-device-general-page"></a>백업 디바이스(일반 페이지)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **일반** 페이지를 사용하여 논리적 백업 디바이스의 일반 속성을 지정하거나 확인할 수 있습니다.  
  
 **SQL Server Management Studio를 사용하여 백업 디바이스의 내용을 보려면**  
  
-   [백업 테이프 또는 파일의 내용 보기&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [논리적 백업 디바이스의 속성 및 내용 보기&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>옵션  
 **디바이스 이름**  
 기존 논리적 백업 디바이스의 이름을 확인하거나 새 논리적 백업 디바이스의 이름을 지정합니다.  
  
 **테이프**  
 **테이프** 목록에서 대상 테이프 디바이스를 확인하거나 선택합니다. 이 옵션은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스를 실행하는 컴퓨터에 테이프 드라이브가 연결된 경우에만 사용할 수 있습니다.  
  
> [!NOTE]  
>  원격 컴퓨터의 테이프 백업 디바이스는 올바른 백업 대상이 아닙니다.  
  
 **최근에 사용한 파일**  
 기존 논리적 백업 디바이스의 대상 파일을 확인하거나 새 논리적 백업 디바이스의 대상 파일을 지정합니다.  
  
-   기존 논리적 백업 디바이스의 경우 백업 파일의 경로가 표시됩니다. **파일** 필드를 편집할 수 없으며 찾아보기 단추를 사용할 수 없습니다.  
  
-   새 논리적 백업 디바이스의 경우 논리적 백업 디바이스를 정의할 백업 파일의 경로를 제공해야 합니다. 아직 이 파일이 있을 필요는 없습니다.  
  
     로컬 백업 파일을 지정하려면 **파일** 입력란 오른쪽에 있는 찾아보기 단추를 클릭합니다. 그런 다음 **데이터베이스 파일 찾기** 대화 상자에서 서버 인스턴스를 실행하는 컴퓨터의 고정 드라이브 중 하나에 있는 임의의 위치로 이동할 수 있습니다. 백업 파일이 아직 없을 경우 해당 대화 상자의 **파일 이름** 필드에 사용할 파일 이름을 입력해야 합니다.  
  
     또는 **파일** 필드를 수동으로 편집하여 기본 경로, 파일 이름 및 확장명을 재정의할 수 있습니다. 원격 파일을 백업 대상으로 지정하려면 해당 파일의 정규화된 UNC(Universal Naming Convention) 이름을 입력합니다. 자세한 내용은 [백업 디바이스&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 참조하세요.  
  
    > [!IMPORTANT]  
    >  네트워크를 통해 데이터를 백업할 경우에는 네트워크 오류가 발생할 수 있으므로 완료된 후에 백업 작업을 확인하는 것이 좋습니다. 자세한 내용은 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>설명  
 하나 이상의 백업 디바이스 세트에서의 백업이 미디어 세트 하나를 구성합니다. *미디어 세트* 는 하나 이상의 백업 작업에서 고정된 유형과 개수의 백업 디바이스를 사용하여 기록한 백업 미디어, 테이프 또는 디스크 파일의 모음입니다. 미디어 세트에 대한 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)인스턴스를 실행하는 컴퓨터에 테이프 드라이브가 연결되어 있는 경우에만 사용할 수 있습니다.  
  
 미디어 세트의 첫 번째 백업이 논리적 백업 디바이스에 기록되면 논리적 백업 디바이스에 해당하는 물리적 백업 디바이스가 초기화됩니다. 물리적 백업 디바이스가 아직 존재하지 않는 파일인 경우 이 시점에 만들어집니다.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [디스크 파일에 대한 논리적 백업 디바이스 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [테이프 드라이브에 대한 논리적 백업 디바이스 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [디스크 또는 테이프를 백업 대상으로 지정&#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [백업 디바이스 삭제&#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [백업의 만료 날짜 설정&#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [백업 테이프 또는 파일의 내용 보기&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [백업 세트의 데이터와 로그 파일 보기&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [논리적 백업 디바이스의 속성 및 내용 보기&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [디바이스에서 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [백업 디바이스&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
