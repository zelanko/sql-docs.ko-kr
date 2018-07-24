---
title: SQL Server 설치 로그 파일 보기 및 읽기 | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying log files
- Setup [SQL Server], logs
- installation log files [SQL Server]
- installing SQL Server, logs
- errors [SQL Server], Setup
- logs [SQL Server], Setup
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
caps.latest.revision: 54
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c25b54f30a9e8c0ce66c1a833aef4c5daf35e6b8
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38050241"
---
# <a name="view-and-read-sql-server-setup-log-files"></a>SQL Server 설치 로그 파일 보기 및 읽기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 설치 프로그램은 기본적으로 **\%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log** 내의 일자 및 시간 스탬프가 포함된 폴더에서 로그 파일을 만듭니다. 여기서 *nnn*은 설치되는 SQL 버전에 해당하는 숫자입니다. 타임스탬프 로그 폴더 이름 형식은 YYYYMMDD_hhmmss입니다. 설치 프로그램을 무인 모드로 실행하면 % temp%\sqlsetup*.log 내에 로그가 생성됩니다. 로그 폴더의 모든 파일은 각각의 로그 폴더에 Log\*.cab 파일로 보관됩니다.  

   | 파일           | 경로 |
   | :------        | :----------------------------- |
   | **Summary.txt**    | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log |
   | **Summary_\<MachineName>\_Date.txt**  | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Detail.txt** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss|
   | **Datastore** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\Datastore
   | **MSI 로그 파일** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\\\<Name>.log|
   | **ConfigurationFile.ini** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **SystemConfigurationCheck_Report.htm** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **무인 설치용** | %temp%\sqlsetup*.log |


 ![setup-bootstrap-example.png](media/view-and-read-sql-server-setup-log-files/setup-bootstrap-example.png)

 >[!NOTE]
 > *nnn* 경로에 있는 숫자는 설치 중인 SQL 버전에 해당합니다. 위의 그림에서는 SQL 2017이 설치되었으므로 폴더가 140입니다. SQL 2016의 폴더는 130이고, SQL 2014의 폴더는 120입니다.
  
 SQL Server 설치 프로그램은 3가지 기본 단계를 완료합니다. 
  
1.  전역 규칙 확인: 기본 시스템 요구 사항 확인
2.  구성 요소 업데이트: 설치 중인 미디어에 사용 가능한 업데이트가 있는지 확인
3.  사용자 요청 동작: 사용자가 기능을 선택하고 사용자 지정하도록 허용
  

이 워크플로는 단일 요약 로그 및 기본 SQL Server 설치용 단일 정보 로그 또는 서비스 팩 같은 업데이트를 기본 설치와 함께 설치할 경우 두 개의 세부 정보 로그 중 하나를 생성합니다. 
  
또한 설치 프로세스에서 추적하는 모든 구성 개체 상태의 스냅숏이 포함되며 구성 오류 문제를 해결하는 데 유용한 데이터 저장소 파일이 있습니다. 각 실행 단계에서 XML 덤프 파일이 생성되어 타임스탬프가 있는 로그 폴더 아래 데이터 저장소 로그 하위 폴더에 저장됩니다. 

다음 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 로그 파일에 대해 설명합니다.  
  
## <a name="summarytxt-file"></a>Summary.txt 파일 
  
### <a name="overview"></a>개요  
 이 파일은 설치 중에 검색된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소, 운영 체제 환경, 명령줄 매개 변수 값(지정된 경우) 및 각 MSI/MSP의 전반적인 실행 상태를 보여 줍니다.
  
 로그는 다음 섹션으로 구성됩니다.
  
