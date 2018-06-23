---
title: 데이터 흐름 성능 카운터에 대 한 로그 추가 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- performance counters [Integration Services]
- counters [Integration Services]
- logs [Integration Services], data flow counters
ms.assetid: b500d166-33ba-4b82-a92d-b0a333924e8d
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e659cfb46c514a13e090e244ee56c4bbc7ce8e61
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36180550"
---
# <a name="add-a-log-for-data-flow-performance-counters"></a>데이터 흐름 성능 카운터에 대한 로그 추가
  이 절차에서는 데이터 엔진에서 제공하는 성능 카운터에 대한 로그를 추가하는 방법을 설명합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 을 실행하는 컴퓨터에 [!INCLUDE[winxpsvr](../includes/winxpsvr-md.md)]를 설치한 다음 해당 컴퓨터를 [!INCLUDE[firstref_longhorn](../includes/firstref-longhorn-md.md)]로 업그레이드하는 경우 업그레이드 프로세스는 컴퓨터에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 성능 카운터를 제거합니다. 컴퓨터에 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 성능 카운터를 복원하려면 복원 모드에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 설치 프로그램을 실행합니다.  
  
### <a name="to-add-logging-of-performance-counters"></a>성능 카운터 로깅을 추가하려면  
  
1.  클래식 보기를 사용하는 경우 **제어판**에서 **관리 도구**를 클릭합니다. 종류별 보기를 사용하는 경우 **성능 및 유지 관리** 를 클릭한 다음 **관리 도구**를 클릭합니다.  
  
2.  **성능**을 클릭합니다.  
  
3.  **성능** 대화 상자에서 **성능 로그 및 경고**를 확장하고 **카운터 로그**를 마우스 오른쪽 단추로 클릭한 다음 **새 로그 설정**을 클릭합니다. 로그 이름을 입력합니다. 예를 들어 **MyLog**를 입력합니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  **MyLog** 대화 상자에서 **카운터 추가**를 클릭합니다.  
  
6.  **로컬 컴퓨터 카운터 사용** 을 클릭하여 로컬 컴퓨터에 성능 카운터를 로그하거나 **다음 컴퓨터에서 카운터 선택** 을 클릭하고 목록에서 컴퓨터를 선택하여 지정된 컴퓨터에서 성능 카운터를 로그합니다.  
  
7.  **카운터 추가** 대화 상자의 **성능 개체** 목록에서 **SQL Server:SSIS Pipeline** 을 선택합니다.  
  
8.  다음 중 하나를 수행하여 성능 카운터를 선택합니다.  
  
    -   **모든 카운터** 를 선택하여 모든 성능 카운터를 로그합니다.  
  
    -   **목록에서 카운터 선택** 을 선택하고 사용할 성능 카운터를 선택합니다.  
  
9. **추가**를 클릭합니다.  
  
10. **닫기**를 클릭합니다.  
  
11. **MyLog** 대화 상자의 **카운터** 목록에서 로깅 성능 카운터 목록을 검토합니다.  
  
12. 추가 카운터를 추가하려면 5단계~10단계를 반복합니다.  
  
13. **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  Administrators 그룹의 멤버인 로컬 계정 또는 도메인 계정을 사용하여 성능 로그 및 경고 서비스를 시작해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [성능 카운터](performance/performance-counters.md)   
 [이벤트 로그 창에서 로그 항목 보기](../../2014/integration-services/view-log-entries-in-the-log-events-window.md)  
  
  