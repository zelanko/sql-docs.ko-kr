---
title: 작업 속성(Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.jobproperties.f1
ms.assetid: 807ffd0e-9363-4f8f-9c36-c5d746ad19fd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f00250011f3c325ca39c3c040e5252b804182d86
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66100223"
---
# <a name="job-properties-management-studio"></a>작업 속성(Management Studio)
  **작업 속성** 페이지를 사용하여 진행 중인 보고서 또는 구독을 취소하기 전에 이에 대한 정보를 볼 수 있습니다.  
  
 이 페이지를 열려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작하고 보고서 서버에 연결한 다음 **작업** 폴더를 엽니다. 실행 중인 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services에서는 이 기능을 지원하지 않습니다. [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]를 실행하는 경우 페이지가 나타나지 않습니다.  
  
## <a name="tasks"></a>태스크  
 작업에 대한 정보를 보려면 페이지를 새로 고쳐 현재 보고서 서버에서 실행 중인 작업에 대한 정보를 가져와야 합니다.  
  
1.  보고서 서버 폴더를 엽니다.  
  
2.  **작업**을 마우스 오른쪽 단추로 클릭한 다음 **새로 고침**을 클릭합니다.  
  
3.  작업이 표시되면 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
## <a name="options"></a>변수  
 **작업 ID**  
 작업이 처리되는 중에 작업에 할당된 GUID입니다. 이 값은 보고서 또는 구독이 실행될 때마다 임의로 생성됩니다.  
  
 **작업 상태**  
 유효한 값은 **신규** 와 **실행 중**입니다. 작업이 시작될 때의 상태는 항상 **새 항목** 입니다. 60초 후에 상태는 **실행 중**으로 변경됩니다. 변경 내용을 표시하려면 페이지를 새로 고쳐야 합니다.  
  
 **작업 유형**  
 유효한 값은 **사용자** 와 **시스템**입니다. 사용자 작업은 개별 사용자가 시작한 작업입니다. 여기에는 요청 시 보고서 실행, 보고서 기록 스냅숏 수동 생성, 보고서 실행 스냅숏 수동 생성 등이 포함됩니다. 진행 중인 표준 구독도 사용자 작업입니다. 시스템 작업은 보고서 서버에서 시작하는 작업입니다. 시스템 작업에는 예약에 따라 트리거되는 보고서 처리가 포함됩니다.  
  
 **작업 동작**  
 보고서의 경우 이 열에서 진행 중인 보고서 실행 프로세스를 표시합니다. 이 값은 항상 **렌더링**입니다.  
  
 **작업 설명**  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서는 기본적으로 작업 설명이 제공되지 않습니다.  
  
 **서버 이름**  
 작업을 처리 중인 보고서 서버의 이름을 표시합니다. 스케일 아웃 배포를 구성한 경우 이 값은 작업을 처리 중인 서버를 표시합니다.  
  
 **보고서 이름**  
 보고서 이름을 표시합니다. 구독은 설명으로 확인할 수 있습니다.  
  
 **보고서 경로**  
 보고서 서버 폴더 계층에 있는 보고서의 경로를 표시합니다.  
  
 **Start Time**  
 프로세스를 시작한 시간을 표시합니다.  
  
 **사용자 이름**  
 사용자가 시작한 프로세스인 경우 이 열에서 사용자 이름을 표시합니다. 시스템 작업의 경우 보고서 서버의 이름입니다.  
  
## <a name="see-also"></a>관련 항목  
 [Management Studio의 보고서 서버 F1 도움말](report-server-in-management-studio-f1-help.md)   
 [Management Studio에서 보고서 서버에 연결](connect-to-a-report-server-in-management-studio.md)   
 [실행 중인 프로세스 관리](../subscriptions/manage-a-running-process.md)  
  
  
