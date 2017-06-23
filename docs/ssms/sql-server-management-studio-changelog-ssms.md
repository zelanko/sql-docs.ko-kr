---
title: "SQL Server Management Studio - 변경 로그(SSMS) | Microsoft 문서"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: 72
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 470e6c83318eaf8eb579d053f65b5353862eb4c7
ms.openlocfilehash: 23e304e52967d5d16672872d8d5712f26ef8c610
ms.contentlocale: ko-kr
ms.lasthandoff: 06/23/2017

---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)

## <a name="ssms-171-release"></a>SSMS 17.1 릴리스
일반적으로 사용할 수 있는 | 빌드 번호: 14.0.17119.0

### <a name="enhancements"></a>개선 사항

- 프로파일러: 도움말 >에 대 한 정보 (예: 17.1) 릴리스 버전 번호를 이제 표시
- 서비스 사용자가 자신의 데이터 원본에 대 한 자격 증명을 새로 고칠 수 1200에 대 한 분석 TM 모델 이상 datasource에서 상황에 맞는 메뉴
- 기본 제공 SSIS CTP 2.1에서 SSIS 확장 실행에서 이제 표시 로그를 보고합니다.
- SSIS 확장 관리 응용 프로그램
  - 확장 마스터에 대 한 기본 정보를 봅니다.
  - 확장 배포에 작업자를 쉽게 추가할 수 있습니다.
  - 모든 확장 작업자 및 그에 대 한 기본 정보를 확인 및 또한 활성화 하거나 비활성화할 수을 쉽게 합니다.

### <a name="bug-fixes"></a>버그 수정
- Always On:
  - 가용성 복제본의 속성 WSFC Ag "자동 장애 조치" 모드로 표시 된 항상 있는 문제가 해결 되었습니다.
  - 가용성 그룹을 업데이트할 때 읽기 전용 라우팅 목록을 덮어 쓰여졌습니다 여기서 문제 해결
- 항상 암호화: 생성 된 로그 파일에서 DacFx 생성 되는 정보를 누락 된 문제가 해결 됨
- 실행 계획: UI 적응 아닌 조인 연산자에 대 한 실제 조인 유형 특성 표시 항상 되어 문제에 고정 합니다.
- 설치:
  - SSMS 17.0 [연결 항목 3133479] Visual Studio 2013에서 SSDT를 분리 된 문제 해결
  - 문제가 해결 되었습니다. 여기서 설치 프로그램의 끝에 "다시 시작"를 클릭 하가 되지 컴퓨터를 다시 시작
- SSMS에서 해당 옵션을 사용 하지 않도록 설정 하 여 삭제 작업을 스크립팅하려면 하려고 할 때 Azure 데이터베이스 개체를 실수로 삭제 인해 일시적으로 스크립팅: 없습니다.  SSMS의 예정 된 릴리스에서 적절 한 수정 될 수 있습니다.
- 개체 탐색기: 문제가 해결 되었습니다. "데이터베이스" 노드 "AS 복사"를 사용 하 여 만든 Azure 데이터베이스에 연결 하는 경우 확장 되지 않았습니다.

## <a name="ssms-170-release"></a>SSMS 17.0 릴리스
일반적으로 사용할 수 있는 | 빌드 번호: 14.0.17099.0

### <a name="enhancements"></a>개선 사항 

- 업그레이드 패키지 및 소프트웨어 업데이트 서비스 WSUS (Windows) 
    - 17.X 릴리스할 작은 누적 업데이트 패키지를 포함합니다. 
  - 업데이트 패키지도 WSUS 카탈로그에 게시 됩니다.  
- 아이콘 업데이트
    - VS Shell 제공 아이콘와 일치 하 고 높은 DPI 해상도 지원 하도록 업데이트 된 아이콘
    - 16.X 및 17.X 버전을 구분하는 새 SSMS 및 Profiler 프로그램 아이콘
- SQL PowerShell 모듈
  - SQL Server PowerShell 모듈 SSMS에서 제거 되 고 이제 (PowerShell 5.0 이제 지 원하는 데 필요한 모듈 버전 관리) PowerShell 갤러리를 통해 제공
  - "프레젠테이션" (서식) (예: 데이터베이스 이제에서는 크기와 사용 가능한 공간 및 테이블 표시 행 수와 공간 사용량) 일부 SMO 개체의 기타 개선 사항
  - PowerShell 명령 프롬프트는 OE의 "PowerShell 시작" 메뉴에서 호출 될 때 추가 된 색 지정
  - AG cmdlet(New-SqlAvailabilityGroup, Join-SqlAvailabilityGroup 및 Set-SqlAvailabilityGroup cmdlet)에 -ClusterType 및 -RequiredCopiesToCommit 매개 변수를 추가함
  - Add-SqlAzureAuthenticationContext cmdlet에 -ActiveDirectoryAuthority 및 -AzureKeyVaultResourceId 매개 변수를 추가함
  - 추가 된 Revoke SqlAvailabilityGroupCreateAnyDatabase, Grant SqlAvailabilityGroupCreateAnyDatabase 및 집합 SqlAvailabilityReplicaRoleToSecondary cmdlet
  - Set-sqlavailabilityreplica 및 New-sqlavailabilityreplica cmdlet에 추가 된-SeedingMode 매개 변수
  - Get sql 데이터베이스에 추가 된-ConnectionString 매개 변수
- Linux의 SQL Server
    - 일반 개선 사항 및 로그 전달에 대한 수정
  - 기본 Linux 경로 연결에 대 한 지원 추가, 복원과 백업 데이터베이스
  - 감사 로그 대상 폴더에 대 한 네이티브 Linux 경로 대 한 지원 추가
- Analysis Services
  - DAX 쿼리 창:
    - 편집기에서 일치 하는 괄호
    - 측정값 정의 및 정의 VAR 구문 지원
    - 향상 된 다양 한 Intellisense 기능
  - 유니버설 인증
    - 사용자 이름 및 암호 없이 및 Azure 로그인 대화 상자는 연결을 처리 하는 지정할 수 있습니다.
  - SSMS PQ 통합: 
    - 구조화 된 데이터 원본 작업 스크립팅 
    - 보기 및 PQ UI의 구조화 된 데이터 원본 편집
- 새 "UNIQUE 제약 조건 추가" 템플릿
- Showplan
    - 결과 시간에 대한 속성 창에서 전체 스레드의 합계 대신 최대값 표시
    - 새로운 메모리 부여 연산자 속성 노출
    - 활성 쿼리 통계에서 "쿼리 편집" 단추를 사용하도록 설정함
    - 인터리브 실행 지원
  - "실제 실행 계획을 분석"에 대 한 새로운 옵션
  - 실행 계획 비교로 일반 개선 사항
  - 두 개의 쿼리 계획의 일치 하는 노드 간의 카디널리티 예측에서 중요 한 차이점을 찾아 가능한 근본 원인의 기본 분석을 수행 하려면 실행 계획 비교 기능에서 기능을 도입
- 등록된 서버 탐색기에서 구성 관리자를 제거함
- Azure Blob Storage에서 감사 로그 읽기 지원
- Always Encrypted에 대한 매개 변수화가 추가됨, 자세한 내용은 [이 페이지](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/) 참조 
- Azure SQL DB에 대한 AAD 유니버설 인증 연결에서 사용자 지정 테넌트 ID 지원 
- Azure SQL Database에 대한 스크립트 생성, 이제 전체 텍스트, 규칙 및 데이터베이스 스크립팅 가능
- SSMS 및 Profiler의 시작 화면에서 브랜딩 수정
- SSMS에서 유틸리티 제어 지점 UI 제거함
- SSMS에서 이제 "PremiumRS" 버전의 SQL Azure 데이터베이스를 만들 수 있습니다.
- Always On 가용성 그룹
  - 새 클러스터 종류에 대 한 지원 추가: 외부 및 없음
    - Linux에서 SQL Server에 대 한 지원 추가
    - 초기 데이터 동기화에 대 한 옵션으로 자동 시드를 추가 합니다.
    - 예를 들어 DB 새로 고침 및 UI 레이아웃을 처리 하는 끝점 URL 일부 결함을 고정
    - Azure 복제본 제거 관련 기능
  - 여러 가용성 그룹 키워드에 대 한 향상 된 IntelliSense
