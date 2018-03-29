---
title: Microsoft SQL 작업 Studio (미리 보기) 릴리스 정보 | Microsoft Docs
description: Microsoft SQL 작업 Studio (미리 보기) 릴리스 정보
ms.custom: tools|sos
ms.date: 03/28/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba86403e791af25de4f7bcd8b1cbd7b5f188897b
ms.sourcegitcommit: d6881107b51e1afe09c2d8b88b98d075589377de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="sql-operations-studio-preview-release-notes"></a>SQL 작업 Studio (미리 보기) 릴리스 정보

**[년 3 월 공개 미리 보기 다운로드](download.md)**

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

자세한 내용은 참조는 [변경 로그](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md)합니다.


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
- [연결 및 SQL Server 쿼리](quickstart-sql-server.md)
- [연결 및 Azure SQL 데이터베이스 쿼리](quickstart-sql-database.md)
- [연결 및 Azure 데이터 웨어하우스를 쿼리 합니다.](quickstart-sql-dw.md)

에 기여 [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio)
