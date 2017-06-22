---
title: "SQL Server Management Studio의 이전 릴리스 | Microsoft 문서"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 87f593c3-8b76-4c12-963a-31d35f2fb294
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 0927784589c1f7227b432ff49f81f29de20083ec
ms.openlocfilehash: 200753bf64d92043171788852227c6199b64711d
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="previous-sql-server-management-studio-releases"></a>SQL Server Management Studio의 이전 릴리스
  
SQL Server Management Studio의 다음 이전 릴리스를 사용할 수 있습니다.
   
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-1653-releasehttpgomicrosoftcomfwlinklinkid840946"></a>![다운로드](../ssdt/media/download.png) [SQL Server Management Studio 16.5.3 릴리스](http://go.microsoft.com/fwlink/?LinkID=840946)

**버전 정보**  
  
*이 SSMS 릴리스는 Visual Studio 2015의 격리 셸을 사용합니다.*  
릴리스 번호: 16.5.3  
이 릴리스에 대한 빌드 번호: 13.0.16106.4

## <a name="changelog"></a>Changelog  

16.5.3

이 릴리스에서는 다음과 같은 문제가 해결되었습니다.

* 테이블에 스파스 열이 둘 이상 있을 때 'Table' 노드의 확장을 일으키는 SSMS 16.5.2의 문제를 해결함.

