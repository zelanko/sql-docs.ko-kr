---
title: SQL Server의 로컬 언어 버전 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 20b99363-0490-4aa3-9a3d-262f827d81e8
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2bfa451cd670ffd126a1b658c7c96aafe12f1cb5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159914"
---
# <a name="local-language-versions-in-sql-server"></a>SQL Server의 로컬 언어 버전
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 Windows 운영 체제에서 지원하는 모든 언어를 지원합니다.  
  
## <a name="cross-language-support"></a>언어 간 호환성 지원  
  
-   영어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 지역화된 모든 운영 체제에서 지원됩니다.  
  
-   지역화된 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 해당 언어를 사용하는 지역화된 운영 체제에서는 물론 Windows MUI(Multilingual User Interface) Pack 설정을 사용하여 영어 버전의 운영 체제에서도 지원됩니다. 자세한 내용은 [Configure Operating System to Support Localized Versions](../../../2014/sql-server/install/local-language-versions-in-sql-server.md#BK_ConfigureOS)을 참조하세요.  
  
-   지역화된 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 같은 언어로 지역화된 버전으로만 업그레이드할 수 있으며 영어 버전으로는 업그레이드할 수 없습니다.  
  
-   지역화된 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 영어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스와 함께 설치할 수도 있습니다.  
  
##  <a name="BK_ConfigureOS"></a> Configure Operating System to Support Localized Versions  
 Windows MUI(Multilingual User Interface Pack) 설정을 사용하면 지원되는 운영 체제의 영어 버전에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 해당 언어 버전을 사용할 수 있습니다.  
  
 그러나 영어 이외의 MUI 설정을 포함하는 영어 운영 체제가 실행되는 서버에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 해당 언어 버전을 설치하기 전에 특정 운영 체제 설정을 확인해야 합니다. 다음 운영 체제 설정이 설치할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 언어와 일치하는지 확인해야 합니다.  
  
-   운영 체제 사용자 인터페이스 설정  
  
-   운영 체제 사용자 로캘 설정  
  
-   시스템 로캘 설정  
  
 설정이 설치할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 언어와 일치하지 않으면 다음 절차에 따라 이러한 운영 체제 설정을 올바르게 설정하십시오.  
  
> [!CAUTION]  
>  동일한 컴퓨터에서 서로 다른 언어 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 설치는 지원되지 않습니다.  
  
#### <a name="to-change-the-operating-system-user-interface-setting"></a>운영 체제 사용자 인터페이스 설정을 변경하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 해당 언어 버전과 일치하는 운영 체제 MUI를 아직 설치하지 않았으면 설치합니다.  
  
2.  제어판에서 **국가 및 언어 옵션**을 엽니다.  
  
3.  **언어** 탭의 **메뉴 및 대화 상자에 사용된 언어**에서 목록의 값을 선택합니다.  
  
     이 설정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 사용자 인터페이스 언어에 영향을 주므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 해당 언어 버전과 일치해야 합니다.  
  
4.  **적용** 을 클릭하여 변경 내용을 확인하거나 **확인** 을 클릭하여 창을 닫습니다.  
  
#### <a name="to-change-the-operating-system-user-locale-setting"></a>운영 체제 사용자 로캘 설정을 변경하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 해당 언어 버전과 일치하는 운영 체제 MUI를 아직 설치하지 않았으면 설치합니다.  
  
2.  제어판에서 **국가 및 언어 옵션**을 엽니다.  
  
3.  **국가별 옵션** 탭의 **아래에서 원하는 항목을 선택하거나 [사용자 지정]을 클릭하여 필요한 형식을 만드십시오**에서 목록의 값을 선택합니다.  
  
     이 설정은 culture별 데이터 서식에 영향을 줍니다.  
  
4.  **적용** 을 클릭하여 변경 내용을 확인하거나 **확인** 을 클릭하여 창을 닫습니다.  
  
#### <a name="to-change-the-system-locale-setting"></a>시스템 로캘 설정을 변경하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 해당 언어 버전과 일치하는 운영 체제 MUI를 아직 설치하지 않았으면 설치합니다.  
  
2.  제어판에서 **국가 및 언어 옵션**을 엽니다.  
  
3.  **고급** 탭의 **유니코드를 지원하지 않는 프로그램의 언어 버전과 일치하는 언어를 선택하십시오**에서 목록의 값을 선택합니다.  
  
     이 설정을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치에 대한 최상의 기본 데이터 정렬을 선택할 수 있습니다.  
  
4.  **적용** 을 클릭하여 변경 내용을 확인하거나 **확인** 을 클릭하여 창을 닫습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)   
 [SQL Server 2014 설치](../../database-engine/install-windows/install-sql-server.md)  
  
  
