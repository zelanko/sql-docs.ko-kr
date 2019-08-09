---
title: SSMS(SQL Server Management Studio) 릴리스 정보 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 07/31/2019
ms.openlocfilehash: c30179ae89bc69e84005a95a4d370acf4b692bd2
ms.sourcegitcommit: 0d89bcaebdf87db3bd26db2ca263be9c671b0220
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2019
ms.locfileid: "68731136"
---
# <a name="release-notes-for-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio) 릴리스 정보

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

이 문서에서는 SSMS의 현재 버전과 이전 버전에 대한 업데이트, 향상 및 버그 수정에 대한 세부 정보를 제공합니다.

<!--
The latest ## H2 section of this Release Notes article has been reformatted to match the new standard.
The new standard replaces the use of bullet lists with the 2-column markdown table format.
Please use the new 2-column table format going forward.
And please do include the final blank row of "| &nbsp;| &nbsp;|".

The ## H2 titles are also being shortened, by the removal of unnecessary repetitive strings.
In this case, "## SSMS 17.9" is being shortened to "## 17.9" (as one standard actual example).
Also, we are appending the 'Month yyyy.'

Also, this file has been renamed to the new standard, which calls for the file name to be with "release-notes-[techAreaName].md."
The old name for this file was 'sql-server-management-studio-changelog-ssms.md'.
But today the new file name is 'release-notes-ssms.md' (still in 'docs/ssms/').

Thank you.
GeneMi. 2019/04/02.
-->

## <a name="ssms-182"></a>SSMS 18.2

다운로드: [SSMS 18.2 다운로드](download-sql-server-management-studio-ssms.md)  
빌드 번호: 15.0.18142.0  
릴리스 날짜: 2019년 7월 25일

SSMS 18.2는 SSMS의 최신 GA(일반 공급) 릴리스입니다. 이전 버전의 SSMS가 필요한 경우 [이전 SSMS 릴리스](release-notes-ssms.md#previous-ssms-releases)를 참조하세요.

18.2는 18.1의 업데이트로 다음과 같은 새 항목 및 버그가 수정되었습니다.

## <a name="whats-new-in-182"></a>18.2의 새로운 기능

|  새 항목  |  세부 정보  |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Integration Services(SSIS) | Azure에서 SSIS 패키지 스케줄러에 대한 성능 최적화. |
| Intellisense/편집기 | 데이터 분류에 대한 지원이 추가되었습니다. |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | Intellisense 지원이 추가되었습니다. |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | 인덱스에 높은 동시성 삽입에 대한 처리량을 향상시키는 데 도움이 되는 데이터베이스 엔진 내의 최적화를 켭니다. 이 옵션은 ID 열, 시퀀스 또는 날짜/시간 열과 같은 순차 키가 있는 인덱스에서 일반적으로 볼 수 있는 마지막 페이지 삽입 경합에 취약한 인덱스를 대상으로 합니다. 자세한 내용은 [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys)를 참조하세요. |
| 쿼리 실행 또는 결과 | 지정된 쿼리가 실행을 완료한 시간을 추적하기 위해 메시지에 *완료 시간*이 추가되었습니다. |
| 쿼리 실행 또는 결과 | 추가 데이터를 표시하고(결과를 텍스트로) 셀에 저장할 수 있습니다(결과를 표 형태로). 이제 SSMS에서 최대 2M자(각각 256 및 64K)를 허용합니다. 또한 사용자가 표의 셀에서 43680자를 초과해서 가져올 수 없는 문제가 해결되었습니다. |
| 실행 계획 | [인라인 스칼라 UDF 기능](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining)을 사용하도록 설정하는 경우 QueryPlan에 새 특성이 추가되었습니다(ContainsInlineScalarTsqlUdfs). |
| SMO | *기능 제한*에 대한 지원이 추가되었습니다. 기능 자체에 대한 자세한 내용은 [기능 제한](https://docs.microsoft.com/sql/relational-databases/security/feature-restrictions)을 참조하세요. |
| SMO | *SQL 평가 API*에 대한 지원이 추가되었습니다. 자세한 내용은 [SQL 평가 API](https://docs.microsoft.com/sql/sql-assessment-api/sql-assessment-api-overview)를 참조하세요. |
|  |  |

## <a name="bug-fixes-in-182"></a>18.2의 버그 수정

|  새 항목  |  세부 정보  |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 손쉬운 사용 | F3 키를 눌러 정렬할 수 있도록 XEvent UI(표)를 업데이트했습니다. |
| Always On | AG(가용성 그룹)를 삭제하려고 할 때 SSMS에서 오류를 발생하는 문제를 해결했습니다. |
| Always On | SSMS가 동기로 구성된 경우 읽기 확장 AG(클러스터 유형=없음)를 사용할 때 잘못된 장애 조치(failover) 마법사를 표시하는 문제를 해결했습니다. 이제 SSMS는 클러스터 유형이 없음인 가용성에만 허용되는 Force_Failover_Allow_Data_Loss 옵션에 대한 마법사를 표시합니다. |
| Always On | 마법사에서 동기화 횟수를 3회로 제한하는 문제를 해결했습니다. |
| 데이터 분류 | CompatLevel이 150보다 작은 데이터베이스에 대해 데이터 분류 보고서를 보려고 할 때 SSMS가 *0에서 시작하는 인덱스는 0보다 크거나 같아야 합니다.* 오류를 발생하는 문제를 해결했습니다. |
| 일반 SSMS | 사용자가 마우스 휠을 통해 결과 창을 가로로 스크롤할 수 없는 문제를 해결했습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/34145641)를 참조하세요. |
| 일반 SSMS | 무해한 대기 유형 SQLTRACE_WAIT_ENTRIES를 무시하도록 *작업 모니터*가 업데이트되었습니다. |
| 일반 SSMS | 일부 색 옵션 *(텍스트 편집기 > 편집기 탭 및 상태 표시줄)* 이 유지되지 않는 문제가 해결되었습니다. [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37924165)를 참조하세요.
| 일반 SSMS | 기능은 동일하지만 혼동을 줄이기 위해 연결 대화 상자에서 *Azure Active Directory - MFA 지원을 포함한 유니버설*이 *Active Directory - MFA를 통한 유니버설*로 바뀌었습니다. |
| 일반 SSMS | Azure SQL Database를 만들 때 올바른 기본값을 사용하도록 SSMS가 업데이트되었습니다. |
| 일반 SSMS | 서버가 [SQL Linux 컨테이너](../linux/quickstart-install-connect-docker.md)인 경우 [서버 등록](register-servers/register-servers.md)의 노드에서 *PowerShell을 시작*할 수 없는 문제를 해결했습니다. |
| 플랫 파일 가져오기 | SSMS 18.0에서 18.1로 업그레이드 한 후 *플랫 파일 가져오기*가 작동하지 않는 문제를 해결했습니다. [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37912636)를 참조하세요. |
| 플랫 파일 가져오기 | *플랫 파일 가져오기 마법사가 헤더에 유니코드 문자가 포함된 .csv 파일에서 중복되거나 잘못된 열*을 보고하는 문제가 해결되었습니다. |
| 개체 탐색기 | Sql Express에 연결된 경우 일부 메뉴 항목(예: SQL Server *가져오기 및 내보내기 마법사*)이 없거나 사용하지 않도록 설정되는 문제를 해결했습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37500016)를 참조하세요. |
| 개체 탐색기 | 개체 탐색기에서 편집기로 개체를 끌어올 때 SSMS가 충돌하는 문제를 해결했습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37887988)를 참조하세요. |
| 개체 탐색기 | 데이터베이스 이름을 바꾸면 잘못된 데이터베이스 이름이 개체 탐색기에 표시되는 문제를 해결했습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37638472)를 참조하세요. |
| 개체 탐색기 | Windows에서 지원하지 않는 데이터 정렬을 사용하도록 설정된 데이터베이스에 대해 개체 탐색기에서 *테이블* 노드를 확장하려고 할 때 오류를 트리거하는(사용자가 자신의 테이블을 확장할 수 없음) 장기 미해결 문제가 해결되었습니다. 이러한 데이터 정렬의 예는 Korean_Wansung_Unicode_CI_AS입니다. |
| [서버 등록](register-servers/register-servers.md) | 등록된 서버가 *Active Directory - 통합* 또는 *Azure Active Directory - MFA를 통한 유니버설 인증*을 사용할 경우 여러 서버에 대해 쿼리를 실행하려고 하면(등록된 서버의 *그룹*에서) SSMS가 연결되지 못하여 쿼리가 작동되지 않는 문제를 해결했습니다. |
| [서버 등록](register-servers/register-servers.md) | 등록된 서버가 *Active Directory - 암호* 또는 *SQL 인증*을 사용하고 사용자가 암호를 저장하지 않도록 선택할 경우 여러 서버에 대해 쿼리를 실행하려고 하면(등록된 서버의 *그룹*에서) SSMS가 중단되는 문제를 해결했습니다. |
| 보고서 | 데이터 파일에 방대한 수의 익스텐트가 있을 때 보고서에 오류가 발생하는 *디스크 사용* 보고서의 문제를 해결했습니다. |
| 복제 도구 | 복제 모니터가 AG의 게시자 DB 및 AG의 배포자 DB를 사용하지 않는 문제를 해결했습니다(이전에는 SSMS 17.x에서 이 문제가 해결됨). |
| SQL 에이전트 | 작업 단계 추가, 삽입, 편집 또는 제거 시 포커스가 활성 행 대신 첫 번째 행을 재설정하는 문제를 해결했습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/38070892)를 참조하세요. |
| SMO/스크립팅 | *CREATE OR ALTER*가 확장 속성이 있는 개체를 스크립팅하지 않는 문제를 해결했습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035-sql-server/suggestions/37236748)를 참조하세요. |
| SMO/스크립팅 | SSMS가 CREATE EXTERNAL LIBRARY를 올바르게 스크립트로 작성할 수 없는 문제를 해결했습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37868089)를 참조하세요. |
| SMO/스크립팅 |  수천 개의 테이블을 포함하는 데이터베이스에 대해 *스크립트 생성*을 실행하려고 하면 진행률 대화 상자가 중단된 것처럼 나타내는 문제를 해결했습니다. |
| SMO/스크립팅 | SQL 2019에서 *외부 테이블* 스크립팅이 작동하지 않는 문제를 해결했습니다. |
| SMO/스크립팅 | SQL 2019에서 *외부 데이터 원본* 스크립팅이 작동하지 않는 문제를 해결했습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/34295080)를 참조하세요. |
| SMO/스크립팅 | Azure SQL DB를 대상으로 할 때 열의 *확장 속성*이 스크립팅되지 않는 문제를 해결했습니다. 자세한 내용은 [stackoverflow](https://stackoverflow.com/questions/56952337/how-can-i-script-the-descriptions-of-columns-in-ms-sql-server-management-studio)를 참조하세요. |
| SMO/스크립팅 | 마지막 페이지 삽입: SMO - 속성 *Index.IsOptimizedForSequentialKey* 추가 |
|**SSMS 설치**| **SSMS 설치 프로그램이 언어 불일치를 보고하는 SSMS의 설치를 잘못 차단하는 문제를 완화했습니다. 이러한 특성은 중단된 설치 또는 이전 버전 SSMS의 잘못된 제거와 같은 일부 비정상적인 상황에서 문제가 될 수 있습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37483594/)를 참조하세요.** |
| XEvent 프로파일러 | 뷰어를 닫을 때 발생하는 충돌이 해결되었습니다. |

