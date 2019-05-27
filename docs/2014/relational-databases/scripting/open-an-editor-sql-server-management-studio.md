---
title: 편집기 열기(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5d654a60-d205-49d2-a831-b3d986d60024
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6ba0d74b07c21234d7e0f20cb7d9664ee7157f2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090297"
---
# <a name="open-an-editor-sql-server-management-studio"></a>편집기 열기(SQL Server Management Studio)
  이 항목에서는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]쿼리, MDX, DMX 또는 XML/A 편집기를 여는 방법에 대해 설명합니다. 편집기를 열면 각 편집기 창이 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]가운데 창에 탭으로 표시됩니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기( [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 편집용), DMX 및 MDX 편집기(해당 언어를 통한 스크립트 편집용) 및 XML/A 편집기(XML/A 스크립트 또는 XML 파일 편집용)의 네 가지 편집기를 지원합니다. 텍스트 파일은 어떠한 편집기로도 편집할 수 있습니다.  
  
### <a name="limitations-and-restrictions"></a>제한 사항  
 고유한 코드 페이지를 사용하는 다른 사이트의 사용자와 파일을 공유하는 경우에는 파일을 읽을 때 오류가 발생하지 않도록 적절한 유니코드 코드 페이지로 파일을 저장해야 합니다. 또한 UNIX나 Macintosh용으로 파일을 저장할 경우에는 적절한 문서 형식으로 파일을 저장해야 합니다. **파일** 메뉴의 **저장**단추 옆에 있는 아래쪽 화살표에서 **다른 이름으로 저장** , **인코딩하여 저장** 을 클릭한 다음 **줄 끝** 에서 **Unix** 또는 **Macintosh**를 선택합니다.  
  
### <a name="permissions"></a>사용 권한  
 코드 편집기에서 수행하는 작업에는 로그인하는 데 사용된 인증 계정에 부여된 사용 권한이 적용됩니다. 예를 들어 Windows 인증을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창을 열 경우 Windows 로그인 계정에 액세스 권한이 없는 개체를 참조하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 없습니다.  
  
## <a name="how-to-open-editors"></a>방법: 편집기 열기  
 이 섹션에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 다양한 편집기를 여는 방법에 대해 설명합니다.  
  
### <a name="using-the-filenew-menu"></a>파일/새로 만들기 메뉴 사용  
 **파일** 메뉴에서 **새로 만들기**를 클릭한 다음 쿼리 편집기 옵션 중 하나를 선택합니다.  
  
-   **현재 연결에서의 쿼리** - [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 현재 연결에 연결된 유형의 새 편집기 창을 엽니다. 편집기 창에서는 현재 연결과 동일한 인증 정보를 사용합니다. 예를 들어 개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 선택한 다음 **현재 연결에서의 쿼리**를 사용할 경우 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서는 동일한 인증 정보를 사용하여 동일한 인스턴스에 연결된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기를 엽니다.  
  
-   **데이터베이스 엔진 쿼리** - [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기와 대화 상자를 열어서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 인스턴스에 연결하는 데 필요한 정보를 가져옵니다.  
  
-   **Analysis Services MDX 쿼리** - 새 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] MDX 쿼리 편집기와 대화 상자를 열어서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하는 데 필요한 정보를 가져옵니다.  
  
-   **Analysis Services DMX 쿼리** - [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DMX 쿼리 편집기와 대화 상자를 열어서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하는 데 필요한 정보를 가져옵니다.  
  
-   **Analysis Services XML/A 쿼리** - 새 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XML/A 쿼리 편집기와 대화 상자를 열어서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하는 데 필요한 정보를 가져옵니다.  
  
### <a name="using-the-fileopen-menu"></a>파일/열기 메뉴 사용  
 **파일** 메뉴에서 **열기**를 클릭한 다음 파일을 찾아서 엽니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서는 파일 확장명에 적절한 유형의 편집기를 열고, 파일 내용을 편집기 창에 복사하며, 필요한 경우 연결 대화 상자를 엽니다. 예를 들어 확장명이 .sql인 파일을 열 경우 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창을 열고 .sql 파일의 내용을 복사한 다음 연결 대화 상자를 엽니다. 특정 편집기에 연결되지 않은 확장명을 가진 파일을 열 경우 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서는 텍스트 편집기 창을 열고 파일 내용을 복사합니다.  
  
 자세한 내용은 [파일 확장명을 코드 편집기에 연결](associate-file-extensions-to-a-code-editor.md)을 참조하세요.  
  
### <a name="using-the-toolbar"></a>도구 모음 사용  
 **표준** 도구 모음에서 다음 단추 중 하나를 클릭합니다.  
  
-   **새 쿼리** - [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 현재 연결에 연결된 유형의 새 편집기 창을 엽니다. 편집기 창에서는 현재 연결과 동일한 인증 정보를 사용합니다. 예를 들어 개체 탐색기에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 선택한 다음 **새 쿼리** 단추를 클릭하면 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서는 동일한 인증 정보를 사용하여 동일한 인스턴스에 연결된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기를 엽니다.  
  
-   **데이터베이스 엔진 쿼리** - [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기와 대화 상자를 열어서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 인스턴스에 연결하는 데 필요한 정보를 가져옵니다.  
  
-   **Analysis Services MDX 쿼리** - 새 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] MDX 쿼리 편집기와 대화 상자를 열어서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하는 데 필요한 정보를 가져옵니다.  
  
-   **Analysis Services DMX 쿼리** - [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DMX 쿼리 편집기와 대화 상자를 열어서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하는 데 필요한 정보를 가져옵니다.  
  
-   **Analysis Services XML/A 쿼리** - 새 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XML/A 쿼리 편집기와 대화 상자를 열어서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하는 데 필요한 정보를 가져옵니다.  
  
### <a name="using-object-explorer"></a>개체 탐색기 사용  
 **개체 탐색기**에서  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결된 서버 노드를 마우스 오른쪽 단추로 클릭한 다음 **새 쿼리**를 선택합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 동일한 인스턴스에 연결된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창이 열리면 창의 데이터베이스 컨텍스트를 로그인에 대한 기본 데이터베이스로 설정합니다.  
  
-   데이터베이스 노드를 마우스 오른쪽 단추로 클릭하고 **새 쿼리**를 선택합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 동일한 인스턴스에 연결된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창이 열리면 창의 데이터베이스 컨텍스트를 동일한 데이터베이스로 설정합니다.  
  
### <a name="using-solution-explorer"></a>솔루션 탐색기 사용  
 **솔루션 탐색기**에서 폴더를 확장하고 폴더 내의 항목을 마우스 오른쪽 단추로 클릭한 다음 **열기** 를 클릭하고 항목이나 파일을 두 번 클릭합니다.  
  
### <a name="using-template-browser-to-open-the-database-engine-query-editor"></a>템플릿 브라우저를 사용하여 데이터베이스 엔진 쿼리 편집기 열기  
  
-   **보기** 메뉴에서 **템플릿 탐색기**를 클릭합니다.  
  
-   오른쪽 창에 **템플릿 브라우저** 창이 표시됩니다.  
  
-   템플릿을 두 번 클릭하여 데이터베이스 엔진 쿼리 창을 템플릿 텍스트와 함께 엽니다. 예를 들어 CREATE DATABASE 템플릿을 열려면 **SQL Server 템플릿** 폴더, **데이터베이스** 폴더를 차례로 열고 **데이터베이스 만들기**를 두 번 클릭합니다.  
  
  
