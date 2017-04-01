---
title: "설치 또는 R 도구 구성 | Microsoft Docs"
ms.custom: ""
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# 설치 또는 R 도구 구성
  Microsoft R 서버는 모든 기본 R 라이브러리, 배율 R 패키지 및 개발 하 고 R 코드를 테스트 해야 하는 표준 R 도구를 제공 합니다. 그러나 전용된 R 개발 환경을 사용 하려는 경우 몇 가지 사용 가능한를 포함 하 여 많은 무료 도구가 있습니다.  
  
## <a name="basic-r-tools"></a>기본 R 도구  
 모든 표준 R 도구를 때문에 Microsoft R 서버 설치의 추가 도구가 필요 하지 않습니다에 포함 된 한 *설치 기본* R의 기본적으로 설치 됩니다.

-   **RTerm**: R 스크립트를 실행 하기 위한 명령줄 도구 
  
-   **RGui.exe**: R.에 대 한 간단한 대화식 편집기 명령줄 인수 RGui.exe 및 RTerm 동일합니다. 
  
-   **RScript**: 일괄 처리 모드에서 R을 실행 하기 위한 명령줄 도구를 스크립팅 합니다.  

기본적으로 이러한 도구는 다음 폴더에 설치 됩니다.
- SQL Server 2016: `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin\x64`  
- SQL Server vNext: `C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64`  

> [!TIP]  
>  도움이 더 필요하세요? R 도구에 대 한 설명서를 설치 폴더에 있습니다: `C:\Program Files\Microsoft SQL Server\R_SERVER\doc` 및 `C:\Program Files\Microsoft SQL Server\R_SERVER\doc\manual`합니다.  
>   
>  또는 열기만 **RGui**, 클릭 **도움말**, 옵션 중 하나를 선택 합니다.  

## <a name="microsoft-r-client"></a>Microsoft R Client

Microsoft R 클라이언트는 SQL Server R 서비스 또는 Microsoft R 서버에서 쉽게 실행할 수 있는 R 솔루션을 개발할 수 있도록 하는 무료 다운로드 합니다.

일반적으로 Visual Studio 또는 RStudio를 위한 R 도구와 같은 다른 R 개발 환경을 설치 하 고 Microsoft R 클라이언트 R 실행으로 사용할 수 있는지를 지정 합니다. 이렇게 하면 전체 액세스 RevoScaleR 패키지 및 Microsoft R Server의 다른 기능을 합니다.

또한 스크립트를 실행 하거나 작성 하 고 실행할 R 코드를 임시 RGui 및 RTerm와 같은 친숙 한 도구를 사용할 수 있습니다.

[Microsoft R 클라이언트 설치](https://msdn.microsoft.com/microsoft-r/r-client-install)
  
##  <a name="a-namebkmkrtoolsa-r-tools-for-visual-studio"></a> R Tools for Visual Studio  

 작업할 때 편의 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 사용 하 여 고려 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 개발 환경으로 합니다. [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] Visual Studio의 모든 버전에서 작동 하는 Visual Studio 용 무료는 추가 기능에. Visual Studio는 Python 및 F # 통합에 대 한 지원도 제공 합니다.  

자세한 내용은 참조 [VisualStudio.com](https://www.visualstudio.com/vs/rtvs/)합니다.

 이 섹션에서는 설치 하는 방법을 설명 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 무료 커뮤니티 버전의 Visual Studio를 사용 합니다.  
  
#### <a name="install-visual-studio"></a>Visual Studio 설치  
  
1.  무료 커뮤니티 버전의 Visual Studio는이 페이지에서 다운로드할 수 있습니다: [Visual Studio 커뮤니티](http://visualstudio.com/products/visual-studio-community-vs.aspx)  
  
2.  다운로드가 완료 되 면 클릭 **실행** 하 고 설치할 구성 요소를 선택 합니다.  
  
     사용자 지정 설치를 수행 하는 경우 note Microsoft Web Developer 구성 요소는 필수 필드입니다.  
  
3.  선택 된 **일반** 되는 시간에 대 한 설정입니다. 설치 하는 경우 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], toption R 개발에 대해 사용자 지정 레이아웃을 변경할 수 있습니다.  

#### <a name="add-the-r-tools"></a>R 도구 추가

확장은 R, Python, 및를 통해 다른 여러 언어에 사용할 수 있는 Visual Studio를 설치한 후는 **옵션** 메뉴.

4. 메뉴 모음에서 도구를 클릭 한 다음 선택 **확장 및 업데이트**합니다.

5. 설치의 끝 R 도구는 컴퓨터에서 사용할 수 있고 Microsoft R 클라이언트에 대 한 Microsoft R 서버나 R 런타임 R 런타임을 사용 하 여 개발 환경을 변경 하려는 경우 요청 하는 R 런타임 버전을 검색 합니다.

설치 프로그램에서 사용 하려는 R 서버 런타임 검색 되지 않으면, 변경할 수 있습니다 것 수동으로 언제 든 지 사용 하 여는 **옵션** 메뉴. 자세한 내용은 참조 [Your IDE 구성](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide)합니다.

## <a name="rstudio"></a>RStudio

RStudio를 사용 하는 것을 선호 하는 경우 RevoScaleR 라이브러리를 사용 하 여 이러한 추가 단계를 수행 합니다.
- 필수 패키지 및 라이브러리를 가져오는 Microsoft R 서버 또는 Microsoft R 클라이언트를 설치 합니다.
- 적절 한 R 런타임을 사용 하 여 R 경로 업데이트 합니다.

자세한 내용은 참조 [Your IDE 구성](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide)합니다.


## <a name="see-also"></a>관련 항목:  
 [독립 실행형 R 서버 만들기](../../advanced-analytics/r-services/create-a-standalone-r-server.md)   
 [Microsoft R 서버 &#40; 시작 하기 독립 실행형 &#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  