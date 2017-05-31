---
title: "SQL Server Management Studio - 릴리스 정보 | Microsoft 문서"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b95337b-80bf-4624-8f5d-cdaf6181d3b8
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 51e336a22d0c1052c48b8e569330aef26f2af094
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-management-studio----release-notes"></a>SQL Server Management Studio - 릴리스 정보
SQL Server Management Studio의 일반 공급 릴리스를 시작합니다.  이번 릴리스의 SSMS(SQL Server Management Studio)는 SQL Server 릴리스 외의 독립 실행형 설치입니다. Microsoft는 이 SSMS 릴리스를 새 기능과 픽스뿐만 아니라 SQL Server 및 Azure SQL 데이터베이스의 최신 기능에 대한 지원으로 자주 업데이트하고자 합니다.  
  
최신 SQL Server Management Studio를 설치하려면 [SQL Server Management Studio 다운로드&#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.  
  
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

## <a name="feedback"></a>피드백  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 클라이언트 도구 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Microsoft Connect에 문제 또는 제안을 기록하세요](https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>참고 항목  
[SQL Server Management Studio 자습서](../ssms/use-sql-server-management-studio.md)  
[SQL Server Management Studio 다운로드 &amp;#40;SSMS&amp;#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[SQL Server Management Studio의 이전 릴리스](../ssms/previous-sql-server-management-studio-releases.md)  

  

