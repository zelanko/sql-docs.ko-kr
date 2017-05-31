---
title: "SQL Server Management Studio의 창 관리 이해 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- autohide [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], tool windows
- push pin [SQL Server Management Studio]
- tool windows [SQL Server Management Studio]
ms.assetid: bebf8383-dcaf-466e-84f5-63b81c9cfe52
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 010413d849d1d3bdab0c1d72c6bd6375c340a753
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="understand-sql-server-management-studio-windows-management"></a>SQL Server Management Studio의 창 관리 이해
[!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]의 도구 창은 많은 기능을 가진 유연하고 효율적인 시스템입니다. 이 시스템을 사용하여 다음을 수행할 수 있습니다.  
  
-   개발 및 관리를 위한 사용자 작업 영역을 최대화합니다.  
  
-   한 번에 표시되는 사용되지 않는 창 수를 줄입니다.  
  
-   사용자 환경을 쉽게 사용자 지정합니다.  
  
창 조작은 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 환경의 핵심입니다. 사용자는 자주 사용하는 도구와 창에 쉽게 액세스할 수 있습니다. 사용자는 여러 다른 정보에 할당할 공간의 크기를 제어할 수 있으며 환경은 이에 따라서 쿼리를 편집하는 데 사용할 수 있는 공간을 최대화해야 합니다. 화면의 여러 다른 위치로 창을 이동할 수 있습니다. 대부분의 창을 도킹 해제하고 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 프레임의 밖으로 끌 수 있습니다. 이 기능은 여러 모니터를 사용할 경우에 특히 유용합니다.  
  
기능을 유지 관리하면서 편집 공간을 늘리기 위해 모든 창은 자동 숨기기 기능을 제공합니다. 이 기능은 주 [!INCLUDE[ssManStudio](../includes/ssmanstudio_md.md)] 환경의 테두리를 따라 있는 표시줄에 창을 탭으로 표시합니다. 이러한 탭 중 하나에 포인터를 올려 놓으면 해당 창이 표시됩니다. 창의 오른쪽 상단 모서리에 압정으로 표시되는 **자동 숨기기** 단추를 클릭하여 창의 자동 숨기기 기능을 설정/해제할 수 있습니다. 또한 **창** 메뉴에는 **모두 자동 숨기기** 옵션이 있습니다.  
  
동일한 도킹 위치에 구성 요소가 탭으로 표시되는 탭 모드나 각 문서가 고유한 창을 가지는 MDI(다중 문서 인터페이스) 모드로 일부 구성 요소를 구성할 수 있습니다. 이 기능을 구성하려면 **도구** 메뉴에서 **옵션**을 클릭하고 **환경**을 클릭한 다음 **일반**을 클릭합니다.  
  
> [!IMPORTANT]  
> 로그인이나 포함된 데이터베이스 사용자가 연결되고 인증되면 로그인에 대한 ID 정보가 저장됩니다. Windows 인증 로그인을 위해 Windows 그룹의 멤버 자격에 대한 정보가 포함됩니다. 연결이 유지되는 한 로그인의 ID가 인증된 상태로 유지됩니다. 암호 재설정이나 Windows 그룹 멤버 자격 변경 등의 ID 변경 사항을 적용하려면 인증 기관(Windows 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)])에서 로그오프한 후 다시 로그인해야 합니다. **sysadmin** 고정 서버 역할의 멤버나 **ALTER ANY CONNECTION** 권한이 있는 로그인은 **KILL** 명령을 사용하여 연결을 종료하고 다시 연결하도록 할 수 있습니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 개체 탐색기 또는 쿼리 편집기 창에 다중 연결할 때 연결 정보를 다시 사용합니다. 다시 연결하도록 모든 연결을 닫습니다.  
  
> [!IMPORTANT]  
> 로그인 계정(또는 포함된 데이터베이스 사용자)이 연결되고 인증되면 해당 연결에 해당 로그인에 대한 ID 정보가 캐시됩니다. Windows 인증 로그인을 위해 Windows 그룹의 멤버 자격에 대한 정보가 포함됩니다. 연결이 유지되는 한 로그인의 ID가 인증된 상태로 유지됩니다. 암호 재설정이나 Windows 그룹 멤버 자격 변경 등의 ID 변경 사항을 적용하려면 인증 기관(Windows 또는 [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)])에서 로그오프한 후 다시 로그인해야 합니다. **sysadmin** 고정 서버 역할의 멤버나 **ALTER ANY CONNECTION** 권한이 있는 로그인은 **KILL** 명령을 사용하여 연결을 종료하고 다시 연결하도록 할 수 있습니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)] 개체 탐색기 또는 쿼리 편집기 창에 다중 연결할 때 연결 정보를 다시 사용합니다. 다시 연결하도록 모든 연결을 닫습니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server Management Studio 사용](../ssms/use-sql-server-management-studio.md)  
[SQL Server Management Studio 환경](../ssms/the-sql-server-management-studio-environment.md)  
  

