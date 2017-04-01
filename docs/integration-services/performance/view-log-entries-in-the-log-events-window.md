---
title: "이벤트 로그 창에서 로그 항목 보기 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "로그 [Integration Services], 보기"
  - "Integration Services 패키지, 로그"
  - "패키지 [Integration Services], 로그"
ms.assetid: c02123c3-67fc-4370-ad14-91ed259f1873
caps.latest.revision: 21
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 21
---
# 이벤트 로그 창에서 로그 항목 보기
  이 절차에서는 패키지를 실행하고 패키지에서 작성한 로그 항목을 보는 방법을 설명합니다. 로그 항목은 실시간으로 볼 수 있습니다. **이벤트 로그** 창에 기록된 로그 항목을 상세히 분석할 수 있게 복사하여 저장할 수도 있습니다.  
  
 항목을 **이벤트 로그** 창에 쓰기 위해 로그 항목을 로그에 쓰지 않아도 됩니다.  
  
### 로그 항목을 보려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **SSIS** 메뉴에서 **이벤트 로그**를 클릭합니다. 필요한 경우 View.LogEvents 명령을 **옵션** 대화 상자의 **키보드** 페이지에서 선택한 키 조합에 매핑하여 **이벤트 로그** 창을 표시할 수도 있습니다.  
  
3.  **디버그** 메뉴에서 **디버깅 시작**을 클릭합니다.  
  
     로깅하도록 설정한 이벤트 및 사용자 지정 메시지가 런타임에 발생하면 각 이벤트나 메시지의 로그 항목이 **이벤트 로그** 창에 작성됩니다.  
  
4.  **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.  
  
     패키지를 반환하거나, 다른 패키지를 실행하거나, **를 닫을 때까지 로그 항목은** 이벤트 로그 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]창에서 사용할 수 있는 상태로 유지됩니다.  
  
5.  **이벤트 로그** 창에서 로그 항목을 확인합니다.  
  
6.  필요에 따라 복사할 로그 항목을 클릭하고 마우스 오른쪽 단추를 클릭한 다음 **복사**를 클릭합니다.  
  
7.  필요에 따라 로그 항목을 두 번 클릭하고 **로그 항목** 대화 상자에서 단일 로그 항목에 대한 세부 사항을 확인합니다.  
  
8.  **로그 항목** 대화 상자에서 위쪽 및 아래쪽 화살표를 클릭하여 이전 또는 다음 로그 항목을 표시하고 복사 아이콘을 클릭하여 로그 항목을 복사합니다.  
  
9. 텍스트 편집기를 열고 로그 항목을 텍스트 파일에 붙여넣은 다음 저장합니다.  
  
## 관련 항목:  
 [Integration Services&#40;SSIS&#41; 로깅](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  