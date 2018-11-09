---
title: Azure Data Studio 릴리스 정보 | Microsoft Docs
description: Azure Data Studio 릴리스 정보
ms.custom: tools|sos
ms.date: 11/06/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8a330c046d5e8398d03302863013ab9b0c1df37f
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269966"
---
# <a name="azure-data-studio-release-notes"></a>Azure Data Studio 릴리스 정보

**[11 월 릴리스를 다운로드 하십시오!](download.md)**

## <a name="november-2018-november-release"></a>2018 년 11 월 (11 월 릴리스)

릴리스 날짜: 2018 년 11 월 6 일  
버전: 1.2.4

- Idera 확장 소개
- 업데이트 된 [SQL Server 2019 미리 보기 확장](https://docs.microsoft.com/sql/azure-data-studio/sql-server-2019-extension?view=sql-server-ver15)
- 붙여넣기 계획 확장 소개
- 하이 컬러 쿼리 확장이 포함 되 면 SSMS 편집기 테마를 소개 합니다.
- SQL Server 에이전트, Profiler, 및 가져오기 확장의 수정
- .NET Core 해결 macOS에서 비활성 연결을 삭제 소켓 KeepAlive 문제 발생
- .NET Core에 SQL 도구 서비스 업그레이드 (지원용 최종 AAD) 2.2 미리 보기 3

### <a name="bug-fixes"></a>버그 수정
- 수정 [#2933 발급](https://github.com/Microsoft/azuredatastudio/issues/2933): Azure SQL DB에 연결 손실
- 수정 [#2914 발급](https://github.com/Microsoft/azuredatastudio/issues/2914): OE 데이터베이스 노드를 확장 하는 "잘못 된 인수" 예외
- 수정 [#2935 발급](https://github.com/Microsoft/azuredatastudio/pull/2935): 쿼리 결과에 여러 줄 메시지를 올바르게 표시
- 수정 [#2906 발급](https://github.com/Microsoft/azuredatastudio/pull/2906): 데이터를 편집 수정 문서 이름 테이블 이름에 특수 문자가 포함 된 경우
- 수정 [#2929 발급](https://github.com/Microsoft/azuredatastudio/issues/2929): 빌드된 changelog 라는 확장에서 변경 내용에 대 한 VSCode 릴리스를 확인 하려면
- 수정 [#2719 발급](https://github.com/Microsoft/azuredatastudio/issues/2719): 고대비 테마 double/삼중 아이콘
- 수정 [#3047 발급](https://github.com/Microsoft/azuredatastudio/pull/3047): SQL Server에 연결 하기 위한 명령줄 인터페이스를 추가 합니다.
- 수정 [#3031 발급](https://github.com/Microsoft/azuredatastudio/pull/3031): 쿼리 계획 테마 지원 추가
- ...

자세한 내용은 참조는 [변경 로그](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), 및 [릴리스](https://github.com/Microsoft/azuredatastudio/releases)합니다.

## <a name="october-2018-october-release"></a>2018 년 10 월 (10 월 릴리스)

릴리스 날짜: 2018 년 10 월 29 일  
버전: 1.1.4

- Azure SQL Database를 이동할 Azure 리소스 탐색기를 소개 합니다.
- 개체 탐색기와 쿼리 편집기에 해당 하는 연결의 견고성을 향상
- SQL 에이전트 확장 향상 된 기능
- 업데이트 된 [SQL Server 2019 미리 보기 확장](https://docs.microsoft.com/sql/azure-data-studio/sql-server-2019-extension?view=sql-server-ver15)

### <a name="bug-fixes"></a>버그 수정
- 수정 [#2717 발급](https://github.com/Microsoft/azuredatastudio/issues/2717): XML 열으로 된 결과 형식을 클릭
- 수정 [#2993 발급](https://github.com/Microsoft/azuredatastudio/issues/2993): 너비의 결과 windows 완전 하지 않습니다.
- 수정 [#2999 발급](https://github.com/Microsoft/azuredatastudio/issues/2999): DB에 연결 하는 경우 Mac에서 System.Diagnostics.Tracing 파일을 로드할 수 없습니다
- 수정 [#2851 발급](https://github.com/Microsoft/azuredatastudio/issues/2851): 시계열 차트 제대로 렌더링 되지 않습니다.
- 수정 [#2996 발급](https://github.com/Microsoft/azuredatastudio/issues/2996): 임시 갑자기 세션 변경으로 인해 테이블 손실
- ...

자세한 내용은 참조는 [변경 로그](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), 및 [릴리스](https://github.com/Microsoft/azuredatastudio/releases)합니다.

## <a name="september-2018-september-ga-release"></a>2018 년 9 월 (9 월 GA 릴리스)

릴리스 날짜: 2018 년 9 월 24 일  
버전: 1.0

Azure Data Studio (이전의 SQL Operations Studio)의 일반 공급 릴리스 합니다.

- SQL Server 2019 미리 보기 확장을 발표합니다.
  - 포함 하 여 SQL Server 2019 미리 보기 기능에 대 한 지원 [빅 데이터 클러스터](../big-data-cluster/big-data-cluster-overview.md) 지원 합니다.
    - 게이트웨이에 연결 하 여 HDFS/Spark SQL Server 2019 미리 보기와 함께 제공 합니다.
    - HDFS 찾아보기, 파일 업로드, 파일을 저장 및 CSV 파일에 대 한 전자 필기장에서 분석 등의 유용한 작업을 시작 합니다.
    - 대시보드에서 Spark 작업을 제출 하거나 개체 탐색기에서 HDFS/Spark 연결을 마우스 오른쪽 단추로 클릭 합니다.
  - Azure Data Studio Notebook
    - 만들거나 통합된 Notebook 뷰어를 사용 하 여 Notebook을 엽니다. 이 릴리스에서 Notebook 뷰어는 로컬 커널 및 SQL Server 2019 빅 데이터 클러스터에 연결을 지원 합니다.
    - Notebook에서 PROSE 코드 Accelerator 라이브러리를 사용 하 여 빠른 데이터 준비에 대 한 파일 형식 및 데이터 형식에 알아봅니다.
  - Azure 리소스 탐색기
    - Azure 리소스 탐색기 보기를 사용 하 여 Azure 계정에 대 한 끝점 관련 된 데이터를 이동 하 고 개체 탐색기에 대 한 연결을 만들 수 있습니다. 이 릴리스에서 Azure SQL Database 및 서버 지원 됩니다.
  - SQL Server PolyBase 외부 테이블 마법사 만들기
    - 사용이 간편한 마법사를 사용 하 여 외부 테이블 및 지 원하는 메타 데이터 구조를 만듭니다. 이 릴리스에서 원격 SQL Server 및 Oracle 서버는 지원 됩니다.
- 쿼리 결과 표 성능 및 많은 수의 결과 집합에 대 한 UX 향상 합니다.
- 모눈 레이아웃 및 설정 편집기 개선 (미리 보기)를 사용 하 여 1.26.1를 1.23에서 visual Studio Code 소스 코드 새로 고칩니다.
- 화면 판독기, 키보드 탐색 및 고대비에 대 한 내게 필요한 옵션 개선 사항입니다.
- 추가 `Connection name` 서버 보기 사용에는 다른 표시 이름을 제공 하는 옵션입니다.

### <a name="bug-fixes"></a>버그 수정

- 수정 [#2647 발급](https://github.com/Microsoft/azuredatastudio/issues/143): 차트를 큰 단계는 이전 버전과 이었습니다.
- 수정 [#2648 발급](https://github.com/Microsoft/azuredatastudio/issues/143): JSON 하이퍼링크 전체 열을 반환 하는 선택 합니다.
- ...

자세한 내용은 참조는 [변경 로그](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), 및 [릴리스](https://github.com/Microsoft/azuredatastudio/releases)합니다.


## <a name="august-2018-august-public-preview"></a>2018 년 8 월 (8 월 공개 미리 보기)

릴리스 날짜: 2018 년 8 월 30 일  
버전: 0.32.8

*0.32.8 0.32.7 있는 몇 가지 회귀에 대 한 수정 프로그램이 포함 되어 있습니다 ([#1971](https://github.com/Microsoft/azuredatastudio/issues/1971)하십시오 [#2372](https://github.com/Microsoft/azuredatastudio/issues/2372)*)

합니다 *년 8 월 공개 미리 보기* 버그 수정, 제품 안정화 및 기존 시나리오의 간격을 채우는에 중점을 둡니다.  

- SQL Server 가져오기 확장 발표
- SQL Server Profiler 세션 관리
- SQL Server Profiler 세션 템플릿 지원
- SQL Server 에이전트의 향상 된 기능
- 새 커뮤니티 확장: 첫 번째 응답자 키트
- 수명 품질 향상: 연결 문자열

### <a name="bug-fixes"></a>버그 수정

- 쿼리 편집기 창에서 SQL을 사용 하 여 구문 분석 된 `Parse Syntax` 명령입니다.
- 수정 [#143 발급](https://github.com/Microsoft/azuredatastudio/issues/143): 변수 이름의 선택 하지 않으면 두 번 클릭 합니다.
- 수정 [문제 #387](https://github.com/Microsoft/azuredatastudio/issues/387): SQL 탭 DB 아이콘은 빨간색입니다.
- 수정 [#825 발급](https://github.com/Microsoft/azuredatastudio/issues/825): 요청: 자동으로 스크립트 다음 현재 서버에 연결 하는 중... 
- 수정 [#1278 발급](https://github.com/Microsoft/azuredatastudio/issues/1278): sqlops.desktop [데스크톱 항목]-이름 및 설명에 대 한 중복 값입니다.
- 수정 [#1285 발급](https://github.com/Microsoft/azuredatastudio/issues/1285): 업데이트 하면 응용 프로그램 아이콘을 제거 하 고 대체 Windows에서.
- 수정 [#1317 발급](https://github.com/Microsoft/azuredatastudio/issues/1317): 소수 구분 기호를 수정 합니다.
- 수정 [#1474 발급](https://github.com/Microsoft/azuredatastudio/issues/1474): 연결 변경 취소는 현재 연결을 끊습니다.
- 수정 [#1497 발급](https://github.com/Microsoft/azuredatastudio/issues/1497): 아래쪽 옵션 잘립니다 차트로 보기.
- 수정 [#1524 발급](https://github.com/Microsoft/azuredatastudio/issues/1524): 셸/대시보드: 주 viewlet 아이콘 draggable 되며 응용 프로그램 크래시가 발생할 수 있습니다.
- 수정 [#1578 발급](https://github.com/Microsoft/azuredatastudio/issues/1578): 이름을 클릭 하 여 원격 파일 브라우저 폴더를 확장/축소 수 없습니다.
- 수정 [#1620 발급](https://github.com/Microsoft/azuredatastudio/issues/1620): 기능 제안: 기존 연결에 대 한 연결 문자열을 가져옵니다.
- 수정 [#1624 발급](https://github.com/Microsoft/azuredatastudio/issues/1624): SelectBox 사용 하지 않도록 설정 하는 경우 색을 변경 하지 않습니다.
- 수정 [#1728 발급](https://github.com/Microsoft/azuredatastudio/issues/1728): JSON/EXCEL/CSV 작동 하지 않음로 저장 합니다.
- 수정 [#1744 발급](https://github.com/Microsoft/azuredatastudio/issues/1744): 결과 창 탭 간에 전환 하는 경우 해당 스크롤 위치를 손실 됩니다.
- 수정 [#1748 발급](https://github.com/Microsoft/azuredatastudio/issues/1748): Excel 파일 두 번째 (및 후속) 시간을 절약 하는 경우 오류 메시지입니다.
- 수정 [#1782 발급](https://github.com/Microsoft/azuredatastudio/issues/1782): 데이터를 편집: 셀 이스케이프 키를 눌러 원래 값으로 되돌리기 하지 않습니다.
- 수정 [#1836 발급](https://github.com/Microsoft/azuredatastudio/issues/1836): SQL Operations Studio 사용 하 여 연결 되지 않은.sql 파일입니다.
- 수정 [#1850 발급](https://github.com/Microsoft/azuredatastudio/issues/1850): 입력 N ' n 자동 완성 ' '입니다.
- 수정 [#1985 발급](https://github.com/Microsoft/azuredatastudio/issues/1985): 쿼리 결과 표 형태에서 복사 1 열으로 해제 되어 있습니다.
- 수정 [#1998 발급](htpts://github.com/Microsoft/azuredatastudio/pull/1998): VS Code 추가 버전을 대화에 대 한 합니다.
- 수정 [#2042 발급](https://github.com/Microsoft/azuredatastudio/pull/2042): 에이전트: sql 파일에서 쿼리 가져오기 단추를 사용 하도록 설정된 합니다.
- 수정 [#2091 발급](https://github.com/Microsoft/azuredatastudio/issues/2091): 바로 가기 Ctrl + C를 사용 하 여 결과 창에서 복사할 수 없습니다.
- 수정 [#2099 발급](https://github.com/Microsoft/azuredatastudio/pull/2099): saveAsCsv 옵션이 더 추가 합니다.
- 수정 [#2107 발급](https://github.com/Microsoft/azuredatastudio/issues/2107): 대시보드 및 Profiler 문서에 대 한 문서 아이콘 업데이트 합니다.
- 수정 [#2129 발급](https://github.com/Microsoft/azuredatastudio/pull/2129): 탭을 전환 하는 경우 스크롤 위치를 편집 데이터를 저장 합니다.
- 수정 [#2152 발급](https://github.com/Microsoft/azuredatastudio/issues/2152): 결과 그리드 행 표시기 0 기반 합니다.

## <a name="known-issues"></a>알려진 문제

- [문제 #2371](https://github.com/Microsoft/azuredatastudio/issues/2371) Excel 데이터의 첫 번째 행만 저장 하는 대로 저장
- [문제 #2150](https://github.com/Microsoft/azuredatastudio/issues/2150): Ubuntu 16.04를 컨테이너에는 SQL에 연결할 수 없습니다.


## <a name="july-2018-july-public-preview"></a>2018 년 7 월 (7 월 공개 미리 보기)

릴리스 날짜: 2018 년 7 월 19 일  
버전: 0.31.4

합니다 *월 공개 미리 보기* 고객이 보고 한 GitHub 문제에 대 한 초기 릴리스의 SQL Server 에이전트 구성 시나리오, SQL Server Profiler 세션 및 보기 템플릿 향상 및 지속적인된 버그 수정에 중점을 둡니다. 이 릴리스에 다음 주요 사항을 포함 됩니다.  

- [SQL Operations Studio 확장에 대 한 SQL Server 에이전트](sql-server-agent-extension.md) 개선 사항
 - 왼쪽된 창에서 경고, 운영자 및 프록시 및 아이콘 추가 보기
 - 새 작업, 새 작업 단계, 새 경고 및 새 연산자에 대 한 추가 대화 상자
 - 추가 된 삭제 작업, 경고를 삭제 및 Delete 연산자 (마우스 오른쪽 단추로 클릭)
 - 이전에 실행 된 시각화 추가
 - 각 열 이름에 대 한 추가 필터
- [SQL Operations Studio 확장에 대 한 SQL Server Profiler](sql-server-profiler-extension.md) 개선 사항
 - 신속 하 게 시작 하 고 시작/중지 Profiler 추가 바로 가기 키
 - 확장 이벤트를 보기 위해 5 개의 기본 템플릿 추가
 - 추가 서버/데이터베이스 연결 이름
 - Azure SQL Database 인스턴스에 대 한 지원 추가
 - Profiler 실행 되는 경우 탭 닫힐 때 Profiler를 종료 하려면 추가 제안
- 릴리스의 결합 스크립트 확장
- 확장 작성자가 추가 하는 마법사 및 대화 확장성 지점
- GitHub 문제를 해결 합니다.
 - 수정 [728 발급](https://github.com/Microsoft/azuredatastudio/issues/728): macOS에서 추가 연결에 응답
 - 수정 [1612 발급](https://github.com/Microsoft/azuredatastudio/issues/1612): 결과 표에서 텍스트 표시는 중 문제가 발생 한 국제 문자로
 - 수정 [1693 발급](https://github.com/Microsoft/azuredatastudio/issues/1693): 백업 대화 상자: 파일 브라우저 UI 손상 되었습니다.
 - 수정 [1713 발급](https://github.com/Microsoft/azuredatastudio/issues/1713): 영향을 받는 행 수
 - 수정 [1718 발급](https://github.com/Microsoft/azuredatastudio/issues/1718): 모든 데이터 원본에 연결할 수 없습니다.
 - 수정 [1719 발급](https://github.com/Microsoft/azuredatastudio/issues/1719): 서버에 연결할 때 TypeError
 - 수정 [1724 발급](https://github.com/Microsoft/azuredatastudio/issues/1724): 작업 중지 확장 대화 상자
 - 수정 [1749 발급](https://github.com/Microsoft/azuredatastudio/issues/1749): 버그: 열에 HTML 데이터 해석
 - 수정 [1789 발급](https://github.com/Microsoft/azuredatastudio/issues/1789): 확장성: 연결 공급자를 추가 하는 경우 제거 되지에서 제거 됩니다 목록
 - 수정 [1791 발급](https://github.com/Microsoft/azuredatastudio/issues/1791): Sqlops 확장: queryeditor.connect() 대상 데이터베이스에 연결 하지만 UI 편집기가 연결 되는 표시 되지 않습니다
 - 수정 [1799 발급](https://github.com/Microsoft/azuredatastudio/issues/1799): 상위 10 DB 크기 차트에서는 대/소문자 구분 인스턴스가 작동 하지 않습니다
 - 수정 [1814 발급](https://github.com/Microsoft/azuredatastudio/issues/1814): sqlops.d.ts 오타로 인해 암시적인 'any' 형식 정의
 - 수정 [1817 발급](https://github.com/Microsoft/azuredatastudio/issues/1817): 오류 de Ortografia
 - 수정 [1830 발급](https://github.com/Microsoft/azuredatastudio/issues/1830): component() 호출 된 후 iconPath ButtonComponent에서 설정 아이콘 변경 되지 않습니다
 - 수정 [1843 발급](https://github.com/Microsoft/azuredatastudio/issues/1843): 더 나은 테이블 구성


## <a name="june-2018-june-public-preview"></a>2018 년 6 월 (6 월 공개 미리 보기)

릴리스 날짜: 2018 년 6 월 20 일  
버전: 0.30.6

합니다 *년 6 월 공개 미리 보기* 다음 중요 정보를 포함 합니다.  

- **SQL Operations Studio 대 한 SQL Server Profiler *미리 보기***  확장 초기 릴리스.
- 새 **SQL Data Warehouse** 확장 data warehouse에 정보를 표시 하는 다양 한 사용자 지정 가능한 대시보드 위젯을 포함 합니다. 이 관리 및 튜닝에 일관 된 성능을 최적화 하도록 데이터 웨어하우스 관련 주요 시나리오를 잠금 해제 합니다.
- **데이터를 "필터링 및 정렬할" 편집** 지원 합니다.
- **SQL Operations Studio 대 한 SQL Server 에이전트 *미리 보기***  확장의 향상 된 기능 작업 및 작업 기록 보기.
- 개선 **마법사 및 대화 상자 UI 작성기 프레임 워크** 확장성 Api입니다.
- VS 코드 플랫폼 소스 코드 통합 업데이트 [2018 년 3 월 (1.22)](https://code.visualstudio.com/updates/v1_22) 하 고 [2018 년 4 월 (1.23)](https://code.visualstudio.com/updates/v1_23) 해제 합니다.
- GitHub 문제를 해결 합니다.
  - 기능 요청 ([1204 발급](https://github.com/Microsoft/azuredatastudio/issues/1204)): 하세요 데이터를 결과 그리드 자동 맞춤 열 너비를 확인 및/또는 동일한 쿼리가 다시 실행 하는 경우 수동으로 변경 해야 합니다.
  - 수정 [1398 발급](https://github.com/Microsoft/azuredatastudio/issues/1398): 연결 된 계정 비어 있을 때 메시지 추가한 계정을 계정 단추 표시 추가 해야 합니다.
  - 수정 [1399 발급](https://github.com/Microsoft/azuredatastudio/issues/1399): 뷰를 축소할 때 연결 된 계정 탭은 중단 합니다.
  - 수정 [1374 발급](https://github.com/Microsoft/azuredatastudio/issues/1374): 디스크에서.sql 파일을 열면 SQL 도구 서비스가 충돌 합니다.
  - 수정 [1372 발급](https://github.com/Microsoft/azuredatastudio/issues/1372): 누락 된 SQL 키워드 "BETWEEN"입니다.
  - 수정 [1395 발급](https://github.com/Microsoft/azuredatastudio/issues/1395): '일치' 키워드는 SQL 도구 서비스가 충돌 합니다.
  - 수정 [1496 발급](https://github.com/Microsoft/azuredatastudio/issues/1496): 개체 탐색기에서 상황에 맞는 메뉴 옵션 "새 Profiler" 아무 작업도 수행 합니다.
  - 수정 [1495 발급](https://github.com/Microsoft/azuredatastudio/issues/1495): 쿼리 편집기 "설명" 쿼리 계획 손상 되었습니다.


## <a name="may-2018-may-public-preview"></a>2018 년 5 월 (월 공개 미리 보기)

릴리스 날짜: 2018 년 5 월 7 일  
버전: 0.29.3

합니다 *공개 미리 보기로 제공 될 수 있습니다* 안정화 및 버그 수정에 포커스가 있습니다. 이 빌드에는 다음 주요 사항을 포함합니다.  

- 확장 관리자에서 사용 하 여 사용할 수 있는 Redgate SQL 검색 확장을 발표합니다.
- 10 개 언어에 사용할 수 있는 커뮤니티 지역화: 독일어, 스페인어, 프랑스어, 이탈리아어, 일본어, 한국어, 포르투갈어, 러시아어, 중국어 간체 및 중국어 (번체).
- 축소 된 원격 분석 수집, 개선 된 옵트아웃 및 개인정보취급방침 대 한 제품 내 링크입니다.
- 확장 관리자 환경을 쉽게 커뮤니티 확장을 검색 하는 향상 된 Marketplace에 있습니다.
- SQL 에이전트 확장 작업 및 작업 기록 보기 개선 합니다.
- Whoisactive 및 서버 보고서에 대 한 확장을 업데이트합니다.
- 관리 대시보드 속성 스크롤 개선 합니다.
- GitHub 문제를 해결 합니다.
   - 수정 [703 발급](https://github.com/Microsoft/azuredatastudio/issues/703): 편집 데이터에 html 텍스트를 입력 하면 값이 새로 고침까지 제대로 표시 되지 않음
   - 수정 [821 발급](https://github.com/Microsoft/azuredatastudio/issues/821): azuredatastudio.deb 패키지 종속성
   - 수정 [1260 발급](https://github.com/Microsoft/azuredatastudio/issues/1260): 'distinct' 강조 표시 되지 않은 키워드
   - 수정 [1332 발급](https://github.com/Microsoft/azuredatastudio/issues/1332): 편집 데이터 되돌릴 행 작동 하지 않습니다
   - 수정 [1215를 발급](https://github.com/Microsoft/azuredatastudio/issues/1215): SQL Agent 확장 및 상태 표시줄
   - 수정 [1316 발급](https://github.com/Microsoft/azuredatastudio/issues/1316): windows 크기 변경 후 크기를 조정 SQL 에이전트 하지 않음




## <a name="april-2018-april-public-preview"></a>2018 년 4 월 (4 월 공개 미리 보기)

릴리스 날짜: 2018 년 4 월 25 일  
버전: 0.28.6

합니다 *공개 미리 보기 4 월* 버그 수정 및 개선 사항이 포함 되어 있습니다. 

- SQL 에이전트 미리 보기 확장 개선 되었습니다.
- 향상 된 보호 하는 관리자를 저장 하기 위한 대규모 및 보호 된 파일 지원 및 > SQL Operations Studio 내의 256m 파일입니다.
- 통합된 터미널을 한 번에 여러 열고 터미널을 사용 하 여 작업을 분할 합니다.
- 축소 된 설치 디스크에 있는 파일 수 피트 빠른 설치 및 시작 시간에 인쇄 합니다.
- GitHub 문제를 해결 하려면 계속 진행 합니다.
   - 수정 [37 발급](https://github.com/Microsoft/azuredatastudio/issues/37): 차트 뷰어에 오류를 throw 하면 예기치 않은 동작이 발생 합니다.
   - 수정 [462 발급](https://github.com/Microsoft/azuredatastudio/issues/462): 기능 요청: 기본적으로 확장 하는 서버 그룹에 대 한 옵션입니다.
   - 수정 [606 발급](https://github.com/Microsoft/azuredatastudio/issues/606): intellisense-'update' 명령에 대 한 잘못 된 제안 합니다.
   - 수정 [967 발급](https://github.com/Microsoft/azuredatastudio/issues/967): 쿼리 계획을 예상 결과 그리드에서 XML 실행 계획을 선택 하는 경우.
   - 수정 [1023 발급](https://github.com/Microsoft/azuredatastudio/issues/1023): flyfishingdba에서 ms_foreachdb 호출에 대 한 대괄호를 추가 합니다.
   - 수정 [1048 발급](https://github.com/Microsoft/azuredatastudio/issues/1048): 사전 로그인 SSL/TLS 핸드셰이크 오류입니다.
   - 수정 [1050 발급](https://github.com/Microsoft/azuredatastudio/issues/1050): 지우기 insights 오류를 표시 하기 전에 확인 합니다.
   - 수정 [1057 발급](https://github.com/Microsoft/azuredatastudio/issues/1057): 복원 작업과 새 쿼리 탐색기 위젯에서 끊어집니다.
   - 수정 [1068 발급](https://github.com/Microsoft/azuredatastudio/issues/1068): 대시보드 출력 windows 팝업 Azure SQL Database에 대 한 오류 메시지와 함께 합니다.
   - 수정 [1069 발급](https://github.com/Microsoft/azuredatastudio/issues/1069): 연결 대화 상자 처음 표시 될 때 필요한 서버 오류를 표시 합니다.
   - 수정 [1070 발급](https://github.com/Microsoft/azuredatastudio/issues/1070): 서버 그룹을 두 번 클릭으로 확장 하 고 필요 합니다.
   - 수정 [1072 발급](https://github.com/Microsoft/azuredatastudio/issues/1072): 선택 컨트롤 배경에 반투명 하 게 됩니다.
   - 수정 [1115 발급](https://github.com/Microsoft/azuredatastudio/issues/1115): SQL Operations Studio 모든 고대비 액세스 가능성 문제를 해결 합니다.
   - 수정 [1101 발급](https://github.com/Microsoft/azuredatastudio/issues/1101): 업그레이드 "다운로드" 수동으로 링크 확장 되지 못하거나 잘못 된 위치로 이동 합니다.
   - 수정 [1103 발급](https://github.com/Microsoft/azuredatastudio/issues/1103): V 스크롤 홈 탭에서 작동 하지 않음.
   - 수정 [1104 발급](https://github.com/Microsoft/azuredatastudio/issues/1104): SQL 확장 탭 작동을 중지 합니다.


4 월 공개 미리 보기는 중요 한 강조 표시는 Visual Studio 코드 1.21 플랫폼 소스 코드 새로 고침입니다. 이렇게 하면 이전 1.19 동기화 지점에서 핵심 편집기 및 workbench에 몇 가지 업데이트에서 됩니다. 몇 가지 예는 다음과 같습니다.

- [새 알림 UI](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui) -쉽게 관리 하 고 SQL Operations Studio 알림을 검토 합니다.
- [통합 터미널 분할](https://code.visualstudio.com/updates/v1_21#_split-terminals) -한 번에 여러 열고 터미널을 사용 하 여 작동 합니다.
- [크고 보호 된 파일을 저장](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges) -보호 되는 관리자에 저장 하 고 > SQL Operations Studio 내의 256m 파일입니다.
- [대용량 파일 지원 향상](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements) -대용량 파일에 대 한 텍스트 버퍼 최적화 합니다.
- [향상 된 설정 검색](https://code.visualstudio.com/updates/v1_20#_settings-search) -쉽게 자연어 검색을 사용 하 여 올바른 설정을 찾습니다.
- [전역 조각](https://code.visualstudio.com/updates/v1_20#_global-snippets) -만들기 코드 조각에서 모든 파일 형식을 사용할 수 있습니다.
- [다중 선택 탐색기](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer) -한 번에 여러 파일에 대해 작업을 수행 합니다.
- [오류 및 경고 탐색기에서](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer) -신속 하 게 오류 코드 베이스에서로 이동 합니다.
- [끌어 및 삭제, 복사 및 windows에서 붙여](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support) -열기 SQL Operations Studio 창에서 파일을 이동 합니다.
- [Git 하위 모듈 지원](https://code.visualstudio.com/updates/v1_20#_git-submodules) -중첩 된 Git 리포지토리에서 Git 수행할 작업입니다.
- [터미널 화면 판독기 지원](https://code.visualstudio.com/updates/v1_20#_screen-reader-support) -통합 터미널 "화면 판독기 최적화" 모드를 얻었습니다.
- [가운데 맞춤된 편집기 레이아웃](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout) -화면 부동산을 보기에 코드를 극대화 합니다.
- [가로 검색 결과 (미리 보기)](https://code.visualstudio.com/updates/v1_21#_horizontal-search) -이제 가로 패널에서 검색 결과 볼 수 있습니다.

자세한 내용은 체크 아웃 합니다 [Visual Studio Code 2 월 릴리스 정보](https://code.visualstudio.com/updates/v1_21), 및 [Visual Studio Code 년 1 월 릴리스 정보](https://code.visualstudio.com/updates/v1_20)합니다.

자세한 내용은 참조는 [변경 로그](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)합니다.

## <a name="march-2018-march-public-preview"></a>2018 년 3 월 (공개 미리 보기 3 월)

릴리스 날짜: 2018 년 3 월 28 일  
버전: 0.27.3

합니다 *공개 미리 보기 3 월* 은 계속 최상위 GitHub 문제를 해결 하 고 확장성 이야기를 주력 합니다. 특히 확장 관리자를 사용 하도록 설정 하 고 대시보드 관리 개선 및 SQL 에이전트 및 확장 정보를 제공 합니다. 이 릴리스에 다음과 같은 향상 기능이 포함 되어 있습니다.

- 구성 창과 탭된 insights를 지원 하기 위해 대시보드 확장성 모델을 향상 시킵니다.
   - 확장 관리자를 사용 하면 확장의 간단한 획득 합니다.
   - 대시보드 확장에서 sp_whoisactive [whoisactive.com](http://www.whoisactive.com)합니다.
   - 자세한 내용은 참조 하세요 [SQL Operations Studio 기능을 확장](extensions.md)합니다.
- 추가할 [연결 및 개체 탐색기에 대 한 확장성 Api](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API) 관리 합니다.
- 계속에 영향을 주는 중요 한 고객을 해결할 [GitHub 문제](https://github.com/Microsoft/azuredatastudio/issues)합니다.


## <a name="february-2018-february-public-preview"></a>2018 년 2 월 (공개 미리 보기 2 월)

릴리스 날짜: 2018 년 2 월 15 일  
버전: 0.26.7

합니다 *공개 미리 보기 2 월* 몇 가지 기능 제안 및 우선 순위가 높은 버그 수정을 포함 합니다. 이 릴리스에 다음과 같은 향상 기능이 포함 되어 있습니다.

- 자동 업데이트 설치를 도입 하는 경우 알림을 제공 새 릴리스는 다운로드할 수 있습니다. 
- 연결 대화 상자 '데이터베이스' 필드를 동적으로 채워진된 드롭다운 목록에서 지정된 된 서버에서 채워진 데이터베이스의 목록을 포함 하는 되었습니다.
- 수정 [6 발급](https://github.com/Microsoft/azuredatastudio/issues/6): 새 쿼리 탭을 열 때 연결 및 선택한 데이터베이스를 유지 합니다.
- 수정 [22 발급](https://github.com/Microsoft/azuredatastudio/issues/22): ' 서버 이름 ' 및 ' 데이터베이스 이름 '-수 이러한 드롭다운 텍스트 상자 대신 수 있습니까?
- 수정 [549 발급](https://github.com/Microsoft/azuredatastudio/issues/549): 설치 후 여는 응용 프로그램에서 결과 자동/매우 자동 설치 합니다.
- 수정 [481 발급](https://github.com/Microsoft/azuredatastudio/issues/481): "업데이트 확인 옵션을 추가 합니다.
- SQL 편집기 색 지정 및 자동 완성 수정 사항:
   - 수정 [584 발급](https://github.com/Microsoft/azuredatastudio/issues/584): IntelliSense에서 키워드 "전체" 강조 표시 되지 않습니다.
   - 수정 [345 발급](https://github.com/Microsoft/azuredatastudio/issues/345): 편집기에서 색을 지정 SQL 함수입니다.
   - 수정 [300 발급](https://github.com/Microsoft/azuredatastudio/issues/300): [#tempData] 최신 "]" 녹색 표시 됩니다.
   - 수정 [225 발급](https://github.com/Microsoft/azuredatastudio/issues/225): 키워드 색 일치 하지 않습니다.
   - 수정 [60 발급](https://github.com/Microsoft/azuredatastudio/issues/60): 잘못 된 sql 구문 색 강조 from 절에서 임시 테이블을 사용 하는 경우.
- 연결 확장성 API를 소개 합니다.
- VS 코드 편집기 1.19 통합 합니다.
- 여러 쿼리 계획 뷰어 개선 JustinPealing/html-쿼리 계획 구성 요소 수 거를 업데이트 합니다.


## <a name="january-2018-january-public-preview"></a>2018 년 1 월 (1 월 공개 미리 보기)

릴리스 날짜: 2018 년 1 월 17 일  
버전: 0.25.4

합니다 *월 공개 미리 보기* 몇 가지 기능 제안 및 우선 순위가 높은 버그 수정을 포함 합니다. 이 릴리스에 다음과 같은 향상 기능이 포함 되어 있습니다.

- 저장 된 서버 연결의 연결 대화 상자에서 사용할 수 있습니다.
- 핫 종료를 사용 하도록 설정 합니다. 핫 종료가 참조를 사용 하도록 설정 하려면 기본적으로 꺼져 [핫 종료 설정을](settings.md#hot-exit)합니다.
- 탭 색 지정 서버 그룹을 기반으로 합니다. 탭 색 지정이 참조를 사용 하도록 설정 하려면 기본적으로 꺼져 [color 설정 탭](settings.md#tab-color)합니다.
- 변경 *서버 이름* 하 *Server* 연결 대화 상자에서.
- 손상 수정 *현재 쿼리 실행* 명령입니다.
- 끌어서 놓기 주요 스크립팅 버그를 수정 합니다.
- 잘못 된 고정 된 시작 메뉴 아이콘을 수정 합니다.
- 누락 된 Azure 계정 아이콘 브랜딩을 수정 합니다.


## <a name="december-2017-december-public-preview"></a>2017 년 12 월 (12 월 공개 미리 보기)

릴리스 날짜: 2017 년 12 월 19 일  
버전: 0.24.1

*12 월 공개 미리 보기* 모든 기능 영역 뿐 아니라 다음과 같은 향상 기능이 몇 가지 버그 수정을 포함 합니다.

- 만들 방화벽 규칙 대화 상자에서 Azure SQL Database 및 Azure SQL Data Warehouse에 연결 하는 데 활용할 수 있습니다.
- Windows 설치 프로그램을 추가 하 고 Linux DEB 및 RPM 설치 패키지입니다.
- 대시보드 시각적 레이아웃 편집기를 관리 합니다.
- *스크립트와 Alter* 하 고 *실행할 스크립트* 명령입니다.
- *실제 계획으로 현재 쿼리를 실행* 명령입니다.
- VS Code 1.18.1 편집기 platform을 통합 합니다.
- 테스트용 로드의 VSIX 확장 파일을 사용 하도록 설정 합니다.
- "이동 N" 일괄 처리 반복 구문을 지원 합니다.


## <a name="november-2017"></a>2017 년 11 월

릴리스 날짜: 2017 년 11 월 15 일  
버전: 0.23.6

- 초기 릴리스의 [!INCLUDE[name-sos](../includes/name-sos-short.md)]합니다.


## <a name="next-steps"></a>다음 단계

시작 하려면 다음 빠른 시작 중 하나를 참조 하세요.
- [SQL Server 연결 및 쿼리](quickstart-sql-server.md)
- [Azure SQL 데이터베이스 연결 및 쿼리](quickstart-sql-database.md)
- [Azure 데이터 웨어하우스 연결 및 쿼리](quickstart-sql-dw.md)

[!INCLUDE[name-sos](../includes/name-sos-short.md)]에 기여하기:
- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