* 사용자가 Microsoft Dynamics AX/CRM Online 리소스에 연결되는 OData 연결 관리자를 포함하는 SSIS 패키지를 SSIS 카탈로그에 배포할 수 있음. 자세한 내용은 [OData 연결 관리자](https://msdn.microsoft.com/library/dn584133.aspx)를 참조하세요.

* 기존 테이블에 대한 Always Encrypted 구성이 관련 없는 개체에 대한 오류와 함께 실패함. [Connect ID 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* 여러 스키마가 포함된 기존 데이터베이스에 대한 Always Encrypted 구성이 작동하지 않음. [Connect ID 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* Always Encrypted, 암호화된 열 마법사가 시스템 뷰를 참조하는 뷰를 포함하는 데이터베이스로 인해 실패함. [Connect ID 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* Always Encrypted를 사용하여 암호화할 때 암호화가 잘못 처리된 후 모듈을 새로 고치지 못하는 오류가 발생함.

* *최근에 사용한 항목 열기* 메뉴에 최근에 저장한 파일이 표시되지 않음. [Connect ID 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* 원격(인터넷) 연결을 통해 테이블의 인덱스를 마우스 오른쪽 단추로 클릭할 경우 SSMS가 느려짐. [Connect ID 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* SQL 디자이너 스크롤 막대 관련 문제를 해결함. [Connect ID 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* 테이블의 상황에 맞는 메뉴가 잠시 중단됨 
 
* SSMS에서 가끔 [작업 모니터]에서 예외를 발생시키고 작동을 중단함. [Connect ID 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016이 "The process was terminated due to an internal error in the .NET Runtime at IP 71AF8579 (71AE0000) with exit code 80131506"(.NET 런타임의 IP 71AF8579(71AE0000)에서 내부 오류로 인해 프로세스가 종료되었습니다(종료 코드 80131506).) 오류와 함께 작동이 중단됨



## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-165-releasehttpgomicrosoftcomfwlinklinkid832812"></a>[SQL Server Management Studio 16.5 릴리스](http://go.microsoft.com/fwlink/?LinkID=832812) ![다운로드](../ssdt/media/download.png)

**버전 정보**  
  
*이 SSMS 릴리스에서는 Visual Studio 2015의 격리 셸을 사용합니다.*  
릴리스 번호: 16.5  
이 릴리스에 대한 빌드 번호: 13.0.16000.28

**이 빌드의 알려진 문제**  

1. CHECK 제약 조건이 발생할 때 Invoke-Sqlcmd이 여러 행을 잘못 삽입합니다. [Microsoft Connect 항목: 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

2. 가용성 그룹을 만들 때 ENU가 아닌 언어 버전이 완벽히 작동하지 않습니다.

3. 쿼리 계획 XML을 클릭할 때 올바른 SSMS UI가 열리지 않습니다.

**Changelog**

* ";:"을 포함하는 테이블 이름이 있는 데이터베이스를 클릭했을 때 충돌이 발생하는 문제를 해결했습니다.
* AS 테이블 형식 데이터베이스 속성 창에서 모델 페이지를 변경하면 원래 정의가 스크립팅되는 문제를 해결했습니다. 
[Microsoft Connect 항목: 3080744](https://connect.microsoft.com/SQLServer/feedback/details/3080744) 
* 임시 파일이 "최근 파일" 목록에 추가되는 문제를 해결했습니다.  
[Microsoft Connect 항목: 2558789](https://connect.microsoft.com/SQLServer/feedback/details/2558789)
* 개체 탐색기 트리에서 사용자 테이블 노드에 대한 "압축 관리" 메뉴 항목이 비활성화되는 문제를 해결했습니다.  
[Microsoft Connect 항목: 3104616](https://connect.microsoft.com/SQLServer/feedback/details/3104616)

* 사용자가 개체 탐색기, 등록된 서버 탐색기, 템플릿 탐색기 및 개체 탐색기 정보에 대한 글꼴 크기를 설정할 수 없는 문제를 해결했습니다. 탐색기에 대한 글꼴은 환경 글꼴이 사용됩니다.  
[Microsoft Connect 항목: 691432](https://connect.microsoft.com/SQLServer/feedback/details/691432)

* 연결이 끊겼을 때 SSMS가 항상 기본 데이터베이스에 다시 연결되는 문제를 해결했습니다.  
[Microsoft Connect 항목: 3102337](https://connect.microsoft.com/SQLServer/feedback/details/3102337)

* 실행 계획 아이콘을 비롯하여 정책 관리 및 쿼리 편집기 창에서 dpi가 높은 여러 문제를 해결했습니다.

* 확장된 이벤트에 대한 글꼴 및 색 구성 옵션이 없는 문제를 해결했습니다.

* 응용 프로그램을 닫거나 오류 대화 상자를 표시하려는 경우 SSMS 충돌이 발생하는 문제를 해결했습니다.


   
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-1641-september-2016-releasehttpgomicrosoftcomfwlinklinkid828615"></a>[SQL Server Management Studio 16.4.1(2016년 9월) 릴리스](http://go.microsoft.com/fwlink/?LinkID=828615) ![다운로드](../ssdt/media/download.png)

**버전 정보**  
  
*이 SSMS 릴리스는 Visual Studio 2015의 격리 셸을 사용합니다.*  
릴리스 번호: 16.4.1  
이 릴리스에 대한 빌드 번호: 13.0.15900.1
  
**이 빌드의 알려진 문제**  

1. **단일 Azure Active Directory 계정만 Active Directory 유니버설 인증을 사용하여 SSMS 인스턴스에 대해 로그인할 수 있습니다.**  
    이 제한은 Active Directory 유니버설 인증으로 제한됩니다. Active Directory 암호 인증, Active Directory 통합 인증 또는 SQL Server 인증으로는 다른 서버에 로그인할 수 있습니다.
    
    해결 방법으로, 다른 SSMS 인스턴스를 사용하여 다른 Azure Active Directory 계정으로 로그인할 수 있습니다. 
    
2. **데이터 계층 응용 프로그램 프레임워크(DacFx) 명령 및 SSMS의 스키마 디자이너는 Active Directory 유니버설 인증을 지원하지 않습니다.**  
    DacFx를 사용하는 명령(예: 가져오기 및 내보내기), SSMS의 스키마 디자이너는 현재 Active Directory 유니버설 인증을 지원하지 않습니다.
    
    해결 방법으로, SSMS에 제공되는 다른 형식의 인증인 Active Directory 암호 인증, Active Directory 통합 인증 또는 SQL Server 인증을 사용할 수 있습니다.

3. **SSMS는 SSIS 2016(SQL Server 2016 Integrated Services) 인스턴스에만 연결할 수 있습니다.**  
    SQL Server Integration Services의 알려진 호환성 제한 때문에 이전 버전에는 연결할 수 없습니다.
    
    이 문제에 대한 해결 방법으로, [SSIS 인스턴스에 맞게 조정된 SSMS 릴리스](../ssms/previous-sql-server-management-studio-releases.md)를 사용하여 SQL Server Integration Service 인스턴스에 연결할 수 있습니다. 
  
4. **SSMS는 SQL Server 2008 R2 및 이전 버전의 SQL Server 버전에 대한 유지 관리 계획을 저장하지 않습니다.**  
    이 문제는 향후 해결될 것으로 예상되는 알려진 제한 사항입니다. 현재는 [SSMS 2014 릴리스](../ssms/previous-sql-server-management-studio-releases.md) 를 사용하여 유지 관리 계획을 저장할 수 있습니다.  
    
5. **영어 이외의 SSMS 설치에는 추가 보안 패키지를 설치해야 합니다.**  
영어 이외의 지역화된 SSMS 릴리스는 Windows 8, Windows 7, Windows Server 2012 및 Windows Server 2008 R2에 설치하는 경우 [KB 2862966 보안 업데이트 패키지가 필요](https://support.microsoft.com/en-us/kb/2862966) 합니다.
  
6. **클라이언트 컴퓨터에 SQL Server가 없으면 SQL Server 구성 관리자가 시작되지 않습니다.**  
    클라이언트 컴퓨터에 SQL Server가 설치되어 있지 않은 상태에서 SQL Server 구성 관리자를 시작하면 다음과 같은 오류가 표시됩니다.   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`,   
   
     * SQL Server 인스턴스를 SSMS의 ‘등록된 서버’ 목록에 추가한 경우:  
        1. SSMS의 ‘등록된 서버’ 보기로 이동합니다.  
        2. 구성하려는 SQL Server 인스턴스를 마우스 오른쪽 단추로 클릭합니다.  
        3. 오른쪽 클릭 메뉴에서 ‘SQL Server 구성 관리자...’를 선택합니다.    
          
      * SQL Server 인스턴스를 SSMS의 ‘등록된 서버’ 목록에 추가하지 않은 경우:  
        1. 관리자 권한으로 명령 프롬프트를 엽니다.  
        2. 다음 명령을 사용하여 Mofcomp 도구를 실행합니다.  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. Mofcomp 도구를 실행한 후 다음 명령으로 WMI 서비스를 다시 시작하여 변경 내용을 적용합니다.  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  

 
**Changelog** 

*  저장 프로시저를 변경/수정하려는 동안 실패하는 경우 문제 해결  
[Microsoft Connect 항목 #3103831](https://connect.microsoft.com/SQLServer/feedback/details/3103831)

* PowerShell을 사용하여 데이터를 보고 쓰기 위한 새로운 'Read-SqlTableData', 'Read-SqlViewData' 및 'Write-SqlTableData' cmdlet  
[Trello Read-SqlTableData 카드](https://trello.com/c/FXVUNJ8x/131-read-sqltabledata)  
[Microsoft Connect 항목 #2685363](https://connect.microsoft.com/SQLServer/feedback/details/2685363)
    
* PowerShell을 사용하여 새 로그인 관리 시나리오를 지원하기 위한 'Add-SqlLogin' cmdlet  
[Microsoft Connect 항목 #2588952](https://connect.microsoft.com/SQLServer/feedback/details/2588952)
    
*  다양한 국가별 클라우드에 연결하는 사용자에 대한 지원 및 사용 편의성 개선
    
*  메모리 부족 예외를 발생시키던 문제 해결  
[Microsoft Connect 항목 #3062914](https://connect.microsoft.com/SQLServer/feedback/details/3062914)  
[Microsoft Connect 항목 #3074856](https://connect.microsoft.com/SQLServer/feedback/details/3074856)
    
*  스키마별 필터링이 올바른 필터 옵션이 아니던 문제 해결  
[Microsoft Connect 항목 #3058105](https://connect.microsoft.com/SQLServer/feedback/details/3058105)  
[Microsoft Connect 항목 #3101136](https://connect.microsoft.com/SQLServer/feedback/details/3101136)
    
*  늘어난 데이터베이스의 모니터 창에 액세스할 수 없는 문제 해결
    
*  F1 도움말에서 항상 온라인 콘텐츠를 여는 문제 해결. 이제 사용자가 도움말 메뉴의 "도움말 기본 설정 지정"을 통해 온라인 또는 오프라인 도움말 중에서 선택할 수 있습니다.   
[Microsoft Connect 항목 #2826366](https://connect.microsoft.com/SQLServer/feedback/details/2826366)
    
*  1200 수준 Analysis Services 테이블 형식 모델을 스크립팅할 때 서버 버전과 다르게 스크립팅에 사용되는 암호가 제거되지 않는 문제 해결[이제 클라이언트 모델 개체가 스크립팅 전에 동기화됨]
    
*  '상위 N개 행 선택' 옵션으로 더 이상 사용되지 않는 TOP 연산자 구문이 생성되는 문제 해결  
[Microsoft Connect 항목 #3065435](https://connect.microsoft.com/SQLServer/feedback/details/3065435)
    
*  SSMS 전반에서 로그인 속성 페이지, 고급 쿼리 실행 옵션을 비롯한 다양한 레이아웃 문제 해결   
[Microsoft Connect 항목 #3058199](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect 항목 #3079122](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect 항목 #3071384](https://connect.microsoft.com/SQLServer/feedback/details/3071384)
    
*  사용자가 새 쿼리 창을 열 때마다 솔루션이 자동으로 생성되는 문제 해결   
[Microsoft Connect 항목 #2924667](https://connect.microsoft.com/SQLServer/feedback/details/2924667)    
[Microsoft Connect 항목 #2917742](https://connect.microsoft.com/SQLServer/feedback/details/2917742)   
[Microsoft Connect 항목 #2612635](https://connect.microsoft.com/SQLServer/feedback/details/2612635)
    
*  시스템 데이터베이스 내에 있을 때 개체 탐색기에서 임시 테이블을 확장할 수 없는 문제 해결  
[Microsoft Connect 항목 #2551649](https://connect.microsoft.com/SQLServer/feedback/details/2551649)
    
*  SSMS가 일괄 처리 실행 후 SELECT @@trancount에 대한 쿼리를 실행하는 문제 해결    
[Microsoft Connect 항목 #3042364](https://connect.microsoft.com/SQLServer/feedback/details/3042364)
    
*  서버의 속성 페이지에서 스크립트를 만들면 연결 대화 상자가 숨겨지는 Analysis Services의 문제 해결
    
*  Ctrl + Q로 빠른 실행 도구 모음이 선택되지 않는 문제 해결
    
*  2TB가 넘는 데이터베이스의 경우에는 서버 속성 대화 상자를 사용하여 데이터베이스의 MaxSize를 변경할 수 없는 문제 해결  
[Microsoft Connect 항목 #1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  데이터베이스 복원 마법사에서 앞에 공백이 있는 파일 이름을 사용할 수 없는 문제 해결   
[Microsoft Connect 항목 #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)

*  데이터베이스 복원 마법사에서 앞에 공백이 있는 파일 이름을 사용할 수 없는 문제 해결   
[Microsoft Connect 항목 #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-163-august-2016-releasehttpgomicrosoftcomfwlinklinkid824938"></a>[SQL Server Management Studio 16.3(2016년 8월) 릴리스](http://go.microsoft.com/fwlink/?LinkID=824938) ![다운로드](../ssdt/media/download.png)
 2016년 8월 15일 | 버전 번호: 13.0.15700.28

**기능**  
1. 새 인증 옵션 'Active Directory 유니버설 인증'
2. SQL Server PowerShell 모듈에 대한 새 cmdlet
3. DTA(데이터베이스 엔진 튜닝 관리자) 및 확장 이벤트 템플릿에 대해 향상된 기능
4. [High Resolution Display in SSMS](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/)(SSMS의 고해상도 디스플레이)에 대한 베타 지원

[SSMS changelog에서 사용할 수 있는 기능에 대한 추가 정보](../ssms/sql-server-management-studio-changelog-ssms.md)

**알려진 문제**

다음은 이번 SQL Server Management Studio 릴리스의 문제점과 제한 사항입니다.  

1. **단일 Azure Active Directory 계정만 Active Directory 유니버설 인증을 사용하여 SSMS 인스턴스에 대해 로그인할 수 있습니다.**  
    이 제한은 Active Directory 유니버설 인증으로 제한됩니다. Active Directory 암호 인증, Active Directory 통합 인증 또는 SQL Server 인증으로는 다른 서버에 로그인할 수 있습니다.
    
    해결 방법으로, 다른 SSMS 인스턴스를 사용하여 다른 Azure Active Directory 계정으로 로그인할 수 있습니다. 
    
2. **데이터 계층 응용 프로그램 프레임워크(DacFx) 명령 및 SSMS의 스키마 디자이너는 Active Directory 유니버설 인증을 지원하지 않습니다.**  
    DacFx를 사용하는 명령(예: 가져오기 및 내보내기), SSMS의 스키마 디자이너는 현재 Active Directory 유니버설 인증을 지원하지 않습니다.
    
    해결 방법으로, SSMS에 제공되는 다른 형식의 인증인 Active Directory 암호 인증, Active Directory 통합 인증 또는 SQL Server 인증을 사용할 수 있습니다.

3. **SSMS는 SSIS 2016(SQL Server 2016 Integrated Services) 인스턴스에만 연결할 수 있습니다.**  
    SQL Server Integration Services의 알려진 호환성 제한 때문에 이전 버전에는 연결할 수 없습니다.
    
    이 문제에 대한 해결 방법으로, [SSIS 인스턴스에 맞게 조정된 SSMS 릴리스](../ssms/previous-sql-server-management-studio-releases.md)를 사용하여 SQL Server Integration Service 인스턴스에 연결할 수 있습니다. 
  
4. **SSMS는 SQL Server 2008 R2 및 이전 버전의 SQL Server 버전에 대한 유지 관리 계획을 저장하지 않습니다.**  
    이 문제는 향후 해결될 것으로 예상되는 알려진 제한 사항입니다. 현재는 [SSMS 2014 릴리스](../ssms/previous-sql-server-management-studio-releases.md) 를 사용하여 유지 관리 계획을 저장할 수 있습니다.  
    
5. **영어 이외의 SSMS 설치에는 추가 보안 패키지를 설치해야 합니다.**  
영어 이외의 지역화된 SSMS 릴리스는 Windows 8, Windows 7, Windows Server 2012 및 Windows Server 2008 R2에 설치하는 경우 [KB 2862966 보안 업데이트 패키지가 필요](https://support.microsoft.com/en-us/kb/2862966) 합니다.
  
6. **클라이언트 컴퓨터에 SQL Server가 없으면 SQL Server 구성 관리자가 시작되지 않습니다.**  
    클라이언트 컴퓨터에 SQL Server가 설치되어 있지 않은 상태에서 SQL Server 구성 관리자를 시작하면 다음과 같은 오류가 표시됩니다.   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`,   
   
     * SQL Server 인스턴스를 SSMS의 ‘등록된 서버’ 목록에 추가한 경우:  
        1. SSMS의 ‘등록된 서버’ 보기로 이동합니다.  
        2. 구성하려는 SQL Server 인스턴스를 마우스 오른쪽 단추로 클릭합니다.  
        3. 오른쪽 클릭 메뉴에서 ‘SQL Server 구성 관리자...’를 선택합니다.    
          
      * SQL Server 인스턴스를 SSMS의 ‘등록된 서버’ 목록에 추가하지 않은 경우:  
        1. 관리자 권한으로 명령 프롬프트를 엽니다.  
        2. 다음 명령을 사용하여 Mofcomp 도구를 실행합니다.  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. Mofcomp 도구를 실행한 후 다음 명령으로 WMI 서비스를 다시 시작하여 변경 내용을 적용합니다.  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  


**수정 프로그램**
1. SSMS에서 암호 해독된 AlwaysEncrypted LOB(Large Object) 열의 일반 텍스트를 보기 위한 버그 수정(Microsoft Connect 항목 #2413024)
2. Windows 비주얼 스타일이 사용되도록 설정되지 않은 경우 충돌을 해결하기 위한 Always Encrypted 대화 상자의 버그 수정(예: 고대비 디스플레이를 사용하도록 설정)
3. SQL Server 인스턴스에 연결할 수 없게 하는 '메서드를 찾을 수 없음' 오류에 대한 버그 수정
4. 날짜/시간 오프셋으로 파티션 함수를 만들 때 발생하는 SSMS 충돌에 대한 버그 수정
5. Distributed Replay Administration Tool(DReplay.exe)을 시작하기 위해 Microsoft .NET 3.5가 필요한 상황을 제거하도록 버그 수정
6. 정규화된 서버 이름을 지원하기 위한 Analysis Services 배포 마법사의 버그 수정
7. 2016 호환성 모델을 사용하여 Analysis Services 테이블 형식 모델에 파티션을 표시하기 위한 SSMS의 버그 수정(Microsoft Connect 항목 #2845053)

[SSMS changelog에서 사용할 수 있는 수정 사항에 대한 추가 정보](../ssms/sql-server-management-studio-changelog-ssms.md)
 
---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-july-2016-hotfix-update-releasehttpgomicrosoftcomfwlinklinkid822301"></a>[SQL Server Management Studio(2016년 7월) 핫픽스 업데이트 릴리스](http://go.microsoft.com/fwlink/?LinkID=822301) ![다운로드](../ssdt/media/download.png)

2016년 7월 13일 | 버전 번호: 13.0.15600.2

**기능**  
1. SSMS의 Azure SQL 데이터 웨어하우스 지원.   
2. SQL Server PowerShell 모듈에 대한 중요 업데이트.   
3. Azure SQL 데이터베이스에 연결 시간 향상.  
4. Analysis Services 처리 대화 상자의 SQL Server 2016(호환성 수준 1200) 테이블 형식 데이터베이스에 대한 지원 개선 등   

[SSMS changelog에서 사용할 수 있는 추가 정보 및 기능](../ssms/sql-server-management-studio-changelog-ssms.md)

**알려진 문제** 
1. **SSMS 년 7월 핫픽스 릴리스용 설치 관리자가 SSMS 8월 릴리스로 표시됩니다.**
내부 빌드 설정으로 인해 7월 업데이트 핫픽스의 설치 페이지에 8월로 표시됩니다. 이 패키지는 사실상 SSMS 7월 릴리스의 핫픽스입니다. 
2. **SSMS는 '2016년 7월 핫픽스' 릴리스를 설치한 후 SQL Server 인스턴스에 연결할 수 없습니다.**
서버에 연결하려고 하면 다음과 같은 오류 메시지가 표시되는 최신 SSMS 업데이트 관련 문제에 대해 잘 알고 있습니다. 
   ```
    "Method not found: 'Void Microsoft.SqlServer.Management.Common.SqlConnectionInfo.set_ApplicationIntent(System.String)'"
    ```
  
    이 문제에 대한 수정 프로그램은 다음 SSMS 릴리스에 제공될 예정입니다. 이 문제를 해결하려면 SSMS를 제거한 후 다시 설치하면 됩니다. 자세한 내용을 보려면 [문제에 대한 Microsoft Connect 스레드를 방문](https://connect.microsoft.com/SQLServer/feedback/details/2925257/not-able-to-connect-to-sql-server-instances-after-installing-ssms-2016-july-update)하세요.
    
3. **Azure Storage 계정을 선택하려고 하면 SSMS가 충돌합니다.**
Azure Storage 계정을 선택하려고 하고 '클래식' 저장소 계정이 없는 경우 SSMS 7월 릴리스 및 7월 핫픽스 릴리스가 충돌합니다.
이 문제에 대한 수정 프로그램은 향후 SSMS 릴리스에만 제공될 예정입니다. 이 문제를 해결하려면 클래식 저장소 계정을 만들거나 [T-SQL을 통해 백업 또는 복원하여](https://msdn.microsoft.com/library/jj720552(v=sql.120).aspx)Azure Storage 계정으로 데이터베이스를 백업/복원할 수 있습니다.

4. **SSMS의 백업/복원 마법사에는 '클래식' Azure Storage 계정만 표시됩니다.**
SSMS 7월 릴리스 및 7월 핫픽스 릴리스는 사용자가 백업 또는 복원 마법사를 사용하여 백업 또는 복원을 시도하는 경우 새 자격 증명 생성을 위해 '클래식' Azure Storage 계정만 표시합니다.
이 문제에 대한 수정 프로그램은 향후 SSMS 릴리스에만 제공될 예정입니다. 이 문제를 해결하려면 데이터베이스를 사용 가능한 Azure '클래식' 저장소 계정으로 백업/복원하거나 [T-SQL을 통해 백업 또는 복원하여](https://msdn.microsoft.com/library/jj720552(v=sql.120).aspx)'ARM 유형' 저장소 계정으로 백업할 수 있습니다. 

5. **영어 이외의 SSMS 설치에는 추가 보안 패키지를 설치해야 합니다.**
영어 이외의 지역화된 SSMS 릴리스는 Windows 8, Windows 7, Windows Server 2012 및 Windows Server 2008 R2에 설치하는 경우 [KB 2862966 보안 업데이트 패키지](https://support.microsoft.com/en-us/kb/2862966) 가 필요합니다.
6. **SSMS는 SSIS 2016(SQL Server 2016 Integrated Services) 인스턴스에만 연결할 수 있습니다.** SQL Server Integration Services의 알려진 호환성 제한 때문에 이전 버전에는 연결할 수 없습니다.
이 문제에 대한 해결 방법으로, SSIS 인스턴스에 맞게 조정된 SSMS 릴리스를 사용하여 SQL Server Integration Service 인스턴스에 연결할 수 있습니다.
7. **SSMS는 SQL Server 2008 R2 및 이전 버전의 SQL Server 버전에 대한 유지 관리 계획을 저장하지 않습니다.** 이 문제에 대한 수정 프로그램을 제공하기 위해 현재 작업 중입니다. 현재는 아래의 SSMS 2014 릴리스를 사용하여 유지 관리 계획을 저장할 수 있습니다.
8. **클라이언트 컴퓨터에 SQL Server가 없으면 SQL Server 구성 관리자가 시작되지 않습니다.** 클라이언트 컴퓨터에 SQL Server가 설치되어 있지 않은 상태에서 SQL Server 구성 관리자를 시작하면 ‘WMI 공급자에 연결할 수 없습니다.’ 오류가 표시됩니다. 해결 방법:
    * 관리자 권한으로 명령 프롬프트를 엽니다.
    * 다음 명령을 사용하여 Mofcomp 도구를 실행합니다.  
      mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"
    * Mofcomp 도구를 실행한 후 다음 명령으로 WMI 서비스를 다시 시작하여 변경 내용을 적용합니다.  
       net stop "Windows Management Instrumentation"  
       net start "Windows Management Instrumentation"

**수정 프로그램**  
1. 사용자에게 SELECT 권한이 없는 경우 디자이너에 테이블을 추가할 수 있도록 SSMS 쿼리 디자이너의 버그 수정
2. 'TRY_CAST()' 및 'TRY_CONVERT()' 함수에 대한 IntelliSense 지원을 추가하는 버그 수정 [(Microsoft Connect 항목 #2453461)](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast).
3. Sql 파일의 끌어서 놓기 열기를 허용하는 SSMS 편집기 창의 버그 수정 [(Microsoft Connect 항목 #2690658)](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios).
4. 다차원 Analysis Services 모델의 데이터 피드 공급자를 올바르게 표시하도록 Analysis Services의 버그 수정.
5. SSMS 테이블 디자이너에서 참가 링크를 편집하려고 할 때 충돌을 방지하기 위해 SSMS의 버그 수정 [(Microsoft Connect 항목 #2721052)](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms).  

[SSMS changelog에서 사용할 수 있는 추가 정보 및 버그 수정](../ssms/sql-server-management-studio-changelog-ssms.md)

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-june-2016-releasehttpgomicrosoftcomfwlinklinkid799832"></a>[SQL Server Management Studio 2016년 6월 릴리스](http://go.microsoft.com/fwlink/?LinkID=799832) ![다운로드](../ssdt/media/download.png)

2016년 6월 1일 | 버전 번호: 13.0.15000.23

**기능**  
단순화된 새 SSMS 설치 관리자 독립 실행형 SSMS 릴리스 업데이트 자동 확인 새로운 빠른 찾기 대화 상자 Visual Studio 2015 셸에 구축된 SSMS 및 기타 다양한 기능   
[SSMS changelog에서 확인할 수 있는 자세한 내용](../ssms/sql-server-management-studio-changelog-ssms.md)

**알려진 문제** 
1. **현재는 Always Encrypted 마법사에서 PowerShell 스크립트 생성이 지원되지 않습니다.**
이 문제에 대한 수정 프로그램은 후속 월별 SSMS 업데이트에 사용할 수 있습니다.
2. **Azure SQL 데이터베이스에 연결되어 있는 경우 개체 탐색기의 ‘열 암호화’ 상황에 맞는 메뉴 항목을 테이블 및 열에 사용할 수 없습니다.** 이 문제에 대한 수정 프로그램은 후속 월별 SSMS 업데이트에 사용할 수 있습니다. 이 문제를 해결하려면 개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 '작업'을 선택한 후 '열 암호화'를 선택하여 Azure SQL 데이터베이스 열 및 테이블을 암호화합니다.
3. **SSMS는 SSIS 2016(SQL Server 2016 Integrated Services) 인스턴스에만 연결할 수 있습니다.** SQL Server Integration Services의 알려진 호환성 제한 때문에 이전 버전에는 연결할 수 없습니다.
이 문제에 대한 해결 방법으로, SSIS 인스턴스에 맞게 조정된 SSMS 릴리스를 사용하여 SQL Server Integration Service 인스턴스에 연결할 수 있습니다.
4. **SSMS는 SQL Server 2008 R2 및 이전 버전의 SQL Server 버전에 대한 유지 관리 계획을 저장하지 않습니다.** 이 문제에 대한 수정 프로그램을 제공하기 위해 현재 작업 중입니다. 현재는 아래의 SSMS 2014 릴리스를 사용하여 유지 관리 계획을 저장할 수 있습니다.
5. **클라이언트 컴퓨터에 SQL Server가 없으면 SQL Server 구성 관리자가 시작되지 않습니다.** 클라이언트 컴퓨터에 SQL Server가 설치되어 있지 않은 상태에서 SQL Server 구성 관리자를 시작하면 ‘WMI 공급자에 연결할 수 없습니다.’ 오류가 표시됩니다. 해결 방법:
    * 관리자 권한으로 명령 프롬프트를 엽니다.
    * 다음 명령을 사용하여 Mofcomp 도구를 실행합니다.  
      mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"
    * Mofcomp 도구를 실행한 후 다음 명령으로 WMI 서비스를 다시 시작하여 변경 내용을 적용합니다.  
       net stop "Windows Management Instrumentation"  
       net start "Windows Management Instrumentation"

**수정 프로그램**  
1. 현재 문서에 더 잘 통합되고 정규식을 통한 검색을 허용하는 SSMS의 빠른 찾기 대화 상자([Microsoft Connect 항목 #2735513](https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/))
2. 도움말 문서를 올바르게 표시하기 위한 SSMS 상황에 맞는 F1 도움말의 버그 수정
3. 스크롤 시 SSMS가 충돌을 일으키는 쿼리 데이터 저장소 '재발된 쿼리' 보기의 버그 수정
4. Excel 2016에서 SQL Server Analysis Services로 연결할 수 있도록 하는 Excel Analysis Services OLEDB 커넥터의 버그 수정
5. 동일한 모니터의 연결 대화 상자를 다중 모니터 시스템의 기본 SSMS 창으로 표시하기 위한 SSMS 연결 대화 상자의 버그 수정([Microsoft Connect 항목 #724909)](https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/)
6. Always Encrypted 환경의 버그 수정 Stretch 데이터베이스에 대해 Always Encrypted 메뉴 옵션이 사용 가능하도록 올바르게 설정되지 않는 버그가 수정되었습니다. 또한 SafeNet(Luna SA) HSM 공급자가 제대로 사용되지 않던 Always Encrypted 마법사의 버그도 수정되었습니다.

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-2014-sp1httpdownloadmicrosoftcomdownload156156992e6-f7c7-4e55-833d-249bd2348138enux86sqlmanagementstudiox86enuexe"></a>[SQL Server Management Studio 2014 SP1](http://download.microsoft.com/download/1/5/6/156992E6-F7C7-4E55-833D-249BD2348138/ENU/x86/SQLManagementStudio_x86_ENU.exe) ![다운로드](../ssdt/media/download.png)

2015년 5월 14일 | 버전 번호: 12.0.4100.1

**기능**  
개선된 Azure SQL 데이터베이스에서는 새로운 관리 포털 메뉴, 테이블 디자이너 통합 등을 지원합니다.   
[릴리스 정보에서 사용할 수 있는 자세한 내용](https://support.microsoft.com/en-us/kb/3058865)

**알려진 문제**  
해당 사항 없음

**수정 프로그램**
1. 유지 관리 계획 이름 및 첫 번째 SUB_PLAN 이름이 동일한 경우 유지 관리 계획의 이동 작업 동안 SSMS가 충돌합니다.
2. SSMS(SQL Server Management Studio)에서 sp_executesql을 호출하는 저장 프로시저를 디버깅할 수 없습니다. F11 키를 누르면 '개체 참조가 개체의 인스턴스로 설정되지 않음' 오류 메시지가 표시됩니다([Microsoft Connect 항목 #736509](https://connect.microsoft.com/SQLServer/feedback/details/736509/sql-server-2012-rtm-management-studio-cannot-debug-sp-executesql)).
3. SSMS가 SQL Server Express의 전체 텍스트를 완전하게 관리하지 않습니다([Microsoft Connect 항목 #740181](https://connect.microsoft.com/SQLServer/feedback/details/740181/management-studio-does-not-fully-manage-full-text-in-sql-server-express)).
4. SSMS가 번호가 매겨진 저장 프로시저를 일관되게 처리하지 못합니다 [(Microsoft Connect 항목 #764197](https://connect.microsoft.com/SQLServer/feedback/details/764197/ssms-2012-inconsistently-handles-numbered-procedures)).
5. SSMS가 닫힐 때 가끔 충돌하여 자동으로 다시 시작됩니다([Microsoft Connect 항목 #774317](https://connect.microsoft.com/SQLServer/feedback/details/774317/sql-server-management-studio-2012-2014-crashes-when-closing)).
6. SSMS에서 열 수준 사용 권한을 스크립팅할 때 스크립트 생성 중에 문이 복제됩니다([Microsoft Connect 항목 #797967](https://connect.microsoft.com/SQLServer/feedback/details/797967/ssms-create-script-duplicates-the-statements-for-grant-or-deny-column-permissions)).
7. 작업 표시줄에서 SSMS 창 아이콘을 새로 고치려고 하면 SSMS가 충돌할 수 있습니다([Microsoft Connect 항목 #799430](https://connect.microsoft.com/SQLServer/feedback/details/799430/ssms-2012-sp-1-cu-5-installed-crash-when-enforce-refresh-on-connect)).

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-2012-sp3httpdownloadmicrosoftcomdownloadf67f673709c-d371-4a64-8bf9-c1dd73f60990enux86sqlmanagementstudiox86enuexe"></a>[SQL Server Management Studio 2012 SP3](http://download.microsoft.com/download/F/6/7/F673709C-D371-4A64-8BF9-C1DD73F60990/ENU/x86/SQLManagementStudio_x86_ENU.exe) ![다운로드](../ssdt/media/download.png)  
  
2015년 11월 21일 | 버전 번호: 11.0.6020.0

**기능**  
SSMS Express Edition의 전체 기능 코드 조각 열 저장소 인덱스 등  
[릴리스 정보에서 사용할 수 있는 자세한 내용](https://support.microsoft.com/en-us/kb/3072779)
 
**알려진 문제**  
해당 사항 없음

**수정 프로그램**
1. 가져오기 및 내보내기 마법사를 사용하여 데이터를 가져올 때 오류 메시지에 누락된 열을 표시할 수 없습니다.
2. SSMS에서 차등 백업 복원 시 "LSN 체인 중단으로 인해 복원 계획을 만들 수 없습니다." 오류

---
## <a name="additional-downloads"></a>추가 다운로드  
모든 SQL Server Management Studio 다운로드의 전체 목록은 [Microsoft 다운로드 센터](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending)를 검색하세요.  
  
최신 SQL Server Management Studio에 대해서는 [SQL Server Management Studio 다운로드&#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.  

---  
## <a name="related-resources"></a>관련 리소스
[Microsoft SQL Server용 업데이트 센터](https://technet.microsoft.com/sqlserver/ff803383.aspx)   
[SQL Server Management Studio 빠른 시작](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[SQL Server Management Studio 포럼](https://social.msdn.microsoft.com/forums/en-us/home?forum=sqltools)  

  

