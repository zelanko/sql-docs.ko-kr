---
title: "SQL Server R Services 무인 설치 | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 14
---
# SQL Server R Services 무인 설치
    
설치 프로세스를 시작 하기 전에 이러한 요구 사항을 note:

+ 에 있는 R 서비스 (데이터베이스)를 사용할 각 인스턴스를 데이터베이스 엔진을 설치 해야 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]합니다.  
+ 오프 라인 설치를 수행 하는 경우에 필요한 R 구성 요소를 사전에 다운로드 하 고 로컬 폴더를 복사 해야 합니다. 다운로드 위치에 대 한 참조 [인터넷에 액세스할 수 없는 R 구성 요소 설치](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)합니다.   
+ 새 매개 변수는 */IACCEPTROPENLICENSETERMS*, 을 나타내는, 오픈 소스 R 구성 요소를 사용 하기 위한 사용 조건에 동의 했습니다. 명령줄에서이 매개 변수를 포함 되지 않은 경우 설치에 실패 합니다.  
  
## R Services(In-Database) 무인 설치 수행  
 다음 예에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
###  <a name="bkmk_Unattended"></a>  
  
1.  관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.  
  
    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,AdvancedAnalytics /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS  
    ```  
  
2.  설치가 완료된 후 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 다음 명령을 실행하여 기능을 사용하도록 설정합니다.  
  
    ```  
    Exec sp_configure  'external scripts enabled', 1  
    Reconfigure  with  override  
  
    ```  
  
    > [!NOTE]  
    >  엔진 기능은 명시적으로 사용하도록 설정해야 합니다. 그렇지 않으면 설치 프로그램을 통해 기능을 설치하고 구성했더라도 R 스크립트를 호출할 수 없습니다.  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작합니다. 그러면 관련 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스도 자동으로 다시 시작됩니다.  
  
## 관련 항목:  
 [R 서비스 설정 문제 해결](../Topic/Troubleshooting%20R%20Services%20Setup.md)  
  
  