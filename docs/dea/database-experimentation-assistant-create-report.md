---
title: 데이터베이스 실험 도우미에서 SQL Server 업그레이드에 대 한 분석 보고서를 만들기
description: 데이터베이스 실험 도우미에서 분석 보고서 만들기
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 901d410fc7aa954dcd39a852f240168f2a690e3c
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "56987689"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant"></a>데이터베이스 실험 도우미에서 분석 보고서 만들기

대상 서버 모두에서 원본 추적을 재생 하면 데이터베이스 실험 도우미 (비활성화)에서 분석 보고서를 생성할 수 있습니다. 분석 보고서 제안 된 변경의 성능에 미치는 영향에 대 한 통찰력을 얻는 데 도움이 됩니다.

## <a name="create-an-analysis-report"></a>분석 보고서 만들기

비활성화를에서 메뉴 아이콘을 선택 합니다. 확장 된 메뉴에서 선택 **분석 보고서** 검사 목록 아이콘 옆에 있습니다.

![분석 메뉴](./media/database-experimentation-assistant-create-report/dea-create-reports-menu.png)

아래 **분석 보고서**를 선택 **새 분석 보고서**합니다.

![새 분석 보고서 메뉴](./media/database-experimentation-assistant-create-report/dea-create-reports-new-report.png)

입력 하거나 다음 정보를 선택 합니다.

- **보고서 이름을**: 보고서의 이름을 입력 합니다. 보고서 이름이 사용 됩니다 모두 A 및 B 데이터베이스입니다. 예: *A (또는 B)* + *보고서 이름* + *고유 식별자*합니다. 
- **서버 이름**: 에 포함 하려는 서버 컴퓨터의 이름을 입력 B 및 분석 데이터베이스입니다.
- **SQL Server 인스턴스 이름을**: 보고서에 사용할 SQL Server 인스턴스의 이름을 입력 합니다.
- **원본 서버에 대 한 추적**: SQL Server (2008 R2) 첫 번째 추적 (.trc) 파일을 입력 합니다.
- **대상 서버에 대 한 추적**: 대상 SQL Server (2014) 첫 번째.trc 파일을 입력 합니다.

![새 분석 보고서 페이지](./media/database-experimentation-assistant-create-report/dea-create-reports-inputs.png)

## <a name="generate-a-report"></a>보고서를 생성 합니다.

필요한 정보를 선택 하거나 입력 하면 후 합니다 **새 분석 보고서** 페이지에서 **시작** 보고서 만들기를 시작 합니다. 입력 정보가 올바르면 분석 보고서 생성 됩니다. 그렇지 않으면 잘못 된 정보가 포함 된 입력란 빨간색 강조 표시 됩니다. 올바른 값을 입력 하 고 선택한 **시작**합니다. 

새 분석 보고서가 생성 됩니다. 분석 데이터베이스의 이름 지정 체계 분석 따릅니다 + *사용자 지정 보고서 이름을* + *고유 식별자*합니다.

## <a name="frequently-asked-questions-about-analysis-reports"></a>분석 보고서에 대 한 질문과 대답

### <a name="what-does-my-analysis-report-tell-me"></a>새로운 않습니다 분석 보고서에 대 한 설명?
    
워크 로드를 분석 하 고 각 쿼리 대상 1에서 대상 2를 실행 하는 방법을 확인 하려면 통계적 테스트를 사용 하는 비활성화 합니다. 각 쿼리에 대 한 성능 정보를 제공합니다. 비활성화에 자세히 알아보려면 [시작](database-experimentation-assistant-get-started.md)합니다.
    
### <a name="can-i-create-a-new-analysis-report-while-another-report-is-being-generated"></a>만들기 새 분석 보고서를 다른 보고서를 생성 하는 동안
    
아니요.  현재 충돌을 방지 하려면 한 번에 하나의 보고서를 생성할 수 있습니다. 그러나 둘 이상의 캡처를 실행 하 고 동시에 재생 수 있습니다.

### <a name="i-upgraded-dea-to-version-20-can-i-still-view-and-use-my-old-reports"></a>비활성화 버전 2.0으로 업그레이드 합니다. 여전히 보기 및 수 이전 내 보고서 사용?
    
예 이전에 생성 된 보고서를 보려면 보고서의 스키마를 업데이트 해야 합니다. 자세한 내용은 참조 하세요. [비활성화 2.0: 분석 보고서 비활성화에 대 한 데이터베이스 스키마 업데이트](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-updating-db-schema-for-analysis-report-in-the-database-experimentation-assistant/)합니다.
    
