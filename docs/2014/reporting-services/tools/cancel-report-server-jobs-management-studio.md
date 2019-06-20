---
title: 보고서 서버 작업 취소(Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.cancelreportserverjobs.f1
ms.assetid: 1c5b4975-49e9-4d0b-b298-2638e81edbfd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ab7c4496465de8297f07dd18b3aa2acf26ab305d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100494"
---
# <a name="cancel-report-server-jobs-management-studio"></a>보고서 서버 작업 취소(Management Studio)
  **보고서 서버 작업 취소** 대화 상자를 사용하여 진행 중인 보고서를 보거나 취소할 수 있습니다. 이 대화 상자에는 현재 보고서 서버에서 실행 중인 모든 작업이 표시됩니다. 현재 처리 중인 작업을 일시 중지하거나 다시 시작할 수는 없지만 완료하는 데 오랜 시간이 걸릴 경우 모든 작업 또는 개별 작업을 취소할 수 있습니다.  
  
 사용자 작업과 시스템 작업을 취소할 수 있습니다.  
  
-   사용자 작업은 개별 사용자가 시작한 작업입니다. 여기에는 요청 시 보고서 실행, 보고서 기록 스냅숏 수동 작성, 보고서 실행 스냅숏 수동 작성 등이 포함됩니다. 진행 중인 표준 구독도 사용자 작업입니다.  
  
-   시스템 작업은 보고서 서버에서 시작하는 작업입니다. 시스템 작업에는 예약된 보고서 처리가 포함됩니다.  
  
 이 페이지를 열려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 열고 보고서 서버에 연결한 다음 **작업**을 마우스 오른쪽 단추로 클릭하고 **모든 작업 취소**를 클릭합니다. **작업**을 열고 보고서 서버에서 실행 중인 작업을 마우스 오른쪽 단추로 클릭한 다음 **작업 취소**를 선택할 수도 있습니다.  
  
 작업을 취소하기 전에 해당 작업의 속성을 보면 작업이 시작된 시점을 확인할 수 있습니다. 자세한 내용은 [작업 속성&#40;Management Studio&#41;](job-properties-management-studio.md)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services에서는 이 기능을 지원하지 않습니다. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]를 실행하는 경우 페이지가 나타나지 않습니다.  
  
## <a name="options"></a>변수  
 **이름**  
 보고서 이름을 표시합니다. 구독은 설명으로 확인할 수 있습니다.  
  
 **형식**  
 유효한 값은 **사용자** 와 **시스템**입니다.  
  
 **Start Time**  
 작업이 시작된 시간을 표시합니다.  
  
 **사용자 이름**  
 사용자가 시작한 작업인 경우 이 열에서 사용자 이름을 표시합니다.  
  
 **상태**  
 작업 상태를 표시합니다. 유효한 값은 **신규** 와 **실행 중**입니다. 작업이 시작될 때의 상태는 항상 **새 항목** 입니다. 60초 후에 상태는 **실행 중**으로 변경됩니다. 변경 내용을 표시하려면 페이지를 새로 고쳐야 합니다.  
  
 **확인**  
 하나의 작업 또는 여러 작업을 취소합니다. 작업은 즉시 취소되며 재개할 수 없습니다. 작업을 실수로 취소한 경우 보고서 또는 구독을 다시 요청하여 새 작업을 시작해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Management Studio의 보고서 서버 F1 도움말](report-server-in-management-studio-f1-help.md)   
 [Management Studio에서 보고서 서버에 연결](connect-to-a-report-server-in-management-studio.md)   
 [실행 중인 프로세스 관리](../subscriptions/manage-a-running-process.md)  
  
  
