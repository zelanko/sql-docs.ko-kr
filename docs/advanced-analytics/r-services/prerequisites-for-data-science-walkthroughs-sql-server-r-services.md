---
title: "데이터 과학 연습을 위한 필수 조건(SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# 데이터 과학 연습을 위한 필수 조건(SQL Server R Services)
동일한 네트워크의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 연결할 수 있는 R 워크스테이션에서 연습을 수행하는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 R 개발 환경이 둘 다 포함된 컴퓨터에서 이 연습을 실행할 수도 있습니다. 
  
  
## <a name="install-sql-server-2016-r-services-in-database"></a>SQL Server 2016 R Services(In-Database) 설치  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  이 설치되어 있는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 인스턴스에 액세스할 수 있어야 합니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 설정하는 방법에 대한 자세한 내용은 [SQL Server R Services 설정(In-Database)](https://msdn.microsoft.com/library/mt696069.aspx)을 참조하세요.  
  
  
> [!IMPORTANT]  
> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이상을 사용해야 합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 이전 SQL Database를 ODBC 데이터 원본으로 사용할 수는 있지만 R과의 통합을 지원하지 않습니다.  
  
## <a name="install-an-r-development-environment"></a>R 개발 환경 설치  
컴퓨터에서 이 연습을 완료하려면 R 개발 환경 또는 R 명령을 실행할 수 있는 다른 명령줄 도구가 필요합니다.    
  
- **R Tools for Visual Studio** 는 Intellisense, 디버깅, Microsoft R Server 및 SQL Server R Services 지원을 제공하는 무료 플러그 인입니다. 다운로드하려면 [R Tools for Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx)를 참조하세요.  
    
- **Microsoft R Client**는 R에서 ScaleR 패키지를 사용한 개발을 지원하는 간단한 개발 도구입니다. 가져오려면 [Microsoft R Client 시작](https://msdn.microsoft.com/microsoft-r/r-client-get-started)을 참조하세요.
  
- **RStudio** 는 R 개발에 많이 사용되는 환경 중 하나입니다. 자세한 내용은 [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)를 참조하세요.  
  
    그러나 RStudio의 일반 설치 또는 다른 환경에서는 이 자습서를 완료할 수 없습니다. Microsoft R Open용 연결 라이브러리 및 R 패키지도 설치해야 합니다. 자세한 내용은 [데이터 과학 클라이언트 설정](https://msdn.microsoft.com/library/mt696067.aspx)을 참조하세요.  

- [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]을 설치할 때 R 도구(R.exe, RTerm.exe, RScripts.exe)가 기본적으로 설치됩니다. IDE를 설치하지 않으려면 이러한 도구를 사용할 수 있습니다.  
  
  
## <a name="get-permissions-to-connect-to-sql-server"></a>SQL Server에 연결할 수 있는 권한 얻기  
이 연습에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하여 스크립트를 실행하고 데이터를 업로드합니다. 이렇게 하려면 데이터베이스 서버에 유효한 로그인이 있어야 합니다.  SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. R을 사용할 데이터베이스에서 다음 권한이 있는 계정을 서버에 만들도록 데이터베이스 관리자에게 요청하세요.  
  
-   데이터베이스, 테이블, 함수 및 저장 프로시저 만들기    
-   테이블에 데이터 삽입  
  
  
## <a name="start-the-walkthrough"></a>연습 시작  
[1단원: 데이터 준비&#40;데이터 과학 종단 간 연습&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
  
  