### <a name="can-i-generate-an-analysis-report-by-using-the-command-prompt"></a>명령 프롬프트를 사용 하 여 분석 보고서를 생성할 수 있습니까?
    
예 명령 프롬프트에서 분석 보고서를 생성할 수 있습니다. 그런 다음 UI에서 보고서를 볼 수 있습니다. 자세한 내용은 [명령 프롬프트에서 실행](database-experimentation-assistant-run-command-prompt.md)합니다.
    
## <a name="troubleshoot-analysis-reports"></a>분석 보고서 문제 해결

###  <a name="what-security-permissions-do-i-need-to-generate-and-view-an-analysis-report-on-my-server"></a>보안 권한을를 내 서버에서 분석 보고서를 보고 하나요?
    
비활성화에 로그온 된 사용자는 analysis server에서 sysadmin 권한이 있어야 합니다. 사용자 그룹의 일부 이면 그룹에 대 한 sysadmin 권한이 있는지 확인 합니다.

|가능한 오류|해결 방법|  
|---|---|  
|데이터베이스에 연결할 수 없습니다. 분석 및 보고서를 보기에 대 한 sysadmin 권한이 있는지 확인 합니다.|서버 또는 데이터베이스에 대 한 액세스 또는 sysadmin 권한이 없을 수 있습니다. 로그인 권한을 확인 하 고 다시 시도 하세요.|  
|생성할 수 없습니다 **보고서 이름** 서버의 **서버 이름**합니다. 세부 정보를 확인 합니다 **보고서 이름** 보고서입니다.|새 보고서를 생성 하는 데 필요한 sysadmin 권한이 없을 수 있습니다. 오류 세부 정보를 보려면 오류 보고서를 선택 하 고 %temp% 로그를 확인\\비활성화 합니다.|  
|현재 사용자 작업을 실행 하는 데 필요한 권한이 없습니다. 추적을 수행 하 고 보고서를 분석에 대 한 sysadmin 권한이 있는지 확인 합니다.|새 보고서를 생성 하는 데 필요한 sysadmin 권한이 없습니다.|  

### <a name="i-cant-connect-to-the-computer-running-sql-server"></a>SQL Server를 실행 하는 컴퓨터에 연결할 수 없습니다.
    
- SQL Server를 실행 하는 컴퓨터의 이름이 올바른지 확인 합니다. 를 확인 하려면 SQL Server Management Studio (SSMS)를 사용 하 여 서버에 연결 하려고 합니다.
- 방화벽 구성에 SQL Server를 실행 하는 컴퓨터에 대 한 연결을 차단 하지 확인 합니다.
- 사용자는 필요한 사용자 권한이 있는지 확인 합니다. 

% Temp %에 로그에서 자세한 정보를 볼 수 있습니다\\비활성화 합니다. 문제가 지속 되 면 제품 팀에 문의 합니다.

### <a name="i-see-an-error-when-i-generate-an-analysis-report"></a>분석 보고서를 생성 하려면 때 오류가 표시 됩니다.
    
인터넷 액세스를 비활성화를 설치한 후 분석 보고서를 생성 처음으로 필요 합니다. 통계 분석에 필요한 패키지를 다운로드 하려면 인터넷 액세스가 필요 합니다.

보고서를 만드는 동안 오류가 발생 하는 경우 진행률 페이지에는 분석을 생성 하지 못했습니다 특정 단계를 보여 줍니다. % Temp %에 로그에서 자세한 정보를 볼 수 있습니다\\비활성화 합니다. 필요한 사용자 권한으로 서버에 올바르게 연결 되어 다시 시도 확인 합니다. 문제가 지속 되 면 제품 팀에 문의 합니다.