### <a name="known-issues-182"></a>알려진 문제(18.2)

- SSMS 충돌이 발생할 수 있기 때문에 머신 A에서 실행되는 SSMS에서 만든 데이터베이스 다이어그램을 머신 B에서 수정할 수 없습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37992649)를 참조하세요.

- 여러 쿼리 창 간을 전환할 때 SSMS 18.0이 다시 그려지는 문제 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37474042)를 참조하세요. 이 문제의 해결 방법은 **도구** > **옵션**에서 하드웨어 가속을 사용하지 않도록 설정하는 것입니다.

- SSMS 결과에서 표시되는 데이터의 크기에는 그리드, 텍스트 또는 파일로 표시되는 제한 사항이 있습니다.

다른 알려진 문제를 확인하고 제품 팀에 피드백을 제공하려면 [UserVoice](https://feedback.azure.com/forums/908035-sql-server)를 참조할 수 있습니다. 

## <a name="previous-ssms-releases"></a>이전 SSMS 릴리스

다음 섹션의 제목 링크를 클릭하여 이전 SSMS 버전을 다운로드하세요.

## <a name="downloadssdtmediadownloadpng-ssms-181httpsgomicrosoftcomfwlinklinkid2094583"></a>![다운로드](../ssdt/media/download.png) [SSMS 18.1](https://go.microsoft.com/fwlink/?linkid=2094583)

- 릴리스 번호: 18.1  
- 빌드 번호: 15.0.18131.0  
- 릴리스 날짜: 2019년 6월 11일  

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40a)

SSMS 18.1은 SSMS의 최신 GA(일반 공급) 릴리스입니다. 이전 버전의 SSMS가 필요한 경우 [이전 SSMS 릴리스](release-notes-ssms.md#previous-ssms-releases)를 참조하세요.

18.1은 18.0의 작은 업데이트로 다음과 같은 새 항목 및 버그가 수정되었습니다.

## <a name="whats-new-in-181"></a>18.1의 새로운 기능

| 새 항목| 세부 정보|
| :-------| :------|
| 데이터베이스 다이어그램 | [데이터베이스 다이어그램이 SSMS에 다시 추가됨](https://feedback.azure.com/forums/908035/suggestions/37507828).
| SSBDIAGNOSE.EXE |SQL Server 진단 명령줄 도구가 SSMS 패키지에 다시 추가되었습니다.|
| Integration Services(SSIS) | Azure의 SSIS 카탈로그 또는 Azure의 파일 시스템에 있는 SSIS 패키지 일정 예약이 지원됩니다. 새 일정 대화 상자를 실행할 수 있는 항목은 세 가지입니다. *새 일정…* 메뉴 항목은 Azure의 SSIS 카탈로그에서 SSIS 패키지를 마우스 오른쪽 단추로 클릭하면 나타납니다. *Schedule SSIS Package in Azure* 메뉴 항목은 *도구* 메뉴 항목 아래 *Azure로 마이그레이션* 메뉴 항목에 있습니다. "Schedule SSIS in Azure"는 Azure SQL Database Managed Instance의 SQL Server 에이전트 아래 있는 작업 폴더를 마우스 오른쪽 단추로 클릭하면 표시됩니다.|

## <a name="bug-fixes-in-181"></a>18.1의 버그 수정

| 새 항목 | 세부 정보 |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 손쉬운 사용 | 에이전트 작업 UI의 향상된 내게 필요한 옵션. |
| 손쉬운 사용 | *자동 새로 고침* 단추에 액세스 가능한 이름을 추가하고 사용자가 어떤 단추가 있는지뿐만 아니라 단추 누름의 영향을 알 수 있도록 도와주는 지능형 액세스 가능 이름을 추가하여 Stretch 모니터 페이지의 액세스 가능성을 개선했습니다. |
| ADS 통합| ADS 등록 서버를 사용하려고 할 때 SSMS에서 발생할 수 있는 오류를 해결했습니다.|
| 데이터베이스 디자이너 | Latin1_General_100_BIN2_UTF8 데이터 정렬에 대한 지원 추가(SQL Server 2019 CTP3.0에서 사용 가능) |
| 데이터 분류 | 지원되지 않은 기록 테이블의 열에 민감도 레이블을 추가하지 마세요. |
| 데이터 분류 | 호환성 수준(서버 및 데이터베이스)의 잘못된 처리와 관련된 문제를 해결했습니다. |
| 데이터베이스 디자이너 | Latin1_General_100_BIN2_UTF8 데이터 정렬에 대한 지원이 추가되었습니다(SQL2019 CTP3.0에서 사용 가능). |
| 일반 SSMS | 인덱스의 pseudo 열 스크립팅이 올바르지 않은 문제를 해결했습니다. |
| 일반 SSMS | *자격 증명 추가* 단추를 클릭하면 Null 참조 예외가 throw될 수 있는 로그인 속성 페이지의 문제가 해결되었습니다. |
| 일반 SSMS | 인덱스 속성 페이지에 비용 열 크기 표시가 수정되었습니다. |
| 일반 SSMS | SSMS가 SQL 편집기 창의 *도구/옵션*에서 Intellisense 설정을 준수하지 않는 문제가 해결되었습니다. |
| 일반 SSMS | SSMS가 도움말 설정을 준수하지 않은 문제가 해결되었습니다(온라인 및 오프라인). |
| 높은 DPI | 지원되지 않는 쿼리 옵션에 대한 오류 대화 상자의 컨트롤 레이아웃이 수정되었습니다. |
| 높은 DPI | 일부 지역화 버전의 SSMS에 있는 *새 가용성 그룹* 페이지의 컨트롤 레이아웃이 수정되었습니다. |
| 높은 DPI | *새 작업 일정* 페이지의 레이아웃이 수정되었습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37632094)를 참조하세요. |
| 플랫 파일 가져오기 | 가져오기 중에 행이 자동으로 손실될 수 있는 문제가 해결되었습니다.|
| Intellisense/편집기 | Intellisense용 Azure SQL 데이터베이스에 대한 SMO 기반 쿼리 트래픽이 줄어듭니다. |
| Intellisense/편집기 | 사용자를 만들기 위해 T-SQL을 입력할 때 표시되는 도구 설명의 문법적 오류가 해결되었습니다. 또한 사용자와 로그인 사이의 모호함을 없애기 위해 오류 메시지를 수정했습니다. |
| 로그 뷰어 | 개체 탐색기에서 이전 보관 기호를 두 번 클릭하더라도 SSMS가 항상 현재 서버(또는 에이전트) 로그를 여는 문제가 해결되었습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37633648)를 참조하세요. |
| SSMS 설치 | 설치 로그 경로에 공백이 포함되어 있을 때 SSMS 설치가 실패하는 문제가 해결되었습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37496110)를 참조하세요. |
| SSMS 설치 | SSMS가 시작 화면을 표시한 후 바로 종료되는 문제가 해결되었습니다. </br> 자세한 내용은 다음 사이트를 참조하세요. [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37502512)[SSMS에서 시작 거부](https://dba.stackexchange.com/questions/238609/ssms-refuses-to-start), [데이터베이스 관리자](https://dba.stackexchange.com/questions/237086/sql-server-management-studio-18-wont-open-only-splash-screen-pops-up) |
| 개체 탐색기 | Linux의 SQL에 연결된 경우 *PowerShell 시작* 활성화에 대한 제한이 해제되었습니다. |
| 개체 탐색기 | Polybase/스케일 아웃 그룹 노드를 확장하려고 할 때(컴퓨팅 노드에 연결될 때) SSMS가 충돌하는 문제가 해결되었습니다. |
| 개체 탐색기 | 지정된 인덱스를 비활성화한 후에도 *사용 안 함* 메뉴 항목이 여전히 활성화되는 문제가 해결되었습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37735375)를 참조하세요. |
| 보고서 | 보고서(SQL 성능 대시보드 보고서)를 수정하여 GrantedQueryMemory를 KB 단위로 표시합니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37167289)를 참조하세요. |
| 보고서 | Always-On 시나리오에서 로그 블록의 추적을 개선했습니다. |
| 실행 계획 | 실행 계획 스키마에 새 실행 계획 요소 *SpillOccurred*가 추가되었습니다. |
| 실행 계획 | 실행 계획 스키마에 원격 읽기(*ActualPageServerReads*, *ActualPageServerReadAheads* *ActualLobPageServerReads*, *ActualLobPageServerReadAheads*)를 추가했습니다. |
| SMO/스크립팅 | 비그래프 테이블에 대한 스크립팅 중에 에지 제약 조건을 쿼리하지 마세요. |
| SMO/스크립팅 | *데이터 분류*로 열을 스크립팅할 때 민감도 분류에 대한 제약 조건이 제거되었습니다. |
| SMO/스크립팅 | 데이터 생성 시 그래프 테이블의 "스크립트 생성"이 실패하는 문제가 해결되었습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898466)를 참조하세요. |
| SMO/스크립팅 | EnumObjects() 메서드가 동의어의 스키마 이름을 가져오지 않는 문제가 해결되었습니다. |
| SMO/스크립팅 | *AdvancedOptions* 섹션을 읽지 않은(암호가 지정되지 않은 경우) UIConnectionInfo.LoadFromStream()의 문제가 해결되었습니다. |
| SQL 에이전트 | 작업 속성 창을 사용하여 작업하는 동안 SSMS가 충돌하는 문제가 해결되었습니다. 자세한 내용은 [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37164244)를 참조하세요. |
| SQL 에이전트 | *작업 단계 속성*의 "보기" 단추가 항상 활성화되지 않아 지정된 작업 단계의 출력을 볼 수 없게 되는 문제가 해결되었습니다. |
| XEvent UI | 동일한 이름의 이벤트와 구분하기 위해 XEvent 목록에 "Package" 열을 추가했습니다. |
| XEvent UI | 누락된 "EXTERNAL LIBRARY" 클래스 형식 매핑이 XEventUI에 추가되었습니다. |

