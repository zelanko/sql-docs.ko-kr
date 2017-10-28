---
title: "SQL Server Management Studio 시작 | Microsoft Docs"
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 25ffaea6-0eee-4169-8dd0-1da417c28fc6
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: dab569e1d758587233b6f6a0cd00e966e325fcd1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="lesson-1-1---start-sql-server-management-studio"></a>1-1단원 - SQL Server Management Studio 시작
이 자습서를 시작하기 전에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 간단히 살펴봅니다.  
  
## <a name="opening-sql-server-management-studio"></a>SQL Server Management Studio 열기  
  
#### <a name="to-open-sql-server-management-studio"></a>SQL Server Management Studio를 열려면  
  
1.  SSMS([!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)])를 시작하는 방법은 운영 체제에 따라 달라집니다.  
  * **시작 페이지**가 있는 최신 버전의 Windows에서는 **시작 페이지**에서 **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**를 입력하면 프로그램이 나타납니다. 프로그램을 클릭하여 SSMS를 엽니다. 프로그램을 마우스 오른쪽 단추로 클릭한 다음 **시작 페이지**에 고정하는 것이 좋습니다.   
  * 이전 버전의 Windows에서는 **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]을 차례로 가리킨 다음 **SQL Server Management Studio**를 클릭합니다. 또는 **실행** 대화 상자에서 **SSMS.exe** 를 입력한 다음 **확인**을 클릭합니다.  
  
    > [!NOTE]  
    >  SSMS가 나타나지 않을 경우 SSMS가 제대로 설치되지 않았을 수 있습니다. [다운로드 센터](../download-sql-server-management-studio-ssms.md)에서 SSMS를 설치합니다. SSMS는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016과 함께 자동으로 설치되지 않습니다. 모든 기능에 액세스하려면 최신 버전을 사용합니다.  
  
2.  다음 단계에서는 SSMS의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 탐색기 **구성 요소를 사용하여** 에 연결합니다. 개체 탐색기 창이 표시되지 않는 경우 **보기** 메뉴에서 **개체 탐색기**를 클릭합니다. 개체 탐색기 메뉴에서 **연결** 단추, **데이터베이스 엔진**을 차례로 클릭합니다. **서버에 연결** 대화 상자가 표시됩니다. 이전에 SSMS를 설치한 경우 사용자 설정 때문에 **서버에 연결** 대화 상자가 자동으로 표시될 수도 있습니다.  
  
3.  **서버에 연결** 대화 상자의 **서버 이름** 상자에 정보를 입력합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 세 가지 유형 중 하나에 연결할 수 있습니다. 각 유형마다 **서버 이름** 상자의 형식이 약간씩 다릅니다. 다음 형식 중 하나를 선택합니다.  
  -  **기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스:**  컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 기본값(명명되지 않은 인스턴스) 또는 명명된 인스턴스로 지정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 인스턴스에 연결하는 경우 컴퓨터 이름을 삽입합니다. 예를 들어 Accounting이라는 컴퓨터에서 SSMS를 실행 중이며 해당 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  의 기본 인스턴스에 연결하는 경우 **서버 이름** 상자에 **Accounting** 을 입력합니다.  
  -  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 명명된 인스턴스:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 도중에 인스턴스 이름을 지정할 수 있습니다. 예를 들어 Accounting이라는 컴퓨터에서는 **Receivables**라는 명명된 인스턴스를 지정할 수 있습니다. 명명된 인스턴스에 연결하려면 **서버 이름** 상자에 컴퓨터 이름 백슬래시 인스턴스 이름을 입력합니다(예: **Accounting\Receivables**).  
  -  **Azure SQL Database:** SQL Database에 대한 서버 이름의 형식은 SQL_Server_name.database.windows.net입니다(예: **mydb2.database.windows.net**). 서버 이름을 확인하는 데 문제가 있는 경우 Azure Portal에서 연결 문자열을 만드는 방법에 대한 도움말을 확인하세요.  
  
4. **인증** 영역에서 인증 방법을 선택합니다.  
  - 컴퓨터의 관리자이며 방금 SQL Server를 설치한 경우 **Windows 인증**을 시도합니다.  이 인증은 SQL Server에 대한 액세스 권한이 있는 도메인 사용자로 구성된 경우에도 진행됩니다. 로그인 시도 시 Windows에 로그인할 때 사용한 자격 증명이 사용되므로 **사용자 이름** 및 **암호** 상자는 둘 다 흐리게 표시됩니다. 
  -  사용자 계정의 이름 및 암호를 알고 있는 경우 **SQL Server 인증**을 선택한 다음 **사용자 이름** 및 **암호**를 제공합니다.
  - 최신 버전의 SSMS가 있는 경우 **Active Directory 인증**으로 시작하는 3개의 옵션이 추가로 제공됩니다. 이러한 추가 고급 옵션에 대한 자세한 내용은 [SQL 데이터베이스 및 SQL 데이터 웨어하우스를 사용한 유니버설 인증(MFA에 대한 SSMS 지원)](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.  
  
## <a name="management-studio-components"></a>Management Studio 구성 요소  
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 는 유형에 따른 전용 창에 정보를 나타냅니다. 데이터베이스 정보는 개체 탐색기 및 문서 창에 표시됩니다.  
  
-   개체 탐색기는 서버에 있는 모든 데이터베이스 개체의 트리 뷰로, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]및 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]데이터베이스를 포함할 수 있습니다. 개체 탐색기에는 연결된 모든 서버에 대한 정보가 포함되어 있습니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 열면 마지막으로 사용된 설정에 개체 탐색기를 연결하라는 메시지가 표시됩니다. 등록된 서버 구성 요소에서 서버를 두 번 클릭하여 연결할 수 있지만 연결할 서버를 등록하지 않아도 됩니다.  
  
-   문서 창은 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 가장 큰 부분으로, 쿼리 편집기와 브라우저 창을 포함할 수 있습니다. 기본적으로 현재 컴퓨터의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결된 요약 페이지가 표시됩니다.  
  
## <a name="showing-additional-windows"></a>추가 창 표시  
  
#### <a name="to-show-the-registered-servers-window"></a>등록된 서버 창을 표시하려면  
  
1.  **보기** 메뉴에서 **등록된 서버**를 클릭합니다.  
  
    등록된 서버 창은 개체 탐색기 위나 인접한 곳에 나타납니다. 창을 끌어서 다양한 위치에 고정할 수 있습니다. 예약된 서버에는 사용자가 자주 관리하는 서버가 나열됩니다. 이 목록에서 서버를 추가하거나 제거할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행 중인 컴퓨터의 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]인스턴스만 나열됩니다.  
  
2.  사용 중인 서버가 나타나지 않으면 등록된 서버에서 **데이터베이스 엔진**을 마우스 오른쪽 단추로 클릭하고 **작업**을 클릭한 다음 **로컬 서버 등록 업데이트**를 클릭합니다. 다른 SQL Server 또는 SQL Database를 추가하려면 등록된 서버에서 한 위치를 마우스 오른쪽 단추로 클릭한 다음 **새 서버 등록**을 클릭합니다. **서버에 연결** 대화 상자와 마찬가지로 **로그인** 영역에서 정보를 입력합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[등록된 서버 및 개체 탐색기와 연결](../../tools/sql-server-management-studio/lesson-1-2-connect-with-registered-servers-and-object-explorer.md)  

  

