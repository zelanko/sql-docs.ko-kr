---
title: Visual Studio .NET에서 Visual C# SMO 프로젝트 만들기
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual C# [SMO]
ms.assetid: 1e7abb16-23a0-4a18-91ad-253261e6bf84
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 60d0f5b55664312be1bdf6501cf54e78a826434b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900631"
---
# <a name="how-to-create-a-visual-c-smo-project-in-visual-studio-net"></a>방법: Visual Studio .NET에서 Visual C# SMO 프로젝트 만들기
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw.md)]

  이 섹션에서는 간단한 SMO 콘솔 애플리케이션을 빌드하는 방법을 설명합니다.  
  
 이 예에서는 프로그램이 SMO 형식을 참조할 수 있도록 네임스페이스를 가져옵니다. **에이전트** 네임 스페이스 가져오기는 선택 사항입니다. 이 네임스페이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하는 프로그램을 작성하는 경우에 필요합니다. **공용** 네임 스페이스는 인스턴스에 대 한 보안 연결을 설정 하는 데 필요 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. **SqlClient** 네임 스페이스는 SQL 예외 오류를 처리 하는 데 사용 됩니다.  
  
### <a name="creating-a-visual-c-smo-project-in-visual-studionet"></a>Visual Studio .NET에서 Visual C# SMO 프로젝트 만들기  
  
1. Visual Studio를 시작합니다.
  
2. **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 클릭 합니다.  **새 프로젝트** 대화 상자가 나타납니다.   
  
3. [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **설치 됨** 창에서 **템플릿** \\ **Visual c #** \\ **Windows** 로 이동 하 고 **콘솔 응용 프로그램**을 선택 합니다.  
  
4. 필드 **이름** 텍스트 상자에 새 응용 프로그램의 이름을 입력 합니다.  

5. **확인** 을 클릭 하 여 콘솔 응용 프로그램 템플릿을 로드 합니다.  

6. [SMO 설치](installing-smo.md) 의 지침에 따라 참조할 프로젝트에 대 한 패키지를 설치 합니다.
  
7. **보기** 메뉴에서 **코드**를 클릭합니다.
    
8. 코드에서 네임 스페이스 문 앞에 다음 **using** 문을 입력 하 여 SMO 네임 스페이스의 형식을 한정 합니다.
  
    ```  
    using Microsoft.SqlServer.Management.Smo;  
    using Microsoft.SqlServer.Management.Common;  
    ```  
  
15. SMO의 Microsoft.SqlServer.Management.Smo 아래에는 Microsoft.SqlServer.Management.Smo.Agent와 같은 다양한 네임스페이스가 있습니다. 이러한 네임스페이스를 필요에 따라 추가합니다.  
  
16. 이제 SMO 코드를 추가할 수 있습니다.  

