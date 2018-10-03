---
title: 저장 된 구성 파일을 사용 하 여 로깅을 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], logs
- logs [Integration Services], containers
ms.assetid: e5fdbbcb-94ca-4912-aa7c-0d89cebbd308
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f3c22ca7f44844b434dc74e881830363a79475ee
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48146393"
---
# <a name="configure-logging-by-using-a-saved-configuration-file"></a>저장된 구성 파일을 사용하여 로깅 구성
  이 절차에서는 이전에 저장된 로깅 구성 파일을 로드하여 패키지 내의 새 컨테이너를 위한 로깅을 구성하는 방법을 설명합니다.  
  
 기본적으로 패키지의 모든 컨테이너는 부모 컨테이너와 동일한 로깅 구성을 사용합니다. 예를 들어 Foreach 루프 내의 태스크는 Foreach 루프와 동일한 로깅 구성을 사용합니다.  
  
### <a name="to-configure-logging-for-a-container"></a>컨테이너에 대한 로깅을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  **SSIS** 메뉴에서 **로깅**을 클릭합니다.  
  
3.  패키지 트리 뷰를 확장하고 구성할 컨테이너를 선택합니다.  
  
4.  **공급자 및 로그** 탭에서 컨테이너로 사용할 로그를 선택합니다.  
  
    > [!NOTE]  
    >  패키지 수준에서만 로그를 만들 수 있습니다. 자세한 내용은 [SQL Server Data Tools에서 패키지 로깅 사용](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)을 참조하세요.  
  
5.  **자세히** 탭을 클릭하고 **로드**를 클릭합니다.  
  
6.  사용할 로깅 구성 파일을 찾고 **열기**를 클릭합니다.  
  
7.  필요에 따라 **이벤트** 열에서 해당 확인란을 선택하여 기록할 다른 로그 항목을 선택합니다. **고급** 을 클릭하여 이 항목에 대해 기록할 정보 유형을 선택합니다.  
  
    > [!NOTE]  
    >  새 컨테이너는 원래 로깅 구성을 만드는 데 사용된 컨테이너에는 사용할 수 없는 추가 로그 항목을 포함할 수 있습니다. 이러한 추가 로그 항목을 로그하려면 수동으로 선택해야 합니다.  
  
8.  로깅 구성의 업데이트된 버전을 저장하려면 **저장**을 클릭합니다.  
  
9. 업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **선택한 항목 저장** 을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services&#40;SSIS&#41; 로깅](performance/integration-services-ssis-logging.md)  
  
  