- 작업 모니터
  - SSMS 출력 창에 추가 된 새 "작업 모니터" 창
  - 연결 오류/제한 시간 메시지 나타내는 팝업 메시지가 대신 창 출력을 정보를 기록 하도록 변경
  - 제거 된 빈 개요 섹션에서 (5 일 차트) 차트
  - 작업 모니터 데이터 수집을 일시 중지 되 면 개요 제목에 "(일시 중지)" 추가
  - SQL Server-그래프 노드와 edge 테이블에 대 한 새 아이콘-그래프 노드와 edge 테이블에 대 한 그래프 확장 그래프 테이블 폴더 아래 나타납니다-를 만드는 템플릿을 사용할 수 있는 노드 및 가장자리 테이블 그래프
- 프레젠테이션 모드
    - 빠른 실행(Ctr Q)을 통해 사용할 수 있는 세 가지 새 작업
    - PresentOn - 프레젠테이션 모드 켜기
    - PresentEdit - 프레젠테이션 모드에 대한 프레젠테이션 글꼴 크기 편집.  쿼리 편집기의 경우 "텍스트 편집기 글꼴".  다른 구성 요소의 경우 "환경 글꼴"
    - RestoreDefaultFonts - 기본 설정으로 되돌리기
    - *참고: 현재 PresentOff 명령이 없습니다.  프레젠테이션 모드를 끄려면 RestoreDefaultFonts를 사용 하세요.*

### <a name="bug-fixes"></a>버그 수정

- 여기서 SSMS showplan surfacebook 터치를 통해 스크롤할 때 충돌이 발생 한 문제 해결
- SSMS는 long 한 지연 되는 위치에 문제를 해결 하 고 복원 됨 또는 오프 라인 데이터베이스의 속성을 가져오는 동안 시간 
- 여기서 "도움말 뷰어" 열 수 없습니다 RC의 빌드에는 문제가 해결
- 문제가 해결 되었습니다 "유지 관리 계획 태스크 도구 상자" 항목 SSMS에서 누락 될 수 있습니다.
- 사용자 데이터베이스 이름에는 중괄호 안에 포함 된 경우 데이터베이스를 축소 하 여가 SSMS에서 문제를 해결 합니다. [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/3122618)
- 문제가 해결 되었습니다. 삭제 작업을 스크립팅하려면 SSMS를 시도 하는 Azure의 데이터베이스를 실제로 일으킨 데이터베이스 자체를 삭제 합니다. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3131458/)
- 사용자 정의 테이블 형식에 대해 기본값이 스크립팅되지 않은 문제를 해결함. [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/3119027)
- 인덱스의 상황에 맞는 메뉴에 대한 또 한차례의 성능 주위 성능 향상. [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/3120783)
- 실행 계획에서 누락된 인덱스를 마우스로 가리킬 때 과도한 깜박임 발생하는 문제를 해결함. [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/3118510)
- 스크립팅할 때 SSMS가 DB를 오프라인으로 전환하는 문제를 해결함. [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/3118550)
- 지역화된(영어 이외) 버전의 SSMS에서 기타 UI 수정
- SQL 2016 SP1 Standard Edition을 대상으로 할 경우 "Always Encrypted 키" 노드가 없는 문제를 해결함
- 항상 암호화
    - SQL 2016 RTM Standard Edition 또는 SQL 2014 이하 서버를 대상으로 할 경우 "Always Encrypted" 메뉴가 잘못 사용하도록 설정됨
    - CREATE 또는 ALTER 구문을 사용할 때 IntelliSense가 오류를 보고하는 문제를 해결함
    - CMK/CEK에 이스케이프(즉, 괄호로 묶음)해야 하는 문자가 포함된 경우 암호화가 실패하는 문제를 해결함
    - SSMS에서 메모리 부족 예외가 발생하는 경우 네이티브(64 비트) PowerShell을 대신 사용하도록 제안하는 오류가 표시됨
    - 사용자가 클래식 Azure 구독 대신 리소스 그룹 관리자 구독을 사용하는 경우 AE 마법사가 실패하는 문제를 해결함
    - 사용자가 구독에 사용 권한이 없거나 Azure Key Vault가 없는 경우 AE 마법사에 잘못된 오류가 표시되는 문제를 해결함
    - AAD가 여럿인 경우 Azure Key Vault 로그인 페이지에 Azure 구독이 표시되지 않는 AE 마법사의 문제를 해결함
    - Azure Key Vault 로그인 페이지에 사용자에게 읽기 권한이 있는 Azure 구독이 표시되지 않는 AE 마법사의 문제를 해결함
  - 문제가 해결 되었습니다. 여기서 리소스 파일이 로드 되지 않습니다 올바르게, 정확 하지 않은 오류 메시지 생성
