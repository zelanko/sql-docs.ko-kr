---
title: 새 서버 등록 편집 (일반 탭) (Reporting Services) 또는 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerserver.general.reportserver.f1
ms.assetid: 5f899a8e-52ef-46b5-b7a9-f200ccd9f724
caps.latest.revision: 26
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d03ee36c46ba0fb4e4c026c61d94c1b4ee29befc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202043"
---
# <a name="new-or-edit-server-registration-general-tab-reporting-services"></a>새 서버 등록 또는 서버 등록 편집(일반 탭)(Reporting Services)
  이 탭을 사용하여 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]인스턴스의 등록 옵션을 지정할 수 있습니다.  
  
 이 페이지에 액세스하려면 등록된 서버에서 **등록된 서버** 도구 모음의 **Reporting Services** 를 클릭하고 **Reporting Services**와 같은 등록된 서버 그룹을 마우스 오른쪽 단추로 클릭한 다음 **새로 만들기**를 가리키고 **서버 등록**을 클릭합니다.  
  
## <a name="options"></a>변수  
 **서버 유형**  
 등록된 서버에서 서버를 등록하는 경우 **서버 유형** 상자는 읽기 전용이며 **등록된 서버** 창에 표시된 서버 유형과 일치합니다. 다른 유형의 서버를 등록하려면 새 서버를 등록하기 전에 **등록된 서버** 도구 모음에서 원하는 서버를 클릭합니다.  
  
 **서버 이름**  
 연결할 보고서 서버 인스턴스를 지정합니다. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에서는 해당 인스턴스 이름을 통해 보고서 서버에 액세스할 수 있습니다. 설치하는 각 SQL Server 인스턴스에 대해 하나의 보고서 서버 인스턴스를 만들 수 있습니다. 기본 인스턴스를 사용하는 경우에는 SQL Server 인스턴스의 이름을 입력합니다. 명명된 인스턴스를 사용하는 경우에는 MSSQL$InstanceName 형식으로 보고서 서버에 연결할 명명된 인스턴스를 지정합니다.  
  
 **인증**  
 보고서 서버에 대한 인증은 인터넷 정보 서비스(IIS)를 통해 수행됩니다. Reporting Services에 연결할 때는 다음 인증 모드 중 하나를 선택합니다.  
  
 **Windows 인증 모드(Windows 인증)**  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 자격 증명을 사용하여 보고서 서버 인스턴스에 연결합니다.  
  
 **기본 인증**  
 Reporting Services 설치에서 기본 인증을 사용하도록 구성되어 있는 경우 **기본 인증** 을 사용하여 연결합니다.  
  
 **폼 인증**  
 Reporting Services 설치에서 사용자 지정 인증 확장 프로그램을 사용하도록 구성되어 있는 경우 **폼 인증** 을 사용하여 연결합니다.  
  
 **사용자 이름**  
 연결에 사용할 로그인 이름을 입력합니다. 이 옵션은 **기본 인증** 또는 **폼 인증**을 선택한 경우에만 사용할 수 있습니다.  
  
 **암호**  
 사용자 이름에 대한 암호를 입력합니다. 이 옵션은 **기본 인증** 또는 **폼 인증**을 선택한 경우에만 편집할 수 있습니다.  
  
 **암호 저장**  
 입력한 암호를 저장합니다. 이 옵션은 **기본 인증** 또는 **폼 인증**을 클릭한 경우에만 사용할 수 있습니다.  
  
> [!NOTE]  
>  저장한 암호를 더 이상 저장하지 않으려면 이 확인란의 선택을 취소하고 **저장**을 클릭합니다.  
  
 **등록된 서버 이름**  
 등록된 서버에 표시할 이름입니다. 이 이름은 **서버 이름** 상자에 있는 이름과 일치할 필요가 없습니다.  
  
 **등록된 서버 설명**  
 서버에 대한 선택적 설명을 입력합니다.  
  
 **테스트**  
 **서버 이름**에서 선택한 서버 연결을 테스트하려면 클릭합니다.  
  
 **저장**  
 등록된 서버 설정을 저장하려면 클릭합니다.  
  
  