-   전반적인 실행 요약  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 실행된 컴퓨터의 속성 및 구성  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 기능  
-   설치 버전 및 설치 패키지 속성에 대한 설명
-   설치 중에 제공된 런타임 입력 설정  
-   구성 파일의 위치  
-   실행 결과의 세부 사항  
-   전역 규칙  
-   설치 시나리오 관련 규칙  
-   실패한 규칙  
-   규칙 보고서 파일의 위치


  >[!NOTE]
  > 패치 적용 시 유사한 파일 집합이 포함된 하위 폴더(패치 중인 각 인스턴스와 공유 기능당 하나씩)가 여러 개 있을 수 있습니다(예: %programfiles%\MicrosoftSQL Server\130\Setup Bootstrap\Log\<YYYYMMDD_HHMM>\MSSQLSERVER). 
  
### <a name="location"></a>위치  
 summary.txt는 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\ 내에 있습니다.
  
 요약 텍스트 파일에서 오류를 찾으려면 "오류" 또는 "실패" 키워드를 사용하여 파일을 검색하십시오.
  
## <a name="summarymachinenameyyyymmddhhmmsstxt-file"></a>Summary_\<MachineName>_YYYYMMDD_HHMMss.txt 파일
  
### <a name="overview"></a>개요  
 summary_engine base 파일은 요약 파일과 비슷하며 주 워크플로 중에 생성됩니다.
  
### <a name="location"></a>위치  
 Summary_\<MachineName>_YYYYMMDD_HHMMss.txt 파일은 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\에 있습니다.
  
  
## <a name="detailtxt-file"></a>Detail.txt 파일
  
### <a name="overview"></a>개요
 Detail.txt는 설치 또는 업그레이드와 같은 주 워크플로 중에 생성되며 실행 세부 사항을 제공합니다. 이 파일의 로그는 각 설치 동작이 호출된 경우 시간을 기준으로 생성됩니다. 이 텍스트 파일은 동작이 실행된 순서와 종속성을 보여 줍니다.  
  
### <a name="location"></a>위치  
 Detail.txt 파일은 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt 내에 있습니다.  
  
 설치 프로세스 중에 오류가 발생하면 이 파일 끝에 예외나 오류가 로깅됩니다. 이 파일에서 오류를 찾으려면 먼저 파일 끝을 검사한 다음, "오류" 또는 "예외" 키워드로 파일을 검색하세요.
    
## <a name="msi-log-files"></a>MSI 로그 파일
  
### <a name="overview"></a>개요  
 MSI 로그 파일은 설치 패키지 프로세스의 세부 사항을 제공하며, 지정된 패키지를 설치하는 동안 MSIEXEC에 의해 생성됩니다.  
  
 MSI 로그 파일의 유형:
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### <a name="location"></a>위치  
 MSI 로그 파일은 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<Name\>.log에 있습니다.  
  
 파일 끝에 성공/실패 상태 및 속성을 포함하는 실행 요약이 표시됩니다. MSI 파일에서 오류를 찾으려면 "값 3"을 검색하고 이전 및 이후 텍스트를 검토합니다.  
  
## <a name="configurationfileini-file"></a>ConfigurationFile.ini 파일
  
### <a name="overview"></a>개요  
 구성 파일은 설치 중에 제공된 입력 설정을 포함합니다. 이 파일을 사용하면 수동으로 설정을 입력하지 않고도 설치를 다시 시작할 수 있습니다. 그러나 계정의 암호, PID 및 일부 매개 변수는 구성 파일에 저장되지 않습니다. 이러한 설정은 파일에 추가하거나 명령줄 또는 설치 사용자 인터페이스를 사용하여 제공할 수 있습니다. 자세한 내용은 [구성 파일을 사용하여 SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)를 참조하세요.  
  
### <a name="location"></a>위치  
 ConfigurationFile.ini는 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\에 있습니다.  
  
## <a name="systemconfigurationcheckreporthtm-file"></a>SystemConfigurationCheck_Report.htm 파일
  
### <a name="overview"></a>개요  
 시스템 구성 검사 보고서는 각 실행 규칙에 대한 간단한 설명과 실행 상태를 포함합니다.
  
### <a name="location"></a>위치  
SystemConfigurationCheck_Report.htm은 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\에 있습니다.

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 2017 설치](../../database-engine/install-windows/install-sql-server.md)
