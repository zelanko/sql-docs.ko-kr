---
title: 대화형 충돌 해결 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interactive conflict resolution [SQL Server replication]
- interactive resolver [SQL Server replication]
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 172c60c7-f605-4eb5-b185-54ae9e9d3c60
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e138e501e4cf42ba5c48c1bdf1a6bf0f2947ed20
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079244"
---
# <a name="interactive-conflict-resolution"></a>Interactive Conflict Resolution
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 동기화 관리자에서 요청 시 동기화 중에 수동으로 충돌을 해결할 수 있는 대화형 해결 프로그램을 제공합니다. 런타임 시 활성화되는 대화형 해결 프로그램은 충돌하는 각 행의 데이터를 표시하여 충돌 데이터를 보고 편집하며 각 충돌을 개별적으로 해결하는 옵션을 제공하는 그래픽 인터페이스입니다.  
  
 대화형 해결 프로그램은 충돌 뷰어와 비슷합니다. 그러나 충돌 뷰어는 병합 동기화 후 이미 해결된 충돌의 결과를 표시하는 반면 대화형 해결 프로그램은 해결 전 각 충돌을 표시하여 병합 동기화 중 각 충돌의 결과를 결정하도록 허용합니다. 사용자는 충돌 발생 시 대화형 해결 프로그램을 모니터링할 수 있어야 합니다.  
  
> [!NOTE]  
>  대화형 해결을 사용하려면 Windows 동기화 관리자가 필요합니다. 동기화가 Windows 동기화 관리자 외부(예: [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 또는 복제 모니터의 예약 동기화 또는 요청 시 동기화)에서 수행된 경우 아티클에 지정된 해결 프로그램에 따라 사용자 개입 없이도 자동으로 충돌이 해결됩니다. 논리적 레코드와 관련된 충돌은 대화형 해결 프로그램에 표시되지 않습니다. 이러한 충돌에 대한 정보를 보려면 복제 저장 프로시저를 사용합니다. 자세한 내용은 [병합 게시에 대한 충돌 정보 보기&#40;복제 Transact-SQL 프로그래밍&#41;](../view-conflict-information-for-merge-publications.md)을 참조하세요.  
  
## <a name="article-resolvers-and-the-interactive-resolver"></a>아티클 해결 프로그램 및 대화형 해결 프로그램  
 게시가 만들어질 때 충돌 해결 프로그램(기본 해결 프로그램, 비즈니스 논리 처리기 또는 사용자 지정 해결 프로그램)은 특정 아티클에 할당되며 규칙 집합을 사용하여 충돌하는 행 데이터 입력 시 사용해야 하는 데이터 집합을 결정합니다. 대화형 해결 프로그램은 충돌 시 적용되는 내용과 삭제되는 내용을 결정하는 규칙을 가진 별도의 충돌 해결 프로그램이 아니라 기본 및 사용자 지정 해결 프로그램과 함께 사용되는 도구입니다. 아티클 해결 프로그램도 적용할 행 및 삭제할 행을 결정하지만 대화형 해결 프로그램으로 사용자는 결과를 승인, 거부 또는 수정할 수 있는 간섭 기능을 가집니다.  
  
 대화형 해결 프로그램을 사용하려면 필요한 각 아티클과 구독에 대해 대화형 해결을 사용할 수 있게 설정해야 합니다. 하나 이상의 아티클과 구독에 대해 대화형 해결을 사용할 수 있게 설정하면 병합 동기화 중 충돌이 감지될 때 대화형 해결 프로그램이 사용됩니다.  
  
 대화형 해결 프로그램을 사용하려면 [병합 아티클에 대한 상호 충돌 해결 프로그램 지정](../publish/specify-interactive-conflict-resolution-for-merge-articles.md) 및 [Windows 동기화 관리자를 사용하여 구독 동기화&#40;Windows 동기화 관리자&#41;](../synchronize-a-subscription-using-windows-synchronization-manager.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Advanced Merge Replication Conflict Detection and Resolution](advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  