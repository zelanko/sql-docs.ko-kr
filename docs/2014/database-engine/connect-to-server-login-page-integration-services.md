---
title: 서버에 연결(로그인 페이지) Integration Services | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttodtsserver.login.f1
- sql12.swb.connecttodts.login.f1
ms.assetid: 402c2de4-f4ea-40b0-909f-3ddf3bd59950
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 53a9793fc2a8770c8d926c945ba31a335bdfed3f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143146"
---
# <a name="connect-to-server-login-page-integration-services"></a>서버에 연결(로그인 페이지) Integration Services
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에 연결할 때 이 탭을 사용하여 다음 옵션을 확인하거나 지정할 수 있습니다.  
  
## <a name="options"></a>변수  
 **서버 유형**  
 개체 탐색기에서 서버를 등록할 때 연결할 서버 유형을 [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services 또는 Integration Services 중에서 선택합니다. 대화 상자의 나머지 부분에는 선택한 서버 유형에 적용되는 옵션만 표시됩니다. 등록된 서버에서 서버를 등록하는 경우 **서버 유형** 상자는 읽기 전용이며 등록된 서버 구성 요소에 표시된 서버 유형과 일치합니다. 다른 유형의 서버를 등록하려면 새 서버를 등록하기 전에 등록된 서버 도구 모음에서 [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services 또는 Integration Services를 선택합니다.  
  
 **서버 이름**  
 연결할 서버를 선택합니다. 마지막으로 연결한 서버 인스턴스가 기본적으로 표시됩니다.  
  
> [!NOTE]  
>  사용 하지 마세요  *\<서버 이름 >*\\*\<n a m e >* 이므로 [!INCLUDE[ssIS](../includes/ssis-md.md)] 컴퓨터에서 여러 인스턴스를 지원 하지 않습니다.  
  
 **인증**  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 에는 [!INCLUDE[ssIS](../includes/ssis-md.md)]Windows 인증만 사용할 수 있습니다. Windows 인증 모드에서는 사용자가 Windows 사용자 계정을 통해 연결할 수 있습니다.  
  
 **사용자 이름**  
 [!INCLUDE[ssIS](../includes/ssis-md.md)]에는 Windows 인증만 사용 가능하므로 이 옵션은 사용할 수 없습니다.  
  
 **암호**  
 [!INCLUDE[ssIS](../includes/ssis-md.md)]에는 Windows 인증만 사용 가능하므로 이 옵션은 사용할 수 없습니다.  
  
 **암호 저장**  
 [!INCLUDE[ssIS](../includes/ssis-md.md)]에는 Windows 인증만 사용 가능하므로 이 옵션은 사용할 수 없습니다.  
  
 **연결**  
 위에서 선택한 서버에 연결합니다.  
  
 **옵션**  
 대화 상자를 변경하고 암호 저장과 같은 추가 서버 연결 옵션을 숨기려면 클릭합니다.  
  
  