- SSMS 설치 페이지에서 하이퍼링크의 대비 향상
- SQL Server Express(2016 SP1)에 연결된 경우 Polybase 노드가 표시되지 않는 문제를 해결함
- SSMS v 140 Azure DB의 호환성 수준을 변경할 수 없는 문제 해결
- Azure 데이터베이스 목록을 확장할 때 개체 탐색기의 성능이 향상됨. [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/3100675)
- 비관계형 서버 유형(AS\RS\IS)에 대해 "SQL Server 로그 보기" 상황에 맞는 메뉴 항목이 잘못 표시되는 문제를 해결함 
- SQL 인증을 사용하여 Analysis Services 파티션 쿼리의 구문을 확인할 때 로그인 실패 메시지가 표시될 수 있는 문제를 해결함
- SSMS에서 미리 보기 1400 호환성 수준 AS 테이블 형식 모델의 이름을 바꾸지 못하는 문제를 해결함
- 드문 경우이지만 AS 서버에서 잘못된 작업을 시도한 후 발생할 수 있는 “operation failed on model”(모델에서 작업 실패) 문제를 해결함(모델에서 저장 실패 후 로컬 변경 내용을 되돌림)
- Analysis Services [데이터베이스 동기화] 팝업 대화 상자에서 오타를 수정함
- 컨테이너 백업/복원 대화 상자가 여러 모니터 설정에서 화면 밖에 표시됨. 
- 대상 개체의 이름에 ]가 있으면 SecurityPolicy 만들기에 실패함.
- SSMS 2016 "최근에 사용한 항목 열기" 메뉴에 최근에 저장한 파일이 표시되지 않음. [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)
- VS Shell을 업데이트할 때 사용자 설정에 대한 재설정이 제거됨.
- SQL Server 2017에서 데이터베이스의 호환성 수준을 변경 하지 못하도록 때문에 사용자가 하는 문제를 수정 했습니다.
- AAD 유니버설 인증을 사용하는 쿼리 창에서는 1시간 후 쿼리를 새로 고칠 수 없음.
- SSMS에서 유틸리티 제어 지점 UI가 제거됨.
- AD 유니버설 인증 연결에서 초기 토큰 만료 후 데이터를 쿼리하지 못함.
- Azure SQL DB에서 Azure SQL DB로 규칙을 스크립팅할 수 없음.
- SQL PowerShell에서 레거시 SQL 인스턴스(2014 이전)에 연결할 수 없는 문제를 해결함. [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/1138754/sql-server-sqlps-powershell-module-fails-connection-to-sql-2012-instance)
- 등록된 서버를 가져올 수 없는 경우 SSMS 작동이 중단되게 하는 문제를 해결함.
- 사용자에게 데이터베이스에 대한 특정 사용 권한이 있는 경우 SSMS 작동이 중단되게 하는 문제를 해결함. 
- SSMS - 보기를 검토하는 동안 디자인 화면에서 테이블이 사라짐. [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/2946125/ssms-tables-disappears-from-design-surface-while-reviewing-views) 
- 사용자는 테이블 스크롤 막대를 사용하여 테이블 내용을 스크롤할 수 없고, 위쪽/아래쪽 화살표로만 이 작업을 할 수 있음. 버그인 스크롤 막대를 사용하여 스크롤하려고 시도한 후 테이블 내용을 스크롤할 수도 있음. [Connect 항목](
http://connect.microsoft.com/SQLServer/feedback/details/3106561/sql-server-manager-2016-bug-in-design-view) 
- 루트 노드를 새로 고치고 나면 등록된 서버에서 아이콘을 표시하지 않음.
- Azure v12 서버에서 [데이터베이스 만들기]에 대한 스크립트 단추를 누르면 스크립트가 실행된 후 "No action to be scripted"(스크립팅할 동작이 없습니다.) 메시지를 표시함.
- SSMS [서버에 연결] 대화 상자에서 새로운 각 연결에 대해 "추가 속성" 탭을 지우지 않음.
- [Generate Tasks](작업 생성) 스크립트에서 Azure SQL DB에 대한 [데이터베이스 만들기] 스크립트를 생성하지 않음.
- 뷰 디자이너의 스크롤 막대가 사용하지 않도록 설정된 것으로 보임.
- Always Encrypted AVK 키 경로에 버전 ID가 포함되지 않음.
- 쿼리 창의 엔진 버전 쿼리 수 줄임. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3113387)
- 암호화가 잘못 처리된 후 모듈을 새로 고치지 못하는 Always Encrypted 오류.
- OLTP 및 OLAP에 대한 기본 연결 제한 시간을 15초에서 30초로 변경하여 무시된 연결 실패의 클래스를 수정함. 
- 사용자 지정 보고서가 시작될 때 SSMS 작동이 중단되는 문제를 해결함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3118856)
- Azure SQL 데이터베이스에 대한 "스크립트 생성..."에 실패하는 문제를 해결함
- 저장 프로시저와 같은 개체를 스크립팅할 때 줄 바꿈이 추가되지 않도록 "스크립팅" 및 "스크립트 생성 마법사"를 수정함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3115850)
- SQLAS PowerShell 공급자: Dimension 및 MeasureGroup 폴더에 LastProcessed 속성을 추가함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3111879)
- 활성 쿼리 통계: 배치에 있는 첫 번째 쿼리만 표시하던 문제를 해결함. [연결 항목] (http://connect.microsoft.com/SQLServer/feedback/details/3114221)  
- 실행 계획: 속성 창에서 전체 스레드의 합계 대신 최대값을 표시함.
- 쿼리 저장소: 실행 변형이 높은 쿼리에 대해 새 보고서를 추가함.
- 개체 탐색기 성능 문제: [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3114074)
    - 테이블의 상황에 맞는 메뉴가 잠시 중단됨
    - 원격(인터넷) 연결을 통해 테이블의 인덱스를 마우스 오른쪽 단추로 클릭할 경우 SSMS가 느려짐. 
    - 서버에서 정렬되는 테이블 쿼리 실행 차단
- SSMS에서 Azure 배포 마법사를 제거함(Azure VM에 데이터베이스 배포)
- SSMS에서 실행 계획에 누락된 인덱스가 표시되지 않았던 문제를 해결함 [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3114194)
- SSMS에서 종료 시 발생하는 일반적인 작동 중단 문제를 해결함
- Polybase|규모 확장 그룹 노드에서 상황에 맞는 메뉴를 표시할 때 오류가 발생하는 개체 탐색기의 문제를 해결함 [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3115128)
- 데이터베이스에 대한 사용 권한을 표시하려고 할 때 SSMS의 작동이 중단되는 문제를 해결함
- 쿼리 저장소: 쿼리 저장소 보고서의 결과 표에 대한 상황에 맞는 메뉴 항목의 일반적인 개선 사항
- 기존 테이블에 대한 Always Encrypted 구성이 관련 없는 개체에 대한 오류와 함께 실패함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3103181)
- 여러 스키마가 포함된 기존 데이터베이스에 대한 Always Encrypted 구성이 작동하지 않음. [연결 항목] (http://connect.microsoft.com/SQLServer/feedback/details/3109591)
- Always Encrypted, 암호화된 열 마법사가 시스템 뷰를 참조하는 뷰를 포함하는 데이터베이스로 인해 실패함. [연결 항목] (http://connect.microsoft.com/SQLServer/feedback/details/3111925)
- Always Encrypted를 사용하여 암호화할 때 암호화가 잘못 처리된 후 모듈을 새로 고치지 못하는 오류가 발생함.
- "새 서버 등록" 대화 상자에서 UI 잘림 문제를 해결함
- 따옴표가 있는 문자열 상수 값을 포함하는 식을 잘못 업데이트하는 DMF 조건 UI 수정
- 사용자 지정 보고서를 실행할 때 SSMS 작동을 중단시킬 수 있는 문제를 수정함
- 폴더 노드에 "Execution in Scale Out…"(규모 확장에서 실행…) 메뉴 항목 추가
- Azure SQL DB 방화벽 화이트 리스트 IP 주소 기능 관련 문제 해결
- 개체 참조를 일으킨 SSMS에서 문제 설정 하지 예외 다차원 파티션으로 소스를 편집 하는 경우 고정
- 개체 참조를 일으킨 SSMS에서 문제 설정 하지 예외 다차원 AS에서 고객 어셈블리를 삭제할 때 고정 서버
- 문제가 해결 되었습니다. AS 테이블 형식 1400 db 이름 바꾸기 실패 했습니다.
- 연결 속성 대화 상자에서 테이블 형식 데이터 원본으로 1400 compat 수준 스크립팅 관련 문제 해결
- 가정 1400 compat 수준 모델 테이블에 파티션이 하나 이상 제거 합니다.
- Ctrl-R을 이제 SSMS DAX 쿼리 편집기에서 결과 창 설정/해제


## <a name="ssms-1653-release"></a>SSMS 16.5.3 릴리스
일반 공급 | 빌드 번호: 13.0.16106.4

이 릴리스에서는 다음과 같은 문제가 해결되었습니다.

* 테이블에 스파스 열이 둘 이상 있을 때 'Table' 노드의 확장을 일으키는 SSMS 16.5.2의 문제를 해결함.

* 사용자가 Microsoft Dynamics AX/CRM Online 리소스에 연결되는 OData 연결 관리자를 포함하는 SSIS 패키지를 SSIS 카탈로그에 배포할 수 있음. 자세한 내용은 [OData 연결 관리자](https://msdn.microsoft.com/library/dn584133.aspx)를 참조하세요.

* 기존 테이블에 대한 Always Encrypted 구성이 관련 없는 개체에 대한 오류와 함께 실패함. [Connect ID 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* 여러 스키마가 포함된 기존 데이터베이스에 대한 Always Encrypted 구성이 작동하지 않음. [Connect ID 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* Always Encrypted, 암호화된 열 마법사가 시스템 뷰를 참조하는 뷰를 포함하는 데이터베이스로 인해 실패함. [Connect ID 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* Always Encrypted를 사용하여 암호화할 때 암호화가 잘못 처리된 후 모듈을 새로 고치지 못하는 오류가 발생함.

* *최근에 사용한 항목 열기* 메뉴에 최근에 저장한 파일이 표시되지 않음. [Connect ID 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* 원격(인터넷) 연결을 통해 테이블의 인덱스를 마우스 오른쪽 단추로 클릭할 경우 SSMS가 느려짐. [Connect ID 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* SQL 디자이너 스크롤 막대 관련 문제를 해결함. [Connect ID 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* 테이블의 상황에 맞는 메뉴가 잠시 중단됨 
 
* SSMS에서 가끔 [작업 모니터]에서 예외를 발생시키고 작동을 중단함. [Connect ID 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016이 "The process was terminated due to an internal error in the .NET Runtime at IP 71AF8579 (71AE0000) with exit code 80131506"(.NET 런타임의 IP 71AF8579(71AE0000)에서 내부 오류로 인해 프로세스가 종료되었습니다(종료 코드 80131506).) 오류와 함께 작동이 중단됨


## <a name="ssms-1651-release"></a>SSMS 16.5.1 릴리스
일반 공급 | 빌드 번호: 13.0.16100.1

* CHECK 제약 조건이 발생할 때 Invoke-Sqlcmd이 여러 행을 잘못 삽입하는 문제를 해결했습니다. [Microsoft Connect 항목: 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* 가용성 그룹을 만들 때 ENU가 아닌 언어 버전이 완벽히 작동하지 않는 문제를 해결했습니다.

* 쿼리 계획 XML을 클릭할 때 올바른 SSMS UI가 열리지 않는 문제를 해결했습니다.


## <a name="ssms-165-release"></a>SSMS 16.5 릴리스
일반 공급 | 빌드 번호: 13.0.16000.28

* ";:"을 포함하는 테이블 이름이 있는 데이터베이스를 클릭했을 때 충돌이 발생하는 문제를 해결했습니다.
* AS 테이블 형식 데이터베이스 속성 창에서 모델 페이지를 변경하면 원래 정의가 스크립팅되는 문제를 해결했습니다. 
[Microsoft Connect 항목: 3080744](https://connect.microsoft.com/SQLServer/feedback/details/3080744) 
* 임시 파일이 "최근 파일" 목록에 추가되는 문제를 해결했습니다.  
[Microsoft Connect 항목: 2558789](https://connect.microsoft.com/SQLServer/feedback/details/2558789)
* 개체 탐색기 트리에서 사용자 테이블 노드에 대한 "압축 관리" 메뉴 항목이 비활성화되는 문제를 해결했습니다.  
[Microsoft Connect 항목: 3104616](https://connect.microsoft.com/SQLServer/feedback/details/3104616)

* 사용자가 개체 탐색기, 등록된 서버 탐색기, 템플릿 탐색기 및 개체 탐색기 정보에 대한 글꼴 크기를 설정할 수 없는 문제를 해결했습니다. 탐색기에 대한 글꼴은 환경 글꼴이 사용됩니다.  
[Microsoft Connect 항목: 691432](https://connect.microsoft.com/SQLServer/feedback/details/691432)

* 연결이 끊겼을 때 SSMS가 항상 기본 데이터베이스에 다시 연결되는 문제를 해결했습니다.  
[Microsoft Connect 항목: 3102337](https://connect.microsoft.com/SQLServer/feedback/details/3102337)

* 실행 계획 아이콘을 비롯하여 정책 관리 및 쿼리 편집기 창에서 dpi가 높은 여러 문제를 해결했습니다.

* 확장된 이벤트에 대한 글꼴 및 색 구성 옵션이 없는 문제를 해결했습니다.

* 응용 프로그램을 닫거나 오류 대화 상자를 표시하려는 경우 SSMS 충돌이 발생하는 문제를 해결했습니다.


## <a name="ssms-1641-september-2016-release"></a>SSMS 16.4.1(2016년 9월) 릴리스
일반 공급 | 빌드 번호: 13.0.15900.1

*  저장 프로시저를 변경/수정하려는 동안 실패하는 경우 문제 해결  
[Microsoft Connect 항목 #3103831](https://connect.microsoft.com/SQLServer/feedback/details/3103831)

* PowerShell을 사용하여 데이터를 보고 쓰기 위한 새로운 'Read-SqlTableData', 'Read-SqlViewData' 및 'Write-SqlTableData' cmdlet  
[Trello Read-SqlTableData 카드](https://trello.com/c/FXVUNJ8x/131-read-sqltabledata)  
[Microsoft Connect 항목 #2685363](https://connect.microsoft.com/SQLServer/feedback/details/2685363)
    
* PowerShell을 사용하여 새 로그인 관리 시나리오를 지원하기 위한 'Add-SqlLogin' cmdlet  
[Microsoft Connect 항목 #2588952](https://connect.microsoft.com/SQLServer/feedback/details/2588952)
    
*  다양한 국가별 클라우드에 연결하는 사용자에 대한 지원 및 사용 편의성 개선
    
    
*  메모리 부족 예외를 발생시키던 문제 해결  
[Microsoft Connect 항목 #3062914](https://connect.microsoft.com/SQLServer/feedback/details/3062914)  
[Microsoft Connect 항목 #3074856](https://connect.microsoft.com/SQLServer/feedback/details/3074856)
    
*  스키마별 필터링이 올바른 필터 옵션이 아니던 문제 해결  
[Microsoft Connect 항목 #3058105](https://connect.microsoft.com/SQLServer/feedback/details/3058105)  
[Microsoft Connect 항목 #3101136](https://connect.microsoft.com/SQLServer/feedback/details/3101136)
    
*  늘어난 데이터베이스의 모니터 창에 액세스할 수 없는 문제 해결
    
*  F1 도움말에서 항상 온라인 콘텐츠를 여는 문제 해결. 이제 사용자가 도움말 메뉴의 "도움말 기본 설정 지정"을 통해 온라인 또는 오프라인 도움말 중에서 선택할 수 있습니다.   
[Microsoft Connect 항목 #2826366](https://connect.microsoft.com/SQLServer/feedback/details/2826366)
    
*  1200 수준 Analysis Services 테이블 형식 모델을 스크립팅할 때 서버 버전과 다르게 스크립팅에 사용되는 암호가 제거되지 않는 문제 해결[이제 클라이언트 모델 개체가 스크립팅 전에 동기화됨]
    
*  '상위 N개 행 선택' 옵션으로 더 이상 사용되지 않는 TOP 연산자 구문이 생성되는 문제 해결  
[Microsoft Connect 항목 #3065435](https://connect.microsoft.com/SQLServer/feedback/details/3065435)
    
*  SSMS 전반에서 로그인 속성 페이지, 고급 쿼리 실행 옵션을 비롯한 다양한 레이아웃 문제 해결   
[Microsoft Connect 항목 #3058199](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect 항목 #3079122](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect 항목 #3071384](https://connect.microsoft.com/SQLServer/feedback/details/3071384)
    
*  사용자가 새 쿼리 창을 열 때마다 솔루션이 자동으로 생성되는 문제 해결   
[Microsoft Connect 항목 #2924667](https://connect.microsoft.com/SQLServer/feedback/details/2924667)    
[Microsoft Connect 항목 #2917742](https://connect.microsoft.com/SQLServer/feedback/details/2917742)   
[Microsoft Connect 항목 #2612635](https://connect.microsoft.com/SQLServer/feedback/details/2612635)
    
*  시스템 데이터베이스 내에 있을 때 개체 탐색기에서 임시 테이블을 확장할 수 없는 문제 해결  
[Microsoft Connect 항목 #2551649](https://connect.microsoft.com/SQLServer/feedback/details/2551649)
    
*  SSMS가 일괄 처리 실행 후 SELECT @@trancount에 대한 쿼리를 실행하는 문제 해결    
[Microsoft Connect 항목 #3042364](https://connect.microsoft.com/SQLServer/feedback/details/3042364)
    
*  서버의 속성 페이지에서 스크립트를 만들 때 연결 대화 상자가 숨겨지던 Analysis Services의 문제를 해결했습니다.
    
*  Ctrl + Q로 빠른 실행 도구 모음이 선택되지 않는 문제 해결
    
*  2TB가 넘는 데이터베이스의 경우에는 서버 속성 대화 상자를 사용하여 데이터베이스의 MaxSize를 변경할 수 없는 문제 해결  
[Microsoft Connect 항목 #1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  데이터베이스 복원 마법사에서 앞에 공백이 있는 파일 이름을 사용할 수 없는 문제 해결   
[Microsoft Connect 항목 #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="ssms-163-august-2016-release"></a>SSMS 16.3(2016년 8월) 릴리스
일반 공급 | 버전 번호: 13.0.15700.28

* SSMS 월별 릴리스는 이제 번호로 브랜딩됩니다.

* [새 인증 옵션 **'Active Directory 유니버설 인증'**](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/) Azure Active Directory에 의해 구동되는 토큰 기반 인증 메커니즘으로, 다단계, 암호 및 통합 인증 메커니즘을 지원합니다.

* SQL Server Profiler 템플릿 기능과 일치하는 새로운 확장 이벤트 템플릿 [(Microsoft Connect 항목 #2543925)](https://connect.microsoft.com/SQLServer/feedback/details/2543925/sql-server-extended-events-profiler-tool) 포함된 [SQL Server Profiler 템플릿](https://msdn.microsoft.com/library/ms190176.aspx)에 대해 자세히 알아보세요.

* Azure SQL 데이터베이스에 대한 새 데이터베이스 만들기 및 데이터베이스 속성 대화 상자

* PowerShell을 사용하여 SQL Server 로그인 관리를 수행하도록 도움을 주는 새 'Get-SqlLogin' 및 'Remove-SqlLogin' cmdlet  
*연결된 고객 버그 요청:*   
[Microsoft Connect 항목 #2588952](https://connect.microsoft.com/SQLServer/feedback/details/2588952/)

* 임의 공급자 및 키 경로에 대한 열 마스터 키 생성 지원을 추가하는 새 PowerShell cmdlet 'New-SqlColumnMasterKeySettings'

* SSMS에서 Azure SQL 데이터베이스를 원활하게 만들 수 있는 새 '데이터베이스 만들기’ 대화 상자>

* SSMS 개체 탐색기의 '데이터베이스' 노드에서 필터링을 지원. 개체 탐색기의 '데이터베이스' 노드로 이동한 후 개체 탐색기 도구 모음에 있는 필터 아이콘을 클릭하여 데이터베이스 목록을 필터링합니다.

* 백업 및 복원 마법사에서 ARM(Azure Resource Manager) 형식 저장소 계정을 지원

* [고해상도 디스플레이에 대한 초기 베타 지원](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/)  
*연결된 고객 버그 요청:*   
[Microsoft Connect 항목 #1129301](https://connect.microsoft.com/SQLServer/feedback/details/1129301/management-studio-is-unusable-on-a-4k-display), [Microsoft Connect 항목 #1858763](https://connect.microsoft.com/SQLServer/feedback/details/1858763/), [Microsoft Connect 항목 #1852671](https://connect.microsoft.com/SQLServer/feedback/details/1852671/), [Microsoft Connect 항목 #1487643](https://connect.microsoft.com/SQLServer/feedback/details/1487643/),  [Microsoft Connect 항목 #1355641](https://connect.microsoft.com/SQLServer/feedback/details/1355641/), [Microsoft Connect 항목 #2161595](https://connect.microsoft.com/SQLServer/feedback/details/2161595/), [Microsoft Connect 항목 #1854041](https://connect.microsoft.com/SQLServer/feedback/details/1854041/), [Microsoft Connect 항목 #1055617](https://connect.microsoft.com/SQLServer/feedback/details/1055617/), [Microsoft Connect 항목 #2448774](https://connect.microsoft.com/SQLServer/feedback/details/2448774/), [Microsoft Connect 항목 #1521405](https://connect.microsoft.com/SQLServer/feedback/details/1521405/), [Microsoft Connect 항목 #2117853](https://connect.microsoft.com/SQLServer/feedback/details/2117853/), [Microsoft Connect 항목 #2014256](https://connect.microsoft.com/SQLServer/feedback/details/2014256/), [Microsoft Connect 항목 #2162218](https://connect.microsoft.com/SQLServer/feedback/details/2162218/), [Microsoft Connect 항목 #2344551](https://connect.microsoft.com/SQLServer/feedback/details/2344551/), [Microsoft Connect 항목 #1664436](https://connect.microsoft.com/SQLServer/feedback/details/1664436/), [Microsoft Connect 항목 #2554043](https://connect.microsoft.com/SQLServer/feedback/details/2554043/), [Microsoft Connect 항목 #2983216](https://connect.microsoft.com/SQLServer/feedback/details/2983216/), [Microsoft Connect 항목 #2021706](https://connect.microsoft.com/SQLServer/feedback/details/2021706/)

* SQL Server 쿼리 저장소의 작업 자동 읽기를 지원하도록 DTA(데이터베이스 엔진 튜닝 관리자) 개선

* 클러스터형 columnstore 인덱스, 비클러스터형 columnstore 인덱스 및 rowstore 인덱스에 대한 인덱스 권장 사항을 표시하도록 DTA(데이터베이스 엔진 튜닝 관리자) 개선

* SQL Server Analysis Services PowerShell cmdlet을 사용하여 DBCC(데이터베이스 콘솔) 명령을 전송하도록 지원

* SSMS에서 해독된 AlwaysEncrypted LOB(Large Object) 열의 일반 텍스트를 보기 위한 버그 수정  
*연결된 고객 버그 요청:*   
[Microsoft Connect 항목 #2413024](https://connect.microsoft.com/SQLServer/feedback/details/2413024/cannot-view-cleartext-of-alwaysencrypted-lob-columns-in-ssms)

* Windows 비주얼 스타일이 사용되도록 설정되지 않은 경우 충돌을 해결하기 위한 Always Encrypted 대화 상자의 버그 수정(예: 고대비 디스플레이를 사용하도록 설정)

* SQL Server 인스턴스에 연결할 수 없게 하는 '메서드를 찾을 수 없음' 오류에 대한 버그 수정

* 날짜/시간 오프셋으로 파티션 함수를 만들 때 발생하는 SSMS 충돌에 대한 버그 수정

* Distributed Replay Administration Tool(DReplay.exe)을 시작하기 위해 Microsoft .NET 3.5가 필요한 상황을 추가/제거하도록 버그 수정

* 정규화된 서버 이름을 지원하기 위한 Analysis Services 배포 마법사의 버그 수정

* 2016 호환성 모델을 사용하여 Analysis Services 테이블 형식 모델에 파티션을 표시하기 위한 SSMS의 버그 수정  
*연결된 고객 버그 요청:*   
[Microsoft Connect 항목 #2845053](https://connect.microsoft.com/SQLServer/feedback/details/2845053/ssms-cannot-display-partitions-in-tabular-models-in-2016-compatibility-level) 

* Analysis Services 테이블 형식 모델 및 SMO(SQL Server 공유 관리 개체)의 성능 향상 및 버그 수정 


---
## <a name="ssms-july-2016-hotfix-update-release"></a>SSMS 2016년 7월 핫픽스 업데이트 릴리스 
일반 공급 | 버전 번호: 13.0.15600.2

* **누락된 오른쪽 클릭 메뉴 항목을 사용하도록 설정하기 위한 SSMS의 버그 수정**  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Microsoft Connect 항목 #2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Microsoft Connect 항목 #2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016-release"></a>SSMS 2016년 7월 릴리스 
일반 공급 | 버전 번호: 13.0.15500.91

* *편집(7월 5일):* **Analysis Services 처리 대화 상자 및 Analysis Services 배포 마법사의 SQL Server 2016(호환성 수준 1200) 테이블 형식 데이터베이스에 대해 향상된 지원**

* *편집(7월 5일):* **'XACT_ABORT'를 설정하는 SSMS '쿼리 실행 옵션' 대화 상자의 새 옵션. 이 옵션은 이 SSMS 릴리스에서 기본적으로 설정되어 있으며 런타임 오류가 발생하는 경우 SQL Server에서 전체 트랜잭션을 롤백하고 배치를 중단하도록 지시합니다.**

* **SSMS의 Azure SQL Data Warehouse 지원.**

* **SQL Server PowerShell 모듈에 대한 중요 업데이트. 여기에는 새 [SQL PowerShell 모듈, Always Encrypted, SQL 에이전트 및 SQL 오류 로그에 대한 새 CMDLET](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update)**이 포함됩니다.

* **Always Encrypted 마법사에서 PowerShell 스크립트 생성에 대한 지원**

* **Azure SQL Database에 연결 시간 향상.**

* **SQL Server 2016 데이터베이스 백업에 대한 Azure Storage 자격 증명 생성을 지원하기 위한 새 'URL에 백업' 대화 상자. 이는 Azure Storage 계정에 데이터베이스 백업을 저장하는 더욱 간소화된 환경을 경험을 제공합니다.**
 
* **Microsoft Azure Storage 서비스에서 SQL Server 2016 데이터베이스 백업 복원을 간소화하는 새 복원 대화 상자.**
 
* **사용자에게 SELECT 권한이 없는 경우 디자이너에 테이블을 추가할 수 있도록 SSMS 쿼리 디자이너의 버그 수정**

* **'TRY_CAST()' 및 'TRY_CONVERT()' 함수에 대한 IntelliSense 지원을 추가하는 버그 수정**  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2453461](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast)

* **‘SQLAS’ Analysis Services 확장 로드를 사용하도록 설정하는 PowerShell 모듈의 버그 수정**  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2544902](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension)

* **SQL 파일의 끌어서 놓기 열기를 허용하는 SSMS 편집기 창의 버그 수정**  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2690658](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios)

* **종료 시 프로파일러 충돌을 해결하는 프로파일러 버그 수정**  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2616550](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped).  
[Microsoft Connect 항목 #2319968](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968)

* **SSMS 테이블 디자이너에서 참가 링크를 편집하려고 할 때 충돌을 방지하기 위해 SSMS의 버그 수정**  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2721052](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms)

* **db_owner 역할 멤버에 대해 데이터베이스 스크립트 생성을 사용하도록 SSMS의 버그 수정**  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2869241](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june)

* **서버가 오프라인으로 전환된 경우 쿼리 탭 닫기의 지연을 제거하도록 SSMS 편집기의 버그 수정**  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2656058](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline).

* **SQL Server Express 데이터베이스의 백업 옵션을 설정하도록 버그 수정**  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2801910](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks).  
[Microsoft Connect 항목 #2874434](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance).

* **다차원 Analysis Services 모델의 데이터 피드 공급자를 올바르게 표시하도록 Analysis Services의 버그 수정.**

----
## <a name="ssms-june-2016-generally-available-release"></a>SSMS 2016년 6월 일반 공급 릴리스
일반 공급 | 버전 번호: 13.0.15000.23

* **SSMS는 2016년 6월 릴리스부터 일반 사용자에게 공급됩니다.**

* **현재 문서에 더 잘 통합되고 정규식을 통한 검색을 허용하는 SSMS의 새로운 빠른 찾기 대화 상자**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* **스크립트를 통해 무인 설치에 대한 설치 진행률 및 프로세스를 추적할 수 있도록 하는 SSMS 설치 관리자 기능 개선**

* **도움말 문서를 올바르게 표시하기 위한 SSMS 상황에 맞는 F1 도움말의 버그 수정**

* **스크롤 시 SSMS가 충돌을 일으키는 쿼리 데이터 저장소 '재발된 쿼리' 보기의 버그 수정** 

* **Excel 2016에서 SQL Server Analysis Services로 연결할 수 있도록 하는 Excel Analysis Services OLEDB 커넥터의 버그 수정**

* **동일한 모니터의 연결 대화 상자를 다중 모니터 시스템의 기본 SSMS 창으로 표시하기 위한 SSMS 연결 대화 상자의 버그 수정**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* **Always Encrypted 환경의 버그 수정 Stretch 데이터베이스에 대해 Always Encrypted 메뉴 옵션이 사용 가능하도록 올바르게 설정되지 않는 버그가 수정되었습니다. 또한 SafeNet(Luna SA) HSM 공급자가 제대로 사용되지 않던 Always Encrypted 마법사의 버그도 수정되었습니다.**

---
## <a name="ssms-april-2016-preview"></a>SSMS 2016년 4월 미리 보기 
버전 번호: 13.0.14000.36
  
* **사람이 읽을 수 있는 오류 메시지를 추가하도록 SSMS 설치 관리자 기능 개선**  
  
* **조건자에 대한 지원을 추가하도록 Stretch 데이터베이스 마법사 기능 개선**  
  
* **키 암호화 API를 추가하도록 AlwaysEncrypted Powershell commandlet 기능 개선**  
  
* **도구, 옵션 대화 상자에서 사용되지 않도록 설정된 경우 SSMS 도구 모음에서 IntelliSense를 해제하기 위한 버그 수정**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2555163/sql-2016-rc2-turning-off-intellisense-from-options-does-not-turn-it-off-on-toolbar/>  
    
* **장기 쿼리 계획에 사용되는 간격을 줄이도록 Showplan 비교 사용자 인터페이스의 기능 개선 및 버그 수정**  
  
* **SSMS를 종료할 때 충돌하던 문제를 해결하는 SSMS의 버그 수정**   
  
* **암호화 중에 사용자 권한을 유지하고 Always Encrypted 마법사가 완료된 후 데이터베이스 분리 작업을 허용하도록 하는 마법사의 버그 수정**  
  
* **지원되지 않는 CNG(암호화 알고리즘) 공급자를 사용하여 키를 생성하려는 시도에 대해 피드백을 제공하도록 하는 Always Encrypted 새 열 마스터 키 대화 상자의 버그 수정**  
  
---  
## <a name="ssms-march-2016-preview-refresh"></a>SSMS 2016년 3월 미리 보기 새로 고침
버전 번호: 13.0.13000.55
  
* **SSMS는 이제 Visual Studio 2015의 격리 셸을 사용합니다.**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2390544/update-ssms-to-use-visual-studio-2015-dependencies/>  
  
* **메뉴 항목 및 옵션을 빠르게 찾을 수 있도록 하는 새로운 빠른 실행 도구 모음 (VS 2015 격리 셸)**  
  
* **SSMS 밝은 테마에 대한 지원을 추가하도록 SSMS 테마 옵션 개선 (VS 2015 격리 셸)**  
  
* **"기본값으로 다시 설정" 단추를 누르는 경우 쿼리 바로 가기 키를 올바르게 다시 설정하도록 하는 SSMS 도구 메뉴 옵션 버그 수정**  
  
* **쉽게 읽을 수 있는 템플릿 이름을 표시하도록 하는 SSMS 새 프로젝트 템플릿의 버그 수정**  
  
* **SSMS에서 SQL 에이전트 작업 기록 보기와 관련된 오류가 해결되었습니다.**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2458860/error-viewing-job-history-microsoft-datawarehouse-sqm/>  
    
* **SSMS의 오프라인 설치를 허용하도록 하는 버그 수정 이를 통해 인터넷에 연결하지 않고도 설치할 수 있습니다. (VS 2015 격리 셸)**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2497178/cannot-install-ssms-when-server-has-no-internet-access/>  
    
* **SQL Server PowerShell(SQLPS) 모듈을 가져올 때 사용자의 현재 디렉터리를 유지하기 위한 버그 수정**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2434605/loading-sqlps-module-changes-current-directory-to-ps-sqlserver/>  
    
* **승인된 PowerShell 동사를 사용하기 위한 SQL Server PowerShell(SQLPS) 모듈의 버그 수정**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2432891/sqlps-module-uses-unapproved-powershell-verbs/>  
    
* **모듈을 더 빠르게 로드하기 위한 SQL Server PowerShell(SQLPS) 모듈의 버그 수정**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2429153/sqlps-module-is-slow-to-load/>  
    
* **작업 단계 수정을 허용하기 위한 SQL 에이전트 작업 단계의 버그 수정**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2453996/issues-with-agent-in-ssms-2016-rc0-13-0-12000-65/>  
    
* **테이블을 사전 순으로 나열하기 위한 SSMS 개체 탐색기의 버그 수정**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2424718/sql-server-2016-ssms-table-list-confusing/>  
    
* **SQL Server 연결이 변경될 때 정확한 데이터베이스 이름 목록을 표시하기 위한 '사용 가능한 데이터베이스' 드롭다운의 버그 수정**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2513420/available-databases-drop-down-box-does-not-update-when-connection-changes-in-ssms/>  
    
* **'Ctrl+U' 키를 누를 경우 포커스가 '사용 가능한 데이터베이스' 드롭다운으로 이동되도록 하는 SSMS 바로 가기 키의 버그 수정**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2534820/ssms-ctrl-u-doesnt-work/>  
  
---  
## <a name="ssms-march-2016-preview"></a>SSMS 2016년 3월 미리 보기 
버전 번호: 13.0.12500.29 
  
* **키보드 키를 사용하는 탐색을 허용하도록 SSMS 웹 설치 관리자 개선**  
  
* **암호화에 대해 별칭 데이터 형식을 지원하도록 Always Encrypted 마법사 개선**  
  
* **최대 자동 장애 조치 대상의 정확한 수를 표시하도록 하는 AlwaysOn '새 가용성 그룹’ 마법사의 버그 수정**  
*연결된 고객 버그 요청:* <https://connect.microsoft.com/SQLServer/feedback/details/2333670/ssms-is-showing-the-wrong-number-of-maximum-automatic-failover-targets/>  
    
* **설치에 영향을 주는 오류를 수정하기 위한 SSMS 웹 설치 관리자의 버그 수정**  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2181548/sql-server-2016-ctp-3-2-management-studio-setup/>  
    
* **SQL Server 2012 이하 버전에서 유지 관리 계획을 저장할 수 있도록 하는 SSMS 미리 보기 릴리스의 버그 수정**  
      
* **스트라이프 백업에 대해 여러 사용자 지정 백업 이름을 허용하고, Storage 자격 증명이 선택된 후 새 이름을 입력하는 경우 적절한 백업 파일 이름을 표시하도록 하는 백업 마법사의 버그 수정**  
  
---  
## <a name="ssms-february-2016-preview"></a>SSMS 2016년 2월 미리 보기 
버전 번호: 13.0.12000.65
  
* **SSMS에서 고대비 설정을 사용하도록 설정한 경우 텍스트 옵션을 표시하도록 활동 모니터 개선**  
  
* **암호화 프로세스 중 한 열에 대한 데이터 정렬이 변경될 경우 경고를 표시하도록 Always Encrypted 마법사 대화 상자 개선**  
  
* **열 암호화 키, 열 암호화 키 값 및 열 마스터 키에 대해 조건을 만들기 위한 지원을 추가하도록 정책 관리 개선**  
  
* **Always Encrypted 마스터 키 정리 대화 상자 및 Always Encrypted 오류 메시지의 유용성을 향상시키기 위한 버그 수정**  
  
* **키가 하나만 있는 경우 Always Encrypted 열 마스터 키 회전을 사용하지 않도록 하는 버그 수정**  
  
* **Always Encrypted 대화 상자가 SSMS 1월 릴리스 또는 SQL Server RC0 미디어와 번들로 제공되는 SSMS 릴리스를 사용하여 시작될 경우에 발생하는 '형식 이니셜라이저' 오류에 대한 버그 수정**  
  
---  
## <a name="ssms-january-2016-preview"></a>SSMS 2016년 1월 미리 보기 
버전 번호: 13.0.11000.78 
  
* **확장 이벤트(XEvent) 세션을 삭제할 수 있도록 SSMS의 버그 수정**  
  
* **SQL Server 2014 가용성 그룹에 대한 속성 대화 상자를 열 수 있도록 버그 수정**  
 *연결된 고객 버그 요청:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/1609719/>  
     
* **가용성 그룹에 Azure 복제본을 추가하는 기능을 지원하도록 버그 수정**  
 *연결된 고객 버그 요청:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2029135/>  
     
* **SQL Server 2014 데이터베이스에 대한 속성 대화 상자를 열 수 있도록 버그 수정**  
 *연결된 고객 버그 요청:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2080209/>  
     
* **Azure SQL Database에 연결된 경우 각 테이블에 대해 표시되는 중복 열을 제거할 수 있도록 버그 수정**  
 *연결된 고객 버그 요청:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2103116/>  
---  
## <a name="ssms-december-2015-preview"></a>SSMS 2015년 12월 미리 보기 
버전 번호: 13.0.900.73
  
* **현재 쿼리 실행 계획의 파일에 저장된 계획과 비교할 수 있도록 실행 계획 비교 개선**  
  
* **SSMS에서 인라인 columnstore 인덱스에 대한 IntelliSense 지원 향상**  
  
* **Azure V12 서버에 연결되어 있을 때 템플릿을 선택할 수 있도록 확장 이벤트 세션 마법사의 버그 수정**  
  
* **보안 폴더 아래의 "감사 만들기" 및 "새 로그인" 대화 상자에서 키보드 탐색을 더 쉽게 하는 새 탭 정지**  
  
* **SSMS에서 결과를 표 형식으로 표시하도록 설정된 경우 "쿼리 실행 후 결과 탭으로 전환"하는 기능을 사용할 수 있도록 버그 수정**   
 *연결된 고객 버그 요청:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1390296/switch-to-results-tab-after-query-execution-grid-mode-in-ssms-2016>  
  
* **SSMS에서 결과를 표 형식으로 표시하도록 설정된 경우 잘리지 않은 열 머리글을 표시하도록 버그 수정**  
 *연결된 고객 버그 요청:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/2004111/bugbash-column-headers-in-grid-mode-truncated-with-courier-new-8>  
      
* **SSMS 웹 설치 관리자를 올바로 설치할 수 있도록 버그 수정**  
 *연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2003865/ssms-october-preview-incoherent-error-message>  
<https://connect.microsoft.com/SQLServer/feedback/details/2079557/unable-to-instal-sql-server-update-13-0-800-111-over-13-0-700-242-error-code-2711>  
  
---  
## <a name="ssms-november-2015-preview"></a>SSMS 2015년 11월 미리 보기
버전 번호: 13.0.800.111
  
* **SSMS의 높은 DPI 디스플레이에 대한 비트맵 확장 지원**  
  
* **데이터베이스 암호화 키를 만드는 과정을 간소화하도록 AlwaysEncrypted 대화 상자 및 마법사의 사용자 인터페이스 개선**  
  
* **활성 쿼리 통계를 볼 수 있도록 작업 모니터의 "프로세스" 목록에 새로운 오른쪽 클릭 상황에 맞는 메뉴 제공**  
  
* **클라이언트 컴퓨터에서 SSMS 시험판 릴리스를 적절히 제거할 수 있도록 버그 수정**  
  *연결된 고객 버그 요청:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1868474/ssms-2016-preview-can-be-installed-but-not-uninstalled>  
  
* **파일이 없는 경우에도 SQL 작업 에이전트에서 작업 단계를 편집할 수 있도록 버그 수정**  
  *연결된 고객 버그 요청:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
    <https://connect.microsoft.com/SQLServer/feedback/details/1502100/ssms-preview-error>  
      
* **Azure 가상 컴퓨터에서 실행 중인 데이터베이스에서 확장 이벤트 세션에 대한 "대상 데이터 보기" 메뉴 옵션의 버그 수정**  
  *연결된 고객 버그 요청*:  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
***  

## <a name="ssms-october-2015-preview"></a>SSMS 2015년 10월 미리 보기 
버전 번호: 13.0.700.242  
* **SSMS 다운로드 및 설치 프로세스를 간소화하는 현대화된 새로운 경량 웹 설치 관리자**  
  
* **선택한 열의 클라이언트 쪽 암호화 및 암호 해독을 지원하는 새로운 항상 암호화 열 암호화 마법사**  
  
* **데이터 보안 유지를 위한 암호화 키 회전 프로세스를 간소화하는 항상 암호화 데이터베이스의 새로운 CMK(열 마스터 키) 회전 대화 상자**  
  
* **Azure 클라우드로 데이터가 마이그레이션되는 상태를 모니터링하고 문제를 해결할 수 있는 새로운 Stretch Database 모니터**  
  
* **기본 Microsoft Azure 구독에 없는 Microsoft Azure 서버의 선택을 지원하도록 개선된 Stretch Database 마법사**  
  *연결된 고객 버그 요청:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1687063/cannot-choose-from-multiple-microsoft-azure-subscriptions>  
* **SSMS에서 라이브 실행 계획을 적절하게 표시할 수 있도록 하는 버그 수정**  
  *연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1774446/viewing-live-execution-plan-from-activity-monitor-crashes-ssms>    
* **데이터베이스 스냅숏의 SSMS 스크립팅에서 잘못된 옵션을 제거하는 버그 수정**  
  *연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1515168/ssms-scripting-of-database-snapshots-includes-invalid-options>  
* **"Top Resource Consuming Queries(상위 리소스 소비 쿼리)" 창에서 세부 정보를 표시하는 쿼리 데이터 저장소 UI의 버그 수정**  
  *연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1737185/sql-server-2016-overall-resource-consumption-query-store-pane-issue>  
***  

## <a name="ssms-september-2015-preview"></a>SSMS 2015년 9월 미리 보기 
버전 번호: 13.0.600.65  
* **Azure SQL Database에 연결하는 과정을 간소화하는 새로운 방화벽 규칙 대화 상자**      
    
* **클러스터된 columnstore 인덱스가 있는 경우에도 클러스터되지 않은 rowstore 인덱스를 만들 수 있도록 업데이트된 "새 인덱스" 대화 상자. 이 기능은 SQL 2016 이상에서 사용할 수 있습니다.**      
  *연결된 고객 버그 요청:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1552617/creation-of-nc-index-when-clustered-columnstore-index>  
      
* **Windows 7에서 실행되는 SSMS 미리 보기 릴리스에서 SQL 에이전트 작업 단계를 보고 편집할 수 있도록 하는 버그 수정**      
  *연결된 고객 버그 요청:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1548140/cannot-view-or-edit-any-sql-agent-job-step>,    
  <https://connect.microsoft.com/SQLServer/feedback/details/1626895/unable-to-load-dll-dts>,    
  <https://connect.microsoft.com/SQLServer/feedback/details/1576662/error-creating-new-job-step>     
      
* **SQL Server 2014 이상의 SSMS에서 트리거 노드를 표시하는 버그 수정**      
  *연결된 고객 버그 요청:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1617533/trigger-node-missing>   
      
* **헤더에서 버전 정보를 제외하는 데이터베이스 및 서버 표준 보고서 사용자 인터페이스의 버그 수정**      
  *연결된 고객 버그 요청:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1387471/report-headings-wrongly-named>  
      
* **라이브 쿼리 통계 노드가 불완전할 때 완전한 것으로 표시되지 못하게 하는 버그 수정**      
  *연결된 고객 버그 요청:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1589096/live-query-statistics-node-shows-as-completed>  
  
***      
## <a name="ssms-august-2015-preview"></a>SSMS 2015년 8월 미리 보기 
버전 번호: 13.0.500.53
  
* **많은 데이터베이스가 있을 때 로드 지연을 줄이는 개체 탐색기 업데이트**  
  
* **Windows 10 컴퓨터에 SSMS를 설치하는 기능 개선**  
  
* **SQL Server 구성 관리자와 SSMS 사용자 보고서 사용자 인터페이스의 버그 수정 및 업데이트**    
***  
  
## <a name="ssms-july-2015-preview"></a>SSMS 2015년 7월 미리 보기
버전 번호: 13.0.400.91
  
* **Azure SQL Database(V12)의 데이터베이스 다이어그램**  
  
* **새로운 임시 테이블 구문에 대한 향상된 IntelliSense 지원**  
  
* **행 수준 보안 및 Azure Active Directory 인증을 비롯한 최신 Azure SQL Database 기능을 지원하도록 업데이트된 DacFx 라이브러리**  
  
* **버그 수정(업데이트된 ‘업데이트 확인’ UI, ‘호환성 수준’ 목록의 UI 수정 등)**  
***  
  
## <a name="ssms-june-2015-preview"></a>SSMS 2015년 6월 미리 보기 
버전 번호: 13.0.300.44
  
* **새로운 SSMS 경량 웹 설치 관리자**  
  
* **업데이트 자동 확인**  
  
* **이제 SSMS에서 Azure SQL Database(V12)에 대한 전체 텍스트 검색을 지원함**  
  
* **상위 고객 요청이 처리됨:**  
  * 개체 편집기에서 테이블 및 뷰에 ‘상위 200개의 행 편집’을 사용할 수 있음  
  * Azure SQL 데이터베이스(V12)에 테이블 디자이너를 사용할 수 있음  
  * Azure SQL 데이터베이스(V12)에 데이터베이스 및 테이블 속성 대화 상자를 사용할 수 있음  
    
 * **T-SQL 파일 저장의 확인을 건너뛰는 새로운 옵션**  
   
 * **새로운 Azure SQL Database 서비스 계층(기본, 표준, 프리미엄)에 대한 가져오기/내보내기 마법사 지원**  
   
 * **수많은 버그 수정(시나리오 스크립팅, SQL 데이터베이스에 대한 변경 내용 추적 사용 등)**   

