---
title: Visual Studio.NET에서에서 Visual C# SMO 프로젝트 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 371da8231138fb43e9b001808b9fb88ad09543b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63131649"
---
# <a name="create-a-visual-c-smo-project-in-visual-studio-net"></a>Visual Studio .NET에서 Visual C# SMO 프로젝트 만들기
  이 섹션에서는 간단한 SMO 콘솔 응용 프로그램을 빌드하는 방법을 설명합니다.  
  
 이 예에서는 프로그램이 SMO 형식을 참조할 수 있도록 네임스페이스를 가져옵니다. `Agent` 네임스페이스 가져오기는 선택 사항입니다. 이 네임스페이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하는 프로그램을 작성하는 경우에 필요합니다. `Common` 네임스페이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 보안 연결을 설정하는 데 필요합니다. `SqlClient` 네임스페이스는 SQL 예외 오류를 처리하는 데 사용됩니다.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Visual Studio .NET에서 Visual C# SMO 프로젝트 만들기  
  
1.  [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] (또는 [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)])을 시작합니다.  
  
2.  **파일** 메뉴에서 **새 프로젝트**를 클릭합니다. **새 프로젝트** 대화 상자가 나타납니다.  
  
3.  **프로젝트 형식** 대화 상자에서 **Visual C#** 를 선택한 후 **Windows**합니다. 에 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 설치 된 템플릿 창 **Windows 응용 프로그램**합니다.  
  
4.  (선택 사항) 에 **이름을** 필드에 새 응용 프로그램의 이름을 입력 합니다.  
  
5.  Visual C# 응용 프로그램 형식을 선택합니다. 에 따라 선택 하는 예제 **콘솔 응용 프로그램**합니다.  
  
6.  **프로젝트** 메뉴에서 **참조 추가**를 선택합니다. **참조 추가** 대화 상자가 나타납니다.  
  
7.  클릭 **찾아보기**에서 SMO 어셈블리를 찾아서는 [!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)] 폴더를 선택한 후 다음 파일입니다. SMO 응용 프로그램을 빌드하려면 최소한 다음 파일이 있어야 합니다.  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
    > [!NOTE]  
    >  두 개 이상의 파일을 선택하려면 `Ctrl` 키를 사용합니다.  
  
8.  그 밖에 필요한 SMO 어셈블리를 모두 추가합니다. 예를 들어 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 대상으로 프로그래밍하는 경우 다음 어셈블리를 추가합니다.  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. **열기**를 클릭합니다.  
  
10. 에 **뷰** 메뉴에서 클릭 **코드**. 또는 Program1.cs [Design] Windows를 선택 하 고 코드 창을 표시 하려면 windows form을 두 번 클릭 합니다.  
  
11. 이 코드에서 네임스페이스 문 앞에 다음 `using` 문을 입력하여 SMO 네임스페이스의 형식을 한정합니다.  
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
12. SMO의 Microsoft.SqlServer.Management.Smo 아래에는 Microsoft.SqlServer.Management.Smo.Agent와 같은 다양한 네임스페이스가 있습니다. 이러한 네임스페이스를 필요에 따라 추가합니다.  
  
13. 이제 SMO 코드를 추가할 수 있습니다.  
  
  
