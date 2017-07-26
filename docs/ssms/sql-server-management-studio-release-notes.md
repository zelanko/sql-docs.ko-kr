---
title: "SQL Server Management Studio - 릴리스 정보 | Microsoft Docs"
ms.custom: 
ms.date: 06/22/2017
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
ms.sourcegitcommit: fe6de2b16b9792a5399b1c014af72a2a5ee52377
ms.openlocfilehash: f593303a681e2f52161777fc48f0fb1b479d20d9
ms.contentlocale: ko-kr
ms.lasthandoff: 06/23/2017

---
# <a name="sql-server-management-studio----release-notes"></a>SQL Server Management Studio - 릴리스 정보
SQL Server Management Studio의 일반 공급 릴리스를 시작합니다.  이번 릴리스의 SSMS(SQL Server Management Studio)는 SQL Server 릴리스 외의 독립 실행형 설치입니다. Microsoft는 이 SSMS 릴리스를 새 기능과 픽스뿐만 아니라 SQL Server 및 Azure SQL 데이터베이스의 최신 기능에 대한 지원으로 자주 업데이트하고자 합니다.  
  
최신 SQL Server Management Studio를 설치하려면 [SQL Server Management Studio 다운로드&#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.  
  
다음은 이번 SQL Server Management Studio 릴리스의 문제점과 제한 사항입니다.  

1. **대상 데이터베이스 파일 위치에 대 한 잘못 된 경로 패턴에서는 발생 하는 복원 데이터베이스 마법사** 
    SSMS Linux 서버에 연결 되어 있을 때 알려진된 문제입니다. 경로 잘못 된/홀수 보이지만, 서버 쪽에서 올바르게 처리, 즉,는 기능적 문제가 없습니다.

2. **파일 브라우저 문제**
    - Windows 기반 SQL Server 2017 CTP 2.0 인스턴스를 사용할 때는 ssms에서 UI 파일 브라우저는 서버에는 빈 플로피 드라이브 또는 고정된 디스크를 설치 하는 Bitlocker로 보호 되는 경우이를 열려면 실패할 수 있습니다. 
    - 파일 탐색기 UI는 더 이상 SQL Server 2017 CTP 2.0 이전 버전의 버전을 지원합니다.
    


3. **단일 Azure Active Directory 계정만 Active Directory 유니버설 인증을 사용하여 SSMS 인스턴스에 대해 로그인할 수 있습니다.**  
    이 제한은 Active Directory 유니버설 인증으로 제한됩니다. Active Directory 암호 인증, Active Directory 통합 인증 또는 SQL Server 인증으로는 다른 서버에 로그인할 수 있습니다.
    
    해결 방법으로, 다른 SSMS 인스턴스를 사용하여 다른 Azure Active Directory 계정으로 로그인할 수 있습니다. 
    
4. **데이터 계층 응용 프로그램 프레임워크(DacFx) 명령 및 SSMS의 스키마 디자이너는 Active Directory 유니버설 인증을 지원하지 않습니다.**  
    DacFx를 사용하는 명령(예: 가져오기 및 내보내기), SSMS의 스키마 디자이너는 현재 Active Directory 유니버설 인증을 지원하지 않습니다.
    
    해결 방법으로, SSMS에 제공되는 다른 형식의 인증인 Active Directory 암호 인증, Active Directory 통합 인증 또는 SQL Server 인증을 사용할 수 있습니다.

5. **SSMS는 SSIS 2016(SQL Server 2016 Integrated Services) 인스턴스에만 연결할 수 있습니다.**  
    SQL Server Integration Services의 알려진 호환성 제한 때문에 이전 버전에는 연결할 수 없습니다.
    
    이 문제에 대한 해결 방법으로, [SSIS 인스턴스에 맞게 조정된 SSMS 릴리스](../ssms/previous-sql-server-management-studio-releases.md)를 사용하여 SQL Server Integration Service 인스턴스에 연결할 수 있습니다. 
  
5. **SSMS는 SQL Server 2008 R2 및 이전 버전의 SQL Server 버전에 대한 유지 관리 계획을 저장하지 않습니다.**  
    이 문제는 향후 해결될 것으로 예상되는 알려진 제한 사항입니다. 현재는 [SSMS 2014 릴리스](../ssms/previous-sql-server-management-studio-releases.md) 를 사용하여 유지 관리 계획을 저장할 수 있습니다.  
    
5. **영어 이외의 SSMS 설치에는 추가 보안 패키지를 설치해야 합니다.**  
영어 이외의 지역화된 SSMS 릴리스는 Windows 8, Windows 7, Windows Server 2012 및 Windows Server 2008 R2에 설치하는 경우 [KB 2862966 보안 업데이트 패키지가 필요](https://support.microsoft.com/en-us/kb/2862966) 합니다.

5. **도움말을 클릭하거나 F1 키를 눌러도 도움말이 열리지 않음**  
일부 환경에서는 도움말을 클릭하거나 F1 키를 누르면 **이 ms xhelp을(를) 열려면 새 앱이 필요합니다.**라는 메시지가 나타납니다. 이 오류는 알려진 문제이며 향후 릴리스에서 수정될 예정입니다.
  
## <a name="feedback"></a>피드백  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 클라이언트 도구 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Microsoft Connect에 문제 또는 제안을 기록하세요](https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>참고 항목  
[SQL Server Management Studio 자습서](../ssms/use-sql-server-management-studio.md)  
[SQL Server Management Studio 다운로드 &amp;#40;SSMS&amp;#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[SQL Server Management Studio의 이전 릴리스](../ssms/previous-sql-server-management-studio-releases.md)  

  

