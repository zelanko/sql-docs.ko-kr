---
title: 원본 제어 기본 사항 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- source controls [SQL Server Management Studio], providers
- source controls [SQL Server Management Studio]
- source controls [SQL Server Management Studio], about source controls
- source controls [SQL Server Management Studio], clients
ms.assetid: ca35b67a-104a-41fb-ac58-a61be06fe114
caps.latest.revision: 23
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1c70c039fd32643dc69c12e76109f5a7fc900379
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217853"
---
# <a name="source-control-basics"></a>원본 제어 기본 사항
  소스 제어란 서버 소프트웨어의 중심부에서 파일 버전을 저장 및 추적하고 파일에 대한 액세스를 제어하는 시스템을 말합니다. 일반 원본 제어 시스템에는 원본 제어 공급자 및 둘 이상의 원본 제어 클라이언트가 포함됩니다.  
  
## <a name="source-control-benefits"></a>원본 제어의 이점  
 파일이 원본 제어에서 사용 중일 경우 다음 작업을 수행할 수 있습니다.  
  
-   항목 제어가 특정 사용자에서 다른 사용자에게 전달되는 프로세스를 관리합니다. 원본 제어 공급자는 공유 및 배타 파일 액세스를 모두 지원합니다. 프로젝트 파일에 대한 액세스가 배타적이면 원본 제어 공급자는 한 번에 한 명의 사용자만 파일을 체크 아웃하고 수정하도록 허용합니다. 액세스가 공유될 경우 둘 이상의 사용자가 스크립트 파일을 체크 아웃할 수 있으며 원본 제어 공급자는 체크 인되는 버전을 병합하기 위한 메커니즘을 제공합니다.  
  
-   연속된 버전의 원본 제어 항목을 보관합니다. 원본 제어 공급자는 특정 버전의 원본 제어 항목을 다른 버전의 항목과 구별하는 데이터를 저장합니다. 소스 제어 공급자는 버전 간의 차이점뿐만 아니라 버전에 대한 중대한 정보, 즉 버전을 작성 및 수정한 시점과 버전을 작성 및 수정한 사람에 대한 정보를 저장합니다. 동일한 파일에서 여러 사람이 작업하는 중이면 동일한 코드 페이지를 사용해야만 버전을 정확하게 비교할 수 있습니다. 결과적으로 모든 버전의 원본 제어 항목을 검색할 수 있습니다. 또한 임의의 버전을 해당 항목의 최신 버전으로 지정할 수 있습니다.  
  
-   원본 제어 항목에 대한 자세한 기록 및 버전 정보를 유지 관리합니다. 원본 제어는 항목을 만든 날짜와 시간, 체크 아웃 및 체크 인된 시기, 동작을 수행한 사용자에 대한 정보를 저장합니다.  
  
-   여러 프로젝트에서 공동 작업을 수행합니다. 파일 공유를 사용하면 여러 프로젝트에서 원본 제어 항목을 공유할 수 있습니다. 공유 항목을 변경하면 해당 항목을 공유하는 모든 프로젝트에 변경 내용이 반영됩니다.  
  
-   자주 반복되는 원본 제어 작업을 자동화합니다. 원본 제어 공급자는 원본 제어의 주요 기능을 지원하는 명령 프롬프트에서 인터페이스를 정의할 수 있습니다. 배치 파일에서 이 인터페이스를 사용하여 정기적으로 수행하는 원본 제어 태스크를 자동화할 수 있습니다.  
  
-   실수로 삭제한 내용을 복원합니다. 원본 제어에 체크 인된 최신 파일 버전을 복원할 수 있습니다.  
  
-   원본 제어 클라이언트 및 서버 모두에서 디스크 공간을 절약합니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe와 같은 일부 원본 제어 공급자는 파일의 최신 버전과 각 버전 및 이전 또는 이후 버전의 차이를 저장하여 서버에서 디스크 공간을 절약할 수 있습니다. 클라이언트에서도 Visual SourceSafe는 디스크 공간 절약을 지원합니다. 로컬 디스크로 다운로드되지 않도록 폴더와 파일을 숨길 수 있습니다.  
  
 파일 체크 아웃, 체크 인 및 기타 원본 제어 작업은 실제로 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 같은 원본 제어 클라이언트를 통해 수행합니다. 원본 제어 클라이언트는 대상 사용자 그룹에서 공급자의 기능을 사용할 수 있도록 공급자와 상호 작용하도록 설계되었습니다. 원본 제어 클라이언트를 사용하면 사용자는 공급자에 의해 저장된 파일을 탐색하거나 파일을 추가 및 삭제하거나 파일을 체크 인 및 체크 아웃하거나 로컬 파일의 복사본을 검색할 수 있습니다.  
  
> [!NOTE]  
>  이 설명서에서는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe를 원본 제어 공급자로 사용한다고 가정합니다. 다른 원본 제어 공급자를 사용하는 경우 이 설명서와 실행 중인 소프트웨어 간에 차이점이 발견될 수 있습니다. 이러한 차이점이 있을 경우에는 해당 원본 제어 공급자의 설명서를 참조하십시오.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|**태스크**|**항목**|  
|원본 제어 옵션 설정|[원본 제어 옵션 설정](../../2014/database-engine/set-source-control-options.md)|  
|원본 제어 연결 변경|[원본 제어 연결 변경](../../2014/database-engine/change-source-control-connections.md)|  
|원본 제어에서 파일 제외|[원본 제어에서 파일 제외](../../2014/database-engine/exclude-files-from-source-control.md)|  
  
  
