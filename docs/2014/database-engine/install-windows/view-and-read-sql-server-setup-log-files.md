---
title: SQL Server 설치 로그 파일 보기 및 읽기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d6a81258e87bf2422f3ae5a55afc5eb6429856b2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62774325"
---
# <a name="view-and-read-sql-server-setup-log-files"></a>SQL Server 설치 로그 파일 보기 및 읽기
  설치 프로그램의 각 실행\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은% programfiles% \120\Setup Bootstrap\Log\\에 새 타임 스탬프 로그 폴더를 사용 하 여 만들어집니다. 타임스탬프 로그 폴더 이름 형식은 YYYYMMDD_hhmmss입니다. 설치 프로그램을 무인 모드로 실행하면 % temp%\sqlsetup*.log에 로그가 생성됩니다. 로그 폴더의 모든 파일은 각각의 로그 폴더에 Log\*.cab 파일로 보관됩니다.  
  
 일반적인 설치 요청은 다음과 같은 세 가지 실행 단계를 거칩니다.  
  
1.  전역 규칙 텍스트  
  
2.  구성 요소 업데이트  
  
3.  사용자 요청 동작  
  
 각 단계에서 설치 프로그램이 자세한 로그 및 요약 로그를 생성하며 필요한 경우 추가 로그가 생성됩니다. 설치 프로그램은 사용자가 요청한 설치 동작마다 세 번 이상 호출됩니다.  
  
 데이터 저장소 파일에는 설치 프로세스에서 추적하는 모든 구성 개체 상태의 스냅샷이 포함되어 있으며 이는 구성 오류 문제를 해결하는 데 유용합니다. 각 실행 단계에서는 데이터 저장소 개체에 대한 XML 파일 덤프가 생성됩니다. 이러한 덤프는 타임스탬프 로그 폴더의 다음과 같은 자체 로그 하위 폴더에 저장됩니다.  
  
-   Datastore_GlobalRules  
  
-   Datastore_ComponentUpdated  
  
-   데이터 저장소  
  
 다음 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 로그 파일에 대해 설명합니다.  
  
## <a name="summary-text"></a>요약 텍스트  
  
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
  
### <a name="location"></a>위치  
 %\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Programfiles% \120\Setup Bootstrap\Log\\에 있습니다.  
  
 요약 텍스트 파일에서 오류를 찾으려면 "오류" 또는 "실패" 키워드를 사용하여 파일을 검색하십시오.  
  
## <a name="summary_engine-base_yyyymmdd_hhmmsstxt"></a>Summary_engine-base_YYYYMMDD_HHMMss.txt  
  
### <a name="overview"></a>개요  
 summary_engine base 파일은 요약 파일과 비슷하며 주 워크플로 중에 생성됩니다.  
  
### <a name="location"></a>위치  
 % Programfiles\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% \120\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\에 있습니다.  
  
## <a name="summary_engine-base_yyyymmdd_hhmmss_componentupdatetxt"></a>Summary_engine-base_YYYYMMDD_HHMMss_ComponentUpdate.txt  
  
### <a name="overview"></a>개요  
 구성 요소 업데이트 요약 로그 파일은 요약 파일과 비슷하며 구성 요소 업데이트 워크플로 중에 생성됩니다.  
  
### <a name="location"></a>위치  
 % Programfiles\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% \120\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\에 있습니다.  
  
## <a name="summary_engine-base_versionnumbermmdd_hhmmss_globalrulestxt"></a>Summary_engine-base_\<VersionNumber>MMDD_HHMMss_GlobalRules.txt  
  
### <a name="overview"></a>개요  
 전역 규칙 요약 로그 파일은 요약 파일과 비슷하며 전역 규칙 워크플로 중에 생성됩니다.  
  
### <a name="location"></a>위치  
 % Programfiles\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% \120\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\에 있습니다.  
  
## <a name="detailtxt"></a>Detail.txt  
  
### <a name="overview"></a>개요  
 Detail.txt는 설치 또는 업그레이드와 같은 주 워크플로 중에 생성되며 실행 세부 사항을 제공합니다. 파일의 로그는 각 설치 동작이 호출된 시간을 기준으로 생성되며 동작이 실행된 순서와 종속성을 보여 줍니다.  
  
### <a name="location"></a>위치  
 % Programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup에 있습니다.  
  
 Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt  
  
 설치 프로세스 중에 오류가 발생하면 이 파일 끝에 예외나 오류가 로깅됩니다. 이 파일에서 오류를 찾으려면 먼저 파일 끝을 검사한 다음 "오류" 또는 "예외" 키워드로 파일을 검색하십시오.  
  
## <a name="detail_componentupdatetxt"></a>Detail_ComponentUpdate.txt  
  
### <a name="overview"></a>개요  
 Detail_ComponentUpdate.txt 파일은 구성 요소 업데이트 워크플로 중에 생성되며 Detail.txt와 비슷합니다.  
  
### <a name="location"></a>위치  
 % Programfiles\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% \120\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\에 있습니다.  
  
## <a name="detail_globalrulestxt"></a>Detail_GlobalRules.txt  
  
### <a name="overview"></a>개요  
 Detail_GlobalRules.txt 파일은 전역 규칙 실행 중 생성되며 Detail.txt와 비슷합니다.  
  
### <a name="location"></a>위치  
 % Programfiles\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% \120\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\에 있습니다.  
  
## <a name="msi-log-files"></a>MSI 로그 파일  
  
### <a name="overview"></a>개요  
 MSI 로그 파일은 설치 패키지 프로세스의 세부 사항을 제공하며, 지정된 패키지를 설치하는 동안 MSIEXEC에 의해 생성됩니다.  
  
 MSI 로그 파일의 유형:  
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log  
  
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log  
  
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### <a name="location"></a>위치  
 MSI 로그 파일 은% programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<이름\>.log에 있습니다.  
  
 파일 끝에 성공/실패 상태 및 속성을 포함하는 실행 요약이 표시됩니다. MSI 파일에서 오류를 찾으려면 "값 3"을 검색하십시오. 그러면 대개 이 문자열 부근에서 오류를 찾을 수 있습니다.  
  
## <a name="configurationfileini"></a>ConfigurationFile.ini  
  
### <a name="overview"></a>개요  
 구성 파일은 설치 중에 제공된 입력 설정을 포함합니다. 이 파일을 사용하면 수동으로 설정을 입력하지 않고도 설치를 다시 시작할 수 있습니다. 그러나 계정의 암호, PID 및 일부 매개 변수는 구성 파일에 저장되지 않습니다. 이러한 설정은 파일에 추가하거나 명령줄 또는 설치 사용자 인터페이스를 사용하여 제공할 수 있습니다. 자세한 내용은 [구성 파일을 사용 하 여 SQL Server 2014 설치](install-sql-server-using-a-configuration-file.md)를 참조 하세요.  
  
### <a name="location"></a>위치  
 % Programfiles\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% \120\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\에 있습니다.  
  
## <a name="systemconfigurationcheck_reporthtm"></a>SystemConfigurationCheck_Report.htm  
  
### <a name="overview"></a>개요  
 시스템 구성 검사 보고서는 각 실행 규칙에 대한 간단한 설명과 실행 상태를 포함합니다.  
  
### <a name="location"></a>위치  
 % Programfiles\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% \120\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\에 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [설치 방법 도움말 항목](../../sql-server/install/installation-how-to-topics.md)   
 [SQL Server 2014 설치](install-sql-server.md)  
  
  
