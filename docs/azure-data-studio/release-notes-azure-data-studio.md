---
title: 릴리스 정보
titleSuffix: Azure Data Studio
description: Azure Data Studio 릴리스 정보
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 06/06/2019
ms.openlocfilehash: 6e2d4ff6e300290381f75ff4ab984743d7ea106e
ms.sourcegitcommit: cc4651df495920413ad54f585dbbe5ccef728899
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749150"
---
# <a name="release-notes-for-azure-data-studio"></a>Azure Data Studio에 대 한 릴리스 정보

**[다운로드 하 고 최신 릴리스를 설치!](download.md)**

## <a name="june-2019"></a>2019 년 6 월

2019 년 6 월 6 일 &nbsp;  /  &nbsp; 버전: 1.8.0 

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 중앙 관리 서버 (CMS) 확장의 릴리스 | 중앙 관리 서버에는 하나 이상의 중앙 관리 서버 그룹으로 구성 된 SQL server 인스턴스 목록을 저장 합니다. 사용자는 자신의 기존 CMS 서버에 연결 하 고 추가 서버를 제거 하는 등 해당 서버를 관리할 수 있습니다. 자세한 내용은 읽어보세요 [여기](https://docs.microsoft.com/sql/relational-databases/administer-multiple-servers-using-central-management-servers) |
| Windows에 대 한 데이터베이스 관리 도구 확장의 릴리스 | 이 확장에 두 Azure 데이터 Studio에서 SQL Server Management Studio에서 자주 사용 하는 환경을 시작합니다. 사용자 수 많은 다른 개체 (예: 데이터베이스, 테이블, 열, 뷰 등)을 마우스 오른쪽 단추로 클릭 하 고 속성을 해당 개체에 대 한 SSMS 속성 대화 상자를 선택 합니다. 또한 사용자 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 잘 알려진 SSMS 스크립트 생성 마법사를 시작 하려면 스크립트 생성을 선택할 수 있습니다. 
| 스키마 비교 개선 | &bull; &nbsp; 추가 제외/포함 옵션 <br/>&bull; &nbsp; 생성 후 스크립트 열립니다 스크립트를 생성 합니다. <br/>&bull; &nbsp; 이중 스크롤 막대를 제거합니다.  <br/>&bull; &nbsp; 서식 및 레이아웃 개선 <br/>&bull; &nbsp; 전체 변경 내용을 확인할 수 있습니다 [여기](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22June+2019+Release%22+label%3A%22Area%3A+Schema+Compare%22+is%3Aclosed)|
| 사용자 탭으로 이동된 Messages 섹션 | SQL 쿼리를 실행 하는 사용자가 결과 및 메시지 누적된 패널에 있었습니다. 이제 SSMS에서 같은 패널에 별도 탭에는 합니다. |
| SQL 전자 필기장 개선 사항 | &bull; &nbsp; 사용자가 이제 노트북에서 자신의 Python 3 또는 Anaconda 설치를 사용 하도록 선택할 수 있습니다. <br/>&bull; &nbsp; 여러 안정성 + 맞춤/완료 픽스 &bull; &nbsp; 개선의 전체 목록을 보려면 [여기](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22June+2019+Release%22+is%3Aclosed+label%3A%22Area%3A+Notebooks%22)|
| Visual Studio Code 1.34 병합을 해제할 수 있습니다. | 향상 된 최신 버전을 찾을 수 있습니다 [여기](https://code.visualstudio.com/updates/v1_34) |
| 해결 된 버그 및 문제입니다. | 참조 [버그 및 GitHub에서 문제](https://github.com/microsoft/azuredatastudio/milestone/32?closed=1)합니다. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제
- Windows에 대 한 데이터베이스 관리 도구 확장
    - 연결이 끊어진된 서버 노드에서 속성을 시작할 수 없습니다.
    - Azure 서버에 대 한 속성을 시작할 수 없습니다.
    - 일부 개체에 속성 대화 상자
    - 대화 상자를 시작 하는 데 시간이 오래 걸릴
    - 일부 유형의 연결 (예: AAD)를 사용 하 여 서버를 시작 하는 오류
- 전자 필기장
    - [5838](https://github.com/microsoft/azuredatastudio/issues/5838) 시스템 Python Notebook을 사용 하는 작업을 할 수 있습니다.
- 스키마 비교
    - [5804](https://github.com/microsoft/azuredatastudio/issues/5804) 스키마 비교 작업에는 아무 작업도 수행 하지는 기본 취소 상황에 맞는 메뉴 표시

## <a name="may-2019"></a>2019년 5월

2019 년 5 월 8 일 &nbsp;  /  &nbsp; 버전: 1.7.0 

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 스키마 비교 확장 릴리스 | 스키마 비교는 SQL Server 데이터 도구 (SSDT)에서 잘 알려진 기능 및 해당 기본 사용 사례 이며를 비교 하 여 데이터베이스 및.dacpac 파일 간의 차이점을 시각화할 수 있도록 동일한 작업을 실행 합니다. |
| 작업 보기 출력 창으로 이동 | 사용자가 출력 창에서 작업 보기에서 백업, 복원 및 스키마 비교 등의 장기 실행 작업의 상태를 볼 수 있습니다.
| 추가 시작 페이지 | &bull; &nbsp; 일반적인 작업에 대 한 링크 같은 새 쿼리를 새 파일을 새 노트북 <br/>&bull; &nbsp; 설명서 및 GitHub에 대 한 링크 |
| SQL 전자 필기장 개선 사항 | &bull; &nbsp; 메모 및 테이블에 대 한 더 나은 지원을 비롯 하 여 markdown 렌더링 향상 된 기능 <br/>&bull; &nbsp; 도구 모음 유용성 개선 <br/>&bull; &nbsp; 더 이상 신뢰할 수 있는 notebook에 대 한 markdown 링크 Cmd/Ctrl + 클릭 하며 직접 클릭할 수 있습니다. <br/>&bull; &nbsp; Notebook을 닫고 동시에 여러 notebook을 시작할 때 오류를 줄이고 후 Jupyter 프로세스 정리의 향상 된 기능 <br/>&bull; &nbsp; 동일한 데이터베이스에 대해 2 notebook을 실행 하는 경우 향상 된 SQL notebook 연결 오류 발생 하지 않습니다. <br/>&bull; &nbsp; 도구 모음에서 셀 실행 단추를 클릭 하면 현재 실행 중인 셀에 노트북 자동 스크롤의 향상 된 기능 <br/>&bull; &nbsp; 일반 안정성 및 성능 향상 |
| 해결 된 버그 및 문제입니다. | 참조 [버그 및 GitHub에서 문제](https://github.com/microsoft/azuredatastudio/milestone/31?closed=1)합니다. |
| &nbsp; | &nbsp; |

## <a name="april-2019"></a>2019년 4월

2019 년 4 월 18 일 &nbsp;  /  &nbsp; 버전: 1.6.0 

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 이름을 바꿀 **서버** 탭을 **연결** | |
| Azure 리소스 탐색기는 Azure viewlet 연결에서로 이동 | 이제 사용자가 연결 보기에서 Azure viewlet 통해 자신의 Azure SQL 인스턴스를 볼 수 있으며 각 서버 또는 데이터베이스에서 개체를 보려면 확장.|
| SQL 전자 필기장 개선 사항 | &bull; &nbsp; 모든 셀에 대 한 출력을 지우려면 도구 모음에서 추가 단추 <br/>&bull; &nbsp; 모든 셀을 실행 하려면 도구 모음의 추가 단추 <br/>&bull; &nbsp; 서버 이름 대신 고정된 연결 이름 (하는 경우 설정) 드롭다운에 연결 <br/>&bull; &nbsp; 상대 이미지 경로 사용 하는 경우 렌더링 되지 않는 markdown에서 이미지에 대 한 수정 <br/>&bull; &nbsp; 향상 된 기능을 추가 하 여 notebook 표가 자동으로 조정 열 크기를 두 번 클릭 및 마우스 휠을 지원 향상 <br/>&bull; &nbsp; 향상 된 오류 처리 및 python notebook 통해 python을 설치 하는 경우 복원 력을 설치합니다 <br/>&bull; &nbsp; Notebook 셀을 선택 하는 경우 "모두 선택" 기능 향상 <br/>&bull; &nbsp; Notebook을 닫고는 개체 탐색기 연결에 영향을 주지 않으려면 notebook 연결의 향상 된 기능 <br/>&bull; &nbsp; Notebook의 연결이 끊어지고 셀을 실행 하는 연결이 필요한 경우 사용자에 게 메시지를 표시 하려면 향상 된 전자 필기장 환경<br/>&bull; &nbsp; 광고를 다시 시작할 때 광고에서 리하이드레이션 하는 저장 되지 않은 전자 필기장에 대 한 향상 된 지원 |
| 해결 된 버그 및 문제입니다. | 참조 [버그 및 GitHub에서 문제](https://github.com/Microsoft/azuredatastudio/milestone/26?closed=1)합니다. |
| &nbsp; | &nbsp; |

## <a name="march-2019-hotfix"></a>3 월 2019 (핫픽스)

2019 년 3 월 22 일 &nbsp;  /  &nbsp; 버전: 1.5.2 &nbsp;  /  &nbsp; 핫픽스 릴리스

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 1.5.1 발견 된 몇 가지 문제를 해결 합니다. | 참조 [GitHub에서 핫픽스 릴리스 년 3 월](https://github.com/Microsoft/azuredatastudio/milestone/28)합니다.<br/> <br/>&bull; &nbsp; 사용자 전자 필기장 대시보드에서 "전자 필기장 열기" 작업에서 열에 닫지 못했습니다 문제 해결된 <br/>&bull; &nbsp; Notebook JSON 추가 있는 문제를 해결 함} 저장 후 <br/>&bull; &nbsp; 여기서 notebook 표 된 테마 변경에 응답 하지 문제 해결된 <br/>&bull; &nbsp; 전체 notebook 경로 탭 헤더에 표시 된 위치에 문제를 해결 합니다. 이제 파일 이름만 표시 됩니다. |
| &nbsp; | &nbsp; |

## <a name="march-2019"></a>2019 년 3 월

2019 년 3 월 18 일 &nbsp;  /  &nbsp; 버전: 1.5.1

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 추가 [Azure Data Studio 용 PostgreSQL 확장](postgres-extension.md) | 지원 되는 기능: <br/>&bull; &nbsp; 연결 대화 상자 <br/>&bull; &nbsp; 개체 탐색기 <br/>&bull; &nbsp; Query Editor <br/>&bull; &nbsp; 차트 <br/>&bull; &nbsp; 대시보드 <br/>&bull; &nbsp; 코드 조각 <br/>&bull; &nbsp; Edit Data <br/>&bull; &nbsp; Notebooks |
| 추가 SQL Notebook | 기본 제공 전자 필기장 뷰어에 대 한 SQL 커널 지원이 추가 되었습니다. <br/>&bull; &nbsp; 지원 T-SQL <br/>&bull; &nbsp; PGSQL 지원 |
| 추가 PowerShell 확장  | 통해 제공 합니다 [PowerShell 확장](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell) VS Code에서 발생 합니다.  |
| 추가 SQL Server dacpac 확장  | 새 확장으로 SQL Server 가져오기 확장에서 데이터 계층 응용 프로그램 마법사를 제거합니다.  |
| 추가 커뮤니티 확장 QueryPlan.show | 쿼리 계획을 시각화 하는 통합 지원을 추가합니다  |
| 업데이트 된 SQL Server 2019 미리 보기 확장 | &bull; &nbsp; Jupyter Notebook 지원, 특히 Python3 및 Spark 커널에는 핵심 Azure Data Studio 도구에 옮겼습니다. <br/>&bull; &nbsp; 외부 데이터 마법사의 버그 수정  |
| 해결 된 버그 및 문제입니다. | 참조 [버그 및 GitHub에서 문제](https://github.com/Microsoft/azuredatastudio/milestone/25?closed=1)합니다. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제
- [#4427](https://github.com/Microsoft/azuredatastudio/issues/4427): 준비는 셀 전 커널 실행을 클릭 하면 심각한 오류에서 결과 Spark **해결 방법:** 모든 셀을 실행 하기 전에 커널에서 로드 될 때까지 대기
- [#4493](https://github.com/Microsoft/azuredatastudio/issues/4493): SQL 인증-암호에 대 한 사용자 프롬프트를 사용 하 여 SSMS에서 시작 하는 광고 **해결 방법:** 이제 Windows 인증을 사용 합니다. 
- [#4494](https://github.com/Microsoft/azuredatastudio/issues/4494): SQL 전자 필기장 기능을 설치할 수 없습니다. <br/>
**해결 방법:** 문제 해결 단계를 따릅니다 [여기](https://github.com/Microsoft/azuredatastudio/issues/4494#issuecomment-473043832)합니다. 
- [#4503](https://github.com/Microsoft/azuredatastudio/issues/4503): Azure Data Studio 다운로드 폴더 (Mac)에서 직접 열 수 없습니다. <br />
**해결 방법:** 응용 프로그램 압축을 푼 후 컴퓨터를 다시 시작 합니다. 조사 됩니다. 
- [#4539](https://github.com/Microsoft/azuredatastudio/issues/4539):  Notebook에서 다른 이름으로 저장 되는 연결 컨텍스트를 잃을 <br />
**해결 방법:** 다음 릴리스에서 수정 될 예정입니다. 
- [#4458](https://github.com/Microsoft/azuredatastudio/issues/4458): Dacpac 추출 충돌 SqlToolsService 잘못 된 버전을 사용 하는 경우 <br/>
**해결 방법:** Azure Data Studio를 다시 시작 하 고 올바른 버전 사용 되는지 확인 합니다.
- 새 Notebook 및 전자 필기장 열기 아이콘 손실 됩니다. <br/> 
**해결 방법:** 레거시 연결 형식이 사용 되지 않습니다. 예상 대로 모든 작업 (새 노트북에서 Spark 작업)을 얻게 및 SQL Server 끝점에 연결 하는 것이 좋습니다. 

## <a name="february-2019"></a>2019년 2월

2019 년 2 월 13 일 &nbsp;  /  &nbsp; 버전: 1.4.5

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 추가 **SQL Server 용 관리 팩** 확장 팩입니다. | 이 쉽게 SQL Server 관리자와 관련 된 확장을 설치 합니다. 다음을 포함합니다.<br/>&bull; &nbsp; [SQL Server Agent](sql-server-agent-extension.md?view=sql-server-2017)<br/>&bull; &nbsp; [SQL Server Profiler](https://docs.microsoft.com/sql/azure-data-studio/sql-server-profiler-extension)<br/>&bull; &nbsp; [SQL Server Import](sql-server-import-extension.md?view=sql-server-2017) |
| 추가 필터링 Profiler 확장에서 이벤트 지원을 확장 합니다. | &nbsp; |
| 추가 T-SQL 결과 XML로 저장할 수 있는 XML 기능으로 저장 합니다. | &nbsp; |
| 추가 된 데이터 계층 응용 프로그램 마법사 개선 사항입니다. | &bull; &nbsp; 추가 스크립트 생성 단추<br/>&bull; &nbsp; 배포 중 경고 데이터가 손실 될 수 있도록 추가 보기입니다. |
| SQL Server 2019 미리 보기 확장을 업데이트 합니다. | 참조 [SQL Server 2019 미리 보기 확장](sql-server-2019-extension.md?view=sql-server-ver15)합니다. |
| 오랫동안 기본적 스트리밍 결과 쿼리를 실행 합니다. | &nbsp; |
| 해결 된 버그 및 문제입니다. | 참조 [버그 및 GitHub에서 문제](https://github.com/Microsoft/azuredatastudio/milestone/23?closed=1)합니다. |
| &nbsp; | &nbsp; |

## <a name="january-2019-hotfix"></a>1 월 2019 (핫픽스)

2019 년 1 월 16 &nbsp;  /  &nbsp; 버전: 1.3.9 &nbsp;  /  &nbsp; 핫픽스 릴리스

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 1.3.8 발견 된 몇 가지 문제를 해결 합니다. | 참조 [GitHub에서 1 월 핫픽스 릴리스](https://github.com/Microsoft/azuredatastudio/milestone/24?closed=1)합니다.<br/><br/>자세한 내용은 다음을 참조 하세요.<br/>&bull; &nbsp; [GitHub에서 로그온 변경](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)합니다.<br/>&bull; &nbsp; [GitHub의 릴리스](https://github.com/Microsoft/azuredatastudio/releases)합니다. |
| &nbsp; | &nbsp; |

## <a name="january-2019"></a>2019년 1월

2019 년 1 월 9 &nbsp;  /  &nbsp; 버전: 1.3.8

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| Windows에 대 한 새 사용자 설치 관리자를 추가 합니다. | 기존 체제 설치 관리자와 달리 새 사용자 설치 관리자에 관리자 권한이 필요 하지 않습니다. 또한 관리자가 아닌 쉽게 업그레이드할 수 있습니다. |
| Azure Active Directory 인증 지원이 추가 되었습니다. | &nbsp; |
| Idera SQL DM Performance Insights (미리 보기)를 발표합니다. | &nbsp; |
| SQL Server 가져오기 확장에서 데이터 계층 응용 프로그램 마법사를 지원 합니다. | &nbsp; |
| SQL Server 2019 미리 보기 확장을 업데이트 합니다. | 참조 [SQL Server 2019 미리 보기 확장](sql-server-2019-extension.md?view=sql-server-ver15)합니다. |
| SQL Server Profiler 개선 사항입니다. | &nbsp; |
| 대규모 쿼리 (미리 보기)에 대 한 스트리밍 결과입니다. | &nbsp; |
| 커뮤니티 확장: sp_executesql to sql 및 새 데이터베이스입니다. | &nbsp; |
| 해결 된 버그 및 문제입니다. | 참조 [버그 및 GitHub에서 문제](https://github.com/Microsoft/azuredatastudio/milestone/19?closed=1)합니다. |
| &nbsp; | &nbsp; |

## <a name="november-2018"></a>2018 년 11 월

2018 년 11 월 6 일 &nbsp;  /  &nbsp; 버전: 1.2.4

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| SQL Server 2019 미리 보기 확장을 업데이트 합니다. | 참조 [SQL Server 2019 미리 보기 확장](sql-server-2019-extension.md?view=sql-server-ver15)합니다. |
| 붙여넣기 계획 확장을 소개합니다. | &nbsp; |
| 하이 컬러 쿼리 확장이 포함 되 면 SSMS 편집기 테마를 소개 합니다. | &nbsp; |
| SQL Server 에이전트, Profiler, 및 가져오기 확장에서 수정합니다. | &nbsp; |
| .NET Core 해결 macOS에서 비활성 연결을 삭제 소켓 KeepAlive 문제가 발생 합니다. | &nbsp; |
| .NET Core에 SQL 도구 서비스 업그레이드 (지원용 최종 AAD) 2.2 미리 보기 3. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-november-2018"></a>버그 수정, 2018 년 11 월

- 수정 [#2933 발급](https://github.com/Microsoft/azuredatastudio/issues/2933): Azure SQL DB에 연결
- 수정 [#2914 발급](https://github.com/Microsoft/azuredatastudio/issues/2914): "잘못 된 인수" 예외 확장 OE 데이터베이스 노드
- 수정 [#2935 발급](https://github.com/Microsoft/azuredatastudio/pull/2935): 쿼리 결과에 여러 줄 메시지를 올바르게 표시
- 수정 [#2906 발급](https://github.com/Microsoft/azuredatastudio/pull/2906): 테이블 이름에 특수 문자가 포함 된 경우 데이터 편집 문서 이름 수정
- 수정 [#2929 발급](https://github.com/Microsoft/azuredatastudio/issues/2929): 기본 제공 changelog 라는 확장에서 변경 내용에 대 한 VSCode 릴리스를 확인 하려면
- 수정 [#2719 발급](https://github.com/Microsoft/azuredatastudio/issues/2719): 높은 대비 테마 double/삼중 아이콘
- 수정 [#3047 발급](https://github.com/Microsoft/azuredatastudio/pull/3047): SQL Server에 연결 하기 위한 명령줄 인터페이스를 추가 합니다.
- 수정 [#3031 발급](https://github.com/Microsoft/azuredatastudio/pull/3031): 쿼리 계획 테마 지원 추가

## <a name="october-2018"></a>2018 년 10 월

2018 년 10 월 29 일 &nbsp;  /  &nbsp; 버전: 1.1.4

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| Azure SQL Database를 이동할 Azure 리소스 탐색기를 소개 합니다. | &nbsp; |
| 개체 탐색기와 쿼리 편집기에 해당 하는 연결의 견고성을 향상 합니다. | &nbsp; |
| SQL 에이전트 확장 향상 되었습니다. | &nbsp; |
| SQL Server 2019 미리 보기 확장을 업데이트 합니다. | 참조 [SQL Server 2019 미리 보기 확장](sql-server-2019-extension.md?view=sql-server-ver15)합니다. |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-october-2018"></a>버그 수정, 2018 년 10 월

- 수정 [#2717 발급](https://github.com/Microsoft/azuredatastudio/issues/2717): XML 열으로 된 결과 형식을 클릭합니다
- 수정 [#2993 발급](https://github.com/Microsoft/azuredatastudio/issues/2993): 너비의 결과 windows 완전 하지 않습니다.
- 수정 [#2999 발급](https://github.com/Microsoft/azuredatastudio/issues/2999): DB에 연결 하는 경우 Mac에서 System.Diagnostics.Tracing 파일을 로드할 수 없습니다.
- 수정 [#2851 발급](https://github.com/Microsoft/azuredatastudio/issues/2851): 시계열 차트 제대로 렌더링 되지 않습니다.
- 수정 [#2996 발급](https://github.com/Microsoft/azuredatastudio/issues/2996): 갑자기 세션 변경으로 인해 손실 임시 테이블

자세한 내용은 참조는 [변경 로그](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), 및 [릴리스](https://github.com/Microsoft/azuredatastudio/releases)합니다.

## <a name="september-2018-ga-release"></a>2018 년 9 월 (GA 릴리스)

2018 년 9 월 24 일부 &nbsp;  /  &nbsp; 버전: 1.0 &nbsp;  /  &nbsp; GA 릴리스

Azure Data Studio (이전의 SQL Operations Studio)의 일반 공급 릴리스 합니다.

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 쿼리 결과 표 성능 및 많은 수의 결과 집합에 대 한 UX 향상 합니다. | &nbsp; |
| 모눈 레이아웃 및 설정 편집기 개선 (미리 보기)를 사용 하 여 1.26.1를 1.23에서 visual Studio Code 소스 코드 새로 고칩니다. | &nbsp; |
| 화면 판독기, 키보드 탐색 및 고대비에 대 한 내게 필요한 옵션 개선 사항입니다. | &nbsp; |
| 추가 `Connection name` 서버 보기 사용에는 다른 표시 이름을 제공 하는 옵션입니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="announcing-the-sql-server-2019-preview-extension"></a>SQL Server 2019 미리 보기 확장 발표

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 포함 하 여 SQL Server 2019 미리 보기 기능에 대 한 지원 [빅 데이터 클러스터](../big-data-cluster/big-data-cluster-overview.md) 지원 합니다. | 게이트웨이에 연결 하 여 HDFS/Spark SQL Server 2019 미리 보기와 함께 제공 합니다.<br/><br/>HDFS 찾아보기, 파일 업로드, 파일을 저장 및 CSV 파일에 대 한 전자 필기장에서 분석 등의 유용한 작업을 시작 합니다.<br/><br/>대시보드에서 Spark 작업을 제출 하거나 개체 탐색기에서 HDFS/Spark 연결을 마우스 오른쪽 단추로 클릭 합니다. |
| Azure Data Studio 노트북입니다. | 만들거나 통합된 Notebook 뷰어를 사용 하 여 Notebook을 엽니다. 이 릴리스에서 Notebook 뷰어는 로컬 커널 및 SQL Server 2019 빅 데이터 클러스터에 연결을 지원 합니다.<br/><br/>Notebook에서 PROSE 코드 Accelerator 라이브러리를 사용 하 여 빠른 데이터 준비에 대 한 파일 형식 및 데이터 형식에 알아봅니다. |
| Azure 리소스 탐색기입니다. | Azure 리소스 탐색기 보기를 사용 하 여 Azure 계정에 대 한 끝점 관련 된 데이터를 이동 하 고 개체 탐색기에 대 한 연결을 만들 수 있습니다. 이 릴리스에서 Azure SQL Database 및 서버 지원 됩니다. |
| SQL Server PolyBase 외부 테이블 마법사를 만듭니다. | 사용이 간편한 마법사를 사용 하 여 외부 테이블 및 지 원하는 메타 데이터 구조를 만듭니다. 이 릴리스에서 원격 SQL Server 및 Oracle 서버는 지원 됩니다. |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-september-2018"></a>버그 수정, 2018 년 9 월

- 수정 [#2647 발급](https://github.com/Microsoft/azuredatastudio/issues/143): 차트를 큰 단계는 이전 버전과 이었습니다.
- 수정 [#2648 발급](https://github.com/Microsoft/azuredatastudio/issues/143): JSON 하이퍼링크 전체 열을 반환 하는 선택 합니다.

자세한 내용은 참조는 [변경 로그](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), 및 [릴리스](https://github.com/Microsoft/azuredatastudio/releases)합니다.

## <a name="august-2018"></a>2018년 8월

2018 년 8 월 30 일 &nbsp;  /  &nbsp; 버전: 0.32.8 &nbsp;  /  &nbsp; 공개 미리 보기

합니다 *년 8 월 공개 미리 보기* 버그 수정, 제품 안정화 및 기존 시나리오의 간격을 채우는에 중점을 둡니다.

_0.32.8 0.32.7 있는 몇 가지 회귀에 대 한 수정 프로그램이 포함 되어 있습니다 ([#1971](https://github.com/Microsoft/azuredatastudio/issues/1971)하십시오 [#2372](https://github.com/Microsoft/azuredatastudio/issues/2372))_

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| SQL Server 가져오기 확장을 발표합니다. | &nbsp; |
| SQL Server Profiler 세션 관리 합니다. | &nbsp; |
| SQL Server Profiler 세션 템플릿 지원 합니다. | &nbsp; |
| SQL Server 에이전트 개선 사항입니다. | &nbsp; |
| 새 커뮤니티 확장: 첫 번째 응답자 키트입니다. | &nbsp; |
| 수명 품질 향상: 연결 문자열 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-august-2018"></a>버그 수정, 2018 년 8 월

- 쿼리 편집기 창에서 SQL을 사용 하 여 구문 분석 된 `Parse Syntax` 명령입니다.
- 수정 [#143 발급](https://github.com/Microsoft/azuredatastudio/issues/143): 변수 이름에을 선택 하지 않으면 두 번 클릭 합니다.
- 수정 [문제 #387](https://github.com/Microsoft/azuredatastudio/issues/387): SQL 탭 DB 아이콘은 빨간색입니다.
- 수정 [#825 발급](https://github.com/Microsoft/azuredatastudio/issues/825): 요청: 스크립팅 한 후 현재 서버에 자동 연결 하는 중... 
- 수정 [#1278 발급](https://github.com/Microsoft/azuredatastudio/issues/1278): sqlops.desktop [데스크톱 항목]-이름 및 설명에 대 한 중복 값입니다.
- 수정 [#1285 발급](https://github.com/Microsoft/azuredatastudio/issues/1285): 업데이트 하면 응용 프로그램 아이콘을 제거 하 고 대체 Windows에서.
- 수정 [#1317 발급](https://github.com/Microsoft/azuredatastudio/issues/1317): 소수 구분 기호를 수정 합니다.
- 수정 [#1474 발급](https://github.com/Microsoft/azuredatastudio/issues/1474): 연결 변경 취소는 현재 연결을 끊습니다.
- 수정 [#1497 발급](https://github.com/Microsoft/azuredatastudio/issues/1497): 맨 아래에서 옵션 잘립니다 차트로 보고 합니다.
- 수정 [#1524 발급](https://github.com/Microsoft/azuredatastudio/issues/1524): 셸/대시보드: 주 viewlet 아이콘 draggable 되며 응용 프로그램 크래시가 발생할 수 있습니다.
- 수정 [#1578 발급](https://github.com/Microsoft/azuredatastudio/issues/1578): 이름을 클릭 하 여 원격 파일 브라우저 폴더를 확장/축소를 수 없습니다.
- 수정 [#1620 발급](https://github.com/Microsoft/azuredatastudio/issues/1620): 기능 제안: 기존 연결에 대 한 연결 문자열을 가져옵니다.
- 수정 [#1624 발급](https://github.com/Microsoft/azuredatastudio/issues/1624): SelectBox 사용 하지 않도록 설정 하는 경우 색을 변경 되지 않습니다.
- 수정 [#1728 발급](https://github.com/Microsoft/azuredatastudio/issues/1728): JSON/EXCEL/CSV 작동 하지 않음로 저장 합니다.
- 수정 [#1744 발급](https://github.com/Microsoft/azuredatastudio/issues/1744): 결과 창 탭 간에 전환 하는 경우 해당 스크롤 위치를 잃게 됩니다.
- 수정 [#1748 발급](https://github.com/Microsoft/azuredatastudio/issues/1748): Excel 파일 두 번째 (및 후속) 시간을 절약 하는 경우 오류 메시지입니다.
- 수정 [#1782 발급](https://github.com/Microsoft/azuredatastudio/issues/1782): 데이터를 편집 합니다: 셀 이스케이프 키를 눌러 원래 값으로 되돌리기 하지 않습니다.
- 수정 [#1836 발급](https://github.com/Microsoft/azuredatastudio/issues/1836): SQL Operations Studio 사용 하 여 연결 되지 않은.sql 파일입니다.
- 수정 [#1850 발급](https://github.com/Microsoft/azuredatastudio/issues/1850): 입력 N ' n 자동 완성 ' '입니다.
- 수정 [#1985 발급](https://github.com/Microsoft/azuredatastudio/issues/1985): 표 1 열으로 해제 되어 쿼리 결과에서 복사 합니다.
- 수정 [#1998 발급](htpts://github.com/Microsoft/azuredatastudio/pull/1998): 대화에 대 한 VS Code 버전을 추가 합니다.
- 수정 [#2042 발급](https://github.com/Microsoft/azuredatastudio/pull/2042): 에이전트: Sql 파일에서 쿼리 가져오기 단추를 사용할 수 있습니다.
- 수정 [#2091 발급](https://github.com/Microsoft/azuredatastudio/issues/2091): 결과 창에서 복사할 바로 가기 Ctrl + C를 사용할 수 없습니다.
- 수정 [#2099 발급](https://github.com/Microsoft/azuredatastudio/pull/2099): 더 많은 saveAsCsv 옵션을 추가 합니다.
- 수정 [#2107 발급](https://github.com/Microsoft/azuredatastudio/issues/2107): 대시보드 및 Profiler 문서에 대 한 문서 아이콘을 업데이트 합니다.
- 수정 [#2129 발급](https://github.com/Microsoft/azuredatastudio/pull/2129): 탭을 전환할 때 편집 데이터 스크롤 위치를 저장 합니다.
- 수정 [#2152 발급](https://github.com/Microsoft/azuredatastudio/issues/2152): 결과 표 형태 창의 행 표시기 0부터 시작 합니다.

### <a name="known-issues-august-2018"></a>알려진된 문제, 2018 년 8 월

- [문제 #2371](https://github.com/Microsoft/azuredatastudio/issues/2371) Excel 데이터의 첫 번째 행만 저장 하는 대로 저장
- [문제 #2150](https://github.com/Microsoft/azuredatastudio/issues/2150): Ubuntu 16.04를 컨테이너에는 SQL에 연결할 수 없습니다.

## <a name="july-2018"></a>2018 년 7 월

2018 년 7 월 19 일 &nbsp;  /  &nbsp; 버전: 0.31.4 &nbsp;  /  &nbsp; 공개 미리 보기

합니다 *월 공개 미리 보기* 다음 항목에 중점을 둡니다.

- SQL Server 에이전트 구성 시나리오의 초기 릴리스.
- SQL Server Profiler 세션 및 보기 템플릿 향상입니다.
- GitHub 문제를 보고 하는 고객에 대 한 지속적인된 버그 수정.

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| [SQL Operations Studio 확장에 대 한 SQL Server 에이전트](sql-server-agent-extension.md) 개선 합니다. | 왼쪽된 창에서 경고, 운영자 및 프록시 및 아이콘 추가 보기입니다.<br/><br/>새 작업, 새 작업 단계, 새 경고 및 새 연산자에 대 한 추가 대화 상자.<br/><br/>추가 된 삭제 작업, 경고를 삭제 및 Delete 연산자 (마우스 오른쪽 단추로 클릭).<br/><br/>이전에 실행 된 시각화를 추가 합니다.<br/><br/>각 열 이름에 대 한 필터를 추가 합니다. |
| [SQL Operations Studio 확장에 대 한 SQL Server Profiler](sql-server-profiler-extension.md) 개선 합니다. | 확장 이벤트를 보려는 5 개의 기본 템플릿을 추가 합니다.<br/><br/>추가 서버/데이터베이스 연결 이름입니다.<br/><br/>Azure SQL Database 인스턴스에 대 한 지원이 추가 되었습니다.<br/><br/>Profiler 실행 되는 경우 탭 닫힐 때 Profiler를 종료 하려면 추가 제안 합니다. |
| 결합 스크립트 확장의 릴리스입니다. | &nbsp; |
| 확장 작성자에 대 한 추가 마법사 및 대화 확장성 지점입니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-july-2018"></a>버그 수정, 2018 년 7 월

- 수정 [728 발급](https://github.com/Microsoft/azuredatastudio/issues/728): MacOS에서 추가 연결에 응답
- 수정 [1612 발급](https://github.com/Microsoft/azuredatastudio/issues/1612): 결과 표에서 텍스트 표시는 중 문제가 발생 한 국제 문자로
- 수정 [1693 발급](https://github.com/Microsoft/azuredatastudio/issues/1693): 백업 대화 상자: 파일 브라우저 UI 손상 되었습니다.
- 수정 [1713 발급](https://github.com/Microsoft/azuredatastudio/issues/1713): 영향을 받는 행 수
- 수정 [1718 발급](https://github.com/Microsoft/azuredatastudio/issues/1718): 모든 데이터 원본에 연결할 수 없습니다.
- 수정 [1719 발급](https://github.com/Microsoft/azuredatastudio/issues/1719): 서버에 연결할 때 TypeError
- 수정 [1724 발급](https://github.com/Microsoft/azuredatastudio/issues/1724): 작업 중지 확장 대화 상자
- 수정 [1749 발급](https://github.com/Microsoft/azuredatastudio/issues/1749): 버그: 열에 HTML 데이터 해석
- 수정 [1789 발급](https://github.com/Microsoft/azuredatastudio/issues/1789): 확장성: 연결 공급자를 추가 하는 경우 제거 되지에서 제거 됩니다 목록
- 수정 [1791 발급](https://github.com/Microsoft/azuredatastudio/issues/1791): Sqlops 확장: queryeditor.connect() 대상 데이터베이스에 연결 하지만 UI 편집기가 연결 되는 표시 되지 않습니다.
- 수정 [1799 발급](https://github.com/Microsoft/azuredatastudio/issues/1799): 상위 10 개 DB 크기 차트 대/소문자 구분 인스턴스에서 작동 하지 않습니다.
- 수정 [1814 발급](https://github.com/Microsoft/azuredatastudio/issues/1814): sqlops.d.ts 오타로 인해 암시적인 'any' 형식 정의
- 수정 [1817 발급](https://github.com/Microsoft/azuredatastudio/issues/1817): 오류 de Ortografia
- 수정 [1830 발급](https://github.com/Microsoft/azuredatastudio/issues/1830): Component() 호출 된 후 iconPath ButtonComponent에서 설정 아이콘 변경 되지 않습니다.
- 수정 [1843 발급](https://github.com/Microsoft/azuredatastudio/issues/1843): 더 나은 테이블 구성

## <a name="june-2018"></a>2018 년 6 월

2018 년 6 월 20 일 &nbsp;  /  &nbsp; 버전: 0.30.6 &nbsp;  /  &nbsp; 공개 미리 보기

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| **SQL Operations Studio 대 한 SQL Server Profiler _미리 보기_**  확장 초기 릴리스. | &nbsp; |
| 새 **SQL Data Warehouse** 확장 data warehouse에 정보를 표시 하는 다양 한 사용자 지정 가능한 대시보드 위젯을 포함 합니다. | 이 관리 및 튜닝에 일관 된 성능을 최적화 하도록 데이터 웨어하우스 관련 주요 시나리오를 잠금 해제 합니다. |
| **데이터를 "필터링 및 정렬할" 편집** 지원 합니다. | &nbsp; |
| **SQL Operations Studio 대 한 SQL Server 에이전트 _미리 보기_**  확장의 향상 된 기능 작업 및 작업 기록 보기. | &nbsp; |
| 개선 **마법사 및 대화 상자 UI 작성기 프레임 워크** 확장성 Api입니다. | &nbsp; |
| VS 코드 플랫폼 소스 코드를 업데이트 합니다. | 다음 릴리스를 통합합니다.<br/>&bull; &nbsp; [2018 년 3 월 (1.22)](https://code.visualstudio.com/updates/v1_22)<br/>&bull; &nbsp; [2018 년 4 월 (1.23)](https://code.visualstudio.com/updates/v1_23) |
| &nbsp; | &nbsp; |

### <a name="github-issues-fixes-june-2018"></a>GitHub 문제를 수정 하면 2018 년 6 월

- 기능 요청 ([1204 발급](https://github.com/Microsoft/azuredatastudio/issues/1204)): 데이터를 결과 그리드 자동 맞춤 열 너비를 확인 하 고 동일한 쿼리를 다시 실행 하는 경우 수동으로 변경 해야 하세요.
- 수정 [1398 발급](https://github.com/Microsoft/azuredatastudio/issues/1398): 표시는 메시지를 추가 하 고 연결 된 계정 비어 있는 경우 계정 계정 단추를 추가 해야 합니다.
- 수정 [1399 발급](https://github.com/Microsoft/azuredatastudio/issues/1399): 연결 된 계정 탭 뷰를 축소할 때 손상 되었습니다.
- 수정 [1374 발급](https://github.com/Microsoft/azuredatastudio/issues/1374): SQL 도구 서비스에는 디스크에서.sql 파일을 열 때 작동이 중단 됩니다.
- 수정 [1372 발급](https://github.com/Microsoft/azuredatastudio/issues/1372): SQL 키워드가 "BETWEEN" 없습니다.
- 수정 [1395 발급](https://github.com/Microsoft/azuredatastudio/issues/1395): '일치' 키워드는 SQL 도구 서비스 작동이 중단 됩니다.
- 수정 [1496 발급](https://github.com/Microsoft/azuredatastudio/issues/1496): "새 Profiler" 개체 탐색기에서 상황에 맞는 메뉴 옵션 아무 작업도 수행 합니다.
- 수정 [1495 발급](https://github.com/Microsoft/azuredatastudio/issues/1495): 쿼리 편집기 "설명" 쿼리 계획 손상 되었습니다.

## <a name="may-2018"></a>2018 년 5 월

2018 년 5 월 7 일 &nbsp;  /  &nbsp; 버전: 0.29.3 &nbsp;  /  &nbsp; 공개 미리 보기

합니다 *공개 미리 보기로 제공 될 수 있습니다* 안정화 및 버그 수정에 포커스가 있습니다.

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 확장 관리자에서 사용 하 여 사용할 수 있는 Redgate SQL 검색 확장을 발표합니다. | &nbsp; |
| 커뮤니티 지역화 10 언어에 사용할 수 있습니다. | 독일어, 스페인어, 프랑스어, 이탈리아어, 일본어, 한국어, 포르투갈어, 러시아어, 중국어 간체, 및 중국어 (번체). |
| 원격 분석 컬렉션 변경 됩니다. | &bull; &nbsp; 축소 된 원격 분석 컬렉션입니다.<br/>&bull; &nbsp; 개선 된 옵트아웃 합니다.<br/>&bull; &nbsp; 개인정보취급방침 제품에 연결 됩니다. |
| 확장 관리자 환경을 개선 된 Marketplace에 있습니다. | 커뮤니티 확장을 보다 쉽게 검색 합니다. |
| SQL 에이전트 확장입니다. | &bull; &nbsp; 작업입니다.<br/>&bull; &nbsp; 작업 기록 보기 개선 합니다. |
| Whoisactive 및 서버 보고서에 대 한 확장을 업데이트합니다. | &nbsp; |
| 관리 대시보드 속성의 스크롤 개선 되었습니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues"></a>GitHub 문제 해결

- 수정 [703 발급](https://github.com/Microsoft/azuredatastudio/issues/703): 데이터 편집에에서 html 텍스트를 입력 하면 값이 새로 고침까지 제대로 표시 되지 않음
- 수정 [821 발급](https://github.com/Microsoft/azuredatastudio/issues/821): azuredatastudio.deb 패키지 종속성
- 수정 [1260 발급](https://github.com/Microsoft/azuredatastudio/issues/1260): 키워드 'distinct' 강조 표시가 해제
- 수정 [1332 발급](https://github.com/Microsoft/azuredatastudio/issues/1332): 데이터 편집 되돌리기 행 작동 하지 않습니다
- 수정 [1215를 발급](https://github.com/Microsoft/azuredatastudio/issues/1215): SQL Agent 확장 및 상태 표시줄
- 수정 [1316 발급](https://github.com/Microsoft/azuredatastudio/issues/1316): Windows 크기 변경 후 크기 조정 SQL 에이전트 하지 않음

## <a name="april-2018"></a>2018 년 4 월

2018 년 4 월 25 일 &nbsp;  /  &nbsp; 버전: 0.28.6 &nbsp;  /  &nbsp; 공개 미리 보기

합니다 *공개 미리 보기 4 월* 버그 수정 및 개선 사항이 포함 되어 있습니다.

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| SQL 에이전트 미리 보기 확장 기능 개선: | &nbsp; |
| &nbsp; &nbsp; &nbsp; 파일에 대 한 지원이 향상 되었습니다. | &bull; &nbsp; 큰 파일입니다.<br/>&bull; &nbsp; 보호 된 파일을 보호 하는 관리자를 저장 합니다.<br/>&bull; &nbsp; 저장 \>SQL Operations Studio 내의 256m 파일입니다. |
| &nbsp; &nbsp; &nbsp; 통합된 터미널을 분할 합니다. | 동시에 여러 열고 터미널을 사용 하 여 작동 합니다. |
| &nbsp; &nbsp; &nbsp; 빠른 설치 및 시작 시간입니다. | 디스크에 있는 파일 수 foot 인쇄의 축소 된 설치 합니다. |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues-april-2018"></a>2018 년 4 월 GitHub 문제를 해결 합니다.

- 수정 [37 발급](https://github.com/Microsoft/azuredatastudio/issues/37): 차트 뷰어에 오류를 throw 하면 예기치 않은 동작이 발생 합니다.
- 수정 [462 발급](https://github.com/Microsoft/azuredatastudio/issues/462): 기능 요청: 기본적으로 확장 하는 서버 그룹에 대 한 옵션입니다.
- 수정 [606 발급](https://github.com/Microsoft/azuredatastudio/issues/606): intellisense-'update' 명령에 대 한 잘못 된 제안 합니다.
- 수정 [967 발급](https://github.com/Microsoft/azuredatastudio/issues/967): 쿼리 계획을 예상 결과 그리드에서 XML 실행 계획을 선택 하는 경우.
- 수정 [1023 발급](https://github.com/Microsoft/azuredatastudio/issues/1023): Flyfishingdba에서 ms_foreachdb 호출에 대 한 대괄호를 추가 합니다.
- 수정 [1048 발급](https://github.com/Microsoft/azuredatastudio/issues/1048): 사전 로그인 SSL/TLS 핸드셰이크 오류입니다.
- 수정 [1050 발급](https://github.com/Microsoft/azuredatastudio/issues/1050): 오류를 표시 하기 전에 지우기 insights 보기입니다.
- 수정 [1057 발급](https://github.com/Microsoft/azuredatastudio/issues/1057): 복원 및 새 쿼리 작업 탐색기 위젯에서 끊어집니다.
- 수정 [1068 발급](https://github.com/Microsoft/azuredatastudio/issues/1068): 대시보드 출력 windows 팝업 Azure SQL Database에 대 한 오류 메시지와 함께 합니다.
- 수정 [1069 발급](https://github.com/Microsoft/azuredatastudio/issues/1069): 연결 대화 상자 처음 표시 될 때 필요한 서버 오류를 보여 줍니다.
- 수정 [1070 발급](https://github.com/Microsoft/azuredatastudio/issues/1070): 서버 그룹에는 이제 두 번 클릭 하 여 확장 필요 합니다.
- 수정 [1072 발급](https://github.com/Microsoft/azuredatastudio/issues/1072): 선택 컨트롤 배경이 반투명입니다.
- 수정 [1115 발급](https://github.com/Microsoft/azuredatastudio/issues/1115): SQL Operations Studio 모든 고대비 액세스 가능성 문제를 해결 합니다.
- 수정 [1101 발급](https://github.com/Microsoft/azuredatastudio/issues/1101): 확장 되지 못하거나 업그레이드 "다운로드" 수동으로 링크 잘못 된 위치로 이동 합니다.
- 수정 [1103 발급](https://github.com/Microsoft/azuredatastudio/issues/1103): 홈 탭에서 작동 하지 않는 V 스크롤입니다.
- 수정 [1104 발급](https://github.com/Microsoft/azuredatastudio/issues/1104): SQL 확장 탭 작동을 중지 합니다.

### <a name="visual-studio-code-121-platform"></a>Visual Studio 코드 1.21 플랫폼

4 월 공개 미리 보기는 강조 표시는 Visual Studio 코드 1.21 플랫폼에 대 한 소스 코드의 새로 고침입니다. 이전 1.19 동기화 지점에서 업데이트를 여러 개 핵심 편집기 및 workbench에 나타납니다. 몇 가지 예는 다음과 같습니다.

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| [새 알림 UI](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui)합니다. | 쉽게 관리 하 고 SQL Operations Studio 알림을 검토 합니다. |
| [통합 터미널 분할](https://code.visualstudio.com/updates/v1_21#_split-terminals)합니다. | 한 번에 여러 열고 터미널을 사용 하 여 작동 합니다. |
| [대형 및 보호 된 파일을 저장할](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges)합니다. | 보호 하는 관리자를 저장 하 고 \>SQL Operations Studio 내의 256m 파일입니다. |
| [대용량 파일 지원 향상](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements)합니다. | 큰 파일에 대 한 텍스트 버퍼 최적화 합니다. |
| [향상 된 설정 검색](https://code.visualstudio.com/updates/v1_20#_settings-search)합니다. | 자연어 검색을 사용 하 여 올바른 설정을 쉽게 찾을. |
| [전역 조각](https://code.visualstudio.com/updates/v1_20#_global-snippets)합니다. | 모든 파일 형식에서 사용할 수 있습니다 하는 코드 조각을 만듭니다. |
| [다중 선택 탐색기](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer)합니다. | 한 번에 여러 파일에 대해 작업을 수행 합니다. |
| [오류 및 경고 탐색기에서](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer)합니다. | 코드 베이스에서 오류를 신속 하 게 이동 합니다. |
| [끌어 및 삭제, 복사 및 windows에서 붙여](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support)합니다. | 열려 있는 SQL Operations Studio 창에서 파일을 이동 합니다. |
| [Git 하위 모듈 지원](https://code.visualstudio.com/updates/v1_20#_git-submodules)합니다. | 중첩 된 Git 리포지토리에서 Git 작업을 수행 합니다. |
| [터미널 화면 판독기 지원](https://code.visualstudio.com/updates/v1_20#_screen-reader-support)합니다. | 통합된 터미널 바뀌었습니다 **화면 판독기 액세스에 최적화 된** 모드입니다. |
| [가운데 맞춤된 편집기 레이아웃](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout)합니다. | 코드 보기 화면 부동산을 최대화 합니다. |
| [가로 검색 결과 (미리 보기)](https://code.visualstudio.com/updates/v1_21#_horizontal-search)합니다. | 가로 패널에 뷰 검색 결과 이제 수 있습니다. |
| &nbsp; | &nbsp; |

자세한 내용은 체크 아웃 합니다 [Visual Studio Code 2 월 릴리스 정보](https://code.visualstudio.com/updates/v1_21), 및 [Visual Studio Code 년 1 월 릴리스 정보](https://code.visualstudio.com/updates/v1_20)합니다.

자세한 내용은 참조는 [변경 로그](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)합니다.

## <a name="march-2018"></a>2018 년 3 월

2018 년 3 월 28 일 &nbsp;  /  &nbsp; 버전: 0.27.3 &nbsp;  /  &nbsp; 공개 미리 보기

합니다 *공개 미리 보기 3 월* 은 계속 최상위 GitHub 문제를 해결 하 고 확장성 이야기를 주력 합니다. 특히 확장 관리자를 사용 하도록 설정 하 고 대시보드 관리 개선 및 SQL 에이전트 및 확장 정보를 제공 합니다. 이 릴리스에 다음과 같은 향상 기능이 포함 되어 있습니다.

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 구성 창과 탭된 insights를 지원 하기 위해 대시보드 확장성 모델을 향상 시킵니다. | 확장 관리자를 사용 하면 확장의 간단한 획득 합니다.<br/><br/>Sp에 대 한 대시보드 확장\_에서 whoisactive [whoisactive.com](http://www.whoisactive.com)합니다.<br/><br/>자세한 내용은 참조 하세요 [SQL Operations Studio 기능을 확장](extensions.md)합니다. |
| 추가할 [연결 및 개체 탐색기에 대 한 확장성 Api](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API) 관리 합니다. | &nbsp; |
| 계속에 영향을 주는 중요 한 고객을 해결할 [GitHub 문제](https://github.com/Microsoft/azuredatastudio/issues)합니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="february-2018"></a>2018년 2월

2018 년 2 월 15 일 &nbsp;  /  &nbsp; 버전: 0.26.7 &nbsp;  /  &nbsp; 공개 미리 보기

합니다 *공개 미리 보기 2 월* 몇 가지 기능 제안 및 우선 순위가 높은 버그 수정을 포함 합니다. 이 릴리스에 다음과 같은 향상 기능이 포함 되어 있습니다.

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 자동 업데이트 설치를 도입 하는 경우 알림을 제공 새 릴리스는 다운로드할 수 있습니다. | &nbsp; |
| 연결 대화 상자 **데이터베이스** 필드는 이제 지정된 된 서버에서 채워진 데이터베이스의 목록을 포함 하는 동적으로 채워진된 드롭다운 목록입니다. | &nbsp; |
| 연결 확장성 API를 소개 합니다. | &nbsp; |
| VS 코드 편집기 1.19 통합 합니다. | &nbsp; |
| 여러 쿼리 계획 뷰어 개선 JustinPealing/html-쿼리 계획 구성 요소 수 거를 업데이트 합니다. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixed-issues-february-2018"></a>수정 된 문제, 2018 년 2 월

- 수정 [6 발급](https://github.com/Microsoft/azuredatastudio/issues/6): 새 쿼리 탭을 열 때 연결 및 선택한 데이터베이스를 유지 합니다.
- 수정 [22 발급](https://github.com/Microsoft/azuredatastudio/issues/22): '서버 이름' 및 ' 데이터베이스 이름 '-수 이러한 드롭다운 텍스트 상자 대신 수 있나요?
- 수정 [549 발급](https://github.com/Microsoft/azuredatastudio/issues/549): 자동/매우 자동 설치는 설치 후 여는 응용 프로그램에서 발생 합니다.
- 수정 [481 발급](https://github.com/Microsoft/azuredatastudio/issues/481): "업데이트 확인 옵션을 추가 합니다.
- SQL 편집기 색 지정 및 자동 완성 수정 사항:
  - 수정 [584 발급](https://github.com/Microsoft/azuredatastudio/issues/584): IntelliSense에서 강조 표시 되지 않은 "전체" 키워드입니다.
  - 수정 [345 발급](https://github.com/Microsoft/azuredatastudio/issues/345): 편집기 내에서 SQL 함수 색을 지정 합니다.
  - 수정 [300 발급](https://github.com/Microsoft/azuredatastudio/issues/300): [#tempData] 최신 "]" 녹색 표시 됩니다.
  - 수정 [225 발급](https://github.com/Microsoft/azuredatastudio/issues/225): 키워드 색 일치 하지 않습니다.
  - 수정 [60 발급](https://github.com/Microsoft/azuredatastudio/issues/60): 잘못 된 sql 구문 색 강조 from 절에서 임시 테이블을 사용 하는 경우.

## <a name="january-2018"></a>2018 년 1 월

2018 년 1 월 17 &nbsp;  /  &nbsp; 버전: 0.25.4 &nbsp;  /  &nbsp; 공개 미리 보기

합니다 *월 공개 미리 보기* 몇 가지 기능 제안 및 우선 순위가 높은 버그 수정을 포함 합니다. 이 릴리스에 다음과 같은 향상 기능이 포함 되어 있습니다.

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 저장 된 서버 연결의 연결 대화 상자에서 사용할 수 있습니다. | &nbsp; |
| 핫 종료를 사용 하도록 설정 합니다. 핫 종료가 참조를 사용 하도록 설정 하려면 기본적으로 꺼져 [핫 종료 설정을](settings.md#hot-exit)합니다. | &nbsp; |
| 탭 색 지정 서버 그룹을 기반으로 합니다. 탭 색 지정이 참조를 사용 하도록 설정 하려면 기본적으로 꺼져 [color 설정 탭](settings.md#tab-color)합니다. | &nbsp; |
| 변경 *서버 이름* 하 *Server* 연결 대화 상자에서. | &nbsp; |
| 손상 수정 *현재 쿼리 실행* 명령입니다. | &nbsp; |
| 끌어서 놓기 주요 스크립팅 버그를 수정 합니다. | &nbsp; |
| 잘못 된 고정 된 시작 메뉴 아이콘을 수정 합니다. | &nbsp; |
| 누락 된 Azure 계정 아이콘 브랜딩을 수정 합니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="december-2017"></a>2017 년 12 월

2017 년 12 월 19 일 &nbsp;  /  &nbsp; 버전: 0.24.1 &nbsp;  /  &nbsp; 공개 미리 보기

*12 월 공개 미리 보기* 모든 기능 영역 뿐 아니라 다음과 같은 향상 기능이 몇 가지 버그 수정을 포함 합니다.

&nbsp;

| 변경 | 설명 |
| :----- | :------ |
| 만들 방화벽 규칙 대화 상자에서 Azure SQL Database 및 Azure SQL Data Warehouse에 연결 하는 데 활용할 수 있습니다. | &nbsp; |
| Windows 설치 프로그램을 추가 하 고 Linux DEB 및 RPM 설치 패키지입니다. | &nbsp; |
| 대시보드 시각적 레이아웃 편집기를 관리 합니다. | &nbsp; |
| *스크립트와 Alter* 하 고 *실행할 스크립트* 명령입니다. | &nbsp; |
| *실제 계획으로 현재 쿼리를 실행* 명령입니다. | &nbsp; |
| VS Code 1.18.1 편집기 platform을 통합 합니다. | &nbsp; |
| 테스트용 로드의 VSIX 확장 파일을 사용 하도록 설정 합니다. | &nbsp; |
| "이동 N" 일괄 처리 반복 구문을 지원 합니다. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="november-2017"></a>2017 년 11 월

2017 년 11 월 15 일 &nbsp;  /  &nbsp; 버전: 0.23.6

- 초기 릴리스의 [!INCLUDE[name-sos](../includes/name-sos-short.md)]합니다.

## <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작 중 하나를 참조 하세요.

- [SQL Server 연결 및 쿼리](quickstart-sql-server.md)
- [Azure SQL 데이터베이스 연결 및 쿼리](quickstart-sql-database.md)
- [Azure 데이터 웨어하우스 연결 및 쿼리](quickstart-sql-dw.md)

[!INCLUDE[name-sos](../includes/name-sos-short.md)]에 기여하기:

- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
