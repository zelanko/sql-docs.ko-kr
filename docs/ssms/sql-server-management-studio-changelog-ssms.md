---
title: "SQL Server Management Studio - 변경 로그(SSMS) | Microsoft 문서"
ms.custom: 
ms.date: 12/07/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 051c080de8a5b670a7fe3dbe70ccebf73bfb57a3
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2018
---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 이 문서에서는 SSMS의 현재 버전과 이전 버전에 대한 업데이트, 향상 및 버그 수정에 대한 세부 정보를 제공합니다. [아래의 이전 SSMS 버전](#previous-ssms-releases)을 다운로드하세요.


## <a name="ssms-174download-sql-server-management-studio-ssmsmd"></a>[SSMS 17.4](download-sql-server-management-studio-ssms.md)
일반 공급 | 빌드 번호: 14.0.17213.0

### <a name="whats-new"></a>새로운 기능

**일반 SSMS**

취약성 평가:
- 데이터베이스를 검색하여 구성 오류, 과도한 사용 권한, 중요한 데이터 노출 등의 잠재적 취약성 및 모범 사례와의 차이점을 발견하는 새로운 SQL Vulnerability Assessment 서비스가 추가되었습니다. 
- 평가 결과에는 각 문제를 해결하는 실행 가능한 단계와 사용자 정의 재구성 스크립트(해당하는 경우)가 포함됩니다. 평가 보고서는 각 환경에 맞게 사용자 지정하고 특정 요구 사항에 맞게 조정할 수 있습니다. [SQL Vulnerability Assessment](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment)에서 자세히 알아보세요.

SMO:
- *HasMemoryOptimizedObjects*가 Azure에서 예외를 throw하는 문제를 수정했습니다.
- 새로운 CATALOG_COLLATION 기능에 대한 지원이 추가되었습니다.

Always On 대시보드:
- 가용성 그룹의 대기 시간 분석 기능이 향상되었습니다.
- 두 개의 새 보고서 *AlwaysOn\_대기 시간\_기본* 및 *AlwaysOn\_대기 시간\_보조* 보고서가 추가되었습니다.

실행 계획:
- 올바른 설명서를 가리키도록 링크가 업데이트되었습니다.
- 생성된 실제 계획에서 바로 단일 계획 분석을 수행할 수 있습니다.
- 새 아이콘 집합이 추가되었습니다.
- GbApply, InnerApply처럼 "논리 연산자 적용"을 인식하는 지원이 추가되었습니다.
        
XE 프로파일러:
- 이름이 XEvent 프로파일러로 변경되었습니다.
- 이제 중지/시작 메뉴가 기본적으로 세션을 중지/시작합니다.
- 바로 가기 키를 사용할 수 있습니다(예: CTRL + F 키를 누르면 검색).
- XEvent 프로파일러 세션의 적절한 이벤트에 데이터베이스\_이름 및 클라이언트\_호스트 이름 작업이 추가되었습니다. 변경 내용을 적용하려면 서버에서 기존 QuickSessionStandard 또는 QuickSessionTSQL 세션 인스턴스를 삭제해야 할 수도 있습니다 - [3142981 연결](https://connect.microsoft.com/SQLServer/feedback/details/3142981).

명령줄:
- SSMS가 Active Directory 인증('통합' 또는 '암호')을 사용하여 자동으로 서버/데이터베이스에 연결하도록 하는 새로운 명령줄 옵션("-G")이 추가되었습니다. 자세한 내용은 [Ssms 유틸리티](ssms-utility.md)를 참조하세요.

플랫 파일 가져오기 마법사:
- 테이블을 만들 때 기본값("dbo")이 아닌 스키마 이름을 선택하는 방법이 추가되었습니다.

쿼리 저장소:
- 쿼리 저장소 사용 가능 보고서 목록을 확장할 때 "회귀된 쿼리" 보고서가 복원되었습니다.

**IS(Integration Services)**
- 사용자가 Azure SSIS IR에서 지원되지 않는 SSIS 패키지 내부 구성 요소를 파악하는 데 도움을 주는 패키지 유효성 검사 함수가 배포 마법사에 추가되었습니다.

### <a name="bug-fixes"></a>버그 수정

**일반 SSMS**

- 개체 탐색기:
    - 데이터베이스 스냅숏에 대해 테이블 반환 함수 노드가 표시되지 않는 문제를 수정했습니다 - [연결 3140161](https://connect.microsoft.com/SQLServer/feedback/details/3140161).
    - 서버가 데이터베이스를 자동으로 닫을 때 *데이터베이스* 노드를 확장하는 성능이 개선되었습니다.
- 쿼리 편집기:
    - master 데이터베이스에 액세스할 수 없는 사용자에 대해 IntelliSense가 실패하는 문제를 수정했습니다.
    - 원격 컴퓨터에 대한 연결이 닫히면 SSMS 크래시가 발생하는 문제를 수정했습니다 - [연결 3142557](https://connect.microsoft.com/SQLServer/feedback/details/3142557).
- XEvent Viewer:
    - XEL을 내보내는 기능을 다시 사용할 수 있게 되었습니다.
    - 사용자가 전체 XEL 파일을 로드할 수 없는 문제를 수정했습니다.
- XEvent 프로파일러:
    - 사용자에게 *VIEW SERVER STATE* 권한이 없는 경우 SSMS 크래시가 발생하는 문제를 수정했습니다.
    - XE 프로파일러 라이브 데이터 창을 닫아도 기본 세션이 중지되지 않는 문제를 수정했습니다.
- 등록된 서버:
    - "Move To…" 명령이 멈추는 문제를 수정했습니다 - [연결 3142862](https://connect.microsoft.com/SQLServer/feedback/details/3142862) 및 [Connect 3144359](https://connect.microsoft.com/SQLServer/feedback/details/3144359/).
- SMO:
    - 전송 개체의 TransferData 메서드가 작동하지 않는 문제를 수정했습니다.
    - 일시 중지된 SQL DW 데이터베이스에 대해 서버 데이터베이스가 예외를 throw하는 문제를 수정했습니다.
    - SQL DW에 대해 SQL 데이터베이스를 스크립팅하면 잘못된 T-SQL 매개 변수 값이 생성되는 문제를 수정했습니다.
    - 확대된 DB를 스크립팅하면 *데이터\_압축* 옵션을 잘못 내보내는 문제를 수정했습니다.
- 작업 활동 모니터:
    - 사용자가 범주를 기준으로 필터링하려고 할 때 "인덱스가 범위를 벗어났습니다. 인덱스는 음수가 아니어야 하며 컬렉션의 크기보다 작아야 합니다. 
        매개 변수 이름: 인덱스(System.Windows.Forms)" 오류가 발생하는 문제를 수정했습니다 - [연결 3138691](https://connect.microsoft.com/SQLServer/feedback/details/3138691).
- 연결 대화 상자:
    - 읽기/쓰기 도메인 컨트롤러에 액세스할 수 없는 도메인 사용자가 SQL 인증을 사용하여 SQL Server에 로그인할 수 없는 문제를 수정했습니다 - [연결 2373381](https://connect.microsoft.com/SQLServer/feedback/details/2373381).
- 복제:
    - SQL Server에서 끌어오기 구독의 속성을 볼 때 "ServerInstance 속성에 'null' 값을 적용할 수 없습니다"와 비슷한 오류가 표시되는 문제를 수정했습니다.
- SSMS 설치:
    - SSMS를 설치하면 컴퓨터에 설치된 모든 제품이 다시 구성되는 문제를 수정했습니다.
- 사용자 설정:
   - 이 픽스를 설치하면 US Government 소버린 클라우드 사용자는 유니버설 인증 및 Azure Active Directory 로그인을 통해 SSMS를 사용하여 Azure SQL Database 및 ARM 리소스에 중단 없이 액세스할 수 있습니다.  이전 버전의 SSMS 사용자는 도구|옵션|Azure Services를 열고 리소스 관리 아래에서 "Active Directory 기관" 속성의 구성을 https://login.microsoftonline.us로 변경해야 합니다.

**AS(Analysis Services)**

- 프로파일러: Azure AS에 대해 Window 인증을 사용하여 연결할 때 발생하는 문제를 수정했습니다.
- 1400 모델에 대한 연결 세부 정보를 취소할 때 크래시를 일으킬 수 있는 문제를 수정했습니다.
- 자격 증명을 새로 고치는 동안 연결 속성 대화 상자에서 Azure BLOB 키를 설정할 때 이제는 키가 시각적으로 마스킹됩니다.
- 검색할 때 개체 ID 대신 응용 프로그램 ID를 표시하도록 Azure Analysis Services 사용자 선택 대화 상자의 문제를 수정했습니다.
- 아이콘이 일부 단추에 올바르지 않게 매핑되는 문제를 일으키는 데이터베이스 찾아보기\MDX 쿼리 디자이너 도구 모음 문제를 수정했습니다.
- msmdpump IIS http/https 주소를 사용하여 SSAS에 연결할 수 없는 문제를 수정했습니다.
- 이제 Azure Analysis Services 사용자 선택 대화 상자의 여러 문자열이 추가 언어로 번역되었습니다.
- 이제 MaxConnections 속성이 테이블 형식 모델의 데이터 원본에 대해 표시됩니다.
- 이제 배포 마법사가 Azure AS 역할 멤버에 대한 올바른 JSON 정의를 생성합니다.
- Azure AS에 대해 Windows 인증을 선택해도 로그인 메시지가 계속 표시되는 SQL 프로파일러 문제를 수정했습니다.


## <a name="previous-ssms-releases"></a>이전 SSMS 릴리스

다음 섹션의 제목 링크를 클릭하여 이전 SSMS 버전을 다운로드하세요.

## <a name="downloadssdtmediadownloadpng-ssms-173httpsgomicrosoftcomfwlinklinkid858904"></a>[SSMS 17.3](https://go.microsoft.com/fwlink/?linkid=858904) ![다운로드](../ssdt/media/download.png)
일반 공급 | 빌드 번호: 14.0.17199.0

[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)


### <a name="enhancements"></a>개선 사항

- 최소한의 사용자 간섭 또는 특수화된 도메인 지식을 요구하는 지능형 프레임워크로 CSV 파일의 가져오기 작업을 단순화하기 위해 새 "플랫 파일 가져오기" 마법사가 추가되었습니다. 자세한 내용은 [SQL 마법사로 플랫 파일 가져오기](../relational-databases/import-export/import-flat-file-wizard.md)를 참조하세요.
- 개체 탐색기에 "XEvent Profiler" 노드가 추가되었습니다. 자세한 내용은 [SSMS XEvent Profiler 사용](../relational-databases/extended-events/use-the-ssms-xe-profiler.md)을 참조하세요.
- 성능 대시보드 기록 대기 작업 보고서에 대기 작업 필터링 및 분류가 업데이트되었습니다.
- "Predict" 함수의 구문 검사가 추가되었습니다.
- 외부 라이브러리 관리 쿼리의 구문 검사가 추가되었습니다.
- 외부 라이브러리 관리에 대한 SMO 지원이 추가되었습니다.
- "등록된 서버" 창에 "PowerShell 시작" 지원이 추가되었습니다(새 SQL PowerShell 모듈 필요).
- Always On: 가용성 그룹에 대한 [읽기 전용 라우팅 지원](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)이 추가되었습니다.
- "Active Directory - MFA 지원을 포함한 유니버설 인증" 로그인에 대한 출력 창에 상세 내용 추적을 전송하는 옵션이 추가되었습니다(기본적으로 꺼짐. "도구 > 옵션 > Azure 서비스 > Azure 클라우드 > ADAL 출력 창 추적 수준" 아래의 사용자 설정에서 켜야 함). 
- 쿼리 저장소: 
  - 쿼리 저장소 UI는 QDS가 모든 데이터를 기록하는 한 QDS가 OFF인 경우에도 액세스할 수 있습니다.
  - 이제 쿼리 저장소 UI는 모든 기존 보고서의 대기 분류를 노출합니다. 이를 통해 고객은 상위 대기 중인 쿼리 등의 시나리오를 잠금 해제할 수 있습니다.
- 스크립팅 매개 변수 헤더 옵션을 포함했습니다(기본적으로 꺼짐. "도구 > 옵션 > SQL Server 개체 탐색기 > 스크립팅 > 스크립팅 매개 변수 헤더 포함" 아래의 사용자 설정에서 활성화될 수 있음). - [연결 항목 3139199](https://connect.microsoft.com/SQLServer/feedback/details/3139199)
- "RC" 브랜딩이 제거되었습니다.

### <a name="bug-fixes"></a>버그 수정

**일반 SSMS**

- XEvent: 
   - SSMS이 .xel 파일에서 이벤트의 일부만 여는 문제를 해결했습니다.
   - 기본 데이터베이스가 '마스터'가 아닌 경우 "라이브 데이터 감시"를 개선했습니다. - [연결 항목 1222582](https://connect.microsoft.com/SQLServer/feedback/details/1222582)
- Always On: "복원 로그 백업"에 "이 백업 집합의 로그는 LSN x에서 종료됩니다. 데이터베이스를 적용하기에 너무 이릅니다."라는 오류가 발생하는 문제를 해결했습니다.
- 작업 활동 모니터: 일관성 없는 아이콘을 수정했습니다. - [연결 항목 3133100](https://connect.microsoft.com/SQLServer/feedback/details/3133100)
- 쿼리 저장소: 쿼리 저장소 보고서에 "사용자 지정" 날짜 범위를 선택할 수 없는 문제를 해결했습니다. 아래 연결 항목에 연결됩니다.
   - [연결 항목 3139842](https://connect.microsoft.com/SQLServer/feedback/details/3139842)
   - [연결 항목 3139399](http://connect.microsoft.com/SQLServer/feedback/details/3139399)
- 저장된 정보에 명명된 데이터베이스가 있고 사용자가 <default>를 선택할 때 연결 대화 상자가 가장 최근에 사용된 데이터베이스를 "정리"하지 않는 문제를 해결했습니다.
- 개체 스크립팅:
    - 사용자가 서버에서 DW 데이터베이스를 일시 중지한 경우 "데이터베이스 스크립트 생성"이 작동하지 않고 오류를 throw하지만 다른 DW가 아닌 데이터베이스를 선택하고 스크립트하려고 시도하는 문제를 해결했습니다.
    - 스크립트된 저장 프로시저의 헤더가 스크립트 설정과 일치하지 않고 잘못된 스크립트를 생성하는 문제를 해결했습니다. - [연결 항목 3139784](http://connect.microsoft.com/SQLServer/feedback/details/3139784)
    - SQL Azure 개체를 대상으로 지정할 때 "스크립트" 단추를 다시 사용합니다.
    - SSMS가 Azure SQL Database에 연결될 때 일부 개체(UDF, 보기, SP, 트리거)에서 "변경" 또는 "실행"하도록 스크립트할 수 없는 문제를 해결했습니다. - [연결 항목 3136386](https://connect.microsoft.com/SQLServer/feedback/details/3136386)
- 쿼리 편집기:
  - Azure SQL Databases를 대상으로 할 때 인텔리전스를 개선했습니다.
  - 만료된 인증 토큰(유니버설 인증)으로 인해 쿼리가 실패하는 문제를 해결했습니다.
  - Azure SQL Databases에 대해 작업할 때 인텔리전스를 향상했습니다(특히, Azure SQL Databases에 연결할 때 최신 T-SQL 문법(140) 사용).
  - 서버의 DataWarehouse가 아닌 데이터베이스에 연결된 쿼리 창을 열 때 DataWarehouse 데이터베이스에 대한 해당 서버의 모든 후속 쿼리 기간이 지원되지 않는 형식/옵션에 대한 다양한 오류를 throw하게 되는 문제를 해결했습니다.
- Always On:
   - Always On 대시보드 및 AG 속성 페이지에 시드 모드 열을 추가했습니다.
   - 주 저장소가 Windows에 있을 때 Linux AG를 만들 수 없는 문제를 해결했습니다. - [연결 항목 3139856](https://connect.microsoft.com/SQLServer/feedback/details/3139856)
- 쿼리를 실행할 때 SSMS의 "메모리 부족" 문제를 해결했습니다. - [연결 항목 2845190](https://connect.microsoft.com/SQLServer/feedback/details/2845190), [연결 항목 3123864](https://connect.microsoft.com/SQLServer/feedback/details/3123864)
- 프로파일러: 
   - SQL 2005를 대상으로 지정할 때 프로파일러가 작동하지 않는 문제를 해결했습니다.
   - 프로파일러가 "서버 인증서 신뢰" 연결 옵션을 인식하지 않는 문제를 해결했습니다.
- 작업 모니터: Linux에서 실행 중인 SQL Server를 가리킬 때 작업 모니터가 작동하지 않는 문제를 해결했습니다.
- 외부 데이터 원본이나 외부 파일 형식 개체를 전송하지 않는 SMO 전송 클래스 관련 문제를 해결했습니다. 이제 해당 유형의 개체는 전송에 정확히 포함되어야 합니다.
- 등록된 서버:
   - UA 서버에 다중 서버 쿼리를 사용할 수 있습니다(그룹의 모든 UA 서버에 동일한 토큰을 사용하려고 함).
- AD 유니버설 인증:
   - Azure AD 인증이 지원되지 않는 문제를 해결했습니다.
   - 테이블/뷰 디자이너가 작동하지 않는 문제를 해결했습니다.
   - "상위 1000개 행 선택"과 "상위 200개 행 편집"이 작동하지 않는 문제를 해결했습니다.
- 데이터베이스 복원: 대체 위치에 파일을 이동할 때 복원이 경로의 마지막 폴더를 생략하는 문제를 해결했습니다.
- 압축 마법사:
   - 인덱스에 대한 압축 마법사 관리와 관련된 문제를 해결했습니다. 데이터 압축 마법사가 SQL 2016 이전 버전에서 중지되는 문제를 해결했습니다.
        https://connect.microsoft.com/SQLServer/feedback/details/3139342
   - Azure 테이블 및 인덱스에 압축 마법사를 추가했습니다.
- 실행 계획: 
   - PDW 연산자가 인식되지 않는 문제를 해결했습니다.
- 서버 속성:
   - 서버 프로세서 선호도를 수정할 수 없는 문제를 해결했습니다.


**AS(Analysis Services)**

- 표 형식 1400 호환성 수준 모델 및 파워 쿼리 데이터 원본을 지원하는 배포 마법사와 관련된 여러 문제를 해결했습니다.
- 이제 배포 마법사는 명령줄에서 실행할 때 AS Azure에 배포할 수 있습니다.
- 이제 AS Azure에서 Windows 인증을 사용하는 경우 사용자는 개체 탐색기에서 사용자 계정의 이름을 정확하게 확인할 수 있습니다.


### <a name="known-issues-in-this-173-release"></a>이 17.3 릴리스의 알려진 문제:

**일반 SSMS**

- MFA를 지원하는 UA를 사용하는 Azure AD 인증에는 다른 SSMS 기능이 지원되지 않습니다.
   - 데이터베이스 엔진 튜닝 관리자는 Azure AD 인증에 지원되지 않습니다. 사용자에게 제공된 오류 메시지가 유용하지 않은 알려진 문제가 있습니다. "예상과는 달리 파일 또는 어셈블리 'Microsoft.IdentityModel.Clients.ActiveDirectory,...를 로드할 수 없습니다." "데이터베이스 엔진 튜닝 관리자는 Microsoft Azure SQL Database를 지원하지 않습니다. (DTAClient)".
- 오류의 DTA 결과에서 쿼리 분석 시도: "개체는 IConvertible을 구현해야 합니다. (mscorlib)".
- *재발된 쿼리*가 개체 탐색기에서 보고서의 쿼리 저장소 목록에서 누락되었습니다.
   - 해결 방법: 마우스 오른쪽 단추로 **쿼리 저장소** 노드를 클릭하고 **재발된 쿼리 보기**를 선택합니다.

**IS(Integration Services)**

- [catalog].[event_messagea]에서 [execution_path]가 Scale Out에서 패키지 실행에 대해 올바르지 않습니다. [execution_path]는 패키지 실행 파일의 개체 이름 대신 "\Package"로 시작합니다. SSMS에서 패키지 실행의 개요 보고서를 볼 때 실행 개요에서 "실행 경로"의 링크는 작동하지 않습니다. 해결 방법은 개요 보고서에서 "메시지 보기"를 클릭하여 모든 이벤트 메시지를 확인하는 것입니다.


## <a name="downloadssdtmediadownloadpng-ssms-172httpsgomicrosoftcomfwlinklinkid854085"></a>[SSMS 17.2](https://go.microsoft.com/fwlink/?linkid=854085) ![다운로드](../ssdt/media/download.png)
일반 공급 | 빌드 번호: 14.0.17177.0

[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

### <a name="enhancements"></a>개선 사항

- MFA(Multi-Factor Authentication)
  - MFA(Multi-Factor Authentication)를 지원하는 UA(유니버설 인증)에 대한 다중 사용자 Azure AD 인증
  - 다중 사용자 인증을 지원하기 위해서 새 사용자 자격 증명 입력 필드가 MFA를 지원하는 유니버설 인증에 대해 추가되었습니다.
- 이제 연결 대화 상자는 다음 5개 인증 방법을 지원합니다.
  - Windows 인증
  - SQL Server 인증(SQL Server Authentication)
  - Active Directory - MFA 지원을 포함한 유니버설 인증
  - Active Directory - 암호
  - Active Directory - 통합

- MFA를 지원하는 유니버설 인증을 사용하여 DACFx 마법사에 대한 데이터베이스 내보내기/가져오기를 사용할 수 있습니다.
- API 지원에 대해서는 [IUniversalAuthProvider 인터페이스](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)를 참조하세요.
- MFA를 지원하는 Azure AD 유니버설 인증에 사용되는 ADAL 관리 라이브러리가 버전 3.13.9로 업그레이드되었습니다.
- 또한 SQL Database 및 SQL Data Warehouse에 대한 Azure AD 관리자 설정을 지원하는 새 CLI 인터페이스가 제공되었습니다.

 Active Directory 인증 방법에 대한 자세한 내용은 [SQL Database 및 SQL Data Warehouse에 대한 유니버설 인증(MFA에 대한 SSMS 지원)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) 및 [SQL Server Management Studio에 대한 Azure SQL Database 다단계 인증 구성](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure)을 참조하세요.

- 출력 창에는 개체 탐색기 노드를 확장하는 동안 실행되는 쿼리에 대한 항목이 있습니다.
- Azure SQL Database에 대해 뷰 디자이너 사용 설정
- SSMS의 개체 탐색기에서 개체를 스크립팅하기 위한 기본 스크립팅 옵션이 변경되었습니다.
  - 이전에는 생성된 스크립트의 대상을 SQL Server의 최신 버전(현재 SQL Server 2017)으로 지정하는 것이 새 설치에 대한 기본값이었습니다.
  - SSMS 17.2에서는 *스크립트 설정을 원본과 일치* 옵션이 새로 추가되었습니다. *True*로 설정하면 생성된 스크립트의 대상은 스크립팅되는 개체가 있는 서버와 동일한 버전, 엔진 유형 및 엔진 버전이 됩니다.
  - *스크립트 설정을 원본과 일치* 값은 기본적으로 *True*로 설정되므로 새 SSMS 설치의 기본값은 자동으로 항상 개체를 원본 서버와 동일한 대상으로 스크립팅이 됩니다.
  - *스크립트 설정을 원본과 일치* 값을 *False*로 설정하면 기본 스크립팅 대상 옵션이 사용하도록 설정되어 이전과 같이 작동합니다.
    - 또한 모든 스크립팅 옵션이 자체 섹션인 *버전 옵션*으로 이동하였습니다. 따라서 더 이상 *일반 스크립팅 옵션* 아래에 없습니다.

- “URL에서 복원”에서 국가 클라우드에 대한 지원 추가
- 이제 QueryStoreUI 보고서는 sys.query_store_runtime_stats에서 추가 메트릭(RowCount, DOP, CLR Time 등)을 지원합니다.
- Azure SQL Database에 IntelliSense 지원
    - https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
- 보안: 연결 대화 상자가 기본적으로 Azure SQL DB 연결을 위해 신뢰하는 서버 인증서 및 요청 암호화에 연결되지 않음
- Linux에서 SQL Server에 대한 지원과 관련된 일반 개선 사항:
 - 데이터베이스 메일 노드의 재등장
 - 경로와 관련된 기타 문제 해결
 - 더욱 안정적인 작업 모니터
 - [연결 속성] 대화 상자에 정확한 플랫폼 표시
- 성능 대시보드 서버 보고서를 기본 보고서로 제공:
  - SQL Server 2008 이상의 버전에 연결할 수 있습니다.
  - 누락된 인덱스 하위 보고서는 점수 매기기를 사용하여 가장 유용한 인덱스를 식별하는 데 도움을 줍니다.
  - 기록 대기 상태 하위 보고서는 대기 범주를 집계합니다. 유휴 및 중지 대기는 기본적으로 필터링됩니다.
  - 새 기록 래치 하위 보고서.
- 실행 계획 노드 검색을 사용하여 계획 속성을 검색할 수 있습니다. 테이블 이름과 같은 연산자 속성을 쉽게 찾을 수 있습니다. 계획을 볼 때 이 옵션을 사용하려면
  - 계획을 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 [노드 찾기] 옵션을 클릭합니다.
  - CTRL+F 사용


**AS(Analysis Services)**

- SSMS의 AS Azure 모델에서 메일 주소가 없는 사용자에 대한 새 AAD 역할 멤버 선택

**IS(Integration Services)**

- SSIS용 실행 보고서에 새 열("실행 수") 추가

### <a name="known-issues-in-this-release"></a>이 릴리스의 알려진 문제:

- “Active Directory - MFA를 지원하는 유니버설” 인증을 사용하는 쿼리 창을 한 시간 동안 연 후 쿼리를 실행하면 다음과 유사한 오류가 발생할 수 있습니다.

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery is not possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of ConnectRetryCount to increase the number of recovery attempts.`

   쿼리를 다시 실행하면 오류를 통과하고 성공하게 됩니다.

- MFA를 지원하는 유니버설 인증을 사용하는 Azure AD 인증에는 다른 SSMS 기능이 지원되지 않습니다.
  - **새 테이블/뷰** 디자이너는 이전 스타일 로그인 프롬프트를 표시하며 Azure AD 인증을 위해 작동하지 않습니다.
  - **상위 200개의 행 편집** 기능은 Azure AD 인증을 지원하지 않습니다.
  - **등록된 서버** 구성 요소는 Azure AD 인증을 지원하지 않습니다.
  - **데이터베이스 엔진 튜닝 관리자**는 Azure AD 인증에 대해 지원되지 않습니다. 사용자에게 제공된 오류 메시지가 유용하지 않은 알려진 문제가 있습니다. *예상과는 달리 파일 또는 어셈블리 'Microsoft.IdentityModel.Clients.ActiveDirectory,...를 로드할 수 없습니다.* *데이터베이스 엔진 튜닝 관리자는 Microsoft Azure SQL Database를 지원하지 않습니다. (DTAClient)*.

**AS(Analysis Services)**

- SSAS의 개체 탐색기는 AS Azure 연결 속성에 Windows 인증 사용자 이름을 표시하지 않습니다.

### <a name="bug-fixes"></a>버그 수정

- 텍스트 형식의 쿼리 결과를 인쇄할 때의 문제 해결.  https://connect.microsoft.com/SQLServer/feedback/details/3055225/
- SQL Azure 데이터베이스에서 개체 삭제를 스크립팅할 때 SSMS가 테이블 및 그러한 개체를 잘못 끌어오는 문제 해결.
- “하나 이상의 구성 요소를 찾을 수 없습니다. 응용 프로그램을 다시 설치하세요.”와 같은 오류로 SSMS가 가끔 시작을 거부하는 문제 해결.
- SSMS UI의 SPID가 부실하고 동기화되지 않는 문제가 해결되었습니다. https://connect.microsoft.com/SQLServer/feedback/details/1898875
- SSMS(자동) 설치 프로그램에서 /passive 인수가 /quiet으로 처리되는 문제 해결.
- SSMS를 시작할 때 가끔 “개체 참조가 개체의 인스턴스로 설정되지 않았습니다.” 오류가 발생하는 문제 해결. http://connect.microsoft.com/SQLServer/feedback/details/3134698
- "데이터 압축 마법사"의 그래프 테이블에서 ‘Calculate’를 누를 때 SSMS가 충돌을 일으켰던 문제 해결.
- 테이블에 대한 인덱스를 마우스 오른쪽 단추로 클릭할 때(느린 인터넷 연결을 통해) 발생하는 성능 문제 해결. https://connect.microsoft.com/SQLServer/feedback/details/3120783
- SSMS가 서버의 백업 파일을 대/소문자 구분 데이터 정렬로 열거하지 못하는 문제 해결. http://connect.microsoft.com/SQLServer/feedback/details/3134787 및 https://connect.microsoft.com/SQLServer/feedback/details/3137000
- 실행 계획 및 실행 계획 비교와 관련된 각종 수정 사항
- SSMS를 실행하는 컴퓨터에 SQL Server를 설치하지 않은 경우 사용자가 [연결] 대화 상자를 이용하여 연결에 사용할 “네트워크 프로토콜”을 지정할 수 없었던 문제 해결. https://connect.microsoft.com/SQLServer/feedback/details/3134997
- 일부 SSMS 대화 상자가 “임의의” 위치에서 나타나는 다중 모니터 구성에 대한 지원 향상. 작업 대화 상자 또는 속성 시트를 종료한 후 그 위치를 기억할 수 있도록 “SQL Server 개체 탐색기 | 명령” 사용자 설정 아래에 새 옵션인 “작업 대화 상자” 추가. https://connect.microsoft.com/SQLServer/feedback/details/889169, https://connect.microsoft.com/SQLServer/feedback/details/1158271, https://connect.microsoft.com/SQLServer/feedback/details/3135260 
- SSMS가 암호화된 Azure SQL DB에 대한 DB 속성을 변경할 수 없었던 문제 해결.
- “실행 후 결과 삭제” 옵션 개선. https://connect.microsoft.com/SQLServer/feedback/details/1196581
- 관리자가 아닌 Azure 구독에 사용자가 액세스할 수 없는 문제 개선/해결.
- “데이터베이스 복원” 마법사가 원본 데이터베이스 선택에 관계없이 OE에서 선택한 대상 데이터베이스를 유지하도록 개선. https://connect.microsoft.com/SQLServer/feedback/details/3118581
- 새롭게 잘못 추가된 “고유하게 컴파일된 저장 프로시저”를 개체 탐색기가 정렬하지 않았던 문제 해결. http://connect.microsoft.com/SQLServer/feedback/details/3133365
- “상위 n개 행 선택”에 “TOP” 절이 포함되지 않았던 문제 해결. Azure SQLDW의 경우. https://connect.microsoft.com/SQLServer/feedback/details/3133551 및 https://connect.microsoft.com/SQLServer/feedback/details/3135874
- QueryStoreUI: 사용자 지정이 아닌 시간 간격이 올바로 작동하지 않는 보고서가 있었던 문제 해결.
- 항상 암호화:
    - 새 CMK 대화 상자에서 AKV 권한 상태에 대한 메시징 기능 개선
    - 긴 이름을 가진 CEK를 보다 쉽게 구분할 수 있도록 CEK 드롭다운에 도구 설명 추가
    - 일부 CNG 키 저장소 공급자가 항상 암호화를 위한 [새 열 마스터 키] 대화 상자에 표시되지 않는 문제 해결
- SSMS 연결에 대해 일관성 없는 “응용 프로그램 이름” 해결. http://connect.microsoft.com/SQLServer/feedback/details/3135115
- SSMS가 SQL Azure에 대한 정확한 스크립트(DATA_COMPRESSIONS 옵션을 포함한 테이블 및 인덱스)를 생성하지 않았던 문제 해결. https://connect.microsoft.com/SQLServer/feedback/details/3133148
- 사용자가 빠른 실행을 위해 CTRL+Q 바로 가기를 사용할 수 없었던 문제 해결(참고: 이제 쿼리 편집기에서 "IntelliSense 사용" 옵션을 설정/해제하기 위한 새 키 바인딩은 CTRL+B, CTRL+I). https://connect.microsoft.com/SQLServer/feedback/details/3131968
- "데이터베이스 복원"에서 사용자 지정 도메인이 정의된 계정을 가진 구독에서 저장소 계정을 선택하려고 할 때 SSMS가 예외를 throw했던 문제 해결
- "데이터베이스 다이어그램"에서 SSMS가 “인덱스가 배열의 범위 밖에 있습니다.” 오류를 throw하고 사용자가 "테이블 보기"를 표준이 아닌 것으로 변경할 수 없었던 문제 해결. https://connect.microsoft.com/SQLServer/feedback/details/3133792 및 http://connect.microsoft.com/SQLServer/feedback/details/3135326
- "URL에 백업/복원"에서 SSMS가 클래식 저장소 계정을 열거하지 않았던 문제 해결.
- 스키마 바운드 보안 개체를 DB 역할에 추가하려고 할 때 예외가 throw되었던 문제 해결. https://connect.microsoft.com/SQLServer/feedback/details/3118143
- 테이블 노드 http://connect.microsoft.com/SQLServer/feedback/details/3136283를 확장할 때 SSMS가 "데이터는 Null입니다. 이 메서드 또는 속성은 Null 값에 호출될 수 없습니다." 오류를 간헐적으로 표시했던 문제 해결.
- DTA: 특정 경계 값으로 파티션 함수를 평가할 때 DTAEngine.exe가 힙 손상으로 종료되는 문제 해결.


**AS(Analysis Services)**

- DB가 ID와 다른 이름을 가진 경우 오류가 발생하여 AS 복원 데이터베이스가 실패하는 문제 해결
- DAX 쿼리 창이 IntelliSense 사용을 설정/해제하기 위한 메뉴 옵션을 무시하는 문제 해결
- msmdpump IIS http/https 주소를 통해 SSAS에 연결하지 못했던 문제 해결
- 세미콜론을 포함한 암호를 사용하여 AS Azure에 연결할 수 있도록 허용
- SQL Server 2017 AS 서버 또는 AS Azure와 함께 사용할 경우 “멤버 등록 생략” 옵션으로 AS 복원 데이터베이스 명령 스크립팅할 때 새로운 해당 JSON 옵션 포함
- 로드할 때 데이터베이스 삭제 대화 상자에서 오류가 발생할 수 있는 매우 드문 문제 해결
- SQL 쿼리 및 M 파티션 정의가 혼합된 1400-compat 수준 모델에서 파티션을 보려고 할 때 발생할 수 있는 문제 해결

**IS(Integration Services)**
- SSISDB 카탈로그의 실행 정보 보고서를 표시할 수 없는 문제 해결
- SSMS에서 수많은 프로젝트/패키지의 성능 저하와 관련된 문제 해결

## <a name="downloadssdtmediadownloadpng-ssms-171httpsgomicrosoftcomfwlinklinkid799832"></a>[SSMS 17.1](https://go.microsoft.com/fwlink/?linkid=799832) ![다운로드](../ssdt/media/download.png)
출시 | 빌드 번호: 14.0.17119.0

[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

### <a name="enhancements"></a>개선 사항

- Profiler: 도움말 > 정보에 이제 릴리스 버전 번호(예: 17.1)가 표시됨
- Analysis Services 사용자가 데이터 원본의 상황에 맞는 메뉴에서 1200 TM 모델 이상에 대해 데이터 원본의 자격 증명을 새로 고칠 수 있음
- 기본 제공 SSIS 보고서에 CTP 2.1에서 SSIS Scale Out 실행의 로그가 표시됨
- SSIS Scale Out 관리 응용 프로그램
  - 스케일 아웃 마스터에 대한 기본 정보 보기
  - 스케일 아웃 배포에 작업자를 쉽게 추가
  - 모든 확장 작업자 및 해당 작업자에 대한 기본 정보를 보고 간단히 작업자를 사용하거나 사용하지 않도록 설정할 수도 있음

### <a name="bug-fixes"></a>버그 수정
- Always On:
  - 가용성 복제본의 속성이 WSFC AG에 대해 항상 “자동 장애 조치(failover)” 모드로 표시되는 문제를 해결함
  - 가용성 그룹을 업데이트할 때 읽기 전용 라우팅 목록을 덮어쓰는 문제를 해결함
- Always Encrypted: 생성된 로그 파일에서 DacFx에서 생성한 정보가 누락되는 문제를 해결함
- 실행 계획: UI에서 비적응 조인 연산자에 대해 항상 실제 조인 유형 특성을 표시하는 문제를 해결함
- 설치:
  - SSMS 17.0이 Visual Studio 2013에서 SSDT를 중단시키는 문제를 해결함[Connect 항목 3133479]
  - 설치 완료 시 “다시 시작”을 클릭해도 컴퓨터가 다시 시작되지 않는 문제를 해결함
- 스크립팅: 해당 옵션을 사용하지 않도록 설정하여 삭제를 스크립팅하려고 할 때 SSMS가 Azure 데이터베이스 개체를 실수로 삭제하지 않도록 일시적으로 제한함.  향후 SSMS 릴리스에서 적절한 수정이 제공될 예정입니다.
- 개체 탐색기: AS COPY를 사용하여 만든 Azure 데이터베이스에 연결할 때 “데이터베이스” 노드가 확장되지 않는 문제를 해결함

## <a name="downloadssdtmediadownloadpng-ssms-170httpgomicrosoftcomfwlinklinkid799832"></a>[SSMS 17.0](http://go.microsoft.com/fwlink/?LinkID=799832) ![다운로드](../ssdt/media/download.png)
출시 | 빌드 번호: 14.0.17099.0

[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

### <a name="enhancements"></a>개선 사항 

- 업그레이드 패키지 및 WSUS(Windows Software Update Services) 
    - 향후 17.X 릴리스에는 더 작은 누적 업데이트 패키지가 포함됨 
  - 업데이트 패키지는 WSUS 카탈로그에도 게시됨  
- 아이콘 업데이트
    - 아이콘이 VS Shell 제공 아이콘과 일치하고 높은 DPI 해상도를 지원하도록 업데이트됨
    - 16.X 및 17.X 버전을 구분하는 새 SSMS 및 Profiler 프로그램 아이콘
- SQL PowerShell 모듈
  - SQL Server PowerShell 모듈이 SSMS에서 제거되고 이제 PowerShell 갤러리를 통해 제공(모듈 버전 관리를 지원하려면 이제 PowerShell 5.0 필요)
  - 일부 SMO 개체의 프레젠테이션(형식) 관련 기타 개선 사항(예: 이제 데이터베이스에 크기와 사용 가능한 공간이 표시되고 테이블에 행 수와 공간 사용량 표시)
  - OE의 “PowerShell 시작” 메뉴에서 PowerShell 명령 프롬프트를 호출할 때 색 지정을 추가함
  - AG cmdlet(New-SqlAvailabilityGroup, Join-SqlAvailabilityGroup 및 Set-SqlAvailabilityGroup cmdlet)에 -ClusterType 및 -RequiredCopiesToCommit 매개 변수를 추가함
  - Add-SqlAzureAuthenticationContext cmdlet에 -ActiveDirectoryAuthority 및 -AzureKeyVaultResourceId 매개 변수를 추가함
  - Revoke-SqlAvailabilityGroupCreateAnyDatabase, Grant-SqlAvailabilityGroupCreateAnyDatabase 및 Set-SqlAvailabilityReplicaRoleToSecondary cmdlet을 추가함
  - Set-SqlAvailabilityReplica 및 New-SqlAvailabilityReplica cmdlet에 -SeedingMode 매개 변수를 추가함
  - Get-SqlDatabase에 -ConnectionString 매개 변수를 추가함
- Linux의 SQL Server
    - 일반 개선 사항 및 로그 전달에 대한 수정
  - 데이터베이스 연결, 복원 및 백업에 대한 네이티브 Linux 경로 지원을 추가함
  - 감사 로그 대상 폴더의 원시 Linux 경로에 대한 지원을 추가함
- Analysis Services
  - DAX 쿼리 창:
    - 편집기에서 괄호 일치
    - DEFINE MEASURE 및 DEFINE VAR 구문 지원
    - 여러 Intellisense 개선 사항
  - 유니버설 인증
    - 사용자가 암호 없이 사용자 이름을 지정할 수 있고 및 Azure 로그인 대화 상자에서 연결 처리
  - SSMS PQ 통합: 
    - 구조적 데이터 원본에 대한 스크립팅이 작동함 
    - PQ UI에서 구조적 데이터 원본 보기 및 편집
- 새 "UNIQUE 제약 조건 추가" 템플릿
- Showplan
    - 결과 시간에 대한 속성 창에서 전체 스레드의 합계 대신 최대값 표시
    - 새로운 메모리 부여 연산자 속성 노출
    - 활성 쿼리 통계에서 "쿼리 편집" 단추를 사용하도록 설정함
    - 인터리브 실행 지원
  - “실제 실행 계획 분석”에 대한 새로운 옵션
  - 실행 계획 비교에 대한 일반 개선 사항
  - 두 쿼리 계획의 일치하는 노드 간에 카디널리티 추정의 큰 차이를 찾고 가능한 근본 원인에 대한 기본 분석을 수행하는 기능을 실행 계획 비교 기능에 도입함
- 등록된 서버 탐색기에서 구성 관리자를 제거함
- Azure Blob Storage에서 감사 로그 읽기 지원
- Always Encrypted에 대한 매개 변수화가 추가됨, 자세한 내용은 [이 페이지](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/) 참조 
- Azure SQL DB에 대한 AAD 유니버설 인증 연결에서 사용자 지정 테넌트 ID 지원 
- Azure SQL Database에 대한 스크립트 생성, 이제 전체 텍스트, 규칙 및 데이터베이스 스크립팅 가능
- SSMS 및 Profiler의 시작 화면에서 브랜딩 수정
- SSMS에서 유틸리티 제어 지점 UI 제거함
- SSMS에서 이제 “PremiumRS” 버전 SQL Azure 데이터베이스를 만들 수 있음
- Always On 가용성 그룹
  - 새 클러스터 유형에 대한 지원 추가: EXTERNAL 및 NONE
    - Linux에서 SQL Server에 대한 지원 추가
    - 초기 데이터 동기화에 대한 옵션으로 자동 시드를 추가
    - 일부 결함을 수정함(예: 끝점 URL 처리, DB 새로 고침, UI 레이아웃)
    - Azure 복제본 관련 기능을 제거함
  - 여러 가용성 그룹 키워드에 대한 IntelliSense를 개선함
- 작업 모니터
  - SSMS 출력 창에 새 “작업 모니터” 창을 추가함
  - 팝업 메시지를 표시하지 않고 정보를 출력 창에 기록하도록 연결 오류/시간 초과 메시지를 변경함
  - 개요 섹션에서 빈 차트(5번째 차트)를 제거함
  - 작업 모니터 데이터 수집이 일시 중지된 경우 개요 제목에 “(일시 중지됨)”을 추가함
  - SQL Server에 대한 그래프 확장 
    - 그래프 노드와 에지 테이블에 대한 새 아이콘
    - 그래프 노드 및 에지 테이블이 그래프 테이블 폴더 아래에 표시됨
    - 그래프 노드와 에지 테이블을 만들기 위한 서식 파일 사용 가능
- 프레젠테이션 모드
    - 빠른 실행(Ctr Q)을 통해 사용할 수 있는 세 가지 새 작업
    - PresentOn - 프레젠테이션 모드 켜기
    - PresentEdit - 프레젠테이션 모드에 대한 프레젠테이션 글꼴 크기 편집.  쿼리 편집기의 경우 "텍스트 편집기 글꼴".  다른 구성 요소의 경우 "환경 글꼴"
    - RestoreDefaultFonts - 기본 설정으로 되돌리기
    - *참고: 현재 PresentOff 명령이 없습니다.  프레젠테이션 모드를 끄려면 RestoreDefaultFonts를 사용 하세요.*

### <a name="bug-fixes"></a>버그 수정

- surfacebook 터치 패드를 통해 실행 계획을 스크롤할 때 SSMS가 중지되는 문제를 해결함
- 복원 중이거나 오프라인 상태인 데이터베이스의 속성을 가져오는 동안 SSMS가 오랫동안 중단되는 문제를 해결함 
- RC 빌드에서 “도움말 뷰어”를 열 수 없는 문제를 해결함
- SSMS에서 “유지 관리 계획 태스크 도구 상자” 항목이 없을 수 있는 문제를 해결함
- SSMS에서 사용자가 데이터베이스 이름에 중괄호가 포함된 경우 데이터베이스를 축소할 수 없는 문제를 해결함 [Connect 항목](https://connect.microsoft.com/SQLServer/feedback/details/3122618)
- SSMS에서 Azure 데이터베이스의 삭제를 스크립팅하려고 할 때 실제로 데이터베이스 자체가 삭제되는 문제를 해결함 [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3131458/)
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
  - 리소스 파일을 제대로 로드할 수 없어서 부정확한 오류 메시지가 표시되는 문제를 해결함
- SSMS 설치 페이지에서 하이퍼링크의 대비 향상
- SQL Server Express(2016 SP1)에 연결된 경우 Polybase 노드가 표시되지 않는 문제를 해결함
- SSMS가 Azure DB의 호환성 수준을 v140으로 변경할 수 없는 문제를 해결함
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
- 사용자가 SQL Server 2017에서 데이터베이스의 호환성 수준을 변경할 수 없게 했었던 문제를 수정함
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
- 활성 쿼리 통계: 배치에 있는 첫 번째 쿼리만 표시하던 문제를 해결함. [Connect 항목] (http://connect.microsoft.com/SQLServer/feedback/details/3114221)  
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
- 여러 스키마가 포함된 기존 데이터베이스에 대한 Always Encrypted 구성이 작동하지 않음. [Connect 항목] (http://connect.microsoft.com/SQLServer/feedback/details/3109591)
- Always Encrypted, 암호화된 열 마법사가 시스템 뷰를 참조하는 뷰를 포함하는 데이터베이스로 인해 실패함. [Connect 항목] (http://connect.microsoft.com/SQLServer/feedback/details/3111925)
- Always Encrypted를 사용하여 암호화할 때 암호화가 잘못 처리된 후 모듈을 새로 고치지 못하는 오류가 발생함.
- "새 서버 등록" 대화 상자에서 UI 잘림 문제를 해결함
- 따옴표가 있는 문자열 상수 값을 포함하는 식을 잘못 업데이트하는 DMF 조건 UI 수정
- 사용자 지정 보고서를 실행할 때 SSMS 작동을 중단시킬 수 있는 문제를 수정함
- 폴더 노드에 "Execution in Scale Out…"(규모 확장에서 실행…) 메뉴 항목 추가
- Azure SQL DB 방화벽 허용 목록 IP 주소 기능 관련 문제를 해결
- SSMS에서 AS 다차원 파티션의 원본을 편집할 때 개체 참조가 설정되지 않음 예외가 발생하는 문제를 해결함
- SSMS에서 다차원 AS 서버에서 고객 어셈블리를 삭제할 때 개체 참조가 설정되지 않음 예외가 발생하는 문제를 해결함
- AS 테이블 형식 1400 db 이름을 바꾸지 못하는 문제를 해결함
- 연결 속성 대화 상자에서 1400 호환성 수준 AS 테이블 형식 데이터 원본을 스크립팅할 때 발생하는 문제를 해결함
- AS 1400 호환성 수준 모델의 테이블에 파티션을 둘 이상 있다는 가정을 제거함
- 이제 SSMS DAX 쿼리 편집기에서 Ctrl-R을 누르면 결과 창이 전환됨


## <a name="downloadssdtmediadownloadpng-ssms-1653httpgomicrosoftcomfwlinklinkid799832"></a>[SSMS 16.5.3](http://go.microsoft.com/fwlink/?LinkID=799832) ![다운로드](../ssdt/media/download.png)
일반 공급 | 빌드 번호: 13.0.16106.4

[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

이 릴리스에서는 다음과 같은 문제가 해결되었습니다.

* 테이블에 스파스 열이 둘 이상 있을 때 'Table' 노드의 확장을 일으키는 SSMS 16.5.2의 문제를 해결함.

* 사용자가 Microsoft Dynamics AX/CRM Online 리소스에 연결되는 OData 연결 관리자를 포함하는 SSIS 패키지를 SSIS 카탈로그에 배포할 수 있음. 자세한 내용은 [OData 연결 관리자](../integration-services/connection-manager/odata-connection-manager.md)를 참조하세요.

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


## <a name="ssms-1651"></a>SSMS 16.5.1
일반 공급 | 빌드 번호: 13.0.16100.1

* CHECK 제약 조건이 발생할 때 Invoke-Sqlcmd이 여러 행을 잘못 삽입하는 문제를 해결했습니다. [Microsoft Connect 항목: 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* 가용성 그룹을 만들 때 ENU가 아닌 언어 버전이 완벽히 작동하지 않는 문제를 해결했습니다.

* 쿼리 계획 XML을 클릭할 때 올바른 SSMS UI가 열리지 않는 문제를 해결했습니다.


## <a name="downloadssdtmediadownloadpng-ssms-165httpgomicrosoftcomfwlinklinkid799832"></a>[SSMS 16.5](http://go.microsoft.com/fwlink/?LinkID=799832) ![다운로드](../ssdt/media/download.png)
일반 공급 | 빌드 번호: 13.0.16000.28


[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

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


## <a name="downloadssdtmediadownloadpng-ssms-1641-september-2016httpgomicrosoftcomfwlinklinkid799832"></a>[SSMS 16.4.1(2016년 9월)](http://go.microsoft.com/fwlink/?LinkID=799832) ![다운로드](../ssdt/media/download.png)
일반 공급 | 빌드 번호: 13.0.15900.1

[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

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
    
*  시스템 데이터베이스 내에 있을 때 개체 탐색기에서 temporal 테이블을 확장할 수 없는 문제 해결  
[Microsoft Connect 항목 #2551649](https://connect.microsoft.com/SQLServer/feedback/details/2551649)
    
*  SSMS가 일괄 처리 실행 후 SELECT @@trancount에 대한 쿼리를 실행하는 문제 해결    
[Microsoft Connect 항목 #3042364](https://connect.microsoft.com/SQLServer/feedback/details/3042364)
    
*  서버의 속성 페이지에서 스크립트를 만들 때 연결 대화 상자가 숨겨지던 Analysis Services의 문제를 해결했습니다.
    
*  Ctrl + Q로 빠른 실행 도구 모음이 선택되지 않는 문제 해결
    
*  2TB가 넘는 데이터베이스의 경우에는 서버 속성 대화 상자를 사용하여 데이터베이스의 MaxSize를 변경할 수 없는 문제 해결  
[Microsoft Connect 항목 #1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  데이터베이스 복원 마법사에서 앞에 공백이 있는 파일 이름을 사용할 수 없는 문제 해결   
[Microsoft Connect 항목 #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="downloadssdtmediadownloadpng-ssms-163-august-2016httpgomicrosoftcomfwlinklinkid799832"></a>[SSMS 16.3(2016년 8월)](http://go.microsoft.com/fwlink/?LinkID=799832) ![다운로드](../ssdt/media/download.png)
일반 공급 | 버전 번호: 13.0.15700.28


[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

* SSMS 월별 릴리스는 이제 번호로 브랜딩됩니다.

* [새 인증 옵션 **'Active Directory 유니버설 인증'**](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/) Azure Active Directory에 의해 구동되는 토큰 기반 인증 메커니즘으로, 다단계, 암호 및 통합 인증 메커니즘을 지원합니다.

* SQL Server Profiler 템플릿 기능과 일치하는 새로운 확장 이벤트 템플릿 [(Microsoft Connect 항목 #2543925)](../tools/sql-server-profiler/sql-server-profiler-templates.md)

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
## <a name="downloadssdtmediadownloadpng-ssms-july-2016-hotfix-updatehttpgomicrosoftcomfwlinklinkid799832"></a>[SSMS 2016년 7월 핫픽스 업데이트](http://go.microsoft.com/fwlink/?LinkID=799832) ![다운로드](../ssdt/media/download.png)
일반 공급 | 버전 번호: 13.0.15600.2

[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

* **누락된 오른쪽 클릭 메뉴 항목을 사용하도록 설정하기 위한 SSMS의 버그 수정**  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Microsoft Connect 항목 #2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Microsoft Connect 항목 #2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016"></a>SSMS 2016년 7월 
일반 공급 | 버전 번호: 13.0.15500.91

* *편집(7월 5일):* [Analysis Services 처리] 대화 상자 및 Analysis Services 배포 마법사의 SQL Server 2016(호환성 수준 1200) 테이블 형식 데이터베이스에 대해 향상된 지원.

* *편집(7월 5일):* ‘XACT_ABORT’를 설정하는 SSMS ‘쿼리 실행 옵션’ 대화 상자의 새 옵션. 이 옵션은 이 SSMS 릴리스에서 기본적으로 설정되어 있으며 런타임 오류가 발생하는 경우 SQL Server에서 전체 트랜잭션을 롤백하고 배치를 중단하도록 지시합니다.

* SSMS의 Azure SQL 데이터 웨어하우스 지원.

* SQL Server PowerShell 모듈에 대한 중요 업데이트. 여기에는 새 [SQL PowerShell 모듈, 상시 암호화, SQL 에이전트 및 SQL 오류 로그에 대한 새 CMDLET](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update)이 포함됩니다.

* 상시 암호화 마법사에서 PowerShell 스크립트 생성에 대한 지원.

* Azure SQL 데이터베이스에 연결 시간 향상.

* SQL Server 2016 데이터베이스 백업에 대한 Azure Storage 자격 증명 생성을 지원하기 위한 새 "URL에 백업" 대화 상자. 이 대화 상자는 Azure Storage 계정에 데이터베이스 백업을 저장하는 더욱 간소화된 환경을 경험을 제공합니다.
 
* Microsoft Azure 저장소 서비스에서 SQL Server 2016 데이터베이스 백업 복원을 간소화하는 새 복원 대화 상자.
 
* 사용자에게 SELECT 권한이 없는 경우 디자이너에 테이블을 추가할 수 있도록 SSMS 쿼리 디자이너의 버그 수정.

* 'TRY_CAST()' 및 'TRY_CONVERT()' 함수에 대한 IntelliSense 지원을 추가하는 버그 수정  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2453461](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast)

* ‘SQLAS’ Analysis Services 확장 로드를 사용하도록 설정하는 PowerShell 모듈의 버그 수정  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2544902](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension)

* SQL 파일의 끌어서 놓기 열기를 허용하는 SSMS 편집기 창의 버그 수정  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2690658](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios)

* 종료 시 프로파일러 충돌을 해결하는 프로파일러 버그 수정  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2616550](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped).  
[Microsoft Connect 항목 #2319968](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968)

* SSMS 테이블 디자이너에서 참가 링크를 편집하려고 할 때 충돌을 방지하기 위해 SSMS의 버그 수정  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2721052](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms)

* db_owner 역할 멤버에 대해 데이터베이스 스크립트 생성을 사용하도록 SSMS의 버그 수정  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2869241](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june)

* 서버가 오프라인으로 전환된 경우 쿼리 탭 닫기의 지연을 제거하도록 SSMS 편집기의 버그 수정  
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2656058](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline).

* SQL Server Express 데이터베이스의 백업 옵션을 설정하도록 버그 수정 
*연결된 고객 버그 요청:*  
[Microsoft Connect 항목 #2801910](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks).  
[Microsoft Connect 항목 #2874434](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance).

* 다차원 Analysis Services 모델의 데이터 피드 공급자를 올바르게 표시하도록 Analysis Services의 버그 수정.

----
## <a name="downloadssdtmediadownloadpng-ssms-june-2016httpgomicrosoftcomfwlinklinkid799832"></a>[SSMS 2016년 6월](http://go.microsoft.com/fwlink/?LinkID=799832) ![다운로드](../ssdt/media/download.png)
일반 공급 | 버전 번호: 13.0.15000.23

[중국어(중국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [중국어(대만)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

* SSMS는 2016년 6월 릴리스부터 일반 사용자에게 공급됩니다.

* 현재 문서에 더 잘 통합되고 정규식을 통한 검색을 허용하는 SSMS의 새로운 빠른 찾기 대화 상자 
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* 스크립트를 통해 무인 설치에 대한 설치 진행률 및 프로세스를 추적할 수 있도록 하는 SSMS 설치 관리자 기능 개선

* 도움말 문서를 올바르게 표시하기 위한 SSMS 상황에 맞는 F1 도움말의 버그 수정

* 스크롤 시 SSMS가 충돌을 일으키는 쿼리 데이터 저장소 '재발된 쿼리' 보기의 버그 수정

* Excel 2016에서 SQL Server Analysis Services로 연결할 수 있도록 하는 Excel Analysis Services OLEDB 커넥터의 버그 수정

* 동일한 모니터의 연결 대화 상자를 다중 모니터 시스템의 기본 SSMS 창으로 표시하기 위한 SSMS 연결 대화 상자의 버그 수정  
*연결된 고객 버그 요청:*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* Always Encrypted 환경의 버그 수정 Stretch 데이터베이스에 대해 Always Encrypted 메뉴 옵션이 사용 가능하도록 올바르게 설정되지 않는 버그가 수정되었습니다. 또한 SafeNet(Luna SA) HSM 공급자가 제대로 사용되지 않던 Always Encrypted 마법사의 버그도 수정되었습니다.


## <a name="additional-downloads"></a>추가 다운로드  
모든 SQL Server Management Studio 다운로드의 전체 목록은 [Microsoft 다운로드 센터](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending)를 검색하세요.  
  
최신 SQL Server Management Studio에 대해서는 [SQL Server Management Studio 다운로드&#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.  
