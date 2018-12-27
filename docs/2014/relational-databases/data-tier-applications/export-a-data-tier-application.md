---
title: 데이터 계층 애플리케이션 내보내기 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.exportdac.settings.f1
- sql12.swb. exportdac.settings.f1
- sql12.swb.exportdac.welcome.f1
- sql12.swb. exportdac.summary.f1
- sql12.swb.exportdac.progress.f1
- sql12.swb.exportdac.summary.f1
- sql12.swb.exportdac.results.f1
- sql12.swb. exportdac.results.f1
helpviewer_keywords:
- How to [DAC], export
- wizard [DAC], export
- export DAC
- data-tier application [SQL Server], export
ms.assetid: 61915bc5-0f5f-45ac-8cfe-3452bc185558
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ae726d90d71259715f9eb80619e74c7bfbf990dd
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43810889"
---
# <a name="export-a-data-tier-application"></a>데이터 계층 애플리케이션 내보내기
  DAC(데이터 계층 애플리케이션) 또는 데이터베이스를 내보내면 데이터베이스의 개체 정의와 테이블에 포함된 모든 데이터를 포함하는 내보내기 파일이 만들어집니다. 이 내보내기 파일을 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 다른 인스턴스 또는 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]로 가져올 수 있습니다. 내보내기-가져오기 작업을 결합하여 인스턴스 간에 DAC를 마이그레이션하거나 논리 백업을 만들거나 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 배포된 데이터베이스의 온-프레미스 복사본을 만들 수 있습니다.  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 내보내기 프로세스에서는 DAC 내보내기 파일을 두 단계로 작성합니다.  
  
1.  내보내기를 수행하면 DAC 추출 시 DAC 패키지 파일에 DAC 정의가 작성되듯이 내보내기 파일(BACPAC 파일)에 DAC 정의가 작성됩니다. 내보낸 DAC 정의에는 현재 데이터베이스의 모든 개체가 포함됩니다. DAC에서 원래 배포된 데이터베이스에 대해 내보내기 프로세스를 실행할 때 배포 후에 데이터베이스를 직접 변경한 경우 내보낸 정의는 원본 DAC에 정의된 개체 집합이 아니라 데이터베이스의 개체 집합과 일치합니다.  
  
2.  보내기에서는 데이터베이스의 모든 테이블에서 데이터를 대량 복사한 다음 내보내기 파일에 통합합니다.  
  
 내보내기 프로세스에서는 DAC 버전을 1.0.0.0으로 설정하고 내보내기 파일의 DAC 설명을 빈 문자열로 설정합니다. 데이터베이스가 DAC에서 배포된 경우에는 내보내기 파일의 DAC 정의에 원본 DAC에 지정된 것과 동일한 이름이 포함되고, 그렇지 않은 경우에는 DAC 이름이 데이터베이스 이름으로 설정됩니다.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 랩에는 DAC 및 데이터베이스 가져오기와 내보내기를 테스트하는 데 사용할 수 있는 샘플 응용 프로그램이 있습니다. 샘플을 다운로드하여 사용하는 방법은 [Windows Azure SQL 데이터베이스에 대한 데이터베이스 가져오기 및 내보내기](http://go.microsoft.com/fwlink/?LinkId=219404)를 참조하세요.  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]또는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4(서비스 팩 4) 이상의 데이터베이스에서만 DAC 또는 데이터베이스를 내보낼 수 있습니다.  
  
 DAC 또는 포함된 사용자가 지원하지 않는 개체가 있는 데이터베이스를 내보낼 수 없습니다. DAC에서 지원되는 개체 유형에 대한 자세한 내용은 [DAC Support For SQL Server Objects and Versions](dac-support-for-sql-server-objects-and-versions.md)을 참조하세요.  
  
###  <a name="Permissions"></a> Permissions  
 DAC를 내보내려면 **sys.sql_expression_dependencies**에 대한 SELECT 권한뿐만 아니라 최소한 ALTER ANY LOGIN 및 데이터베이스 범위 VIEW DEFINITION 권한이 있어야 합니다. DAC를 내보내려면 securityadmin 고정 서버 역할의 멤버이면서 DAC를 내보내는 데이터베이스의 database_owner 고정 데이터베이스 역할의 멤버여야 합니다. sysadmin 고정 서버 역할의 멤버 또는 기본 제공 SQL Server 시스템 관리자 계정인 **sa** 는 DAC를 내보낼 수 있습니다.  
  
##  <a name="UsingDeployDACWizard"></a> 데이터 계층 응용 프로그램 내보내기 마법사 사용  
 **마법사를 사용하여 DAC를 내보내려면**  
  
1.  온-프레미스 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]인스턴스에 연결합니다.  
  
2.  **개체 탐색기**에서 DAC를 내보내려는 인스턴스에 대한 노드를 확장합니다.  
  
