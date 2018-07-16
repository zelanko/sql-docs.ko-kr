---
title: Visual Studio.NET에서에서 Visual Basic SMO 프로젝트 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic [SMO]
ms.assetid: d7a3892c-0f1c-4c4d-8480-b58dce3720bc
caps.latest.revision: 43
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0a3cacc04d8ce4afd863c7ef3cc8d21e1446c319
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213793"
---
# <a name="create-a-visual-basic-smo-project-in-visual-studio-net"></a>Visual Studio .NET에서 Visual Basic SMO 프로젝트 만들기
  이 섹션에서는 간단한 SMO 콘솔 응용 프로그램을 빌드하는 방법을 설명합니다.  
  
 이 예에서는 프로그램이 SMO 형식을 참조할 수 있도록 네임스페이스를 가져옵니다. `Agent` 네임스페이스 가져오기는 선택 사항입니다. 이 네임스페이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하는 프로그램을 작성하는 경우에 필요합니다. `Common` 네임스페이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 보안 연결을 설정하는 데 필요합니다. `SqlClient` 네임스페이스는 SQL 예외 오류를 처리하는 데 사용됩니다.  
  
### <a name="creating-a-visual-basic-smo-project-in-visual-studionet"></a>Visual Studio.NET에서 Visual Basic SMO 프로젝트 만들기  
  
1.  [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] (또는 [!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)])을 시작합니다.  
  
2.  **파일** 메뉴에서 **새 프로젝트**를 클릭합니다. **새 프로젝트** 대화 상자가 나타납니다.  
  
3.  **프로젝트 형식** 대화 상자에서 **Visual Basic**를 선택한 후 **Windows**합니다. 에 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 설치 된 템플릿 창 **콘솔 응용 프로그램입니다.**  
  
4.  (선택 사항) 에 **이름을** 필드에 새 응용 프로그램의 이름을 입력 합니다.  
  
5.  클릭 **확인** 로드 하는 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 콘솔 응용 프로그램 템플릿.  
  
6.  **프로젝트** 메뉴에서 **참조 추가**를 선택합니다. **참조 추가** 대화 상자가 나타납니다.  
  
7.  클릭 **찾아보기**고 C:\Program Files\Microsoft SQL Server\120\SDK\Assemblies 폴더에서 SMO 어셈블리를 찾아서 다음 파일을 선택 합니다. SMO 응용 프로그램을 빌드하려면 최소한 다음 파일이 있어야 합니다.  
  
     Microsoft.SqlServer.ConnectionInfo.dll  
  
     Microsoft.SqlServer.SqlEnum.dll  
  
     Microsoft.SqlServer.Smo.dll  
  
     Microsoft.SqlServer.Management.Sdk.Sfc  
  
    > [!NOTE]  
    >  두 개 이상의 파일을 선택하려면 `Ctrl` 키를 사용합니다.  
  
8.  그 밖에 필요한 SMO 어셈블리를 모두 추가합니다. 예를 들어 [!INCLUDE[ssSB](../../includes/sssb-md.md)]를 대상으로 프로그래밍하는 경우 다음 어셈블리를 추가합니다.  
  
     Microsoft.SqlServer.ServiceBrokerEmum.dll  
  
9. **열기**를 클릭합니다.  
  
10. 에 **뷰** 메뉴에서 클릭 **코드**. 또는 Module1.vb 창을 선택 하 여 코드 창을 표시 합니다.  
  
11. 다른 모든 선언 앞의 코드를 다음 입력 **가져오기** 문을 SMO 네임 스페이스의 형식을 한정 합니다.  
  
    ```  
    Imports Microsoft.SqlServer.Management.Smo  
    Imports Microsoft.SqlServer.Management.Common  
    ```  
  
12. SMO의 Microsoft.SqlServer.Management.Smo 아래에는 Microsoft.SqlServer.Management.Smo.Agent와 같은 다양한 네임스페이스가 있습니다. 이러한 네임스페이스를 필요에 따라 추가합니다.  
  
13. 이제 SMO 코드를 추가할 수 있습니다.  
  
  
