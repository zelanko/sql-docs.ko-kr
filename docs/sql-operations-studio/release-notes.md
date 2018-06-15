---
title: Microsoft SQL 작업 Studio (미리 보기) 릴리스 정보 | Microsoft Docs
description: Microsoft SQL 작업 Studio (미리 보기) 릴리스 정보
ms.custom: tools|sos
ms.date: 05/08/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f461b78c3d76f7e6b848b83d8a2333dffe5de3c
ms.sourcegitcommit: a9da0abd3e17fbcd6339980d7331d0418cdada53
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2018
ms.locfileid: "34473827"
---
# <a name="sql-operations-studio-preview-release-notes"></a>SQL 작업 Studio (미리 보기) 릴리스 정보

**[년 5 월 공개 미리 보기 다운로드](download.md)**


## <a name="may-2018-may-public-preview"></a>년 5 월 2018 (월 공개 미리 보기)

릴리스 날짜: 2018 년 5 월 7  
버전: 0.29.3

*공개 미리 보기 수* 안정화 및 버그 수정에 포커스가 있습니다. 이 빌드는 다음과 같은 주요 기능과를 포함 되어 있습니다.  

- 확장 관리자에서 사용 하 여 사용할 수 있는 Redgate SQL 검색 확장을 발표합니다.
- 10 언어에 사용할 수 있는 커뮤니티 지역화: 독일어, 스페인어, 프랑스어, 이탈리아어, 일본어, 한국어, 포르투갈어, 러시아어, 중국어 간체 및 중국어 (번체).
- 축소 된 원격 분석 수집, 개선 된 옵트아웃 및 개인정보취급방침 대 한 제품에 링크 합니다.
- 확장 관리자는 향상 된 마켓플레이스를 쉽게 커뮤니티 확장을 검색 합니다.
- SQL 에이전트 확장 작업 및 작업 기록 보기 개선 합니다.
- Whoisactive 및 보고서 서버에 대 한 확장을 업데이트합니다.
- 관리 대시보드 속성 스크롤 향상 됩니다.
- GitHub 문제를 수정 합니다.
   - 해결 [703 발급](https://github.com/Microsoft/sqlopsstudio/issues/703): 편집 데이터에 HTML 형식의 텍스트를 입력 하면 값이 새로 고침 될 때까지 제대로 표시 되지 않아서
   - 해결 [821 발급](https://github.com/Microsoft/sqlopsstudio/issues/821): sqlopsstudio.deb 패키지 종속성
   - 해결 [1260 발급](https://github.com/Microsoft/sqlopsstudio/issues/1260): 'distinct' 강조 표시 되지 않은 키워드
   - 해결 [1332 발급](https://github.com/Microsoft/sqlopsstudio/issues/1332): 편집 데이터 되돌릴 행 작동 하지 않습니다
   - 해결 [1215 발급](https://github.com/Microsoft/sqlopsstudio/issues/1215): SQL Agent 확장 및 상태 표시줄
   - 해결 [1316 발급](https://github.com/Microsoft/sqlopsstudio/issues/1316): windows가 크기 변경 후 크기를 조정할 SQL 에이전트 하지 않음


자세한 내용은 참조는 [변경 로그](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md), 및 [릴리스](https://github.com/Microsoft/sqlopsstudio/releases)합니다.



## <a name="april-2018-april-public-preview"></a>년 4 월 2018 (년 4 월 공개 미리 보기)

릴리스 날짜: 2018 년 4 월 25,  
버전: 0.28.6

*공개 미리 보기 4 월* 버그 수정 및 향상 된 기능을 포함 합니다. 

- SQL 에이전트 미리 보기 확장 개선 되었습니다.
- 개선 된 보호는 관리자를 저장 하기 위한 광범위 하 고 보호 된 파일 지원 및 > SQL 작업 Studio 내에서 256 M 파일입니다.
- 한 번에 여러 개의 열기 터미널 작업할 터미널 분할을 통합 합니다.
- 줄어든된 설치 디스크에 파일 개수 발 더 빠른 설치 및 시작 시간에 인쇄 합니다.
- GitHub 문제를 해결 하도록 계속 진행 합니다.
   - 해결 [37 발급](https://github.com/Microsoft/sqlopsstudio/issues/37): 차트 뷰어에 오류를 throw 하면 예기치 않은 동작이 발생 합니다.
   - 해결 [462 발급](https://github.com/Microsoft/sqlopsstudio/issues/462): 기능 요청: 기본적으로 확장 하는 서버 그룹에 대 한 옵션입니다.
   - 해결 [606 발급](https://github.com/Microsoft/sqlopsstudio/issues/606): intellisense-'update' 명령에 대 한 잘못 된 제안 합니다.
   - 해결 [967 발급](https://github.com/Microsoft/sqlopsstudio/issues/967): 쿼리 계획을 예상 결과 표에서 XML 실행 계획을 선택 하는 경우.
   - 해결 [1023 발급](https://github.com/Microsoft/sqlopsstudio/issues/1023): flyfishingdba에서 ms_foreachdb 호출에 대 한 대괄호를 추가 합니다.
   - 해결 [1048 발급](https://github.com/Microsoft/sqlopsstudio/issues/1048): SSL/TLS 사전 로그인 핸드셰이크 오류입니다.
   - 해결 [1050 발급](https://github.com/Microsoft/sqlopsstudio/issues/1050): 지우기 insights 오류를 표시 하기 전에 확인 합니다.
   - 해결 [1057 발급](https://github.com/Microsoft/sqlopsstudio/issues/1057): 위젯 탐색기의에서 새 쿼리 작업 및 복원 끊어집니다.
   - 해결 [1068 발급](https://github.com/Microsoft/sqlopsstudio/issues/1068): 대시보드 출력 windows 나타납니다 Azure SQL 데이터베이스에 대 한 오류 메시지와 함께 합니다.
   - 해결 [1069 발급](https://github.com/Microsoft/sqlopsstudio/issues/1069): 연결 대화 상자에 처음 표시 될 때 필요한 서버 오류가 표시 됩니다.
   - 해결 [1070 발급](https://github.com/Microsoft/sqlopsstudio/issues/1070): 서버 그룹은 이제 확장을 두 번 클릭을 요구 합니다.
   - 해결 [1072 발급](https://github.com/Microsoft/sqlopsstudio/issues/1072): 선택 컨트롤 배경은 반투명 합니다.
   - 해결 [1115 발급](https://github.com/Microsoft/sqlopsstudio/issues/1115): SQL 작업 Studio의 모든 고대비 액세스 가능성 문제를 해결 합니다.
   - 해결 [1101 발급](https://github.com/Microsoft/sqlopsstudio/issues/1101): 확장 실패 업그레이드 "다운로드" 수동으로 링크에 잘못 된 위치로 이동 합니다.
   - 해결 [1103 발급](https://github.com/Microsoft/sqlopsstudio/issues/1103): V 스크롤 홈 탭에서 작동 하지 않습니다.
   - 해결 [1104 발급](https://github.com/Microsoft/sqlopsstudio/issues/1104): SQL 확장 탭 작동을 중지 합니다.


년 4 월 공개 미리 보기에 대 한 중요 한 강조는 Visual Studio 코드 1.21 플랫폼 소스 코드 새로 고치십시오. 이렇게 이전 1.19 동기화 지점에서 코어 편집기 및 워크 벤치를 여러 번 업데이트 됩니다. 몇 가지 예는 다음과 같습니다.

- [새 알림 UI](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui) -쉽게 관리 하 고 SQL 작업 Studio 알림을 검토 합니다.
- [터미널 분할 통합](https://code.visualstudio.com/updates/v1_21#_split-terminals) -여러 개의 열기 터미널을 한 번에 사용 합니다.
- [광범위 하 고 보호 된 파일을 저장](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges) -보호 관리 저장 및 > SQL 작업 Studio 내에서 256 M 파일입니다.
- [큰 파일을 지 원하는 향상 된](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements) -큰 파일에 대 한 텍스트 버퍼 최적화 합니다.
- [향상 된 설정 검색](https://code.visualstudio.com/updates/v1_20#_settings-search) -쉽게 자연어 검색 오른쪽 설정을 찾습니다.
- [전역 코드 조각을](https://code.visualstudio.com/updates/v1_20#_global-snippets) -모든 파일 형식에 대해 사용할 수 있습니다 조각 만들기.
- [탐색기 다중 선택](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer) -한 번에 여러 파일에 대해 작업을 수행 합니다.
- [오류 및 경고 탐색기에서](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer) -구조화 코드 베이스의 오류를 이동 합니다.
- [끌어 및 삭제, 복사 및 붙여넣기 전체 windows](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support) -열려 있는 SQL 작업 Studio 창을 통해 파일을 이동 합니다.
- [Git 하위 모듈 지원](https://code.visualstudio.com/updates/v1_20#_git-submodules) -중첩 된 Git 리포지토리에 대 한 Git 수행 작업 합니다.
- [터미널 화면 판독기 지원](https://code.visualstudio.com/updates/v1_20#_screen-reader-support) -통합 된 터미널은 이제 "화면 판독기 최적화" 모드에 있습니다.
- [가운데에 맞출지 편집기 레이아웃](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout) -코드 보기 화면 공간을 최대화 합니다.
- [가로 검색 결과 (미리 보기)](https://code.visualstudio.com/updates/v1_21#_horizontal-search) -이제 가로 패널에서 검색 결과 보기를 할 수 있습니다.

자세한 내용은 체크 아웃의 [Visual Studio 코드 2 월 릴리스 정보](https://code.visualstudio.com/updates/v1_21), 및 [Visual Studio 코드 년 1 월 릴리스 정보](https://code.visualstudio.com/updates/v1_20)합니다.

자세한 내용은 참조는 [변경 로그](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md)합니다.

## <a name="march-2018-march-public-preview"></a>년 3 월 2018 (공개 미리 보기 3 월)

릴리스 날짜: 2018 년 3 월 28,  
버전: 0.27.3

*공개 미리 보기 3 월* 은 계속 상위 GitHub 문제를 해결 하 고 확장성 이야기 향상에 포커스가 있습니다. 특히 확장 관리자를 사용 하도록 설정, 올바른 대시보드 관리 및 SQL 에이전트 및 insights 확장을 제공 합니다. 이 릴리스에 다음과 같은 향상 기능이 포함 되어 있습니다.

- Insights 탭된 및 창 구성 지원 하기 위해 대시보드 확장성 모델을 향상 시킵니다.
   - 확장 관리자에서 확장의 간단한 취득이 있습니다.
   - sp_whoisactive에 대 한 대시보드 확장 [whoisactive.com](http://www.whoisactive.com)합니다.
   - 자세한 내용은 참조 [SQL 작업 Studio의 기능을 확장할](extensions.md)합니다.
- 더 추가 [연결 및 개체 탐색기에 대 한 확장성 Api](https://github.com/Microsoft/sqlopsstudio/wiki/Extensibility-API) 관리 합니다.
- 영향을 미치는 중요 한 고객을 해결 하려면 계속 [GitHub 문제](https://github.com/Microsoft/sqlopsstudio/issues)합니다.


## <a name="february-2018-february-public-preview"></a>2 월 2018 (공개 미리 보기 2 월)

릴리스 날짜: 2018 년 2 월 15,  
버전: 0.26.7

*공개 미리 보기 2 월* 몇 가지 기능 제안 및 우선 순위가 높은 버그 수정 포함 됩니다. 이 릴리스에 다음과 같은 향상 기능이 포함 되어 있습니다.

- 자동 업데이트 설치를 도입 알림을 제공 하는 새 릴리스는 다운로드 하 여 사용할 때 
- 연결 대화 상자 'Database' 필드는 동적으로 채워진된 드롭다운 목록에서 지정된 된 서버에서 채워진 데이터베이스 목록이 포함 될 되었습니다.
- 해결 [6 발급](https://github.com/Microsoft/sqlopsstudio/issues/6): 새 쿼리 탭을 열 때 연결 하 고 선택한 데이터베이스를 유지 합니다.
- 해결 [22 발급](https://github.com/Microsoft/sqlopsstudio/issues/22): ' 서버 이름 ' 및 ' 데이터베이스 이름 '-수 이러한 드롭다운 텍스트 상자 대신 수 있습니까?
- 해결 [549 발급](https://github.com/Microsoft/sqlopsstudio/issues/549): 설치 후에 여는 응용 프로그램으로 인해 자동/매우 자동 설치 합니다.
- 해결 [481 발급](https://github.com/Microsoft/sqlopsstudio/issues/481): "업데이트 확인" 옵션을 추가 합니다.
- SQL 편집기 색 지정 및 자동 완성 수정 사항:
   - 해결 [584 발급](https://github.com/Microsoft/sqlopsstudio/issues/584): IntelliSense에서 키워드 "완전히" 강조 표시 되지 않습니다.
   - 해결 [345 발급](https://github.com/Microsoft/sqlopsstudio/issues/345): 편집기에서 색을 지정 하는 SQL 함수입니다.
   - 해결 [300 발급](https://github.com/Microsoft/sqlopsstudio/issues/300): [#tempData] 최신 "]" 녹색이 표시 됩니다.
   - 해결 [225 발급](https://github.com/Microsoft/sqlopsstudio/issues/225): 키워드 색 일치 하지 않습니다.
   - 해결 [60 발급](https://github.com/Microsoft/sqlopsstudio/issues/60): 잘못 된 sql 구문을 컬러 강조 표시 from 절에서 임시 테이블을 사용 하는 경우.
- 연결 확장성 API를 소개 합니다.
- VS 코드 편집기 1.19 통합 합니다.
- 여러 가지 쿼리 계획에 대 한 뷰어 향상 기능이 JustinPealing/html-쿼리 계획 구성 요소 선택 하도록 업데이트 됩니다.


## <a name="january-2018-january-public-preview"></a>1 월 2018 (공개 미리 보기 1 월)

릴리스 날짜: 2018 년 1 월 17,  
버전: 0.25.4

*년 1 월 공개 미리 보기* 몇 가지 기능 제안 및 우선 순위가 높은 버그 수정 포함 됩니다. 이 릴리스에 다음과 같은 향상 기능이 포함 되어 있습니다.

- 저장 된 서버 연결을 연결 대화 상자에서 사용할 수 있습니다.
- 핫 종료를 사용 하도록 설정 합니다. 핫 종료 참조를 사용 하도록 설정 하려면 기본적으로 해제 되어 [핫 종료 설정을](settings.md#hot-exit)합니다.
- 탭 색 지정 서버 그룹에 기반 합니다. 참조를 사용 하도록 설정 하려면 기본적으로 꺼져 탭 색 지정 [탭 색 설정을](settings.md#tab-color)합니다.
- 변경 *서버 이름* 를 *서버* 연결 대화 상자에서.
- 손상 수정 *현재 쿼리 실행* 명령입니다.
- 끌어서 놓기 주요 스크립팅 버그를 수정 합니다.
- 잘못 된 고정 된 시작 메뉴 아이콘을 수정 합니다.
- 누락 된 Azure 계정 브랜딩 아이콘을 수정 합니다.


## <a name="december-2017-december-public-preview"></a>2017 년 12 월 (공개 미리 보기 년 12 월)

릴리스 날짜: 2017 년 12 월 19  
버전: 0.24.1

*년 12 월 공개 미리 보기* 다양 한 버그 수정 사항이 모든 기능 영역으로는 다음과 같은 향상 기능이 포함 됩니다.

- 만들 이제 방화벽 규칙 대화 상자를 Azure SQL 데이터베이스 및 Azure SQL 데이터 웨어하우스 연결을 지원 하기 위해 사용할 수 있습니다.
- 추가 된 Windows 설치 프로그램 및 Linux DEB 및 RPM 설치 패키지입니다.
- 대시보드 시각적 레이아웃 편집기를 관리 합니다.
- *변경 스크립트* 및 *실행으로 스크립트* 명령입니다.
- *실제 계획으로 현재 쿼리를 실행* 명령입니다.
- VS Code 1.18.1 편집기 플랫폼을 통합 합니다.
- VSIX 확장 테스트용으로 로드할 파일을 사용 하도록 설정 합니다.
- "N 이동" 일괄 처리 반복 구문을 지원 합니다.


## <a name="november-2017"></a>2017 년 11 월

릴리스 날짜: 2017 년 11 월 15  
버전: 0.23.6

- 초기 버전의 [!INCLUDE[name-sos](../includes/name-sos-short.md)]합니다.


## <a name="next-steps"></a>다음 단계

시작 하려면 다음 퀵 스타트 중 하나를 참조 합니다.
- [SQL Server 연결 및 쿼리](quickstart-sql-server.md)
- [Azure SQL 데이터베이스 연결 및 쿼리](quickstart-sql-database.md)
- [Azure 데이터 웨어하우스 연결 및 쿼리](quickstart-sql-dw.md)

[!INCLUDE[name-sos](../includes/name-sos-short.md)]에 기여하기:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio)
