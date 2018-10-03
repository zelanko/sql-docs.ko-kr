---
title: Integration Services 서비스에 대 한 이벤트 보기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- events [Integration Services]
- service [Integration Services], events
- Integration Services service, events
ms.assetid: 37e23946-10d1-4116-8568-8fd24067102e
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 887fa745a0f4fab9d7faf716fd7ad26fb3be1fb3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158473"
---
# <a name="view-events-for-the-integration-services-service"></a>Integration Services 서비스의 뷰 이벤트
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스의 이벤트는 다음 두 도구를 사용하여 볼 수 있습니다.  
  
-   **의** 로그 파일 뷰어 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]대화 상자. **로그 파일 뷰어** 대화 상자에는 로그를 내보내고 필터링하고 검색하는 옵션이 포함되어 있습니다. **로그 파일 뷰어**의 옵션에 대한 자세한 내용은 [로그 파일 뷰어 F1 도움말](../relational-databases/logs/log-file-viewer-f1-help.md)을 참조하세요.  
  
-   Windows 이벤트 뷰어  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서비스에 의해 기록된 이벤트에 대한 설명은 [Integration Services 서비스에서 기록하는 이벤트](service/events-logged-by-the-integration-services-service.md)를 참조하세요.  
  
### <a name="to-view-service-events-for-integration-services-in-sql-server-management-studio"></a>SQL Server Management Studio에서 Integration Services의 서비스 이벤트를 보려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 엽니다.  
  
2.  **파일** 메뉴에서 **개체 탐색기 연결**을 클릭합니다.  
  
3.  **서버에 연결** 대화 상자에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버 유형을 선택하고 연결할 서버를 선택하거나 찾은 다음 **연결**을 클릭합니다.  
  
4.  개체 탐색기에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 를 마우스 오른쪽 단추로 클릭하고 **로그 보기**를 선택합니다.  
  
5.  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 이벤트를 보려면 **SQL Server Integration Services**를 선택합니다. **NT 이벤트** 옵션은 **SQL Server Integration Services** 옵션에 따라 자동으로 선택 및 선택 취소됩니다.  
  
### <a name="to-view-service-events-for-integration-services-in-windows-event-viewer"></a>Windows 이벤트 뷰어에서 Integration Services의 서비스 이벤트를 보려면  
  
1.  클래식 보기를 사용할 경우에는 **제어판**에서 **관리 도구**를 클릭하고 종류별 보기를 사용할 경우에는 제어판에서 **성능 및 유지 관리** 를 클릭한 후 **관리 도구**를 클릭합니다.  
  
2.  **이벤트 뷰어**를 클릭합니다.  
  
3.  **이벤트 뷰어** 대화 상자에서 **응용 프로그램**을 클릭합니다.  
  
4.  **응용 프로그램** 스냅인의 **원본** 열 값이 **SQLISService**인 항목을 찾아 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
5.  필요에 따라 위쪽 또는 아래쪽 화살표를 클릭하여 이전 또는 다음 이벤트를 표시합니다.  
  
6.  필요에 따라 클립보드로 복사 아이콘을 클릭하여 이벤트 정보를 복사합니다.  
  
7.  바이트 또는 워드를 사용하여 이벤트 데이터를 표시하도록 선택합니다.  
  
8.  **확인**을 클릭합니다.  
  
9. **파일** 메뉴에서 **끝내기** 를 클릭하여 **이벤트 뷰어** 대화 상자를 닫습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 서비스 관리](../../2014/integration-services/manage-the-integration-services-service.md)   
 [데이터 흐름 성능 카운터에 대한 로그 추가](performance/performance-counters.md)  
  
  
