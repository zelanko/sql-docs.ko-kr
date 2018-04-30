---
title: Ssms 유틸리티 | Microsoft Docs
ms.custom: ''
ms.date: 12/08/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], opening
- command prompt utilities [SQL Server], sqlwb
- sqlwb utility
- Management Studio command line
- opening SQL Server Management Studio
ms.assetid: aafda520-9e2a-4e1e-b936-1b165f1684e8
caps.latest.revision: 50
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7af050ee18152754cab5da650a19d49d3bd6a1a8
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="ssms-utility"></a>Ssms 유틸리티
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  **Ssms**유틸리티는 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 엽니다. **Ssms** 를 지정하면 서버 연결도 설정되며 쿼리, 스크립트, 파일, 프로젝트 및 솔루션이 열립니다.  
  
 쿼리, 프로젝트 또는 솔루션이 포함된 파일을 지정할 수 있습니다. 연결 정보를 제공했고 파일 형식이 해당 서버 유형에 연결된 경우 쿼리가 포함된 파일은 서버에 자동으로 연결됩니다. 예를 들어 .sql 파일은 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 SQL 쿼리 편집기 창을 열고 .mdx 파일은 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 MDX 쿼리 편집기 창을 엽니다. **에서** SQL Server 솔루션 및 프로젝트 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]가 열립니다.  
  
> [!NOTE]  
>  **Ssms** 유틸리티는 쿼리를 실행하지 않습니다. 명령줄에서 쿼리를 실행하려면 **sqlcmd** 유틸리티를 사용합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Ssms  
    [scriptfile] [projectfile] [solutionfile]  
    [-S servername] [-d databasename] [-G] [-U username] [-P password]   
    [-E] [-nosplash] [-log [filename]?] [-?]  