### <a name="known-issues-181"></a>알려진 문제(18.1)

- 사용자가 개체 탐색기에서 쿼리 편집기에 테이블 개체를 끌 때 오류가 표시될 수 있습니다. 문제를 인식하고 있고, 수정은 다음 릴리스에 대해 계획되어 있습니다.

- 옵션 -> 텍스트 편집기 -> 편집기 탭 및 상태 표시줄 ->상태 표시줄 레이아웃 및 색상의 *그룹 연결* 및 *단일 서버 연결* 색상 옵션은 SSMS 18.1을 닫은 후에도 유지되지 않습니다. SSMS를 다시 열면 상태 표시줄 레이아웃 및 색상 옵션이 기본값(흰색)으로 돌아갑니다.

- SSMS 결과에서 표시되는 데이터의 크기에는 그리드, 텍스트 또는 파일로 표시되는 제한 사항이 있습니다.

## <a name="downloadssdtmediadownloadpng-ssms-180httpsgomicrosoftcomfwlinklinkid2088649"></a>![다운로드](../ssdt/media/download.png) [SSMS 18.0](https://go.microsoft.com/fwlink/?linkid=2088649)

- 릴리스 번호: 18.0  
- 빌드 번호: 15.0.18118.0  
- 릴리스 날짜: 2019년 4월 24일

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x804)| [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x404)| [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x409)| [프랑스어](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x40c)| [독일어](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x407)| [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x410)| [일본어](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x411)| [한국어](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x412)| [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x416)| [러시아어](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x419)| [스페인어](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x40a)

### <a name="whats-new-in-180"></a>18.0의 새로운 기능

