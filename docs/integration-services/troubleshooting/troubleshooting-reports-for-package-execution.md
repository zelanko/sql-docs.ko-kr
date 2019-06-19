---
title: 패키지 실행 보고서 문제 해결 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8fc476ac-bd69-434e-9636-70776e0b3b6c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2813698ebc127f630c17e8e0ed0db503180e2a67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65713682"
---
# <a name="troubleshooting-reports-for-package-execution"></a>패키지 실행 보고서 문제 해결

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 현재 릴리스에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 카탈로그에 배포된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 모니터링하고 문제를 해결하는 데 도움이 되는 표준 보고서를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 사용할 수 있습니다. 특히 이 두 가지 패키지 보고서는 패키지 실행 상태를 보고 실행 실패 원인을 파악하는 데 도움이 됩니다.  
  
-   **Integration Services 대시보드** - 이 보고서에서는 지난 24시간 내 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 패키지 실행에 대한 개요를 제공합니다. 이 보고서에는 각 패키지에 대한 상태, 작업 유형, 패키지 이름 등의 정보가 표시됩니다.  
  
     시작 시간, 종료 시간 및 기간은 다음과 같이 해석될 수 있습니다.  
  
    -   패키지가 계속 실행 중이면 기간 = 현재 시간 – 시작 시간  
  
    -   패키지가 완료된 경우에는 기간 = 종료 시간 - 시작 시간  
  
     대시보드에서는 서버에서 실행된 각 패키지를 "확대"하여 발생했을 수 있는 패키지 실행 오류에 대한 특정 세부 정보를 찾을 수 있습니다. 예를 들어 **개요** 를 클릭하여 실행에 포함된 태스크의 상태에 대한 상위 수준 개요를 표시하거나 **모든 메시지** 를 클릭하여 패키지 실행의 일부로 캡처된 자세한 메시지를 표시할 수 있습니다.  
  
     **필터** 를 클릭한 다음 **필터 설정** 대화 상자에서 조건을 선택하여 페이지에 표시되는 테이블을 필터링할 수 있습니다. 사용 가능한 필터 조건은 표시되고 있는 데이터에 따라 달라집니다. **필터 설정** 대화 상자에서 정렬 아이콘을 클릭하여 보고서의 정렬 순서를 변경할 수 있습니다.  
  
-   **작업 - 모든 실행 보고서** – 이 보고서에는 서버에서 수행된 모든 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 실행에 대한 요약 내용이 표시됩니다. 요약 내용으로는 상태, 시작 시간 및 종료 시간과 같은 각 실행에 대한 정보가 표시됩니다. 각 요약 항목에는 실행하는 중에 생성된 메시지 및 성능 데이터를 비롯하여 실행에 대한 자세한 내용을 볼 수 있는 링크가 포함됩니다. Integration Services 대시보드를 사용하는 경우와 마찬가지로 테이블에 필터를 적용하여 표시되는 정보를 좁힐 수 있습니다.  
  
## <a name="related-content"></a>관련 내용  
 [Integration Services 서버를 위한 보고서](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)  
  
 [패키지 실행 문제 해결 도구](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