3.  데이터베이스 이름을 마우스 오른쪽 단추로 클릭합니다.  
  
4.   **태스크** 를 클릭한 후 **데이터 계층 응용 프로그램 내보내기...** 를 선택합니다.  
  
5.  마법사 대화 상자를 완료합니다.  
  
    -   [소개 페이지](#Introduction)  
  
    -   [내보내기 설정 페이지](#Export_settings)  
  
    -   [유효성 검사 페이지](#Validation)  
  
    -   [요약 페이지](#Summary)  
  
    -   [진행률 페이지](#Progress)  
  
    -   [결과 페이지](#Results)  
  
##  <a name="Introduction"></a> 소개 페이지  
 이 페이지에서는 데이터 계층 애플리케이션 내보내기 마법사의 단계에 대해 설명합니다.  
  
 **옵션**  
  
 **이 페이지를 다시 표시 안 함** - 앞으로 소개 페이지가 표시되지 않도록 하려면 이 확인란을 클릭합니다.  
  
 **다음** - **DAC 패키지 선택** 페이지로 진행합니다.  
  
 **취소** - 작업을 취소하고 마법사를 닫습니다.  
  
##  <a name="Export_settings"></a> 내보내기 설정 페이지  
 이 페이지에서는 BACPAC 파일을 만들려는 위치를 지정할 수 있습니다.  
  
-   **로컬 디스크에 저장** - 로컬 컴퓨터의 디렉터리에 BACPAC 파일을 만듭니다.  **찾아보기…** 를 클릭합니다. 를 클릭하고 로컬 컴퓨터로 이동하거나 제공된 공간에 경로를 지정합니다. 경로 이름에 파일 이름과 .bacpac 확장명을 모두 포함해야 합니다.  
  
-   **Microsoft Azure에 저장** - - Microsoft Azure 컨테이너에 BACPAC 파일을 만듭니다. 이 옵션의 유효성을 검사하려면 Windows Azure 컨테이너에 연결해야 합니다. 또한 이 옵션을 사용하려면 임시 파일을 보관할 로컬 디렉터리를 지정해야 합니다. 지정된 위치에 임시 파일이 만들어지고 작업이 완료된 후에도 해당 위치에 유지됩니다.  
  
 내보낼 테이블 하위 집합을 지정하려면 **고급** 옵션을 사용합니다.  
  
##  <a name="Validation"></a> 유효성 검사 페이지  
 유효성 검사 페이지에서 작업을 차단한 문제를 검토할 수 있습니다. 계속하려면 차단 문제를 해결하고 **유효성 검사 다시 실행** 을 클릭하여 유효성 검사에 성공했는지 확인합니다.  
  
 계속하려면 **다음**을 클릭합니다.  
  
##  <a name="Summary"></a> 요약 페이지  
 이 페이지에서 작업에 대해 지정한 원본 및 대상 설정을 검토할 수 있습니다. 지정한 설정을 사용하여 내보내기 작업을 완료하려면 **마침**을 클릭합니다. 내보내기 작업을 취소하고 마법사를 종료하려면 **취소**를 클릭합니다.  
  
##  <a name="Progress"></a> 진행률 페이지  
 이 페이지에는 작업 상태를 나타내는 진행률 표시줄이 표시됩니다. 자세한 상태를 보려면 **자세히 보기** 옵션을 클릭합니다.  
  
##  <a name="Results"></a> 결과 페이지  
 이 페이지에서는 내보내기 작업의 성공 또는 실패를 보고하고 각 작업의 결과를 보여 줍니다. 오류가 발생한 동작에는 모두 **결과** 열에 링크가 있습니다. 링크를 클릭하면 해당 동작의 오류에 대한 보고서가 표시됩니다.  
  
 **마침** 을 클릭하여 마법사를 닫습니다.  
  
##  <a name="NetApp"></a> .Net Framework 응용 프로그램 사용  
 **.Net Framework 응용 프로그램에서 Export() 메서드를 사용하여 DAC를 내보냅니다.**  
  
 코드 예제를 보려면 [Codeplex](http://go.microsoft.com/fwlink/?LinkId=219575)에서 DAC 샘플 애플리케이션을 다운로드합니다.  
  
1.  SMO Server 개체를 만든 다음 내보낼 DAC를 포함하는 인스턴스로 설정합니다.  
  
2.  열기는 `ServerConnection` 개체와 동일한 인스턴스에 연결 합니다.  
  
3.  `Export` 형식의 `Microsoft.SqlServer.Management.Dac.DacStore` 메서드를 사용하여 DAC를 내보냅니다. 내보낼 DAC의 이름과 내보내기 파일을 배치할 폴더의 경로를 지정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 계층 응용 프로그램](data-tier-applications.md)   
 [데이터베이스에서 DAC 추출](extract-a-dac-from-a-database.md)  
  
  
