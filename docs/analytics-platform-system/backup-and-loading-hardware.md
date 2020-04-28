---
title: 하드웨어를 로드 하 & 백업
description: PDW (병렬 데이터 웨어하우스)를 사용 하 여 APS (분석 플랫폼 시스템)에 종단 간 데이터 웨어하우징 솔루션을 배포 하려면 데이터 웨어하우스를 백업 하 고 데이터를 로드 하는 계획을 세워야 합니다. 이 지침을 사용 하 여 비즈니스 요구 사항을 충족 하는 백업 및 로드 서버를 확보 하 고 구성할 수 있습니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4dd4fba91b1507f711a66a88f40b2fa2ea35e1ae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401365"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>하드웨어 백업 및 로드 개요-병렬 데이터 웨어하우스
PDW (병렬 데이터 웨어하우스)를 사용 하 여 APS (분석 플랫폼 시스템)에 종단 간 데이터 웨어하우징 솔루션을 배포 하려면 데이터 웨어하우스를 백업 하 고 데이터를 로드 하는 계획을 세워야 합니다. 이 지침을 사용 하 여 비즈니스 요구 사항을 충족 하는 백업 및 로드 서버를 확보 하 고 구성할 수 있습니다.  
  
## <a name="acquire-and-configure-backup-servers"></a>백업 서버 가져오기 및 구성  
![백업 프로세스](media/backup-process.png "백업 프로세스")  
  
PDW 데이터베이스를 백업 하려면 백업 서버가 하나 이상 필요 합니다. 자신의 기존 하드웨어를 사용 하거나 새 하드웨어를 구매할 수 있습니다. 자세한 내용은 [백업 서버 가져오기 및 구성](acquire-and-configure-backup-server.md)을 참조 하세요. 이러한 지침에는 백업에 적합 한 솔루션을 계획 하는 데 도움이 되는 [백업 서버 용량 계획 워크시트가](backup-capacity-planning-worksheet.md) 포함 되어 있습니다.  
  
## <a name="acquire-and-configure-loading-servers"></a>서버 로드 가져오기 및 구성  
![로드 프로세스](media/loading-process.png "프로세스 로드")  
  
데이터를 로드 하려면 로드 서버가 하나 이상 필요 합니다. 자신의 기존 ETL 또는 다른 서버를 사용 하거나 새 서버를 구입할 수 있습니다. 자세한 내용은 [로드 서버 가져오기 및 구성](acquire-and-configure-loading-server.md)을 참조 하세요. 이러한 지침에는 로딩을 위한 적절 한 솔루션을 계획 하는 데 도움이 되는 [로드 서버 용량 계획 워크시트가](loading-server-capacity-planning-worksheet.md) 포함 되어 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[백업 및 복원 개요](backup-and-restore-overview.md)  
[로드 개요](load-overview.md)  
  
