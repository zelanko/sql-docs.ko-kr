---
title: "데이터베이스 엔진 스크립팅 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "스크립트 [SQL Server], PowerShell"
  - "스크립트 [SQL Server]"
  - "스크립팅 [SQL Server 데이터베이스 엔진]"
  - "스크립팅 [SQL Server 데이터베이스 엔진], PowerShell"
ms.assetid: 9978a884-59a2-4e7f-a82a-335149f3a261
caps.latest.revision: 23
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 23
---
# 데이터베이스 엔진 스크립팅
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인스턴스 및 이러한 인스턴스의 개체를 관리하기 위한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] PowerShell 스크립팅 환경을 지원합니다. 또한 스크립팅 환경과 매우 유사한 환경에서는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 XQuery를 포함하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리를 작성 및 실행할 수 있습니다.  
  
## SQL Server PowerShell  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 다음을 구현하는 두 개의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 스냅인이 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 개체 모델 계층을 파일 시스템 경로와 비슷한 PowerShell 경로로 노출하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 공급자. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리 개체 모델 클래스를 사용하여 경로의 각 노드에 표현되는 개체를 관리할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명령을 구현하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cmdlet 집합. **Invoke-Sqlcmd**는 이러한 cmdlet 중 하나로, [!INCLUDE[ssDE](../../includes/ssde-md.md)] sqlcmd **유틸리티와 함께 실행되도록** 쿼리 스크립트를 실행하는 데 사용됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 PowerShell을 실행하기 위한 다음과 같은 기능을 제공합니다.  
  
-   PowerShell 세션으로 가져올 수 있는 **sqlps** PowerShell 모듈. 이 모듈은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스냅인을 로드합니다. 임시 PowerShell 명령을 대화형으로 실행할 수 있습니다. .\MyFolder\MyScript.ps1과 같은 명령을 사용하여 스크립트 파일을 실행할 수 있습니다.  
  
-   PowerShell 스크립트 파일은 예약된 간격이나 시스템 이벤트에 대한 응답으로 스크립트를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 PowerShell 작업 단계에 대한 입력으로 사용할 수 있습니다.  
  
-   PowerShell을 시작하고 **모듈을 가져오는** sqlps [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티. 이를 통해 해당 모듈에서 지원하는 모든 동작을 수행할 수 있습니다. **sqlps** 유틸리티는 명령 프롬프트에서 시작하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio 개체 탐색기 트리의 노드를 마우스 오른쪽 단추로 클릭하고 **PowerShell 시작**을 선택하여 시작할 수 있습니다.  
  
## 데이터베이스 엔진 쿼리  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 스크립트에는 다음과 같은 세 가지 유형의 요소가 포함되어 있습니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 언어 문  
  
-   XQuery 언어 문  
  
-   **sqlcmd** 유틸리티의 명령 및 변수  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리를 작성하는 다음과 같은 세 가지 환경을 제공합니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]쿼리를 대화형으로 실행 및 디버깅할 수 있습니다. 하나의 세션에서 여러 문을 코딩 및 디버깅한 다음 모든 문을 하나의 스크립트 파일에 저장할 수 있습니다.  
  
-   **sqlcmd** 명령 프롬프트 유틸리티를 사용하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리를 대화형으로 실행하고 기존 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 스크립트 파일도 실행할 수 있습니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 스크립트 파일은 일반적으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 대화형으로 코딩됩니다. 이 파일은 나중에 다음 환경 중 하나에서 열 수 있습니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **파일**/**열기** 메뉴를 사용하여 새 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창에 파일을 열 수 있습니다.  
  
-   **-i***input_file* 매개 변수를 사용하여 **sqlcmd** 유틸리티로 파일을 실행할 수 있습니다.  
  
-   **-QueryFromFile** 매개 변수를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 스크립트에서 **Invoke-Sqlcmd** cmdlet으로 파일을 실행할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 [!INCLUDE[tsql](../../includes/tsql-md.md)] 작업 단계를 사용하여 예약된 간격이나 시스템 이벤트에 대한 응답으로 스크립트를 실행할 수 있습니다.  
  
 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트 생성 마법사를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 생성할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기에서 개체를 마우스 오른쪽 단추로 클릭한 후 **스크립트 생성** 메뉴 항목을 선택할 수 있습니다. **스크립트 생성** 은 스크립트를 만드는 과정을 안내하는 마법사를 시작합니다.  
  
## 데이터베이스 엔진 스크립팅 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 코드 및 텍스트 편집기를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 대화식으로 개발, 디버그 및 실행하는 방법에 대해 설명합니다.|[쿼리 및 텍스트 편집기&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)|  
|스크립트를 대화식으로 개발하는 기능을 포함하여 **유틸리티와 함께 실행되도록** 유틸리티를 사용하여 명령 프롬프트에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 실행하는 방법에 대해 설명합니다.|[sqlcmd 방법 도움말 항목](../Topic/sqlcmd%20How-to%20Topics.md)|  
|SQL Server 구성 요소를 Windows PowerShell 환경에 통합한 다음 SQL Server 인스턴스 및 개체를 관리하는 PowerShell 스크립트를 작성하는 방법에 대해 설명합니다.|[SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)|  
|**스크립트 생성 및 게시 마법사** 를 사용하여 데이터베이스에서 하나 이상의 개체를 다시 만드는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 작성하는 방법에 대해 설명합니다.|[스크립트 생성&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/generate-scripts-sql-server-management-studio.md)|  
  
## 참고 항목  
 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)   
 [자습서: Transact-SQL 문 작성](../../t-sql/tutorial-writing-transact-sql-statements.md)  
  
  