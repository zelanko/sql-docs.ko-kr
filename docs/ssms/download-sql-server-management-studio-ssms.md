---
title: "SSMS(SQL Server Management Studio) 다운로드 | Microsoft 문서"
ms.custom: 
ms.date: 04/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "ssms 설치, ssms 다운로드, 최신 ssms"
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- sql management studio install
- download sql management studio
- ms sql management studio
- install sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
caps.latest.revision: 145
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cc827737cec19c11d2102f968dc2b8bc638bda86
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio) 다운로드
SSMS(SQL Server Management Studio)는 SQL Server의 모든 구성 요소를 액세스, 구성, 관리 및 개발할 수 있는 통합 환경입니다. SSMS는 수많은 풍부한 스크립트 편집기와 광범위한 그래픽 도구 그룹을 결합하여 기술 수준에 상관없이 모든 개발자와 관리자가 SQL Server에 액세스할 수 있도록 해줍니다. 이 릴리스는 이전 버전의 SQL Server와의 향상된 호환성, 독립 실행형 웹 설치 관리자 및 새 릴리스를 사용할 수 있는 경우 SSMS 내 알림 메시지 기능을 제공합니다.  

    
| ![다운로드로 사용 가능한 제품 설명서에서 데이터 공급자 설치 섹션을 참조하세요](../ssdt/media/download.png) SSMS(SQL Server Management Studio) 다운로드  |  |
|:---|:---|
|**[SQL Server Management Studio(16.5.3) 다운로드](https://go.microsoft.com/fwlink/?LinkID=840946)**|프로덕션용 최신 릴리스입니다.|
|**[SQL Server Management Studio - 릴리스 후보(17.0 RC3) 다운로드](../ssms/sql-server-management-studio-ssms-release-candidate.md)**|SQL Server vNext CTP1.3을 지원하고 16.x와 병렬로 작동하지만 프로덕션 사용에는 권장되지 않습니다.| 


> [!NOTE]
> 이제 SSMS 릴리스는 월이 아닌 번호로 브랜딩됩니다. SSMS는 무료입니다. 설치 및 사용하는 데 라이선스가 필요하지 않습니다.  


## <a name="sql-server-management-studio"></a>SQL Server Management Studio   
**버전 정보**  
  
릴리스 번호: 16.5.3  
이 릴리스에 대한 빌드 번호: 13.0.16106.4
  
**지원되는 SQL Server 버전**  
  
* 이 버전의 SSMS는 [지원되는 모든 SQL Server 버전(SQL Server 2008 - SQL Server 2016)](https://support.microsoft.com/en-us/lifecycle?C2=1044) 과 작동되며 Azure SQL Database와 Azure SQL Data Warehouse의 최신 클라우드 기능 사용에 대해 최고 수준의 지원을 제공합니다.  
* SQL Server 2000 또는 SQL Server 2005에 대한 명시적 블록은 없지만 일부 기능이 제대로 작동하지 않을 수 있습니다.  
* 또한, 하나의 SSMS 16.x 릴리스 또는 SSMS 2016은 SSMS 2014의 이전 버전과 함께 설치할 수 있습니다. 
  
**지원되는 운영 체제**  
  
이 SSMS 릴리스는 사용 가능한 최신 서비스 팩과 함께 사용할 경우 다음과 같은 플랫폼을 지원합니다.   
 Windows 10, Windows 8, Windows 8.1, Windows 7(SP1), Windows Server 2012(64비트), Windows Server 2012 R2(64비트), Windows Server 2008 R2(64비트)  
   
 **사용 가능한 언어**  
> [!NOTE]  
> 영어 이외의 지역화된 SSMS 릴리스는 Windows 8, Windows 7, Windows Server 2012 및 Windows Server 2008 R2에 설치하는 경우 [KB 2862966 보안 업데이트 패키지](https://support.microsoft.com/en-us/kb/2862966) 가 필요합니다. 
  
 이 SSMS 릴리스는 다음 언어로 설치할 수 있습니다.  
[중국어(중국)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804) | [중국어(대만)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404) | [영어(미국)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409) | [프랑스어](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c)  
[독일어](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407) | [이탈리아어](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410) | [일본어](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411) | [한국어](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412) | [포르투갈어(브라질)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416) | [러시아어](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419) | [스페인어](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)  

 
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





전체 기능 목록은 다음을 참조하세요.   
                [SQL Server Management Studio - 변경 로그(SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)  
  
알려진 문제 및 해결 방법 목록은 다음을 참조하세요.   
                [SQL Server Management Studio - 릴리스 정보](../ssms/sql-server-management-studio-release-notes.md)  
  
사용자 데이터 컬렉션에 대한 정보는   
                [SQL Server 개인 정보 취급 방침](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx)을 참조하세요.  
  
## <a name="previous-releases"></a>이전 릴리스  
[이전 SQL Server Management Studio 릴리스](../ssms/previous-sql-server-management-studio-releases.md)  
  
## <a name="feedback"></a>피드백  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 클라이언트 도구 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Microsoft Connect에 문제 또는 제안을 기록하세요](https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>관련 항목:  
[자습서: SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[SQL Server Management Studio 설명서](https://msdn.microsoft.com/library/hh213248(v=sql.130).aspx)  
[Microsoft SQL Server](https://msdn.microsoft.com/library/bb545450.aspx)  
[추가 업데이트 및 서비스 팩](https://technet.microsoft.com/sqlserver/ff803383.aspx)  
[SSDT(SQL Server Data Tools) 다운로드](../ssdt/download-sql-server-data-tools-ssdt.md)  



