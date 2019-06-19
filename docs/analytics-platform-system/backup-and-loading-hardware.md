---
title: 하드웨어-병렬 데이터 웨어하우스 백업 및 로드
description: 웨어하우스 솔루션에서 Analytics Platform System (APS) 병렬 데이터 웨어하우스 (PDW)을 사용 하 여 종단 간 데이터를 배포 하려면 데이터 웨어하우스를 백업 하 고 데이터를 로드 하는 것에 대 한 계획을 만드는 해야 합니다. 이 지침을 사용 하 여 획득 및 비즈니스 요구를 충족 하는 백업 및 로드 서버를 구성 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4d7f7b6b4edea9dacab7287a7936b7fd87fd7973
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63065140"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>백업 및 하드웨어 개요-병렬 데이터 웨어하우스를 로드 합니다.
웨어하우스 솔루션에서 Analytics Platform System (APS) 병렬 데이터 웨어하우스 (PDW)을 사용 하 여 종단 간 데이터를 배포 하려면 데이터 웨어하우스를 백업 하 고 데이터를 로드 하는 것에 대 한 계획을 만드는 해야 합니다. 이 지침을 사용 하 여 획득 및 비즈니스 요구를 충족 하는 백업 및 로드 서버를 구성 합니다.  
  
## <a name="acquire-and-configure-backup-servers"></a>획득 및 backup server를 구성 합니다.  
![백업 프로세스](media/backup-process.png "프로세스를 백업 합니다.")  
  
PDW 데이터베이스를 백업 하기 위해 하나 이상의 서버를 백업 해야 합니다. 기존 하드웨어를 사용할 수도 있고 새 하드웨어를 구입할 수 있습니다. 자세한 내용은 [백업 서버 획득 및 구성](acquire-and-configure-backup-server.md)합니다. 이러한 지침에 포함 되어는 [백업 서버 용량 계획 워크시트](backup-capacity-planning-worksheet.md) 백업에 적합 한 솔루션을 계획할 수 있습니다.  
  
## <a name="acquire-and-configure-loading-servers"></a>획득 및 로드 서버를 구성 합니다.  
![로드 프로세스](media/loading-process.png "로드 프로세스")  
  
데이터를 로드 하려면 하나 이상의 서버를 로드 해야 합니다. 사용자 고유의 기존 ETL 또는 다른 서버를 사용 하거나 새 서버를 구입할 수 있습니다. 자세한 내용은 [Acquire 로드 서버를 구성 하 고](acquire-and-configure-loading-server.md)입니다. 이러한 지침에 포함 되어는 [로드 서버 용량 계획 워크시트](loading-server-capacity-planning-worksheet.md) 로드에 적합 한 솔루션을 계획할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
[백업 및 복원 개요](backup-and-restore-overview.md)  
[로드 개요](load-overview.md)  
  