```  
  
## <a name="arguments"></a>인수  
 *scriptfile*  
 열려는 스크립트 파일을 하나 이상 지정합니다. 매개 변수에 파일의 전체 경로가 포함되어야 합니다.  
  
 *projectfile*  
 열려는 스크립트 프로젝트를 지정합니다. 매개 변수에 스크립트 프로젝트 파일의 전체 경로가 포함되어야 합니다.  
  
 *solutionfile*  
 열려는 솔루션을 지정합니다. 매개 변수에 솔루션 파일의 전체 경로가 포함되어야 합니다.  
  
 [**-S** *servername*]  
  서버 이름  
  
 [**-d** *databasename*]  
  데이터베이스 이름  

 [**-G**] Active Directory 인증을 사용하여 연결. **-P** 및/또는 **-U**의 포함 여부에 따라 연결 형식이 결정됩니다.
 - **-U** 및 **-P**가 포함되지 *않으면* **Active Directory - 통합**이 사용되고 대화 상자가 표시되지 않습니다.
 - **-U** 및 **-P**가 둘 다 포함되면 **Active Directory - 암호**가 사용됩니다. 이 옵션을 사용하면 명령줄에서 일반 텍스트 암호를 지정해야 하는데, 매우 번거로운 일이므로 이 옵션을 **사용하지 않는 것이 좋습니다**.
 - **-U**는 포함되고 **-P**는 포함되지 않으면 인증 대화 상자가 나타나지만, 모든 로그인 시도가 실패합니다. 

  **Active Directory - MFA 지원을 포함한 유니버설 인증**은 현재 지원되지 않습니다. 
  
[**-U** *username*]  
 'SQL 인증' 또는 'Active Directory - 암호'와 연결할 때의 사용자 이름  
  
[**-P** *password*]  
 'SQL 인증' 또는 'Active Directory - 암호'와 연결할 때의 암호
  
[**-E**]  
 Windows 인증을 사용하여 연결  
  
[**-nosplash**]  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 여는 동안 시작 화면을 표시하지 않습니다. 대역폭이 제한된 연결에서 터미널 서비스를 사용하여 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 실행하는 컴퓨터에 연결할 때 이 옵션을 사용합니다. 이 인수는 대/소문자를 구분하지 않으며 다른 인수 앞이나 뒤에 나타날 수 있습니다.  
  
[**-log***[filename]?*]  
 문제 해결을 위해 지정된 파일에 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 작업을 기록합니다.  
  
[**-?**]  
 명령줄 도움말을 표시합니다.  
  
## <a name="remarks"></a>Remarks  
 모든 스위치는 선택 사항이며 쉼표로 구분되는 파일을 제외하고 공백으로 구분합니다. 스위치를 지정하지 않으면 **Ssms** 가 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 도구 **메뉴의** 옵션 **설정에 지정된 대로** 를 엽니다. 예를 들어 **환경/일반** 페이지에서 **시작 시** 옵션으로 **새 쿼리 창 열기**를 지정할 경우 **Ssms** 는 빈 쿼리 편집기를 엽니다.  
  
 **-log** 스위치는 명령줄 끝에 다른 모든 스위치 뒤에 나타나야 합니다. 파일 이름 인수는 선택 사항입니다. 파일 이름을 지정하는 경우 해당 파일이 없으면 파일이 만들어집니다. 쓰기 권한 부족 등의 이유로 파일을 만들 수 없는 경우 로그는 대신 지역화되지 않은 APPDATA 위치에 작성됩니다(아래 참조). 파일 이름 인수를 지정하지 않으면 현재 사용자의 지역화되지 않은 응용 프로그램 데이터 폴더에 파일이 두 개 작성됩니다. SQL Server에 대한 지역화되지 않은 응용 프로그램 데이터 폴더는 APPDATA 환경 변수에서 찾아볼 수 있습니다. 예를 들어 SQL Server 2012의 경우 해당 폴더는 \<시스템 드라이브>:\Users\\<username\>\AppData\Roaming\Microsoft\AppEnv\10.0\\입니다. 기본적으로 두 파일의 이름은 ActivityLog.xml과 ActivityLog.xsl입니다. ActivityLog.xml에는 작업 로그 데이터가 포함되고 ActivityLog.xsl은 XML 파일을 더 편리하게 볼 수 있는 방법을 제공하는 XML 스타일 시트입니다. Internet Explorer와 같은 기본 XML 뷰어에서 로그 파일을 보려면 시작, 실행...을 차례로 클릭하고 제공된 필드에 “\<시스템 드라이브>:\Users\\<username\>\AppData\Roaming\Microsoft\AppEnv\10.0\ActivityLog.xml”을 입력한 다음 Enter 키를 누릅니다.  
  
 연결 정보를 제공했고 파일 형식이 해당 서버 유형에 연결된 경우 쿼리가 포함된 파일을 서버에 연결할 것인지 묻는 메시지가 나타납니다. 예를 들어 .sql 파일은 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 SQL 쿼리 편집기 창을 열고 .mdx 파일은 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 MDX 쿼리 편집기 창을 엽니다. **에서** SQL Server 솔루션 및 프로젝트 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]가 열립니다.  
  
 다음 표에서는 서버 유형과 연결된 파일 확장명을 보여 줍니다.  
  
|서버 유형|확장명|  
|-----------------|---------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|.sql|  
|SQL Server Analysis Services|.mdx<br /><br /> .xmla|  
  
## <a name="examples"></a>예  
 다음 스크립트는 명령 프롬프트에서 기본 설정으로 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 엽니다.  
  
```  
Ssms  
  
```  
  
 다음은 *Active Directory - 통합*을 사용하여 명령 프롬프트에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 엽니다.  
  
```  
Ssms.exe -S servername.database.windows.net -G
  
``` 


 다음 스크립트는 명령 프롬프트에서 Windows 인증을 사용하여 시작 화면을 표시하지 않고 코드 편집기를 서버 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 로 설정한 상태로 `ACCTG and the database AdventureWorks2012,` 를 엽니다.  
  
```  
Ssms -E -S ACCTG -d AdventureWorks2012 -nosplash  
  
```  

 다음 스크립트는 명령 프롬프트에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 열고 MonthEndQuery 스크립트를 엽니다.  
  
```  
Ssms "C:\Documents and Settings\username\My Documents\SQL Server Management Studio Projects\FinanceScripts\FinanceScripts\MonthEndQuery.sql"  
  
```  
  
 다음 스크립트는 명령 프롬프트에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 열고 `developer`라는 컴퓨터에서 NewReportsProject 프로젝트를 엽니다.  
  
```  
Ssms "\\developer\fin\ReportProj\ReportProj\NewReportProj.ssmssqlproj"  
  
```  
  
 다음 스크립트는 명령 프롬프트에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 를 열고 MonthlyReports 솔루션을 엽니다.  
  
```  
Ssms "C:\solutionsfolder\ReportProj\MonthlyReports.ssmssln"  
  
```  
 



## <a name="see-also"></a>참고 항목  
 [SQL Server Management Studio 사용](http://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
  
  
