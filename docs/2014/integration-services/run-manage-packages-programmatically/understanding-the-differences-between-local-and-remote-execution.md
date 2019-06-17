---
title: 로컬 실행과 원격 실행의 차이점 이해 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- packages [Integration Services], troubleshooting
ms.assetid: 610ee7d9-4fea-4aba-9395-57add826923b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dd8665ee828395e277482b7775131167fcc182eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62889356"
---
# <a name="understanding-the-differences-between-local-and-remote-execution"></a>로컬 실행과 원격 실행의 차이점 이해
  패키지 개발자와 관리자는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지가 실행되는 위치와 관련된 제한 사항을 알고 있어야 합니다.  
  
-   **패키지는 해당 패키지를 실행하는 프로그램과 동일한 컴퓨터에서 실행됩니다**. 프로그램에서 다른 서버에 원격으로 저장된 패키지를 로드하더라도 해당 패키지는 로컬 컴퓨터에서 실행됩니다.  
  
-   **Integration Services가 설치된 컴퓨터의 개발 환경 외부에서만 패키지를 실행할 수 있습니다**. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]가 설치되지 않은 클라이언트 컴퓨터의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 외부에서는 패키지를 실행할 수 없으며, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용권 계약에 따라 추가 컴퓨터에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]를 설치하는 것이 허용되지 않을 수도 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]는 서버 구성 요소이며 클라이언트 컴퓨터에 재배포할 수 없습니다. 클라이언트 컴퓨터에서 패키지를 실행하려면 패키지가 서버에서 실행되도록 하는 방식으로 실행해야 합니다.  
  
 저장된 패키지를 로드 및 실행하는 방법은 다음을 참조하십시오.  
  
-   [프로그래밍 방식으로 로컬 패키지 로드 및 실행](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
  
-   [프로그래밍 방식으로 원격 패키지 로드 및 실행](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
 패키지를 실행하고 해당 출력을 사용자 지정 프로그램으로 로드하는 방법은 다음을 참조하십시오.  
  
-   [로컬 패키지의 출력 로드](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
![Integration Services 아이콘 (작은)](../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [프로그래밍 방식으로 로컬 패키지 로드 및 실행](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [프로그래밍 방식으로 원격 패키지 로드 및 실행](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [로컬 패키지의 출력 로드](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
