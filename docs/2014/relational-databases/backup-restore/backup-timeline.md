---
title: 백업 시간대 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.POINTINTIMERESTORE.F1
- sql12.swb.backuptimeline.f1
helpviewer_keywords:
- Backup Timeline
ms.assetid: ae3565f2-ddb2-4469-a992-7531d4f9ebb8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 92cffa7c280aac559433a8fc7ad5a3223c9f6de2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62876705"
---
# <a name="backup-timeline"></a>백업 시간대
  **백업 시간대** 대화 상자를 사용하여 데이터베이스를 지정 시간으로 복원할 백업을 찾고 지정할 수 있습니다. **데이터베이스 복원(일반 페이지)** 창에서 **시간대** 를 클릭하여 **백업 시간대** 대화 상자에 액세스할 수 있습니다. 이 대화 상자에서 데이터베이스에 대해 수행된 복원 작업의 시간대를 확인할 수 있습니다.  
  
 데이터베이스 복구 관리자는 해당 시점에 복원하는 데 필요한 백업만 선택되도록 합니다. 이러한 선택된 백업은 복원 작업에 필요한 권장 복원 계획을 구성합니다. 선택된 백업만 사용해야 합니다. 데이터베이스 복구 관리자에 대한 자세한 내용은 [복원 및 복구 개요&#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)를 참조하세요.  
  
## <a name="restore-to"></a>복원 위치  
 **수행한 마지막 백업** 은 기본적으로 선택됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 데이터베이스를 복원하는 데 적절한 백업을 선택하고 데이터베이스를 마지막 백업 시점으로 복원합니다. 특정 지정 시간을 선택하여 날짜와 시간을 수동으로 설정하려면 **특정 날짜 및 시간** 을 클릭합니다.  
  
 **특정 날짜 및 시간** 을 사용하여 선택한 날짜와 시간에서 복원을 중지할 수 있습니다. 시간대에는 선택한 날짜 및 시간을 기준으로 24시간 이내에 수행된 백업 작업이 표시됩니다.  
  
 **날짜**  
 날짜를 입력하거나 드롭다운 목록에서 선택합니다.  
  
 **Time**  
 날짜를 입력하거나 선택하여 복원을 중지할 특정 시점을 지정할 수 있습니다.  
  
 **일정 기간**  
 시간대에 표시할 수 있는 간격 유형 옵션을 표시합니다.  
  
## <a name="timeline-and-legend"></a>시간대 및 범례  
 시간대 아래에 있는 스크롤 막대를 사용하여 시간대를 따라 커서를 앞이나 뒤로 이동할 수 있습니다. 백업을 클릭하여 스크롤 막대를 백업의 끝으로 이동할 수 있습니다. 마우스를 표식 위로 이동하면 선택한 백업 세트에 대한 정보를 제공하는 화면 설명이 표시됩니다. 다음 표식은 시간대에 백업 정보를 표시합니다.  
  
 큰 삼각형  
 데이터베이스에 대해 수행된 전체 백업을 나타내며 각 전체 백업이 수행된 특정 지정 시간을 나타냅니다.  
  
 작은 삼각형  
 데이터베이스에 대해 수행된 차등 백업을 나타내며 각 차등 백업이 수행된 특정 지정 시간을 나타냅니다.  
  
 녹색 음영 영역  
 트랜잭션 로그 백업의 범위를 나타냅니다.  
  
 빨강 선  
 시간대에서 복원이 가능한 지점에만 놓일 수 있습니다. 시간대를 따라 빨강 선을 이동하면 **날짜** 및 **시간** 상자에 표시되는 날짜와 시간이 조정됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 복원&#40;일반 페이지&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  