| 새 항목| 세부 정보|
| :-------| :------|
|SQL Server 2019 지원|SSMS 18.0은 SQL Server 2019 (compatLevel 150)에 대해 완전히 *인식*하는 첫 번째 릴리스입니다.|
|SQL Server 2019 지원|SQL Server 2019 및 SQL Managed Instance에서 "BATCH_STARTED_GROUP" 및 "BATCH_COMPLETED_GROUP"을 지원합니다.|
|SQL Server 2019 지원|SMO: UDF 인라인 처리에 대한 지원 추가|
|SQL Server 2019 지원|GraphDB: Graph TC Sequence에 대한 실행 계획에 플래그를 추가합니다.|
|SQL Server 2019 지원|Always Encrypted: AEv2 / Enclave에 대한 지원이 추가되었습니다.|
|SQL Server 2019 지원|Always Encrypted: 사용자가 “옵션” 단추를 클릭하여 Enclave 지원을 활성화/구성하면 연결 대화 상자에는 새로운 “Always Encrypted” 탭이 있습니다.|
|작아진 SSMS 다운로드 크기| 현재 크기는 ~500MB로 SSMS 17.x 번들의 약 절반입니다.
|SSMS는 Visual Studio 2017 격리 셸을 기준으로 합니다.|새로운 셸(SSMS는 Visual Studio 2017 15.9.11을 기반으로 함)은 SSMS와 Visual Studio 모두에 들어 있는 모든 접근성 수정 사항의 잠금을 해제하고 최신 보안 픽스를 포함합니다.|
|SSMS 접근성 개선 사항| 모든 도구(SSMS, DTA 및 프로파일러)에서 접근성 문제를 해결하기 위한 많은 작업이 수행되었습니다.|
|SSMS는 이제 사용자 지정 폴더에 설치할 수 있습니다.| 이 옵션은 명령줄(무인 설치에 유용함)과 설치 UI 모두에서 사용할 수 있습니다. 명령줄에서 이 추가 인수를 SSMS-Setup-ENU.exe에 전달하세요.   SSMSInstallRoot=C:\MySSMS18  기본적으로 새 SSMS 설치 위치는 %ProgramFiles(x86)%\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe입니다.  이는 SSMS가 다중 인스턴스임을 의미하지는 않습니다.|
|SSMS를 통해 OS 언어 이외의 언어로 설치 가능|혼합 언어 설정의 블록이 해제되었습니다. 예를 들어 프랑스어 Windows에 SSMS 독일어를 설치할 수 있습니다. OS 언어가 SSMS 언어와 일치하지 않는 경우 사용자는 **도구** > **옵션** > **국가별 설정**에서 언어를 변경해야 합니다. 그렇지 않으면 SSMS가 영어 UI를 표시합니다.|
|SSMS는 더 이상 SQL 엔진과 구성 요소를 공유하지 않습니다.|SQL 엔진과 구성 요소를 공유하지 않도록 많은 노력을 기울였지만, 서비스 효율성 문제가 자주 발생했습니다(다른 구성 요소에서 설치한 파일을 손상시킴).|
|SSMS를 사용하려면 NetFx 4.7.2 이상 필요|최소 요구 사항을 NetFx4.6.1에서 NetFx4.7.2로 업그레이드했습니다. 이를 통해 새로운 프레임워크에서 제공하는 새로운 기능을 이용할 수 있습니다.|
|SSMS 설정을 마이그레이션하는 기능| 처음 SSMS 18을 시작하면 사용자에게 17.x 설정을 마이그레이션하라는 메시지가 표시됩니다. 사용자 설정 파일은 이제 일반 XML 파일로 저장되므로 이식성이 향상되고 편집이 가능해집니다.|
|높은 DPI 지원| 높은 DPI는 이제 기본적으로 활성화됩니다.|
|SSMS는 Microsoft OLE DB 드라이버와 함께 제공됩니다.| 자세한 내용은 [SQL Server용 Microsoft OLE DB 드라이버 다운로드](https://docs.microsoft.com/sql/connect/oledb/download-oledb-driver-for-sql-server)를 참조하세요.|
|SSMS는 Windows 8에서 지원되지 않습니다. Windows 10 및 Windows Server 2016에는 버전 1607(10.0.14393) 이상이 필요합니다.|NetFx 4.7.2의 새로운 종속성으로 인해 SSMS 18.0은 Windows 8, 이전 버전의 Windows 10 및 Windows Server 2016에 설치되지 않습니다. SSMS를 설치하면 위 시스템은 차단됩니다. Windows 8.1은 여전히 지원됩니다.|
|SSMS는 더 이상 PATH 환경 변수에 추가되지 않습니다.|SSMS.EXE(및 일반적인 도구)의 경로는 더 이상 경로에 추가되지 않습니다. 사용자는 수동으로 추가하거나 최신 Windows 컴퓨터의 경우 시작 메뉴에서 사용할 수 있습니다.|
|패키지 ID는 SSMS 확장을 개발하는 데 더 이상 필요하지 않습니다.| 과거에는 SSMS가 잘 알려진 패키지만 선택적으로 로드하여 개발자가 직접 패키지를 등록해야 했습니다. 더 이상 그렇지 않습니다.|
|일반 SSMS|SSMS의 파일 그룹에 대한 AUTOGROW_ALL_FILES 구성 옵션을 공개합니다.|
|일반 SSMS|문제가 발생할 수 있는 '경량 풀링' 및 '우선순위 높임' 옵션이 SSMS GUI에서 제거되었습니다. 자세한 내용은 [우선순위 높임 세부 정보 및 권장되지 않은 이유](https://blogs.msdn.microsoft.com/arvindsh/2010/01/26/priority-boost-details-and-why-its-not-recommended/)를 참조하세요.
|일반 SSMS|파일을 생성하는 새 메뉴 및 키 바인딩: **CTRL+ALT+N**. **Ctrl+N**을 사용하면 새 쿼리를 계속 만듭니다.|
|일반 SSMS|이제 사용자는 규칙 이름 하나를 자동으로 생성하는 대신 **새 방화벽 규칙** 대화 상자에서 규칙 이름을 지정할 수 있습니다.|
|일반 SSMS|특별히 v140+ T-SQL을 위해 편집기에서 Intellisense를 개선했습니다.|
|일반 SSMS|데이터 정렬 대화 상자에서 UTF-8용 SSMS UI에 지원을 추가했습니다.|
|일반 SSMS|연결 대화 상자 MRU 암호를 위해 “Windows 자격 증명 관리자”로 전환했습니다. 이렇게 하면 암호의 지속성을 항상 신뢰할 수 없다는 오랫동안의 미해결 문제가 해결됩니다.|
|일반 SSMS|예상 모니터에서 더 많은 대화 상자와 창이 표시되도록 하여 다중 모니터 시스템을 더욱 강력하게 지원합니다.|
|일반 SSMS|서버 속성 대화 상자의 새 데이터베이스 설정 페이지에서 ‘백업 체크섬 기본값’ 서버 구성을 제공했습니다. 자세한 내용은 [https://feedback.azure.com/forums/08035-sql-server/suggestions/34634974](https://feedback.azure.com/forums/08035-sql-server/suggestions/34634974)를 참조하세요.|
|일반 SSMS|"SQL Server 오류 로그 구성" 아래에서 "오류 로그 파일의 최대 크기"가 공개됩니다. 자세한 내용은 [https://feedback.azure.com/forums/908035/suggestions/33624115](https://feedback.azure.com/forums/908035/suggestions/33624115)를 참조하세요.|
|일반 SSMS|도구 메뉴 아래에 "Azure로 마이그레이션" 추가 - Database Migration Assistant 및 Azure Database Migration Service를 통합하여 Azure로 마이그레이션을 가속화하는 데 도움이 되는 빠르고 쉬운 액세스를 제공합니다.|
|일반 SSMS|"연결 정보 변경"을 사용하는 경우 열린 트랜잭션을 커밋하도록 사용자에게 표시하는 논리가 추가되었습니다.|
|Azure Data Studio 통합|Azure Data Studio 시작/다운로드에 메뉴 항목이 추가되었습니다.|
|Azure Data Studio 통합|개체 탐색기에 "Azure Data Studio 시작" 메뉴 항목이 추가되었습니다.|
|Azure Data Studio 통합|OE에서 데이터베이스 노드를 마우스 오른쪽 단추로 클릭하면 사용자에게 쿼리를 실행하거나 Azure Data Studio에서 새 Notebook을 만들 수 있는 컨텍스트 메뉴가 나타납니다.|
|Azure SQL 지원| 이제 SLO/Edition/MaxSize 데이터베이스 속성이 사용자 지정 이름을 허용하므로 더 쉽게 Azure SQL 데이터베이스의 향후 버전을 지원할 수 있습니다.|
|Azure SQL 지원| vCore SKU(범용 및 중요 비즈니스용)에 대한 지원 추가: Gen4_24 및 모든 Gen5.|
|Azure SQL Managed Instance|Azure SQL Managed Instance에 연결되는 경우 새 "AAD 로그인"을 새 로그인 유형으로 SMO 및 SSMS에 추가할 수 있습니다.|
|Always On|SSMS Always on 대시보드에서 RTO(예상 복구 시간) 및 RPO(예상 데이터 손실)를 새로 고칩니다. [https://docs.microsoft.com/sql/database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups](../database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups.md)의 업데이트된 설명서를 참조하세요.|
|Always Encrypted| 서버에 연결 상자의 Always Encrypted 탭에 있는 Always Encrypted 확인란을 선택하면 데이터베이스 연결에 대해 Always Encrypted를 활성화/비활성화하는 쉬운 방법이 제공됩니다.|
|보안 Enclave를 사용한 Always Encrypted| SQL Server 2019 미리 보기의 보안 enclave를 사용하는 Always Encrypted를 지원하기 위해 몇 가지 기능을 개선했습니다.  서버에 연결 대화 상자에서 enclave 증명 URL을 지정하기 위한 텍스트 필드(새로운 Always Encrypted 탭).  새 열 마스터 키가 enclave 계산을 허용하는지 여부를 제어하는 새 열 마스터 키 대화 상자의 새로운 확인란.  기타 Always Encrypted 키 관리 대화 상자에는 enclave 계산을 허용하는 열 마스터 키에 대한 정보를 제공합니다.|
|감사 파일|Azure AD 기반 인증을 기반으로 스토리지 계정 키에서 인증 방법을 변경했습니다.|
|감사 파일|FEATURE RESTRICTION ADD/CHANGE GROUP/DROP을 포함하도록 알려진 감사 동작 목록이 업데이트되었습니다.|
|데이터 분류| 재구성된 데이터 분류 작업 메뉴: 데이터베이스 작업 메뉴에 하위 메뉴를 추가하고, 먼저 데이터 분류 창을 열지 않고도 메뉴에서 보고서를 여는 옵션을 추가했습니다.|
|데이터 분류|'데이터 분류' 기능이 SMO에 새로 추가되었습니다. 열 개체에서 새로운 SensitivityLabelName, SensitivityLabelId, SensitivityInformationTypeName, SensitivityInformationTypeId 및 IsClassified(읽기 전용) 속성을 표시합니다. 자세한 내용은 [ADD SENSITIVITY CLASSIFICATION(Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/add-sensitivity-classification-transact-sql)을 참조하세요.|
|데이터 분류|"분류 보고서" 메뉴 항목이 "데이터 분류" 플라이아웃에 새로 추가되었습니다.|
|데이터 분류| 업데이트된 권장 사항.|
|데이터베이스 호환성 수준 업그레이드|***데이터베이스 이름*** > ***작업*** > ***데이터베이스 업그레이드*** 아래에 새 옵션이 추가되었습니다. 그러면 새로운 **QTA(쿼리 튜닝 도우미)** 를 시작하여 사용자에게 다음 프로세스를 안내합니다. 데이터베이스 호환성 수준을 업그레이드하기 전에 성능 기준 수집 원하는 데이터베이스 호환성 수준으로 업그레이드  동일한 워크로드를 통해 두 번째 성능 데이터 전달 수집 워크로드 회귀 검색 및 워크로드 성능 향상을 위한 테스트된 권장 사항 제공  이는 QTA에서 이전에 알려진 정상 상태에 따라 권장 사항을 생성하지 않는 마지막 단계를 제외하고는 [쿼리 저장소 사용 시나리오](https://docs.microsoft.com/sql/relational-databases/performance/query-store-usage-scenarios#CEUpgrade)에 문서화된 데이터베이스 업그레이드 프로세스에 가깝습니다.|
|데이터 계층 애플리케이션 마법사|Graph 테이블을 통한 데이터 계층 애플리케이션 가져오기/내보내기 지원이 추가되었습니다.|
|플랫 파일 가져오기 마법사|가져오기로 인해 열 이름이 변경되었을 수 있음을 사용자에게 알리는 논리가 추가되었습니다.|
|Integration Services(SSIS)|고객이 Azure Government 클라우드에 있는 Azure-SSIS IR에서 SSIS 패키지를 예약할 수 있도록 하는 지원이 추가되었습니다.|
|Integration Services(SSIS)|SSMS를 통해 SQL Managed Instance의 SQL 에이전트를 사용하는 경우 SSIS 에이전트 작업 단계에서 매개 변수 및 연결 관리자를 구성할 수 있습니다.|
|Integration Services(SSIS)|Azure SQL DB/Managed Instance에 연결할 때 *기본값*을 사용하여 초기 db로 연결할 수 있습니다.|
|Integration Services(SSIS)|"Integration Services 카탈로그" 노드에 새로운 **Azure Data Factory에서 SSIS 시도** 항목이 추가되었습니다. 이 항목을 사용하면 "Integration Runtime 만들기 마법사"를 시작하고 "Azure-SSIS Integration Runtime"을 빠르게 만들 수 있습니다.
|Integration Services(SSIS)|"카탈로그 만들기 마법사"에 **SSIS IR 만들기** 단추가 추가되었습니다. 이 단추를 사용하면 "Integration Runtime 만들기 마법사"를 시작하고 "Azure-SSIS Integration Runtime"을 빠르게 만들 수 있습니다.|
|Integration Services(SSIS)|이제 ISDeploymentWizard는 명령줄 모드에서 SQL 인증, Azure Active Directory 통합 인증 및 Azure Active Directory 암호 인증을 지원합니다.|
|Integration Services(SSIS)|이제 배포 마법사는 Azure Data Factory SSIS Integration Runtime 생성 및 배포를 지원합니다.|
|개체 스크립팅|개체를 스크립팅할 때 'CREATE OR ALTER'에 대한 새 메뉴 항목을 추가합니다.|
|쿼리 저장소|차트의 Y축에 표시된 숫자에 수천 개의 구분 기호를 추가하여 일부 보고서(전체 리소스 사용량)의 사용 편의성이 향상되었습니다.|
|쿼리 저장소|새 쿼리 대기 통계 보고서가 추가되었습니다.|
|쿼리 저장소|"추적 쿼리" 보기에 "실행 횟수" 메트릭이 추가되었습니다.|
|복제 도구|복제 모니터 및 SSMS에서 기본이 아닌 포트 사양 기능에 대한 지원이 추가되었습니다.|
|실행 계획|실행 계획 연산자 노드 아래에 실제 경과 시간, 실제 및 예상 행 수를 추가했습니다(사용할 수 있는 경우). 이렇게 하면 실제 계획이 활성 쿼리 통계 계획과 일관되게 표시됩니다.|
|실행 계획|실행 계획에 대한 쿼리 편집 단추를 클릭하면, 쿼리가 4000자를 넘을 경우 SQL 엔진이 실행 계획을 자를 수 있음을 사용자에게 표시하도록 도구 설명을 수정하고 주석을 추가했습니다.|
|실행 계획|“Materializer Operator(외부 Select)”를 표시하는 논리를 추가했습니다.|
|실행 계획|"batch-mode scan on rowstores" 기능을 사용하는 쿼리를 쉽게 식별할 수 있도록 새로운 실행 계획 특성 BatchModeOnRowStoreUsed를 추가합니다. 쿼리가 batch-mode scan on rowstores를 수행할 때마다 새 특성(BatchModeOnRowStoreUsed="true")이 StmtSimple 요소에 추가됩니다.|
|실행 계획|DW ROLLUP 및 CUBE에 대해 LocalCube RelOp에 실행 계획 지원이 추가되었습니다.|
|실행 계획|Azure SQL Data Warehouse의 새로운 ROLLUP 및 CUBE 집계 기능에 대한 새 LocalCube 연산자입니다.|
|SMO| 다시 시작 가능한 인덱스 생성을 위한 SMO 지원을 확장합니다.|
|SMO| SMO 개체에서 새 이벤트(“PropertyMissing”)를 추가하여 애플리케이션 작성자가 SMO 성능 문제를 더 빨리 감지할 수 있도록 했습니다.|
|SMO| "백업 체크섬 기본값" 서버 구성에 매핑되는 구성 개체에 대한 새로운 DefaultBackupChecksum 속성이 공개되었습니다.|
|SMO| 사용 중인 SQL 버전의 서비스 수준(예: CU12, RTM)에 매핑되는 서버 개체에 대한 새 ProductUpdateLevel 속성이 공개되었습니다.|
|SMO| "lastgoodcheckdbtime" 데이터베이스 속성에 매핑되는 데이터베이스 개체에 대한 새 LastGoodCheckDbTime 속성이 공개되었습니다. 해당 속성을 사용할 수 없는 경우 기본값인 1/1/1900 12:00:00 AM이 반환됩니다.|
|SMO|RegSrvr.xml 파일(등록된 서버 구성 파일)의 위치를 "%AppData%\Microsoft\SQL Server Management Studio"(버전이 지정되지 않은 경우 SSMS의 버전 간에 공유할 수 있음)로 이동했습니다.|
|SMO|"클라우드 감시"가 새 쿼럼 유형 및 새 리소스 종류로 추가되었습니다.|
|SMO|SMO 및 SSMS 모두에 "Edge 제약 조건" 지원이 추가되었습니다.|
|SMO|SMO 및 SSMS 모두에 "Edge 제약 조건"에 대한 계단식 삭제 지원이 추가되었습니다.|
|SMO|데이터 분류에 "읽기-쓰기" 권한에 대한 지원이 추가되었습니다.|
|취약성 평가| Azure SQL DW에서 취약성 평가 작업 메뉴를 사용할 수 있습니다.|
|취약성 평가|"취약성 평가" 검사 결과가 Azure SQL DB의 검사 결과와 일치하도록 Azure SQL Managed Instance 서버에서 실행되는 취약성 평가 규칙 세트가 변경되었습니다.|
|취약성 평가| "취약성 평가"는 이제 Azure SQL DW를 지원합니다.|
|취약성 평가|취약성 평가 검사 결과를 Excel로 내보내는 새로운 내보내기 기능이 추가되었습니다.|
|XEvent 뷰어|XEvent 뷰어: 더 많은 XEvent에 대한 실행 계획 창을 활성화합니다.|

### <a name="bug-fixes-in-180"></a>18.0의 버그 수정

| 새 항목| 세부 정보|
| :-------| :------|
|크래시 및 중지|GDI 개체와 관련된 일반적인 SSMS 크래시의 소스를 수정했습니다.|
|크래시 및 중지|"만들기/업데이트/삭제"로 스크립트를 선택할 때 반응이 없거나 성능이 저하되는 공통 소스를 수정했습니다(SMO 개체의 불필요한 페치를 제거함).|
|크래시 및 중지|ADAL 추적을 사용하는 동안 MFA를 사용하여 Azure SQL DB에 연결할 때 반응이 없는 문제를 해결했습니다.|
|크래시 및 중지|작업 모니터에서 호출하면 활성 쿼리 통계에서 반응이 없는(또는 인지된 반응 없음) 문제(“보안 정보 유지”가 설정되지 않은 SQL Server 인증을 사용할 때 발생하는 문제)를 해결했습니다.|
|크래시 및 중지|개체 탐색기에서 “보고서”를 선택할 때 반응이 없는 문제(리소스 연결 대기 시간이 길거나 일시적으로 리소스에 액세스할 수 없으면 발생하는 문제)를 해결했습니다.|
|크래시 및 중지|중앙 관리 서버 및 Azure SQL 서버를 사용하려고 할 때 SSSM에서 발생하는 충돌 문제가 해결되었습니다. 자세한 내용은 [중앙 관리 서버를 사용할 때 SMSS 17.5 애플리케이션 오류 및 충돌](https://feedback.azure.com/forums/908035/suggestions/33374884)을 참조하세요.|
|크래시 및 중지|IsFullTextEnabled 속성을 검색하는 방법을 최적화하여 개체 탐색기의 중단 문제가 해결되었습니다.|
|크래시 및 중지|불필요한 쿼리를 작성하여 데이터베이스 속성을 검색하지 않도록 방지하여 "데이터베이스 복사 마법사"의 중단 문제가 해결되었습니다.|
|크래시 및 중지|T-SQL을 편집하는 동안 SSMS가 중단/충돌하는 문제가 해결되었습니다.|
|크래시 및 중지|대규모 T-SQL 스크립트를 편집할 때 SSMS가 응답하지 않는 문제를 완화했습니다.|
|크래시 및 중지|쿼리에서 반환된 대규모 데이터 세트를 처리할 때 SSMS의 메모리 부족이 발생하는 문제가 해결되었습니다.|
|일반 SSMS|"등록된 서버"의 연결에서 "ApplicationIntent"가 전달되지 않는 문제가 해결되었습니다.|
|일반 SSMS|높은 DPI 모니터에서 "새 XEvent 세션 마법사 UI" 양식이 제대로 렌더링되지 않은 문제가 해결되었습니다.|
|일반 SSMS|bacpac 파일을 가져오려는 문제를 해결했습니다.|
|일반 SSMS|데이터베이스 속성(FILEGROWTH > 2048GB 포함)을 표시하려고 할 때 산술 오버플로 오류를 throw하는 문제가 해결되었습니다.|
|일반 SSMS|성능 대시보드 보고서가 하위 보고서에서 찾을 수 없는 PAGELATCH 및 PAGEIOLATCH 대기를 보고하는 문제가 해결되었습니다.|
|일반 SSMS|올바른 모니터에서 대화 상자를 열어 SSMS를 추가 다중 모니터로 인식하도록 하는 또 다른 수정 사항.|
|AS(Analysis Services)|AS XEvent UI에 대한 "고급 설정"이 잘리는 문제를 해결했습니다.|
|AS(Analysis Services)|DAX 구문 분석에서 파일을 찾을 수 없음 예외가 throw되는 문제가 해결되었습니다.|
|Azure SQL 데이터베이스|마스터 대신 Azure SQL DB에서 사용자 데이터베이스에 연결했을 때 Azure SQL Database 쿼리 창에 대해 데이터베이스 목록이 올바로 채워지지 않는 문제가 해결되었습니다.|
|Azure SQL 데이터베이스|Azure SQL 데이터베이스에 “임시 테이블”을 추가할 수 없는 문제가 해결되었습니다.|
|Azure SQL 데이터베이스|Azure의 통계 메뉴 아래에서 통계 속성 하위 메뉴 옵션을 사용하도록 설정했습니다. 이는 꽤 오랫동안 완벽하게 지원되었기 때문입니다.|
|Azure SQL - 일반 지원|일반적인 Azure UI 컨트롤에서 사용자가 Azure 구독(50개가 넘는 경우)을 표시하지 못하는 문제를 해결했습니다. 또한 정렬 기준이 구독 ID가 아니라 이름으로 변경되었습니다. 예를 들어, URL에서 백업을 복원하려 할 때 이 문제가 발생할 수 있습니다.|
|Azure SQL - 일반 지원|사용자의 일부 테넌트에 구독이 없는 경우 "인덱스가 범위를 벗어났습니다. 인덱스는 음수가 아니어야 하며 컬렉션의 크기보다 작아야 합니다”라는 오류를 발생시킬 수 있는 구독을 열거할 때 일반적인 Azure UI 컨트롤에 있는 문제를 해결했습니다. 예를 들어, URL에서 백업을 복원하려 할 때 이 문제가 발생할 수 있습니다.|
|Azure SQL - 일반 지원|서비스 수준 목표가 하드코딩되어 SSMS가 최신 Azure SQL SLO를 지원하기 어렵게 만드는 문제가 해결되었습니다. 이제 사용자는 Azure에 로그인하여 SSMS에서 모든 해당 SLO 데이터(버전 및 최대 크기)를 검색할 수 있습니다.|
|Azure SQL DB Managed Instance 지원|관리되는 인스턴스 지원을 개선했습니다. UI에서 지원되지 않는 옵션을 사용할 수 없도록 설정하고 URL 감사 대상을 처리하도록 [감사 로그 보기] 옵션을 수정했습니다.|
|Azure SQL DB Managed Instance 지원|“스크립트 생성 및 게시” 마법사는 지원되지 않는 CREATE DATABASE 절을 스크립팅합니다.|
|Azure SQL DB Managed Instance 지원|관리되는 인스턴스에 대한 라이브 쿼리 통계를 사용합니다.|
|Azure SQL DB Managed Instance 지원|데이터베이스 속성->파일이 ALTER DB ADD FILE을 잘못 스크립팅했습니다.|
|Azure SQL DB Managed Instance 지원|일부 다른 일정 유형을 선택한 경우에도 ONIDLE 일정 예약이 선택되는 SQL Agent 스케줄러의 재발 문제를 해결했습니다.|
|Azure SQL DB Managed Instance 지원|Azure Storage에서 백업을 수행하기 위해 MAXTRANSFERRATE, MAXBLOCKSIZE를 조정하는 중입니다.|
|Azure SQL DB Managed Instance 지원|RESTORE 작업(CL에서 지원되지 않음) 전에 비상 로그 백업이 스크립팅되는 문제.|
|Azure SQL DB Managed Instance 지원|데이터베이스 만들기 마법사가 CREATE DATABASE 문을 올바로 스크립팅하지 않습니다.|
|Azure SQL DB Managed Instance 지원|관리되는 인스턴스에 연결하는 경우 SSMS 내의 SSIS 패키지를 특별 처리합니다.|
|Azure SQL DB Managed Instance 지원|관리되는 인스턴스에 연결된 상태에서 “활동 모니터”를 사용하려 할 때 오류가 표시되는 문제를 해결했습니다.|
|Azure SQL DB Managed Instance 지원|SSMS 탐색기의 AAD 로그인 지원이 향상되었습니다.|
|Azure SQL DB Managed Instance 지원|SMO 파일 그룹 개체의 스크립팅이 향상되었습니다.|
|Azure SQL DB Managed Instance 지원|자격 증명에 대한 UI가 향상되었습니다.|
|Azure SQL DB Managed Instance 지원|논리적 복제 지원이 추가되었습니다.|
|Azure SQL DB Managed Instance 지원|데이터베이스를 마우스 오른쪽 단추로 클릭하고 '데이터 계층 애플리케이션 가져오기'를 선택하지 않는 문제가 해결되었습니다.|
|Azure SQL DB Managed Instance 지원|"TempDB"를 마우스 오른쪽 단추로 클릭하여 오류를 표시하는 문제가 해결되었습니다.|
|Azure SQL DB Managed Instance 지원|SMO에서 ALTER DB ADD FILE 문을 스크립팅하려고 할 때 생성된 T-SQL 스크립트가 비어 있는 문제가 해결되었습니다.|
|Azure SQL DB Managed Instance 지원|관리되는 인스턴스 서버별 속성(하드웨어 생성, 서비스 계층, 사용 및 예약된 스토리지)의 표시가 개선되었습니다.|
|Azure SQL DB Managed Instance 지원|데이터베이스의 스크립팅("생성 시 스크립팅...")이 추가 파일 그룹 및 파일을 스크립팅하지 않는 문제가 해결되었습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035/suggestions/37326799](https://feedback.azure.com/forums/908035/suggestions/37326799)를 참조하세요. |
|DB 백업/복원/연결/분리|.mdf 파일의 실제 파일 이름이 원래 파일 이름과 일치하지 않을 때 사용자가 데이터베이스를 연결할 수 없는 문제를 해결했습니다.|
|DB 백업/복원/연결/분리|SSMS가 유효한 복원 계획을 찾지 못하거나 최적이 아닌 계획을 찾을 수 있는 문제를 해결했습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752)를 참조하세요. |
|DB 백업/복원/연결/분리|"데이터베이스 연결" 마법사에서 이름이 변경된 보조 파일을 표시하지 않는 문제가 해결되었습니다. 이제 파일이 표시되며 이에 대한 주석(예: "찾을 수 없음")이 추가되었습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035/suggestions/32897434](https://feedback.azure.com/forums/908035/suggestions/32897434)를 참조하세요. |
|데이터베이스 복사 마법사|스크립트 생성/전송/데이터베이스 복사 마법사가 메모리 테이블이 있는 테이블을 만들려고 해도 ansi_padding이 강제 실행되지 않습니다.|
|데이터베이스 복사 마법사|SQL Server 2017 및 SQL Server 2019에서 데이터베이스 전송 작업/데이터베이스 복사 마법사가 중단되었습니다.|
|데이터베이스 복사 마법사|연결된 외부 데이터 원본을 만들기 전에 스크립트 생성/전송/데이터베이스 복사 마법사 스크립트 테이블을 생성합니다.|
|연결 대화 상자|DEL 키를 눌러 이전 사용자 이름 목록에서 사용자 이름을 제거할 수 있도록 했습니다. 자세한 내용은 [SSMS 로그인 창에서 사용자 삭제 허용](https://feedback.azure.com/forums/908035/suggestions/32897632)을 참조하세요.|
|DAC 가져오기 마법사|AAD를 사용하여 연결할 때 DAC 가져오기 마법사가 작동하지 않는 문제가 해결되었습니다.|
|데이터 분류|다른 데이터베이스에 다른 데이터 분류 창이 열려 있는 동안 데이터 분류 창에 분류를 저장할 때의 문제를 해결했습니다.|
|데이터 계층 애플리케이션 마법사|서버에 대한 액세스가 제한(예: 동일한 서버의 모든 데이터베이스에 액세스할 수 없음)되어 사용자가 데이터 계층 애플리케이션(.dacpac)을 가져올 수 없는 문제가 해결되었습니다.|
|데이터 계층 애플리케이션 마법사|많은 데이터베이스가 동일한 Azure SQL 서버에 호스팅될 때 가져오기가 매우 느려지는 문제가 해결되었습니다.|
|외부 테이블|템플릿, SMO, intellisense 및 속성 표에 있는 Rejected_Row_Location에 대한 지원이 추가되엇습니다.|
|플랫 파일 가져오기 마법사|“플랫 파일 가져오기 마법사”에서 큰따옴표를 올바로 처리(이스케이프)하지 않는 문제를 해결했습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035/suggestions/32897998](https://feedback.azure.com/forums/908035/suggestions/32897998)을 참조하세요. |
|플랫 파일 가져오기 마법사|부동 소수점 유형의 잘못된 처리(부동 소수점에 다른 구분 기호를 사용하는 로케일에서)와 관련된 문제를 해결했습니다.|
|플랫 파일 가져오기 마법사|값이 0 또는 1인 경우 비트를 가져오는 것과 관련된 문제를 해결했습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535)를 참조하세요. |
|플랫 파일 가져오기 마법사|*부동*이 *Null*로 입력되는 문제를 해결했습니다.|
|플랫 파일 가져오기 마법사|가져오기 마법사에서 음수 10진수 값을 처리할 수 없는 문제가 해결되었습니다.|
|플랫 파일 가져오기 마법사|마법사에서 단일 열 CSV 파일로부터 가져올 수 없는 문제가 해결되었습니다.|
|플랫 파일 가져오기 마법사|SSMS 17.9에 있음] 테이블이 이미 있는 경우 플랫 파일 가져오기에서 대상 테이블을 변경할 수 없는 문제가 해결되었습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186](https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186)을 참조하세요. |
|도움말 뷰어|온라인/오프라인 모드에 따라 논리가 개선되었습니다(해결해야 할 몇 가지 문제가 여전히 있을 수 있음).|
|도움말 뷰어|온라인/오프라인 설정을 사용하기 위한 "도움말 보기"를 수정했습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791)을 참조하세요. |
|HADR(고가용성 재해 복구)<BR> AG(가용성 그룹)|"장애 조치(faliover) 가용성 그룹" 마법사의 역할이 항상 "확인 중"으로 표시되는 문제가 해결되었습니다.|
|HADR(고가용성 재해 복구)<BR> AG(가용성 그룹)|SSMS의 "AG 대시보드"에서 잘린 경고가 표시되는 문제가 해결되었습니다.|
|Integration Services(IS)|SQL Server 2019 및 SSMS 18.0이 동일한 머신에 설치되어 있는 경우 배포 마법사에서 SQL Server에 연결하지 못하는 SxS 문제가 해결되었습니다.|
|Integration Services(IS)|유지 관리 계획을 설계할 때 유지 관리 계획 작업을 편집할 수 없는 문제가 해결되었습니다.|
|Integration Services(IS)|배포 중인 프로젝트의 이름이 바뀌면 배포 마법사가 중단되는 문제가 해결되었습니다.|
|Integration Services(IS)|Azure-SSIS IR 일정 기능에서 환경 설정을 사용하도록 설정되었습니다.|
|Integration Services(IS)|고객 계정이 둘 이상의 테넌트에 속할 때 SSIS Integration Runtime 만들기 마법사가 응답하지 않는 문제가 해결되었습니다.|
|작업 활동 모니터|작업 활동 모니터(필터 포함)를 사용하는 동안 발생하는 작업 중단 문제를 해결했습니다.|
|개체 탐색기|SSMS가 OE(잘못 구성된 DataCollector)에서 "관리" 노드를 확장하려고 할 때 "DBNull에서 다른 형식으로 개체를 캐스트할 수 없음" 예외를 throw하는 문제를 해결했습니다.|
|개체 탐색기|"상위 N 편집..."을 호출하기 전에 OE가 따옴표를 이스케이프 처리하지 않아 디자이너가 혼동하게 되는 문제가 해결되었습니다.|
|개체 탐색기|“데이터 계층 애플리케이션 가져오기” 마법사가 Azure Storage 트리에서 시작되지 않던 문제를 해결했습니다.|
|개체 탐색기|SSL 확인란의 상태가 지속되지 않은 "데이터베이스 메일 구성"의 문제가 해결되었습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541](https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541)을 참조하세요. |
|개체 탐색기|SSMS가 is_auto_update_stats_async_on으로 데이터베이스를 복원하려고 할 때 기존 연결을 닫는 옵션을 회색으로 표시하는 문제를 해결했습니다.|
|개체 탐색기|OE에서 노드(예: "테이블")를 마우스 오른쪽 단추로 클릭하고 필터 > 필터 설정으로 차례로 이동하여 테이블 필터링과 같은 작업을 수행하려고 하면 SSMS가 현재 활성화된 위치 이외의 다른 화면에 필터 설정 양식이 나타날 수 있는 문제가 해결되었습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106](https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106)를 참조하세요. |
|개체 탐색기|개체의 이름을 바꾸려고 할 때 OE에서 DELETE 키가 작동하지 않는 오랫동안 미해결 상태였던 문제를 해결했습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/33073510](https://feedback.azure.com/forums/908035-sql-server/suggestions/33073510), [https://feedback.azure.com/forums/908035/suggestions/32910247](https://feedback.azure.com/forums/908035/suggestions/32910247) 및 기타 중복 항목을 참조하세요.|
|개체 탐색기|기존 데이터베이스 파일의 속성을 표시할 때 새 데이터베이스를 생성할 때 표시되는 “처음 크기(MB)” 대신 “크기(MB)” 열 아래에 크기가 나타납니다. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/32629024](https://feedback.azure.com/forums/908035-sql-server/suggestions/32629024)를 참조하세요. |
|개체 탐색기|“Graph 테이블”의 “디자인” 상황에 맞는 메뉴 항목을 사용하지 않도록 설정했습니다. 현재 버전의 SSMS에서 해당 유형의 테이블을 지원하지 않기 때문입니다.|
|개체 탐색기|높은 DPI 모니터에서 "새 작업 일정" 대화 상자가 제대로 렌더링되지 않는 문제가 해결되었습니다. 자세한 내용은 [https://feedback.azure.com/admin/v3/suggestions/35541262](https://feedback.azure.com/admin/v3/suggestions/35541262)를 참조하세요. |
|개체 탐색기|데이터베이스 크기("크기(MB)")가 개체 탐색기 세부 정보에 표시되는 문제 수정/개선: 2자리 소수점 십진수만 사용하고, 형식은 천 단위 구분 기호로 지정됩니다. 자세한 내용은 [https://feedback.azure.com/forums/908035/suggestions/34379308](https://feedback.azure.com/forums/908035/suggestions/34379308)을 참조하세요.|
|개체 탐색기|"이 작업을 수행하려면 PartitionScheme 속성을 설정하세요"와 같은 오류로 인해 "공간 인덱스"를 만드는 데 실패하는 문제가 해결되었습니다.|
|개체 탐색기|가능한 경우 추가 쿼리를 실행하지 않도록 방지하여 개체 탐색기의 성능이 약간 향상되었습니다.|
|개체 탐색기|데이터베이스 이름을 모든 스키마 개체로 변경할 때 확인을 요청하는 논리가 확장되었습니다(설정을 구성할 수 있음).|
|개체 탐색기|개체 탐색기 필터링에 적절한 이스케이프를 추가했습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035/suggestions/36678803](https://feedback.azure.com/forums/908035/suggestions/36678803)을 참조하세요. |
|개체 탐색기|적절한 구분 기호가 있는 숫자를 표시하도록 개체 탐색기 정보의 보기를 수정/개선했습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035/suggestions/32900944](https://feedback.azure.com/forums/908035/suggestions/32900944)를 참조하세요. |
|개체 탐색기|"New" 플라이아웃이 누락되었고, Graph 테이블이 잘못 나열되었으며, System-Versioned 테이블이 누락된 SQL Express에 연결했을 때 "테이블" 노드의 컨텍스트 메뉴 문제가 해결되었습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035/suggestions/37245529](https://feedback.azure.com/forums/908035/suggestions/37245529)를 참조하세요. |
|개체 스크립팅|전체 성능 개선 사항 - WideWorldImporters 스크립트 생성 시간은 SSMS 17.7과 비교하여 반 정도 소요됩니다.|
|개체 스크립팅|개체를 스크립팅할 때 기본값이 있는 DB 범위 지정 구성이 생략됩니다.|
|개체 스크립팅|스크립팅 시 동적 T-SQL을 생성하지 마세요. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391)을 참조하세요. |
|개체 스크립팅|SQL Server 2016 및 그 이전 버전에서 테이블을 스크립팅할 때 그래프 구문 “as edge” 및 “as node”를 생략하세요.|
|개체 스크립팅|MFA와 함께 AAD를 사용하여 Azure SQL DB에 연결할 때 데이터베이스 개체의 스크립팅이 실패하는 문제를 해결했습니다.|
|개체 스크립팅|Azure SQL DB에서 GEOMETRY_AUTO_GRID/GEOGRAPHY_AUTO_GRID를 사용하여 공간 인덱스를 스크립팅하려고 할 때 오류가 throw되는 문제를 해결했습니다.|
|개체 스크립팅|"개체 탐색기" 스크립팅 설정이 원본과 일치하도록 설정되어 있는 경우에도 SQL Azure 데이터베이스의 데이터베이스 스크립팅이 항상 온-프레미스 SQL을 대상으로 하는 문제가 해결되었습니다.|
|개체 스크립팅|클러스터형 및 비클러스터형 인덱스와 관련된 SQL DW 데이터베이스의 테이블을 스크립팅하려고 할 때 잘못된 T-SQL 문이 생성되는 문제가 해결되었습니다.|
|개체 스크립팅|"클러스터형 Columnstore 인덱스"와 "클러스터형 인덱스"를 모두 사용하여 SQL DW 데이터베이스의 테이블을 스크립팅하려고 할 때 잘못된 T-SQL(중복 문)이 생성되는 문제가 해결되었습니다.|
|개체 스크립팅|범위 값이 없는 분할된 테이블(SQL DW 데이터베이스) 스크립팅 문제가 해결되었습니다.|
|개체 스크립팅|사용자가 감사/감사 사양 SERVER_PERMISSION_CHANGE_GROUP을 스크립팅할 수 없는 문제가 해결되었습니다.|
|개체 스크립팅|사용자가 SQL DW에서 통계를 스크립팅할 수 없는 문제가 해결되었습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897296](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897296)을 참조하세요. |
|개체 스크립팅|"오류 시 스크립팅 계속 진행"이 false로 설정된 경우 "스크립트 생성 마법사"에 스크립팅 오류가 있는 잘못된 테이블이 표시되는 문제가 해결되었습니다.|
|개체 스크립팅|SQL Server 2019에서 향상된 스크립트를 생성합니다.|
|프로파일러|프로파일러 이벤트에 "집계 테이블 다시 쓰기 쿼리" 이벤트를 추가했습니다.|
|쿼리 데이터 저장소|"DocumentFrame(SQLEditors)" 예외가 throw될 수 있는 문제를 해결했습니다.|
|쿼리 데이터 저장소|기본 제공 쿼리 저장소에서 사용자 지정 시간 간격을 설정하려고 할 때 사용자가 시작/종료 간격에 AM 또는 PM을 선택할 수 없음을 보고하는 문제를 해결했습니다.|
|결과 표|선택한 행 번호가 고대비 모드에서 표시되지 않는 문제를 해결했습니다.|
|결과 표|그리드를 클릭할 때 "범위를 벗어난 인덱스" 예외가 발생하는 문제가 해결되었습니다.|
|결과 표|그리드 결과 배경색이 무시되는 문제가 해결되었습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035/suggestions/32895916](https://feedback.azure.com/forums/908035/suggestions/32895916)을 참조하세요. |
|실행 계획|둘 이상의 스레드가 있는 경우 새 메모리 부여 연산자 속성이 잘못 표시됩니다.|
|실행 계획|실제 실행 xml 계획의 RunTimeCountersPerThread에 다음과 같은 4개의 특성을 추가합니다. HpcRowCount(hpc 디바이스에서 처리된 행 수), HpcKernelElapsedUs(사용 중인 커널 실행에 대해 경과된 시간 대기), HpcHostToDeviceBytes (호스트에서 디바이스로 전송된 바이트) 및 HpcDeviceToHostBytes (디바이스에서 호스트로 전송된 바이트).|
|실행 계획|유사한 계획 노드가 잘못된 위치에서 강조 표시되는 문제가 해결되었습니다.|
|SMO|SMO/ServerConnection이 SqlCredential 기반 연결을 올바르게 설정하지 않는 문제를 해결했습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941](https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941)을 참조하세요. |
|SMO|SMO를 사용하여 작성된 애플리케이션이 각 스레드에서 별도의 SqlConnection 인스턴스를 사용하더라도 여러 스레드에서 동일한 서버의 데이터베이스를 열거하려고 할 때 오류가 발생하는 문제를 해결했습니다.|
|SMO|외부 테이블의 전송에서 발생하는 성능 회귀 문제가 해결되었습니다.|
|SMO|Azure를 대상으로 할 때 SMO에서 SqlConnection 인스턴스가 누수된 ServerConnection 스레드 안전성 문제가 해결되었습니다.|
|SMO|해당 이름에 중괄호가 있는 데이터베이스를 복원하려고 할 때 StringBuilder.FormatError가 발생하는 문제가 해결되었습니다.|
|SMO|SMO의 Azure 데이터베이스가 데이터베이스에 대해 지정된 데이터 정렬을 사용하는 대신 모든 문자열 비교에 대해 대/소문자 구분 없는 데이터 정렬을 기본값으로 설정하는 문제가 해결되었습니다.|
|SSMS 편집기|기본 색상을 복원하는 "SQL 시스템 테이블"이 기본 녹색이 아니라 라임 녹색으로 변경되어 흰색 배경에서 읽기가 어려워지는 문제가 해결되었습니다. 자세한 내용은 [SQL 시스템 테이블에 대한 잘못된 기본 색 복원](https://feedback.azure.com/forums/908035-sql-server/suggestions/32896906)을 참조하세요. 영어가 아닌 버전의 SSMS에서 문제가 여전히 발생합니다.|
|SSMS 편집기|AAD 인증을 사용하여 Azure SQLDW에 연결할 때 intellisense가 작동하지 않는 문제를 해결했습니다.|
|SSMS 편집기|사용자가 **마스터** 데이터베이스에 액세스할 수 없을 때 Azure의 intellisense에 발생하는 문제를 해결했습니다.|
|SSMS 편집기|대상 데이터베이스의 데이터 정렬이 대/소문자를 구분할 때 손상되던 "임시 테이블"을 만드는 코드 조각이 수정되었습니다.|
|SSMS 편집기|새 TRANSLATE 함수는 이제 intellisense에 의해 인식됩니다. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898430](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898430)을 참조하세요. |
|SSMS 편집기|FORMAT 기본 제공 함수에서 향상된 intellisense. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898676](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898676)을 참조하세요. |
|SSMS 편집기|LAG 및 LEAD는 이제 기본 제공 함수로 인식됩니다. 자세한 내용은 [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898757](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898757)을 참조하세요. |
|SSMS 편집기|"ALTER TABLE...ADD CONSTRAINT...WITH(ONLINE=ON)"를 사용하는 경우 intellisense가 경고를 표시하는 문제를 해결했습니다.|
|SSMS 편집기|여러 시스템 뷰 및 테이블 값 기능의 색상이 제대로 지정되지 않는 문제가 해결되었습니다.|
|SSMS 편집기|편집기 탭을 클릭하면 포커스를 가져오는 대신 탭이 닫힐 수 있는 문제가 해결되었습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035/suggestions/37291114](https://feedback.azure.com/forums/908035/suggestions/37291114)를 참조하세요. |
|SSMS 옵션|**도구** > **옵션** > **SQL Server 개체 탐색기** > **명령** 페이지의 크기가 제대로 조정되지 않는 문제를 해결했습니다.|
|SSMS 옵션|SSMS는 이제 기본적으로 XMLA 편집기에서 DTD의 자동 다운로드를 비활성합니다. XMLA 스크립트 편집기(xml 언어 서비스를 사용)는 잠재적으로 악의적인 xmla 파일에 대한 DTD를 자동으로 다운로드하지 못하도록 차단합니다. 이는 **도구** > **옵션** > **환경** > **텍스트 편집기** > **XML** > **기타**에서 “자동으로 DTD 및 스키마 다운로드” 설정을 해제하여 제어합니다.|
|SSMS 옵션|이전 버전의 SSMS에서 사용되었던 것처럼 바로 가기로 **CTRL+D**가 복원되었습니다. 자세한 내용은 [https://feedback.azure.com/forums/908035/suggestions/35544754](https://feedback.azure.com/forums/908035/suggestions/35544754)를 참조하세요. |
|테이블 디자이너|“200행 편집”의 작동 중단 문제를 수정했습니다.|
|테이블 디자이너|Azure SQL Database에 연결되면 디자이너가 테이블을 추가할 수 있는 문제를 해결했습니다.|
|취약성 평가|검색 결과가 제대로 로드되지 않는 문제가 해결되었습니다.|
|XEvent|작업 ID 및 클래스 유형 필드를 읽기 가능한 문자열로 표시하는 두 개의 열, 즉 "action_name" 및 "class_type_desc" 열이 추가되었습니다.|
|XEvent|이벤트 1,000,000개라는 이벤트 XEvent 뷰어 상한을 제거했습니다.|
|XEvent 프로파일러|96-코어 SQL Server에 연결할 때 XEvent 프로파일러가 실행되지 않는 문제를 해결했습니다.|
|XEvent 뷰어|"확장 이벤트 도구 모음 옵션"을 사용하여 이벤트를 그룹화할 때 XEvent 뷰어가 충돌하는 문제가 해결되었습니다.|

### <a name="deprecated-and-removed-features-in-180"></a>18.0에서 사용되지 않고 제거된 기능

사용되지 않거나 제거된 기능
- T-SQL 디버거
- 데이터베이스 다이어그램
- 다음 도구는 더 이상 SSMS와 함께 설치되지 않습니다.
  - OSQL.EXE
  - DReplay.exe
  - SQLdiag.exe
  - SSBDiagnose.exe
  - bcp.exe
  - sqlcmd.exe
- 구성 관리자 도구:
  - SQL Server 구성 관리자 및 Reporting Server 구성 관리자가 모두 더 이상 SSMS 설정의 일부가 아닙니다.
- DMF 표준 정책
  - 정책이 더 이상 SSMS와 함께 설치되지 않으며 Git으로 이동하게 됩니다. 필요한 경우 참여하고 다운로드/설치할 수 있습니다.
- -P SSMS 명령줄 옵션이 제거됨
  - 보안상의 이유로 명령줄에서 일반 텍스트 암호를 지정하는 옵션이 제거되었습니다.
- 스크립트 생성 > 웹 서비스에 게시가 제거됨
  - 사용되지 않는 이 기능은 SSMS UI에서 제거되었습니다.
- 개체 탐색기에서 "유지 관리 > 레거시" 노드를 제거했습니다.
  - 매우 오래된 "데이터베이스 유지 관리 계획" 및 "SQL 메일" 노드에 더 이상 액세스할 수 없습니다. 최신 “데이터베이스 메일” 및 “유지 관리 계획” 노드는 계속해서 정상적으로 작동합니다.

### <a name="known-issues-180"></a>알려진 문제(18.0)

- SQL Server Management Studio를 실행할 수 없는 버전 18.0 설치 문제가 해결되었습니다. 이 문제가 발생하는 경우 [SSMS2018 - 설치되었지만 실행되지 않음](https://feedback.azure.com/forums/908035-sql-server/suggestions/37502512-ssms2018-installed-but-will-not-run) 문서의 단계를 따르세요.

- SSMS 결과에서 표시되는 데이터의 크기에는 그리드, 텍스트 또는 파일로 표시되는 제한 사항이 있습니다.

## <a name="downloadssdtmediadownloadpng-ssms-1791httpsgomicrosoftcomfwlinklinkid2043154clcid0x409"></a>![다운로드](../ssdt/media/download.png) [SSMS 17.9.1](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409)

- 릴리스 번호: 17.9.1<br>
- 빌드 번호: 14.0.17289.0<br>
- 릴리스 날짜: 2018년 11월 21일

17.9.1은 17.9의 작은 업데이트로 다음과 같은 버그가 수정되었습니다.

- SQL 쿼리 편집기에서 "Azure Active Directory - MFA 지원을 통한 유니버설" 인증을 사용하는 경우 쿼리를 호출할 때마다 연결이 종료되었다가 다시 시작되는 문제가 수정되었습니다. 연결 닫힘으로 인해 글로벌 임시 테이블이 예기치 않게 삭제되고, 연결에 새 SPID가 부여되는 등의 부작용이 발생합니다.
- 복원 계획이 복원 계획을 찾지 못하거나 특정 조건에서 비효율적인 복원 계획을 생성하는 장기 미해결 문제가 수정되었습니다.
- "데이터 계층 애플리케이션 가져오기" 마법사에서 Azure SQL 데이터베이스에 연결할 때 오류가 발생할 수 있는 문제가 수정되었습니다.

> [!NOTE]
> 영어 이외의 지역화된 SSMS 17.x 릴리스를 다음 위치에 설치하는 경우 [KB 2862966 보안 업데이트 패키지](https://support.microsoft.com/kb/2862966)가 필요합니다. Windows 8, Windows 7, Windows Server 2012 및 Windows Server 2008 R2.

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x804)| [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x404)| [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409)| [프랑스어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40c)| [독일어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x407)| [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x410)| [일본어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x411)| [한국어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x412)| [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x416)| [러시아어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x419)| [스페인어](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40a)

## <a name="downloadssdtmediadownloadpng-ssms-1653httpsgomicrosoftcomfwlinklinkid840946"></a>[SSMS 16.5.3](https://go.microsoft.com/fwlink/?LinkID=840946) ![다운로드](../ssdt/media/download.png)
일반 공급 | 빌드 번호: 13.0.16106.4

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804)| [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404)| [영어(미국)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409)| [프랑스어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c)| [독일어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407)| [이탈리아어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410)| [일본어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411)| [한국어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412)| [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416)| [러시아어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419)| [스페인어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)

이 릴리스에서는 다음과 같은 문제가 해결되었습니다.

* 테이블에 스파스 열이 둘 이상 있을 때 'Table' 노드의 확장을 일으키는 SSMS 16.5.2의 문제가 해결되었습니다.

* 사용자가 Microsoft Dynamics AX/CRM Online 리소스에 연결되는 OData 연결 관리자를 포함하는 SSIS 패키지를 SSIS 카탈로그에 배포할 수 있습니다. 자세한 내용은 [OData 연결 관리자](../integration-services/connection-manager/odata-connection-manager.md)를 참조하세요.

* 기존 테이블에 대한 Always Encrypted 구성이 관련 없는 개체에 대한 오류와 함께 실패함. [Connect ID 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* 여러 스키마가 포함된 기존 데이터베이스에 대한 Always Encrypted 구성이 작동하지 않음. [Connect ID 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* Always Encrypted, 암호화된 열 마법사가 시스템 뷰를 참조하는 뷰를 포함하는 데이터베이스로 인해 실패함. [Connect ID 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* Always Encrypted를 사용하여 암호화할 때 암호화가 잘못 처리된 후 모듈을 새로 고치지 못하는 오류가 발생함.

* *최근에 사용한 항목 열기* 메뉴에 최근에 저장한 파일이 표시되지 않음. [Connect ID 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* 원격(인터넷) 연결을 통해 테이블의 인덱스를 마우스 오른쪽 단추로 클릭할 경우 SSMS가 느려짐. [Connect ID 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)

* SQL 디자이너 스크롤 막대 관련 문제를 해결함. [Connect ID 3114856](https://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* 테이블의 상황에 맞는 메뉴가 잠시 중단됨 
 
* SSMS에서 가끔 [작업 모니터]에서 예외를 발생시키고 작동을 중단함. [Connect ID 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016이 "The process was terminated due to an internal error in the .NET Runtime at IP 71AF8579 (71AE0000) with exit code 80131506"(.NET 런타임의 IP 71AF8579(71AE0000)에서 내부 오류로 인해 프로세스가 종료되었습니다(종료 코드 80131506).) 오류와 함께 작동이 중단됨


## <a name="uninstall-and-reinstall-ssms-17x"></a>SSMS 17.x 제거 및 다시 설치

SSMS 설치에 문제가 있고, 표준 제거 및 다시 설치로 해결되지 않는 경우 먼저 Visual Studio 2015 IsoShell을 [복구](https://support.microsoft.com/help/4028054/windows-10-repair-or-remove-programs)해 볼 수 있습니다. Visual Studio 2015 IsoShell을 복구해도 문제가 해결되지 않으면 다음 단계에서 여러 가지 해결해야 할 임의의 문제를 발견합니다.

1. 애플리케이션을 제거한 것과 동일한 방식으로 SSMS를 제거합니다(사용자의 Windows 버전에 따라 *앱 및 기능*, *프로그램 및 기능* 사용).

2. **관리자 권한 cmd 프롬프트에서** Visual Studio 2015 IsoShell을 제거합니다.

    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```

    ```vs_isoshell.exe /Uninstall /Force /PromptRestart```

3. 애플리케이션을 제거하는 것과 동일한 방식으로 Microsoft Visual C++ 2015 재배포 가능 패키지를 제거합니다. x86 및 x64 버전이 컴퓨터에 설치되어 있으면 모두 제거합니다.

4. **관리자 권한 cmd 프롬프트에서** Visual Studio 2015 IsoShell을 다시 설치합니다.  

    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```  

    ```vs_isoshell.exe /PromptRestart```

5. SSMS를 다시 설치합니다.

6. 현재 최신 상태가 아닌 경우 [최신 버전의 Visual C++ 2015 재배포 가능 패키지](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)로 업그레이드합니다.

## <a name="additional-downloads"></a>추가 다운로드

모든 SQL Server Management Studio 다운로드의 전체 목록은 [Microsoft 다운로드 센터](https://www.microsoft.com/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending)를 검색하세요.  
  
최신 SQL Server Management Studio에 대한 자세한 내용은 [SQL Server Management Studio 다운로드&#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.  
