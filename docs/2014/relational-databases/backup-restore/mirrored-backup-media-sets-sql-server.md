---
title: 미러된 백업 미디어 세트(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server], mirrored backups
- mirrored media sets [SQL Server]
- backup mirrors [SQL Server]
- duplicate backup copies
- interchangeable backup copies [SQL Server]
- media sets [SQL Server], mirrored backup media sets
- backup media [SQL Server], mirrored media
ms.assetid: 05a0b8d1-3585-4f77-972f-69d1c0d4aa9b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ad183871e58f5dc64cf763c540e1629a09b4f320
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62876102"
---
# <a name="mirrored-backup-media-sets-sql-server"></a>미러된 백업 미디어 세트(SQL Server)
    
> [!NOTE]  
>  미러된 백업 미디어 세트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Enterprise Edition에서만 지원됩니다.  
  
 미디어 세트를 미러링하면 백업 장치의 오작동에 따른 영향이 감소되어 백업 안정성이 향상됩니다. 데이터 손실을 방지할 수 있는 최후의 수단이 백업이므로 이러한 오작동은 매우 심각합니다. 데이터베이스가 커지면 백업 디바이스 또는 미디어의 실패로 복원 불가능한 백업을 만들게 될 가능성이 커집니다. 백업 미디어를 미러링하면 중복이 가능하여 백업의 안정성이 향상됩니다.  
  
> [!NOTE]  
>  일반적인 미디어 세트에 대한 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)Enterprise Edition에서만 지원됩니다.  
  
 **항목 내용:**  
  
-   [미러된 미디어 세트 개요](#OverviewofMirroredMediaSets)  
  
-   [백업 미러에 대한 하드웨어 요구 사항](#HardwareReqs)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="OverviewofMirroredMediaSets"></a> 미러된 미디어 세트 개요  
 미디어 미러링은 미디어 세트의 속성입니다. *미러된 미디어 세트* 는 미디어 세트의 여러 복사본(*미러*)으로 구성됩니다. 미디어 세트에는 미디어 패밀리가 하나 이상 포함되어 있으며 각각은 백업 디바이스에 해당합니다. 예를 들어 BACKUP DATABASE 문의 TO 절에 디바이스가 3개 나열되어 있으면 BACKUP에서는 디바이스당 하나씩 3개의 미디어 패밀리에 데이터를 분산합니다. 미디어 패밀리 및 미러의 수는 WITH FORMAT을 지정하는 BACKUP DATABASE 문으로 미디어 세트를 만들 때 정의됩니다.  
  
 미러된 미디어 세트에는 2~4개의 미러가 있습니다. 각 미러는 미디어 세트의 모든 미디어 패밀리를 포함합니다. 미러 수는 미디어 패밀리당 하나씩이며 디바이스의 수와 같아야 합니다. 각 미러에서는 미디어 패밀리마다 별도의 백업 디바이스가 있어야 합니다. 예를 들어 3개의 미러가 있는 미디어 패밀리 4개로 구성된 미러된 미디어 세트에는 12개의 백업 디바이스가 있어야 합니다. 이러한 디바이스는 모두 같아야 합니다. 예를 들어 테이프 드라이브는 동일한 제조업체에서 만든 장치로 모델 번호가 같아야 합니다.  
  
 다음 그림에서는 두 개의 미러가 있는 미디어 패밀리 두 개로 구성된 미러된 미디어 세트의 예를 보여 줍니다. 각 미디어 패밀리에는 미디어 볼륨이 3개씩 들어 있으며 미러당 한 번씩 백업됩니다.  
  
 ![미러된 미디어 세트: 미러가 2개 있는 두 패밀리](../../database-engine/media/bnr-backup-media-mirror.gif "미러된 미디어 세트: 미러가 2개 있는 두 패밀리")  
  
 미러의 해당 볼륨의 내용은 동일하므로 복원할 때 서로 교환될 수 있습니다. 예를 들어 위의 그림에서 테이프 2의 3번째 볼륨은 테이프 0의 3번째 볼륨과 바꾸어 사용할 수 있습니다.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 은 장치에 대한 쓰기를 동기화하여 미러된 미디어의 내용이 동일하도록 합니다. 미러 중 하나가 채워지면 나머지 미러도 모두 동시에 스팬됩니다.  
  
> [!IMPORTANT]  
>  미러된 미디어 세트는 미러 제거를 통해 암시적으로 분할될 수 없습니다. 미러의 테이프 또는 디스크가 손상되거나 다시 포맷되는 경우 해당 미러는 추가 백업에 더 이상 사용할 수 없습니다. 채워진 미러가 하나 이상 그대로 유지되는 경우 해당 미디어 세트를 읽을 수 있습니다. 모든 미러에서 지정된 미디어 패밀리가 손실될 경우 해당 미디어 세트는 쓸모없게 됩니다.  
  
 백업 및 복원 작업은 모든 미러가 있어야 하는지에 따라 다른 요구 사항이 적용됩니다. 미러된 미디어 세트에 쓰는(즉, 작성하거나 확장하는) 백업 작업의 경우 모든 미러가 있어야 합니다. 반대로 미러된 미디어 세트의 백업을 복원하려는 경우 각 미디어 패밀리에 하나의 미러만 지정할 수 있습니다. 패밀리 수보다 적은 수의 디바이스에서 복원할 수 있으나 각 미디어 패밀리는 한 번만 처리됩니다. 그러나 오류가 발생할 때 다른 미러가 있으면 일부 복원 문제를 빨리 해결할 수 있습니다. 손상된 미디어 볼륨은 다른 미러에서 상응하는 볼륨으로 대체할 수 있습니다. 이는 RESTORE 및 RESTORE VERIFYONLY가 손상된 미디어를 다른 미러의 해당 백업 미디어 볼륨으로 대체하는 기능을 지원하기 때문입니다.  
  
##  <a name="HardwareReqs"></a> 백업 미러에 대한 하드웨어 요구 사항  
 미러링은 디스크와 테이프에 모두 적용됩니다. 디스크는 연속 테이프를 지원하지 않습니다. 단일 백업 작업 또는 복원 작업에서 사용하는 모든 백업 디바이스는 같은 유형의 디스크 또는 테이프여야 합니다.  
  
 다양한 여러 종류 중에서 속성이 같은 유사한 디바이스를 사용해야 합니다. 유사하지 않은 디바이스를 사용하면 오류 메시지(3212)가 발생합니다. 부합되는 디바이스를 사용하려면 동일한 디바이스, 즉 제조업체가 같고 모델 번호도 같은 드라이브만 사용합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **미러된 백업 장치에 백업하려면**  
  
-   [미러된 미디어 세트에 백업&#40;Transact-SQL&#41;](back-up-to-a-mirrored-media-set-transact-sql.md)  
  
## <a name="see-also"></a>관련 항목  
 [백업 및 복원 중 발생 가능한 미디어 오류&#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)   
 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)   
 [백업 장치&#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