|가능한 오류|해결 방법|  
|---|---|  
|RInterop는 시작 시 오류가 발생 합니다. RInterop 로그를 확인 하 고 다시 시도 합니다.|비활성화에 종속 된 R 패키지를 다운로드 하는 인터넷 액세스가 필요 합니다. RInterop %temp% 로그를 확인\\%temp% 로그 RInterop 및 비활성화\\비활성화 합니다. RInterop 올바르게 초기화 되었는지, 올바른 R 패키지 없이 초기화 되었으므로 비활성화 로그에서 InitializeRInterop 단계를 수행한 후 "새 분석 보고서를 생성 하지 못했습니다" 예외를 볼 수 있습니다.<br><br>RInterop 로그도 수 유사한 오류가 표시 "없습니다 jsonlite 패키지는 사용할 수 있습니다."를 컴퓨터에 인터넷 액세스가 없는 경우 필요한 jsonlite R 패키지를 수동으로 다운로드할 수 있습니다.<br><br><li>% Userprofile %로\\DEARPackages 컴퓨터의 파일 시스템 폴더입니다. 이 폴더 비활성화에 대 한 R을 사용한 패키지 구성 됩니다.</li><br><li>Jsonlite의 릴리스 버전을 다운로드 하려면 인터넷 액세스가 가능한 컴퓨터 jsonlite 폴더가 설치 된 패키지 목록에 없는 경우 해야\_에서 1.4.zip [ https://cran.r-project.org/web/packages/jsonlite/index.html ](https://cran.r-project.org/web/packages/jsonlite/index.html)합니다.</li><br><li>비활성화를 실행 중인 컴퓨터에.zip 파일을 복사 합니다.  Jsonlite 폴더를 추출 하 고 %userprofile% 복사할\\DEARPackages 합니다. 이 단계 R에서 jsonlite 패키지를 자동으로 설치 폴더 이름은 **jsonlite** 내용을 하지 한 수준 아래로 폴더 안에 직접 해야 합니다.</li><br><li>비활성화, 다시 열림, 및 시도 분석을 다시 닫습니다.</li><br>RGUI를 사용할 수도 있습니다. 로 이동 **패키지** > **zip에서 설치**합니다. 이전에 다운로드 한 패키지로 이동한 후 설치 합니다.<br><br>RInterop 초기화 되었으며 올바르게 설정 하는 경우 "설치 종속 R 패키지 jsonlite" RInterop 로그에 표시 됩니다.|  
|SQL Server 인스턴스에 연결 하 고 서버 이름이 올바른지 확인 사용자가 로그인에 대해 필요한 액세스를 확인할 수 없습니다.|액세스 권한이 없을 수 있습니다 또는 사용자 권한, 서버 또는 서버 이름이 잘못 되었을 수 있습니다.| 
|RInterop 프로세스 시간이 초과 되었습니다. 비활성화 및 RInterop 로그를 확인, 작업 관리자에서 RInterop 프로세스를 중지 하 고 다시 시도 하십시오.<br><br>로 구분하거나 여러<br><br>RInterop faulted 상태입니다. 작업 관리자에서 RInterop 프로세스를 중지 하 고 다시 시도 하십시오.|% Temp %에 로그를 확인 하세요\\RInterop 오류를 확인 합니다. 다시 시도 하기 전에 RInterop 프로세스에서 작업 관리자를 제거 합니다. 문제가 지속 되 면 제품 팀에 문의 합니다.| 

### <a name="the-report-is-generated-but-data-appears-to-be-missing"></a>보고서를 생성할 수 있지만 누락 된 데이터가 표시 됩니다.
    
분석 데이터가 있는지 확인 하려면 SQL Server를 실행 하는 컴퓨터에 데이터베이스를 확인 합니다. 분석 데이터베이스가 있는지 확인 하 고 해당 테이블을 확인 합니다. 예를 들어, 이러한 테이블을 확인 합니다. TblBatchesA TblBatchesB, 하며 TblSummaryStats 합니다.

데이터가 존재 하지 않을 경우 데이터가 올바르게 복사 하지 않을 수 있습니다 또는 데이터베이스가 손상 되었을 수 있습니다. 일부 데이터가 누락 된 경우 캡처에서 생성 된 추적 파일 또는 재생 될 수 있습니다 하지가 캡처된 워크 로드에 정확 하 게 합니다. 데이터가 있으면 %temp% 로그 파일을 확인 합니다.\\비활성화 하는 경우 오류가 기록 되었는지 확인 합니다. 그런 다음 다시 시도 분석 보고서를 생성 합니다.

자세한 질문 또는 피드백? 왼쪽 아래 모서리에 있는 웃는 얼굴 아이콘을 선택 하 여 비활성화 도구를 통해 피드백을 제출 합니다.  

## <a name="next-steps"></a>다음 단계

- 분석 보고서를 보는 방법에 알아보려면 참조 [보고](database-experimentation-assistant-view-report.md)합니다.

- 비활성화 및 데모를 19 분 소개의 경우 다음 동영상을 시청 합니다.

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
