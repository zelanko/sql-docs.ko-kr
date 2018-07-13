---
title: 백업 파일이 데이터베이스 파일과 별개의 장치에 있어야 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7039bebb-1f25-4cf3-81f1-393dfb78da12
caps.latest.revision: 12
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5b67881d455e6cb7b29ff2bb6792bafb0e702263
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180340"
---
# <a name="backup-files-must-be-on-separate-devices-from-the-database-files"></a>백업 파일을 데이터베이스 파일과 별개의 장치에 두어야 함
  이 규칙은 데이터베이스 파일이 백업 파일과 별개의 장치에 있는지 검사합니다. 데이터베이스 파일과 백업 파일이 동일한 장치에 있는 경우 해당 장치에 오류가 발생하면 데이터베이스와 백업을 모두 사용할 수 없게 됩니다. 또한 데이터베이스 파일과 백업 파일을 별개의 장치에 두면 데이터베이스의 프로덕션 사용과 백업 작성에 대한 I/O 성능이 모두 최적화됩니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 데이터베이스와 백업은 별개의 백업 장치에 두는 것이 가장 좋습니다.  
  
> [!NOTE]  
>  이 정책은 탑재 지점을 통해 개별 물리적 장치를 검색할 수 없습니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [백업 장치&#40;SQL Server&#41;](../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
 [SQL Server 데이터베이스 백업 및 복원](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
