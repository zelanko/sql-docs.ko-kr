---
title: SQL Server Management Studio - 변경 로그(SSMS) | Microsoft 문서
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 49c01e3daf0561e5082bcba28373c574a65a4c7f
ms.sourcegitcommit: 3a8293b769b76c5e46efcb1b688bffe126d591b3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50226395"
---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
이 문서에서는 SSMS의 현재 버전과 이전 버전에 대한 업데이트, 향상 및 버그 수정에 대한 세부 정보를 제공합니다. [아래의 이전 SSMS 버전](#previous-ssms-releases)을 다운로드하세요.


## <a name="ssms-180-preview-4download-sql-server-management-studio-ssmsmd"></a>[SSMS 18.0(미리 보기 4)](download-sql-server-management-studio-ssms.md)

빌드 번호: 15.0.18040.0<br>
릴리스 날짜: 2018년 9월 24일

미리 보기 4는 SSMS 18.0의 첫 번째 공개 미리 보기입니다. SSMS의 GA(일반 공급) 버전이 필요하면 [SSMS 17.9를 다운로드하여 설치하세요](#ssms-179-latest-ga-release).

### <a name="whats-new"></a>새로운 기능

**일반 SSMS**

작아진 다운로드 크기:

- 번들의 현재 크기가 SSMS 17.x의 절반보다 작습니다(약 400MB). IS(Integration Services) 구성 요소가 다시 추가되면 크기가 증가하지만 전만큼 크지 않아야 합니다.

SSMS 18.x는 새로운 Visual Studio 2017 Shell(격리 모드)을 기준으로 합니다.

- 이는 최신 셸(Visual Studio 2017 15.6.4를 선택함)을 의미합니다. 이 새로운 셸은 SSMS와 Visual Studio 모두에 발생한 모든 접근성 수정 사항의 잠금을 해제합니다.

접근성 개선 사항:

- 모든 도구(SSMS, DTA 및 프로파일러)에서 접근성 문제를 해결하는 데 많은 작업이 있었습니다.

SSMS는 사용자 지정 폴더에 설치할 수 있습니다.

- 현재, 명령줄 설정에서만 사용할 수 있습니다. 이 추가 인수를 SSMS-Setup-ENU.exe에 전달하세요.

  `SSMSInstallRoot=C:\MySSMS18`

  기본적으로 SSMS의 새 설치 위치는 `%ProgramFiles(x86)%\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`입니다.
  
  > [!NOTE]
  > 이는 SSMS가 다중 인스턴스임을 의미하지는 않습니다.

SSMS는 더 이상 SQL 엔진과 구성 요소를 공유하지 않습니다.

- SQL 엔진과의 구성 요소 공유를 방지하기 위해 상당한 노력이 있었습니다. 이로 인해 SQL 또는 SSMS의 서비스 가능성 문제가 발생하여 다른 하나에 의해 설치된 파일을 덮어쓰기도 했습니다.

이제 SSMS를 사용하려면 NetFx 4.7.2 이상이 필요합니다.

- 최소 요구 사항을 NetFx4.6.1에서 NetFx4.7.2로 업그레이드했습니다. 이를 통해 새로운 프레임워크에서 제공하는 새로운 기능을 이용할 수 있습니다.

Windows 8에서는 SSMS가 지원되지 않습니다. Windows 10 / Windows Server 2016에서는 버전 1607(10.0.14393) 이상이 필요합니다.
  
- NetFx 4.7.2의 새로운 종속성으로 인해 SSMS 18.0은 Windows 8, 이전 버전의 Windows 10 및 Windows Server 2016에 설치되지 않습니다. SSMS 설치가 해당 운영 체제에서는 차단됩니다. Windows 8.1은 여전히 지원됩니다.

SSMS는 PATH 환경 변수에 추가되지 않습니다.

- SSMS.EXE(및 일반적인 도구)의 경로가 더 이상 경로에 추가되지 않습니다. 사용자는 직접 추가하거나 최신 Windows를 사용할 경우 시작 메뉴에 의존할 수 있습니다.

[!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)]에 대한 지원

- 다음은 [!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)](compatLevel 150 등...)를 ‘완전히’ 인식하는 첫 번째 SSMS 릴리스입니다.
- [!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)]의 “BATCH_STARTED_GROUP” 및 “BATCH_COMPLETED_GROUP”과 SSMS의 SQL Database Managed Instance를 지원합니다.
- GraphDB: Graph TC Sequence 실행 계획에서 플래그를 추가합니다.
- Always Encrypted: [보안 enclave를 사용한 상시 암호화](../relational-databases/security/encryption/always-encrypted-enclaves.md) 지원을 추가했습니다.
  - 사용자가 “옵션” 단추를 클릭하여 enclave 지원을 사용할 수 있도록 설정하고 구성할 때 연결 대화 상자에는 새로운 “Always Encrypted” 탭이 있습니다.

패키지 ID는 SSMS 확장을 개발하는 데 더 이상 필요하지 않습니다.

- SSMS가 잘 알려진 패키지만 선택적으로 로드하여 개발자는 자신의 패키지를 등록해야 했습니다. 더 이상 그렇지 않습니다.

더 나은 Azure SQL 지원:

- 이제 SLO/Edition/MaxSize 데이터베이스 속성이 사용자 지정 이름을 허용하므로 더 쉽게 Azure SQL Database의 향후 버전을 지원할 수 있습니다.
- vCore SKU(범용 및 중요 비즈니스용)의 Gen4_24 및 모든 Gen5를 추가로 지원합니다.

SMO:

- 다시 시작 가능한 인덱스 생성을 위한 SMO 지원을 확장합니다.
- SMO 개체에서 새 이벤트(“PropertyMissing”)를 추가하여 응용 프로그램 작성자가 SMO 성능 문제를 더 빨리 감지할 수 있도록 했습니다.
- “백업 체크섬 기본값” 서버 구성에 매핑되는 구성 개체에 대한 새로운 *DefaultBackupChecksum* 속성을 공개했습니다.

SSMS:

- SSMS의 파일 그룹에 대한 AUTOGROW_ALL_FILES 구성 옵션 공개
- 문제가 발생할 수 있는 ‘경량 풀링’ 및 ‘우선 순위 높임’ 옵션이 SSMS GUI에서 제거되었습니다(https://blogs.msdn.microsoft.com/arvindsh/2010/01/26/priority-boost-details-and-why-its-not-recommended).
- SQL 편집기는 **Ctrl+D** 바로 가기를 사용하여 행을 복제합니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/32896594).
- 파일을 생성하는 새 메뉴 및 키 바인딩: **Ctrl+Alt+N**. **Ctrl+N**을 사용하면 새 쿼리가 계속 만들어집니다.
- 이제 사용자는 규칙 이름 하나를 자동으로 생성하는 대신 **새 방화벽 규칙** 대화 상자에서 규칙 이름을 지정할 수 있습니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/32902039).
- 데이터 분류: 권장 사항을 업데이트했습니다.
- 특별히 v140 T-SQL을 위해 편집기에서 IntelliSense를 개선했습니다.
- 모든 계층 1 언어에 대한 지원
- 데이터 정렬 대화 상자에서 UTF-8용 SSMS UI에 지원을 추가했습니다.
- 연결 대화 상자 MRU 암호를 위해 “Windows 자격 증명 관리자”로 전환했습니다. 따라서 암호의 지속성을 항상 신뢰할 수 없다는 오랫동안 미해결 상태인 문제가 해결됩니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/32896486).
- 높은 DPI에 대한 지원이 기본적으로 사용됩니다.
- 예상 모니터에서 더 많은 대화 상자와 창이 표시되도록 하여 다중 모니터 시스템을 더욱 강력하게 지원합니다.
- 서버 속성 대화 상자의 새 데이터베이스 설정 페이지에서 ‘백업 체크섬 기본값’ 서버 구성을 제공했습니다. (https://feedback.azure.com/forums/908035-sql-server/suggestions/34634974).


SSMS / 실행 계획:

- 실행 계획 연산자 노드 아래에 실제 경과 시간, 실제 대 예상 행 수를 추가했습니다(사용할 수 있는 경우). 이로 인해 실제 계획의 모습이 활성 쿼리 통계 계획과 일치하게 됩니다.
- 실행 계획에 대한 쿼리 편집 단추를 클릭하면, 쿼리가 4000자를 넘을 경우 SQL 엔진이 실행 계획을 자를 수 있음을 사용자에게 표시하도록 도구 설명을 수정하고 주석을 추가했습니다.
- “Materializer Operator(외부 Select)”를 표시하는 논리를 추가했습니다.
- “batch-mode scan on rowstores” 기능을 사용하는 쿼리를 쉽게 식별할 수 있도록 새로운 실행 계획 특성 BatchModeOnRowStoreUsed를 추가합니다. 쿼리가 batch-mode scan on rowstores를 수행할 때마다 새 특성(BatchModeOnRowStoreUsed="true")이 StmtSimple 요소에 추가됩니다.

Always On:

- SSMS Always on 대시보드에서 RTO(예상 복구 시간) 및 RPO(예상 데이터 손실)를 새로 고칩니다. 자세한 내용은 [Always On 가용성 그룹에 대한 성능 모니터링](../database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups.md)을 참조하세요.

감사 파일:

- Azure AD 기반 인증을 기반으로 저장소 계정 키에서 인증 방법을 변경했습니다.

항상 암호화:

- 항상 데이터베이스 연결을 위해 이제 Always Encrypted를 사용하거나 사용하지 않도록 설정하는 쉬운 방법을 제공하는 *Always Encrypted 사용* 확인란(‘서버에 연결’ 대화 상자에 있음)이 있는 Always Encrypted 탭을 추가했습니다.
- 보안 enclave를 사용하는 Always Encrypted를 지원하기 위해 몇 가지를 개선했습니다.
  - 서버에 연결 대화 상자에서 enclave 증명 URL을 지정하기 위한 텍스트 필드(새로운 Always Encrypted 탭).
  - 새 열 마스터 키가 enclave 계산을 허용하는지 여부를 제어하는 새 열 마스터 키 대화 상자의 새로운 확인란.
  - 기타 Always Encrypted 키 관리 대화 상자에는 enclave 계산을 허용하는 열 마스터 키에 대한 정보를 제공합니다.
  - 자세한 내용은 [보안 Enclave를 사용한 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)를 참조하세요.

        
### <a name="bug-fixes"></a>버그 수정

작동 중단/반응이 없음:

- GDI 개체와 관련된 일반적인 SSMS 작동 중단을 수정했습니다.
- “Script as Create/Update/Drop”(작성/업데이트/삭제로 스크립트)를 선택할 때 반응이 없거나 성능이 저하되는 공통 소스를 수정했습니다(SMO 개체의 불필요한 페치를 제거함).
- ADAL 추적을 사용하는 동안 MFA를 사용하여 Azure SQL DB에 연결할 때 반응이 없는 문제를 해결했습니다.
- 작업 모니터에서 호출하면 활성 쿼리 통계에서 반응이 없는(또는 인지된 반응 없음) 문제(“보안 정보 유지”가 설정되지 않은 SQL Server 인증을 사용할 때 발생하는 문제)를 해결했습니다.
- 개체 탐색기에서 “보고서”를 선택할 때 반응이 없는 문제(리소스 연결 대기 시간이 길거나 일시적으로 리소스에 액세스할 수 없으면 발생하는 문제)를 해결했습니다.

연결 대화 상자:

- DEL 키를 눌러 이전 사용자 이름 목록에서 사용자 이름을 제거할 수 있도록 했습니다(https://feedback.azure.com/forums/908035/suggestions/32897632).

XEvent:

- 작업 ID 및 클래스 유형 필드를 읽기 가능한 문자열로 표시하는 두 개의 열, 즉 “action_name” 및 “class_type_desc” 열을 추가했습니다.
- 이벤트 1,000,000개라는 이벤트 XEvent 뷰어 상한을 제거했습니다.

외부 테이블:

- 템플릿, SMO, IntelliSense 및 속성 표에 있는 `Rejected_Row_Location`에 대한 지원을 추가했습니다.

SSMS 옵션:

- **도구 > 옵션 > SQL Server 개체 탐색기 > 명령** 페이지의 크기가 제대로 조정되지 않는 문제를 해결했습니다.


SSMS 편집기:

- 기본 색상을 복원하면 색상이 기본 녹색이 아니라 라임 녹색으로 변경되어 흰색 배경에서 읽기가 매우 어려워지던 “SQL 시스템 테이블”의 문제를 해결했습니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/32896906).
- AAD 인증을 사용하여 Azure SQL DW에 연결할 때 intellisense가 작동하지 않는 문제를 해결했습니다.
- 사용자에게 마스터 액세스 권한이 없는 경우 Azure의 IntelliSense에 발생하는 문제를 해결했습니다.
- 대상 데이터베이스의 데이터 정렬이 대/소문자를 구분할 때 중단된 “임시 테이블”을 작성하는 코드 조각을 수정했습니다.

개체 탐색기:

- SSMS가 OE(잘못 구성된 DataCollector)에서 “관리” 노드를 확장하려고 할 때 “DBNull에서 다른 형식으로 개체를 캐스트할 수 없음” 예외를 throw하는 문제를 해결했습니다.
- 노드 이름을 바꿀 때 DEL 키가 작동하지 않는 문제를 해결했습니다(https://feedback.azure.com/forums/908035/suggestions/32910247 및 기타 중복 항목).
- “상위 N 편집...”을 호출하기 전에는 OE가 따옴표를 이스케이프 처리하지 않아 디자이너가 혼동하게 되는 문제를 해결했습니다.
- “데이터 계층 응용 프로그램 가져오기” 마법사가 Azure Storage 트리에서 시작되지 않던 문제를 해결했습니다.
- SSL 확인란의 상태가 지속되지 않은 “데이터베이스 메일 구성”의 문제를 해결했습니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541).
- SSMS가 is_auto_update_stats_async_on으로 데이터베이스를 복원하려고 할 때 기존 연결을 닫는 옵션을 회색으로 표시하는 문제를 해결했습니다.
- OE에서 노드(예: “테이블”)를 마우스 오른쪽 단추로 클릭하고 **필터 > 필터 설정**으로 이동하여 필터링 테이블과 같은 작업을 수행하려고 하면 현재 SSMS가 활성 상태가 아닌 다른 화면에 필터가 표시될 수 있는 문제를 해결했습니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106).
- 개체의 이름을 바꾸려고 할 때 개체 탐색기에서 Delete 키가 작동하지 않는 오랫동안 미해결 상태였던 문제를 해결했습니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/33073510).
- 기존 데이터베이스 파일의 속성을 표시할 때 새 데이터베이스를 생성할 때 표시되는 “처음 크기(MB)” 대신 “크기(MB)” 열 아래에 크기가 나타납니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/32629024).
- “그래프 테이블”의 “디자인” 상황에 맞는 메뉴 항목을 사용하지 않도록 설정했습니다. 현재 버전의 SSMS에서 이러한 유형의 테이블을 지원하지 않기 때문입니다.

        
도움말 뷰어:

- 온라인/오프라인 모드를 사용하는 논리를 개선했습니다.
- 온라인/오프라인 설정을 사용하기 위한 “도움말 보기”를 수정했습니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791).
    
개체 스크립팅:

- 전체 성능 개선 사항 - WideWorldImporters 스크립트 생성 시간은 SSMS 17.7과 비교하여 반 정도 소요됩니다.
- 개체를 스크립팅할 때 기본값이 있는 DB 범위 지정 구성이 생략됩니다.
- 스크립팅 시 동적 T-SQL을 생성하지 마세요(https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391).
- SQL Server 2016 및 그 이전 버전에서 테이블을 스크립팅할 때 그래프 구문 “as edge” 및 “as node”를 생략하세요.


테이블 디자이너:

- “200행 편집”의 작동 중단 문제를 수정했습니다.
- Azure SQL Database에 연결되면 디자이너가 테이블을 추가할 수 있는 문제를 해결했습니다.

SMO:

- SMO/ServerConnection이 SqlCredential 기반 연결을 올바로 처리하지 않는 문제를 해결했습니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941).

AS:

- AS Xevent UI에 대한 “고급 설정”이 잘리는 문제를 해결했습니다.

플랫 파일 가져오기 마법사:

- “플랫 파일 가져오기 마법사”에서 큰따옴표를 올바로 처리(이스케이프)하지 않는 문제를 해결했습니다.
- 부동 소수점 유형의 잘못된 처리(부동 소수점에 다른 구분 기호를 사용하는 로케일에서)와 관련된 문제를 해결했습니다.
- 값이 0 또는 1인 경우 비트를 가져오는 것과 관련된 문제를 해결했습니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535).
- 부동이 Null로 입력되는 문제를 해결했습니다.
        
데이터 분류:

- 데이터 분류의 권장 부분이 새 설치에 작동하지 않는 설정 문제를 해결했습니다.

DB 백업/복원/연결/분리:

- .mdf 파일의 실제 파일 이름이 원래 파일 이름과 일치하지 않을 때 사용자가 데이터베이스를 연결할 수 없는 문제를 해결했습니다.
- SSMS가 유효한 복원 계획을 찾지 못하거나 최적이 아닌 계획을 찾을 수 있는 문제를 해결했습니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752).
- URL 백업을 복원하려 할 때 발생하는 SSMS의 작동 중단 문제를 해결했습니다.

작업 활동 모니터:

- 작업 활동 모니터(필터 포함)를 사용하는 동안 발생하는 작업 중단 문제를 해결했습니다.
        
SSMS에서 관리되는 인스턴스 지원:

- 관리되는 인스턴스 지원을 개선했습니다. UI에서 지원되지 않는 옵션을 사용할 수 없도록 설정하고 URL 감사 대상을 처리하도록 [감사 로그 보기] 옵션을 수정했습니다.
- “스크립트 생성 및 게시” 마법사는 지원되지 않는 CREATE DATABASE 절을 스크립팅합니다.
- CL 인스턴스에 대해 실시간 쿼리 통계를 사용하지 않도록 설정했습니다.
- 데이터베이스 속성->파일이 ALTER DB ADD FILE을 잘못 스크립팅했습니다.
- 일부 다른 일정 유형을 선택한 경우에도 ONIDLE 일정 예약이 선택되는 SQL Agent 스케줄러의 재발 문제를 해결했습니다.
- Azure Storage에서 백업을 수행하기 위해 MAXTRANSFERRATE, MAXBLOCKSIZE를 조정하는 중입니다.
- RESTORE 작업(CL에서 지원되지 않음) 전에 비상 로그 백업이 스크립팅되는 문제.
- 데이터베이스 만들기 마법사가 CREATE DATABASE 문을 올바로 스크립팅하지 않습니다.
- 관리되는 인스턴스에 연결된 상태에서 “활동 모니터”를 사용하려 할 때 오류가 표시되는 문제를 해결했습니다.


Azure SQL Database:

- 마스터 대신 Azure SQL DB에서 사용자 데이터베이스에 연결했을 때 Azure SQL Db 쿼리 창에 대해 데이터베이스 목록이 올바로 채워지지 않는 문제를 해결했습니다.
- Azure SQL Database에 “임시 테이블”을 추가할 수 없는 문제를 해결했습니다.


일반적인 Azure SQL 지원:

- 일반적인 Azure UI 컨트롤에서 사용자가 Azure 구독(50개가 넘는 경우)을 표시하지 못하는 문제를 해결했습니다. 또한 정렬 기준이 구독 ID가 아니라 이름으로 변경되었습니다. 예를 들어, URL에서 백업을 복원하려 할 때 이 문제가 발생할 수 있습니다.
- 사용자의 일부 테넌트에 구독이 없는 경우 “인덱스가 범위를 벗어났습니다. 인덱스는 음수가 아니어야 하며 컬렉션의 크기보다 작아야 합니다”라는 오류를 발생시킬 수 있는 구독을 열거할 때 일반적인 Azure UI 컨트롤에 있는 문제를 해결했습니다. 예를 들어, URL에서 백업을 복원하려 할 때 이 문제가 발생할 수 있습니다.

결과 표:

- 선택한 행 번호가 고대비 모드에서 표시되지 않는 문제를 해결했습니다.

XEvent 프로파일러:

- 96-코어 SQL Server에 연결할 때 XEvent 프로파일러가 실행되지 않는 문제를 해결했습니다.


### <a name="deprecated-features"></a>사용되지 않는 기능

SSMS에서는 다음 기능을 더 이상 사용할 수 없습니다.

- T-SQL 디버거
- 데이터베이스 다이어그램
- OSQL.EXE
- Dreplay 관리 UI
- 구성 관리자 도구:
  - SQL Server 구성 관리자 및 Reporting Server 구성 관리자가 모두 더 이상 SSMS 설정의 일부가 아닙니다.

- DMF 표준 정책
  - 정책이 더 이상 SSMS와 함께 설치되지 않으며 Git으로 이동하게 됩니다. 필요한 경우 참여하고 다운로드/설치할 수 있습니다.

- SSMS 명령줄 옵션 -P가 제거됨
  - 보안상의 이유로 명령줄에서 일반 텍스트 암호를 지정하는 옵션이 제거되었습니다.

- [스크립트 생성] | [웹 서비스에 게시]가 제거되었습니다. 이 기능(더 이상 사용되지 않음)은 SSMS UI에서 제거되었습니다.

- 개체 탐색기에서 “유지 관리 | 레거시” 노드를 제거했습니다. [스크립트 생성 및 게시]에서 [웹 서비스에 게시] 옵션이 제거되었습니다. ‘매우 오래된’ “데이터베이스 유지 관리 계획” 및 “SQL 메일” 노드에 더 이상 액세스할 수 없습니다. 최신 “데이터베이스 메일” 및 “유지 관리 계획” 노드는 계속해서 정상적으로 작동합니다.

### <a name="known-issues"></a>알려진 문제

다음은 현재 릴리스에서 알려진 문제입니다.

> [!IMPORTANT]
> SQL 쿼리 편집기에서 ‘Active Directory - MFA 지원을 통한 유니버설’ 인증을 사용하는 경우 쿼리를 호출할 때마다 연결이 닫혔다가 다시 열릴 수 있습니다. 이러한 연결 끊김으로 인해 전역 임시 테이블이 예기치 않게 삭제되고, 연결에 새 SPID가 부여되는 것과 같은 부작용이 발생합니다. 이러한 연결 끊김은 연결에 열려 있는 트랜잭션이 있을 때는 발생하지 않습니다. 이 문제를 해결하기 위해 연결 매개 변수에서 `persist security info=true`를 설정할 수 있습니다.

SSMS

- .sql 파일을 두 번 클릭하면 SSMS가 실행되지만 실제 스크립트는 열리지 않습니다.
  - 해결 방법: .sql 파일을 SSMS 편집기로 끌어다 놓습니다.

SSIS

- 이전 버전의 SQL Server를 대상으로 하고 스크립트 작업/스크립트 구성 요소를 동시에 포함하는 패키지는 배포하거나 실행할 수 없습니다.
- SSMS에서 원격 Integration Services에 연결할 수 없습니다.

## <a name="ssms-179-latest-ga-release"></a>SSMS 17.9(최신 GA 릴리스)

![다운로드](../ssdt/media/download.png)[SSMS 17.9](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x409)

빌드 번호: 14.0.17285.0<br>
릴리스 날짜: 2018년 9월 4일

> [!NOTE]
> 영어 이외의 지역화된 SSMS 17.x 릴리스는 Windows 8, Windows 7, Windows Server 2012 및 Windows Server 2008 R2에 설치하는 경우 [KB 2862966 보안 업데이트 패키지](https://support.microsoft.com/en-us/kb/2862966) 가 필요합니다.

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x40a)


### <a name="whats-new"></a>새로운 기능

**일반 SSMS**


실행 계획:

- 이제 그래픽 실행 계획은 특정 계획에 대해 기능이 활성화되면 새로운 행 모드 메모리 부여 피드백 특성을 보여 줍니다. IsMemoryGrantFeedbackAdjusted 및 LastRequestedMemory가 MemoryGrantInfo 쿼리 계획 XML 요소에 추가됩니다. 행 모드 메모리 부여 피드백에 대한 자세한 내용은 [SQL 데이터베이스의 적응 쿼리 처리](https://docs.microsoft.com/sql/relational-databases/performance/adaptive-query-processing)를 참조하세요.

Azure SQL: 

- Azure DB 생성에서 vCore SKU에 대한 지원이 추가되었습니다. 자세한 내용은 [vCore 기반 구매 모델](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers#vcore-based-purchasing-model)을 참조하세요.
 

### <a name="bug-fixes"></a>버그 수정

**일반 SSMS**
    
복제 모니터:

- 복제 모니터(SqlMonitor.exe)가 시작되지 않도록 만드는 문제를 해결함(사용자 의견 항목: https://feedback.azure.com/forums/908035-sql-server/suggestions/34791079) 

플랫 파일 가져오기 마법사: 

- “플랫 파일 마법사” 대화 상자의 도움말 페이지에 대한 링크를 수정함 
- 테이블이 이미 있는 경우 마법사에서 대상 테이블 변경을 허용하지 않는 문제를 해결했습니다. 사용자는 마법사를 종료하지 않고 다시 시도하고 실패한 테이블을 삭제하고 마법사에 정보를 다시 입력할 수 있습니다(사용자 의견 항목: https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186). 

데이터 계층 응용 프로그램 가져오기/내보내기:

- 파티션이 정의된 테이블과 인덱스가 없는 테이블을 처리할 때 “오류 SQL72014: .Net SqlClient 데이터 공급자: Msg 9108, 수준 16, 상태 10, 줄 1 이러한 유형의 통계는 증분 통계가 될 수 없습니다.” 같은 메시지와 함께 .bacpac 가져오기를 실패하게 만드는 문제(DacFx에서)를 해결했습니다.

IntelliSense:

- MFA와 함께 AAD를 사용할 때 IntelliSense 완료가 작동되지 않는 문제를 해결했습니다. 

개체 탐색기: 

- SSMS가 실행되는 모니터 대신 임의의 모니터에 “필터 대화 상자”가 표시되는 문제를 해결했습니다(다중 모니터 시스템).

Azure SQL: 

- 특정 데이터베이스에 연결될 때 드롭다운에 “마스터”가 표시되지 않는, “사용 가능한 데이터베이스”에서 데이터베이스 열거형과 관련된 문제를 해결했습니다. 
- MFA와 함께 AAD를 사용하여 스크립트(“데이터” 또는 “스키마 및 데이터”)를 생성하려고 하면 실패하고 SQL Azure DB에 연결할 수 없는 문제를 해결했습니다. 
- SQL Azure DB에 연결되어 있을 때 UI에서 “테이블 추가”를 선택할 수 없는 뷰 디자이너(뷰) 문제를 해결했습니다. 
- MFA 토큰 갱신 중 SSMS 쿼리 편집기가 자동으로 연결을 닫았다가 다시 여는 문제를 해결했습니다. 이는 트랜잭션을 종료하고 다시 열지 않는 것처럼 사용자가 모르는 사이에 부작용이 발생하는 것을 방지합니다. 이러한 변경으로 인해 속성 창에 토큰 만료 시간이 추가됩니다. 
- SSMS가 MFA 로그인을 사용하는 AAD에 대해 가져온 MSA 계정에 대한 암호를 묻지 않는 문제를 해결했습니다. 

작업 모니터: 

- 작업 모니터에서 시작되고 SQL 인증이 사용되면 “활성 쿼리 통계”가 중단하는 문제를 해결했습니다. 

Microsoft Azure 통합: 

- SSMS에서 처음 50개 구독만 표시하는 문제를 해결했습니다(Always Encrypted 대화 상자, URL에서 백업/복원 대화 상자 등). 
- URL에서 백업/복원 대화 상자에서 저장소 계정이 없는 Microsoft Azure 계정에 로그인하려고 하면 SSMS에서 예외("인덱스가 범위를 벗어났습니다.")를 throw하는 문제를 해결했습니다. 

개체 스크립팅: 

- “Drop 및 Create”를 스크립팅할 때 SSMS에서 이제 동적 T-SQL 생성을 방지합니다.
- 데이터베이스 개체를 스크립팅할 때 이제 SSMS에서 데이터베이스 범위 구성이 기본값으로 설정된 경우 이를 설정하기 위해 스크립트를 생성하지 않습니다.

Help:

- “도움말에 대한 도움말”이 온라인/오프라인 모드를 적용하지 않는 오랫동안 해결하지 못했던 문제를 해결했습니다.
- “도움말 | Community Projects and Samples(커뮤니티 프로젝트 및 샘플)”을 클릭하면 이제 SSMS에서 Git 페이지로 안내하는 기본 브라우저를 열고 이전 브라우저 사용으로 인한 오류/경고를 표시하지 않습니다.

### <a name="known-issues"></a>알려진 문제


> [!IMPORTANT]
> SQL 쿼리 편집기에서 ‘Active Directory - MFA 지원을 통한 유니버설’ 인증을 사용하는 경우 쿼리를 호출할 때마다 연결이 닫혔다가 다시 열릴 수 있습니다. 이러한 연결 끊김으로 인해 전역 임시 테이블이 예기치 않게 삭제되고, 연결에 새 SPID가 부여되는 것과 같은 부작용이 발생합니다. 이러한 연결 끊김은 연결에 열려 있는 트랜잭션이 있을 때는 발생하지 않습니다. 이 문제를 해결하기 위해 연결 매개 변수에서 `persist security info=true`를 설정할 수 있습니다.




## <a name="previous-ssms-releases"></a>이전 SSMS 릴리스

다음 섹션의 제목 링크를 클릭하여 이전 SSMS 버전을 다운로드하세요.

## <a name="downloadssdtmediadownloadpng-ssms-1781httpsgomicrosoftcomfwlinklinkid875802"></a>![](../ssdt/media/download.png)[SSMS 17.8.1 다운로드](https://go.microsoft.com/fwlink/?linkid=875802)
‘17.8에서 SQL 데이터베이스 프로비전과 관련된 버그가 발견되었으므로 SSMS는17.8.1이 17.8로 대체됩니다.’

빌드 번호: 14.0.17277.0<br>
릴리스 날짜: 2018년 6월 26일

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x40a)


### <a name="whats-new"></a>새로운 기능

**일반 SSMS**

데이터베이스 속성:

- 이 향상된 기능은 파일 그룹의 **AUTOGROW_ALL_FILES** 구성 옵션을 공개합니다. 이 새 구성 옵션은 사용 가능한 각 파일 그룹(파일 스트림 및 메모리 최적화 파일 그룹 제외) 확인란의 새 열(모든 파일 자동 증가) 형식으로 [데이터베이스 속성] > [파일 그룹] 창 아래에 추가됩니다. 사용자는 해당 Autogrow_All_Files 확인란을 토글하여 특정 파일 그룹의 AUTOGROW_ALL_FILES를 사용/사용 안 함으로 설정할 수 있습니다. 이렇게 하면 CREATE용 데이터베이스를 스크립팅/데이터베이스용 스크립트를 생성(SQL2016 이상)할 때 **AUTOGROW_ALL_FILES** 옵션이 제대로 스크립팅됩니다.
    
SQL 편집기:

- 사용자에게 마스터 액세스 권한이 없는 경우 Azure SQL Database에서 Intellisense 관련 환경이 향상되었습니다.

스크립팅:

- 특히 대기 시간이 긴 연결에 대한 일반적인 성능 향상입니다.
    
**AS(Analysis Services)**

- Analysis Services 클라이언트 라이브러리 및 데이터 공급자가 최신 버전으로 업데이트되어, 새로운 Azure Government AAD 기관에 대한 지원이 추가되었습니다(login.microsoftonline.us).



### <a name="bug-fixes"></a>버그 수정

**일반 SSMS**
    
유지 관리 계획:

- SQL 인증으로 유지 관리 계획을 편집할 때 SQL 인증을 사용하면 “운영자에게 알림 태스크”가 작동하지 않는 문제를 해결했습니다.
    
스크립팅:

- SMO의 후처리 작업으로 인해 리소스가 고갈되고 SQL 로그인에 실패하는 문제를 해결했습니다.
    
SMO:

- 기본 제약 조건이 있는 열을 추가하고 테이블에 이미 데이터가 있는 경우 Table.Alter()가 실패하는 문제를 해결했습니다. 자세한 내용은 [sql server smo generating inline default constraint when adding a column to a table containing data](https://feedback.azure.com/forums/908035-sql-server/suggestions/32895625)(데이터가 있는 테이블에 열을 추가할 때 인라인 기본 제약 조건을 생성하는 SQL Server SMO)를 참조하세요.
    
항상 암호화:

- 분할된 테이블에서 Always Encrypted를 사용할 때 잠금 시간 제한 오류를 유발하는 문제를 해결했습니다(DacFx).
    

**AS(Analysis Services)**

- 테이블 형식 Analysis Services 1400 수준 호환성 모델에서 OAuth 데이터 원본을 수정할 때 발생한, OAuth 토큰의 변경 내용이 데이터 원본에서 업데이트되지 않는 문제를 해결했습니다.
- 일부 잘못된 데이터 원본 자격 증명을 사용하거나 Analysis Services 테이블 형식 1400 수준 호환성 모델에서 파워 쿼리(예: Oracle)의 데이터 원본 마이그레이션을 지원하지 않는 데이터 원본을 편집할 때 발생할 수 있는 SSMS의 크래시를 수정했습니다.


### <a name="known-issues"></a>알려진 문제

- ‘속성’ 창에서 파일 그룹 속성을 수정한 후 ‘스크립트’ 단추를 클릭하면 두 개의 스크립트(각각 *USE <database>* 문 및 *USE master* 문을 사용한 스크립트)가 생성됩니다.  *USE master*를 사용한 스크립트는 오류로 생성되므로 무시해야 합니다. *USE<database>* 문을 포함하는 스크립트를 실행합니다.
- 새로운 *범용* 또는 *중요 비즈니스용* Azure SQL Database 버전으로 작업할 때 일부 대화 상자에서 잘못된 버전이라는 오류가 표시됩니다.
- XEvents 뷰어에서 약간의 대기 시간이 발생할 수 있습니다. [.NET Framework의 알려진 문제](https://github.com/Microsoft/dotnet/blob/master/releases/net472/dotnet472-changes.md#sql)입니다. NetFx 4.7.2로 업그레이드해보세요.




## <a name="downloadssdtmediadownloadpng-ssms-177httpsgomicrosoftcomfwlinklinkid873126"></a>[SSMS 17.7](https://go.microsoft.com/fwlink/?linkid=873126) ![다운로드](../ssdt/media/download.png)

빌드 번호: 14.0.17254.0<br>
릴리스 날짜: 2018년 5월 9일

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x40a)


### <a name="whats-new"></a>새로운 기능

**일반 SSMS**

복제 모니터:   
- 복제 모니터는 이제 게시자 데이터베이스 및/또는 배포자 데이터베이스가 가용성 그룹의 일부인 시나리오에서 수신기 등록을 지원합니다. 이제 게시자 데이터베이스 및/또는 배포자 데이터베이스가 Always On의 일부인 복제 환경을 모니터링할 수 있습니다. 
 
Azure SQL Data Warehouse: 
- Azure SQL Data Warehouse에서 외부 테이블에 대한 거부된 행 위치 지원을 추가합니다. 

**IS(Integration Services)**

- Azure SQL Database에 배포할 SSIS 패키지에 대한 예약 기능을 추가했습니다. 고급 작업 스케줄러인 SQL Server 에이전트가 있는 SQL Server 온-프레미스 및 SQL Database Managed Instance와 달리 SQL Database에는 기본 제공 스케줄러가 없습니다. 이 새로운 SSMS 기능은 SQL Database에 배포된 패키지를 예약하는 데 사용되는 SQL Server 에이전트가 유사한 기능을 제공하는 친숙한 사용자 인터페이스를 제공 합니다. SQL Database를 사용하여 SSIS 카탈로그 데이터베이스인 SSISDB를 호스팅하는 경우 이 SSMS 기능을 사용하여 SSIS 패키지를 예약하는 데 필요한 데이터 팩터리 파이프라인, 활동 및 트리거를 생성할 수 있습니다. 그런 다음, 데이터 팩터리에서 이러한 개체를 편집하고 확장할 수 있습니다. 자세한 내용은 [SSMS를 지원하는 Azure SQL Database에서 SSIS 패키지 실행 예약](../integration-services/lift-shift/ssis-azure-schedule-packages-ssms.md)을 참조하세요. Azure Data Factory 파이프라인, 활동 및 트리거에 대한 자세한 내용은 [Azure Data Factory의 파이프라인 및 활동](https://docs.microsoft.com/azure/data-factory/concepts-pipelines-activities) 및 [Azure Data Factory에서 파이프라인 실행 및 트리거](https://docs.microsoft.com/azure/data-factory/concepts-pipeline-execution-triggers)를 참조하세요.
- SQL 관리되는 인스턴스의 SQL 에이전트에서 SSIS 패키지 예약 지원. 이제 관리되는 인스턴스에서 SSIS 패키지를 실행하는 SQL 에이전트 작업을 만들 수 있습니다. 

### <a name="bug-fixes"></a>버그 수정

**일반 SSMS** 

유지 관리 계획:   
- 기존 유지 관리 계획의 일정을 변경하려고 하면 예외가 throw되는 문제가 해결되었습니다. 자세한 내용은 [유지 관리 계획에서 일정을 클릭하면 SSMS 17.6이 충돌함](https://feedback.azure.com/forums/908035-sql-server/suggestions/33712924)을 참조하세요.

Always On: 
- SQL Server 2012에서 Always On 대기 시간 대시보드가 작동하지 않는 문제가 해결되었습니다.
 
스크립팅: 
- 관리자가 아닌 사용자의 경우 Azure SQL Data Warehouse에 대한 저장 프로시저 스크립팅이 작동하지 않는 문제가 해결되었습니다.
- Azure SQL Database에 대한 데이터베이스 스크립팅이 *SCOPED CONFIGURATION* 속성을 스크립팅하지 않는 문제가 해결되었습니다.
 
원격 분석: 
- 원격 분석 전송을 옵트아웃한 후 서버에 연결하려고 하면 SSMS가 충돌하는 문제가 해결되었습니다.
 
Azure SQL Database: 
- 사용자가 호환성 수준을 설정하거나 변경할 수 없는 문제가 해결되었습니다(비어 있는 드롭다운). 참고: 호환성 수준을 150으로 설정하려는 사용자는 여전히 *스크립트* 단추를 사용하여 스크립트를 수동으로 편집해야 합니다. 
 
SMO: 
- SMO의 오류 로그 크기 설정이 공개되었습니다. 자세한 내용은 [SQL Server 오류 로그의 최대 크기 설정](https://feedback.azure.com/forums/908035-sql-server/suggestions/33624115)을 참조하세요.  
- Linux의 SMO에서 라인피드 스크립팅이 수정되었습니다.
- 거의 사용되지 않는 속성을 검색할 때의 기타 성능 개선.  

IntelliSense: 
- 성능 개선: IntelliSense의 열 데이터 쿼리 양이 축소되었습니다. 이는 상당히 많은 열이 있는 테이블에 대해 작업할 때 특히 유용합니다. 

SSMS 사용자 설정:
- 옵션 페이지의 크기가 제대로 조정되지 않는 문제가 해결되었습니다.

기타:  
- *통계 세부 정보* 페이지에 텍스트가 표시되는 방식이 개선되었습니다. 

**IS(Integration Services)**

- Azure SQL Database Managed Instance에 대한 지원이 향상되었습니다.
- 사용자가 SQL Server 2014 이하에 대한 카탈로그를 만들지 못하는 문제가 해결되었습니다.
- 보고서와 관련된 두 가지 문제가 해결되었습니다.
   - Azure 서버의 컴퓨터 이름이 제거되었습니다.
   - 지역화된 개체 이름의 처리가 개선되었습니다.


### <a name="known-issues"></a>알려진 문제

새로운 *범용* 또는 *중요 비즈니스용* Azure SQL Database 버전으로 작업할 때 일부 대화 상자에서 잘못된 버전이라는 오류가 표시됩니다.

## <a name="downloadssdtmediadownloadpng-ssms-176httpsgomicrosoftcomfwlinklinkid870039"></a>![다운로드](../ssdt/media/download.png) [SSMS 17.6](https://go.microsoft.com/fwlink/?linkid=870039)

빌드 번호: 14.0.17230.0<br>
릴리스 날짜: 2018년 3월 20일

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x40a)

### <a name="whats-new"></a>새로운 기능

**일반 SSMS**

SQL Database Managed Instance:

- [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에 대한 지원을 추가했습니다. Azure SQL Database Managed Instance는 SQL Server 온-프레미스로 100%에 가까운 호환성, 일반적인 보안 문제를 해결하는 네이티브 [VNet(가상 네트워크)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) 구현 및 온-프레미스 SQL Server 고객에 대한 편리한 [비즈니스 모델](https://azure.microsoft.com/pricing/details/sql-database/)을 제공합니다.
- 다음과 같은 일반적인 관리 시나리오에 대한 지원:
   - 데이터베이스 만들기 및 변경
   - 데이터베이스 백업 및 복원
   - 데이터 계층 응용 프로그램 가져오기, 내보내기, 추출 및 게시
   - 서버 속성 보기 및 변경
   - 전체 개체 탐색기 지원
   - 데이터베이스 개체 스크립팅
   - SQL 에이전트 작업에 대한 지원
   - 연결된 서버에 대한 지원
- [여기에서](https://azure.microsoft.com/blog/migrate-your-databases-to-a-fully-managed-service-with-azure-sql-database-managed-instance/) 관리되는 인스턴스에 대해 자세히 알아봅니다.

개체 탐색기:
- 개체 탐색기에서 쿼리 창으로 끌어다 놓을 때 이름 주변에 괄호를 적용하지 않도록 추가된 설정 (사용자 제안 [32911933](https://feedback.azure.com/forums/908035-sql-server/suggestions/32911933) 및 [32671051](https://feedback.azure.com/forums/908035-sql-server/suggestions/32671051))

데이터 분류:
- 일반 개선 사항 및 버그 수정

**IS(Integration Services)**

- [SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)로 패키지 배포에 대한 추가된 지원

### <a name="bug-fixes"></a>버그 수정

**일반 SSMS**

데이터 분류:

- 부실한 *정보 유형* 및 *민감도 레이블*로 표시되는 새롭게 추가된 분류를 야기한 *데이터 분류*의 문제를 해결했습니다.
- 대/소문자 구분 데이터 정렬로 설정된 서버를 대상으로 하는 경우 *데이터 분류*가 작동하지 않는 문제를 해결했습니다.
        
Always On:

- *대기 시간 데이터 수집*을 클릭할 때 서버가 대/소문자 구분 데이터 정렬로 설정된 경우 오류가 발생할 수 있는 AG 보기 대시보드의 문제를 해결했습니다.
- SSMS에서 클러스터 서비스가 종료될 때 *분산*으로 AG를 잘못 보고하는 문제를 해결했습니다.
- *가용성 그룹 만들기* 대화 상자를 사용하여 AG를 만들 때 *ReadOnlyRoutingUrl*이 필요한 오류를 수정했습니다.
- 주 서버가 다운되고 보조 서버로 수동으로 장애 조치(failover)할 때 NullReferenceException이 throw되는 오류를 해결했습니다.
- 데이터베이스를 초기화하는 백업/복원을 사용하여 가용성 그룹을 만들 때 보조 복제본에서 기본 디렉터리에 데이터베이스 파일이 생성되는 문제가 해결되었습니다. 수정 사항은 다음을 포함합니다.
   - 데이터/로그 디렉터리 유효성 검사기를 추가합니다.
   - 복제본이 다른 OS에 있는 경우 주 복제본으로만 파일 재배치를 수행합니다.
- SSMS 마법사가 보조 조인 실패를 발생시키는 *CLUSTER_TYPE* 옵션을 생성하지 않는 문제를 해결했습니다.

설치:
- "업그레이드 패키지"를 설치하여 SSMS 업그레이드 시도가 SSMS가 기본이 아닌 위치에 설치되었을 때 실패되는 문제를 해결했습니다.

SMO:
- SQL Server 2016 이상의 테이블 스크립팅에 최대 30초가 걸릴 수 있는 성능 문제를 해결했습니다(이제, 1초 이하로 단축됨).

개체 탐색기:
- SSMS가 개체 탐색기에서 *관리* 노드를 확장하려고 할 때 "DBNull에서 다른 형식으로 개체를 캐스트할 수 없음"과 같은 예외를 throw할 수 있는 문제를 해결했습니다.
- 사용자 정의 PS 프로필에서 출력을 내보냈을 때 *PowerShell 시작*이 SQLServer 모듈을 검색하지 않는 문제를 해결했습니다.
- 개체 탐색기에서 테이블 또는 인덱스 노드를 마우스 오른쪽 단추로 클릭하는 경우 발생할 수 있는 일시적 중단을 수정했습니다.

데이터베이스 메일:
- 16개 이상의 프로필을 표시/관리하려고 할 때 *데이터베이스 메일 구성 마법사*에서 예외를 throw하는 문제를 해결했습니다.


**AS(Analysis Services)**

- 변경 내용이 서버에 저장되지 않는 SSMS의 1400 호환성 수준 모델의 데이터 원본을 수정하는 문제를 해결했습니다.

**IS(Integration Services)**

- SQL Database Managed Instance에 연결한 경우 SSMS에서 SSIS 카탈로그 노드 및 보고서를 표시하지 않는 문제를 해결했습니다.

### <a name="known-issues"></a>알려진 문제

> [!WARNING]
> [Maintenance Plans](../relational-databases/maintenance-plans/maintenance-plans.md)를 사용할 때 SSMS 17.6이 불안정해지고 크래시되는 알려진 문제가 있습니다. Maintenance Plans를 사용하는 경우에는 SSMS 17.6을 설치하지 마세요. 이미 17.6을 설치했고 이 문제가 발생할 경우 SSMS 17.5로 다운그레이드합니다. 



## <a name="downloadssdtmediadownloadpng-ssms-175httpsgomicrosoftcomfwlinklinkid867670"></a>[SSMS 17.5](https://go.microsoft.com/fwlink/?linkid=867670) ![다운로드](../ssdt/media/download.png)
일반 공급 | 빌드 번호: 14.0.17224.0

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x40a)

### <a name="whats-new"></a>새로운 기능

**일반 SSMS**

데이터 검색 및 분류:

- 데이터베이스에서 중요한 데이터를 검색, 분류, 레이블 지정 및 보고하는 새 SQL 데이터 검색 및 분류 기능이 추가되었습니다. 
- 가장 중요한 데이터(비즈니스, 재무, 보건, PII 등)를 자동 검색하고 분류하면 조직 정보 보호 수준에서 중요한 역할을 담당할 수 있습니다.
- [SQL 데이터 검색 및 분류](../relational-databases/security/sql-data-discovery-and-classification.md)에서 자세히 알아보세요.

쿼리 편집기:

- Azure SQL DW의 텍스트 외부 파일 형식에 SkipRows 옵션에 대한 지원이 추가되었습니다. 이 기능을 사용하면 사용자가 SQL DW로 구분된 텍스트 파일을 로드할 때 지정된 수의 행을 건너뛸 수 있습니다. 또한 FIRST_ROW 키워드에 해당하는 intellisense/SMO 지원이 추가되었습니다. 

실행 계획:

- SQL Data Warehouse에 예상된 계획 단추를 표시하도록 설정되었습니다.
- 새 실행 계획 특성 *EstimateRowsWithoutRowGoal*이 추가되었습니다. *QueryTimeStats*에 새 실행 계획 특성 *UdfCpuTime* 및  *UdfElapsedTime*이 추가되었습니다. 자세한 내용은 [SQL Server 2017 CU3에 추가된 쿼리 실행 계획에서 최적화 프로그램 행 목표 정보](http://support.microsoft.com/help/4051361)를 참조하세요.



### <a name="bug-fixes"></a>버그 수정

**일반 SSMS**

실행 계획:

- LQS 연결에 대한 경과 시간 대신 엔진 실행 시간을 표시하도록 라이브 쿼리 통계 경과 시간이 해결되었습니다.
- 실행 계획이 GbApply 및 InnerApply와 같은 논리 연산자를 인식할 수 없는 문제가 해결되었습니다.
- ExchangeSpill과 관련된 문제가 해결되었습니다.

쿼리 편집기:

- SSMS가 다음과 같은 오류를 throw할 수 있는 관련된 문제가 해결되었습니다. "단순 쿼리 앞에 "SET SHOWPLAN_ALL ON"을 실행할 때 입력 문자열의 형식이 잘못되었습니다(mscorlib)." 


SMO:

- 서버 데이터 정렬이 대/소문자를 구분하는 경우에 SMO가 AvailabilityReplica 속성을 페치할 수 없는 문제가 해결되었습니다.(결과적으로 SSMS는 다음과 같은 오류 메시지를 표시할 수 있습니다. "다중 식별자 "a.delimited"를 바인딩할 수 없습니다."
- DatabaseScopedConfigurationCollection 클래스에서 데이터 정렬을 잘못 처리하는 문제가 해결되었습니다.(결과적으로 터키어 로캘로 ma 컴퓨터에서 실행되는 SSMS는 대/소문자를 구분하는 데이터 정렬로 서버에서 실행되는 데이터베이스를 마우스 오른쪽 단추로 클릭할 때 다음과 같은 오류를 표시할 수 있습니다. "레거시 카디널리티 추정은 범위가 잘못 지정된 구성입니다.")
- JobServer 클래스에서 SMO가 SQL 2005 서버에서 SQL 에이전트 속성을 페치할 수 없는 문제가 해결되었습니다.(결과적으로 SSMS가 다음과 같은 오류를 throw합니다. "지역 변수에 기본값을 할당할 수 없습니다. 스칼라 변수 “\@ServiceStartMode”를 선언해야 하고 궁극적으로 개체 탐색기에서 SQL 에이전트 노드가 표시되지 않았습니다.)

템플릿: 

- "데이터베이스 메일": 몇 가지 오타 수정 [(https://feedback.azure.com/forums/908035/suggestions/33143512)](https://feedback.azure.com/forums/908035/suggestions/33143512).  

개체 탐색기:
- 관리되는 압축이 인덱스에 대해 실패하는 문제를 해결했습니다(https://feedback.azure.com/forums/908035-sql-server/suggestions/32610058-ssms-17-4-error-when-enabling-page-compression-o).

감사:
- *감사 파일 병합* 기능과 관련된 문제가 해결되었습니다.
<br>

### <a name="known-issues"></a>알려진 문제

데이터 분류:
- 분류를 제거한 다음, 같은 열에 새로운 분류를 수동으로 추가하면 이전 정보 형식 및 민감도 레이블이 기본 보기에서 열에 할당됩니다.<br>
*해결 방법*: 주 보기에 분류를 다시 추가한 후에 저장하기 전에 새 정보 형식 및 민감도 레이블을 할당합니다.


## <a name="downloadssdtmediadownloadpng-ssms-174httpsgomicrosoftcomfwlinklinkid864329"></a>[SSMS 17.4](https://go.microsoft.com/fwlink/?linkid=864329) ![다운로드](../ssdt/media/download.png)
일반 공급 | 빌드 번호: 14.0.17213.0

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x40a)


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
- SSMS가 Active Directory 인증(‘통합’ 또는 ‘암호’)을 사용하여 자동으로 서버/데이터베이스에 연결하도록 하는 새로운 명령줄 옵션(“-G”)이 추가되었습니다. 자세한 내용은 [Ssms 유틸리티](ssms-utility.md)를 참조하세요.

플랫 파일 가져오기 마법사:
- 테이블을 만들 때 기본값("dbo")이 아닌 스키마 이름을 선택하는 방법이 추가되었습니다.

쿼리 저장소:
- 쿼리 저장소 사용 가능 보고서 목록을 확장할 때 "회귀된 쿼리" 보고서가 복원되었습니다.

**IS(Integration Services)**
- 사용자가 Azure SSIS IR에서 지원되지 않는 SSIS 패키지 내부 구성 요소를 파악하는 데 도움을 주는 패키지 유효성 검사 함수가 배포 마법사에 추가되었습니다.

### <a name="bug-fixes"></a>버그 수정

**일반 SSMS**

- 개체 탐색기: 데이터베이스 스냅숏에 대해 테이블 반환 함수 노드가 표시되지 않는 문제를 해결했습니다 - [연결 3140161](https://connect.microsoft.com/SQLServer/feedback/details/3140161).
서버가 데이터베이스를 자동으로 닫을 때 *데이터베이스* 노드를 확장하는 성능이 개선되었습니다.
- 쿼리 편집기: master 데이터베이스에 액세스할 수 없는 사용자에 대해 IntelliSense가 실패하는 문제를 해결했습니다.
원격 컴퓨터에 대한 연결이 닫히면 SSMS 크래시가 발생하는 문제를 수정했습니다 - [연결 3142557](https://connect.microsoft.com/SQLServer/feedback/details/3142557).
- XEvent 뷰어: XEL을 내보내는 기능을 다시 사용할 수 있게 되었습니다.
사용자가 전체 XEL 파일을 로드할 수 없는 문제를 수정했습니다.
- XEvent 프로파일러: 사용자에게 *VIEW SERVER STATE* 권한이 없는 경우 SSMS의 작동이 중단되는 문제를 해결했습니다.
XE 프로파일러 라이브 데이터 창을 닫아도 기본 세션이 중지되지 않는 문제를 수정했습니다.
- 등록된 서버: “Move To…” 명령이 멈추는 문제를 해결했습니다([연결 3142862](https://connect.microsoft.com/SQLServer/feedback/details/3142862) 및 [Connect 3144359](https://connect.microsoft.com/SQLServer/feedback/details/3144359/)).
- SMO: 전송 개체의 TransferData 메서드가 작동하지 않는 문제를 해결했습니다.
일시 중지된 SQL DW 데이터베이스에 대해 서버 데이터베이스가 예외를 throw하는 문제를 수정했습니다.
SQL DW에 대해 SQL 데이터베이스를 스크립팅하면 잘못된 T-SQL 매개 변수 값이 생성되는 문제를 수정했습니다.
확대된 DB를 스크립팅하면 *데이터\_압축* 옵션을 잘못 내보내는 문제를 수정했습니다.
- 작업 활동 모니터: 사용자가 범주를 기준으로 필터링하려고 할 때 “인덱스가 범위를 벗어났습니다. 인덱스는 음수가 아니어야 하며 컬렉션의 크기보다 작아야 합니다. 
      매개 변수 이름: 인덱스(System.Windows.Forms)" 오류가 발생하는 문제를 수정했습니다 - [연결 3138691](https://connect.microsoft.com/SQLServer/feedback/details/3138691).
- 연결 대화 상자: 읽기/쓰기 도메인 컨트롤러에 액세스할 수 없는 도메인 사용자가 SQL 인증을 사용하여 SQL Server에 로그인할 수 없는 문제를 해결했습니다 - [연결 2373381](https://connect.microsoft.com/SQLServer/feedback/details/2373381).
- 복제: SQL Server에서 끌어오기 구독의 속성을 볼 때 “ServerInstance 속성에 ‘null’ 값을 적용할 수 없습니다”와 비슷한 오류가 표시되는 문제를 해결했습니다.
- SSMS 설치: SSMS를 설치하면 머신에 설치된 모든 제품이 다시 구성되는 문제를 해결했습니다.
- 사용자 설정:
   - 이 수정으로 US Government 소버린 클라우드 사용자는 유니버설 인증 및 Azure Active Directory 로그인을 통해 SSMS를 사용하여 Azure SQL Database 및 Azure Resource Manager 리소스에 중단 없이 액세스할 수 있습니다.  이전 버전의 SSMS 사용자는 도구|옵션|Azure Services를 열고 리소스 관리 아래에서 "Active Directory 기관" 속성의 구성을 https://login.microsoftonline.us로 변경해야 합니다.

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



## <a name="downloadssdtmediadownloadpng-ssms-173httpsgomicrosoftcomfwlinklinkid858904"></a>[SSMS 17.3](https://go.microsoft.com/fwlink/?linkid=858904) ![다운로드](../ssdt/media/download.png)
일반 공급 | 빌드 번호: 14.0.17199.0

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)


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
- 개체 스크립팅: 사용자가 서버에서 DW 데이터베이스를 일시 중지한 경우 “데이터베이스 스크립트 생성”이 작동하지 않고 오류를 throw하지만, DW가 아닌 다른 데이터베이스를 선택하고 스크립팅하려고 시도하는 문제를 해결했습니다.
스크립팅된 저장 프로시저의 헤더가 스크립트 설정과 일치하지 않고 잘못된 스크립트를 생성하는 문제를 해결했습니다. - [연결 항목 3139784](http://connect.microsoft.com/SQLServer/feedback/details/3139784)
SQL Azure 개체를 대상으로 지정할 때 "스크립트" 단추를 다시 사용합니다.
  SSMS에서 Azure SQL Database에 연결된 경우 일부 개체(UDF, 보기, SP, 트리거)에서 “변경” 또는 “실행” 스크립팅을 허용하지 않는 문제를 해결했습니다. - [연결 항목 3136386](https://connect.microsoft.com/SQLServer/feedback/details/3136386)
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
   - 데이터베이스 엔진 튜닝 관리자는 Azure AD 인증에 대해 지원되지 않습니다. 사용자에게 제공된 오류 메시지가 모호하다는 알려진 문제가 있습니다. “파일 또는 어셈블리 ‘Microsoft.IdentityModel.Clients.ActiveDirectory,...’를 로드할 수 없습니다.”가 표시되지만 다음 메시지가 표시되어야 합니다. “데이터베이스 엔진 튜닝 관리자는 Microsoft Azure SQL Database (DTAClient)".
- 오류의 DTA 결과에서 쿼리 분석 시도: "개체는 IConvertible을 구현해야 합니다. (mscorlib)".
- *재발된 쿼리*가 개체 탐색기에서 보고서의 쿼리 저장소 목록에서 누락되었습니다.
   - 해결 방법: 마우스 오른쪽 단추로 **쿼리 저장소** 노드를 클릭하고 **재발된 쿼리 보기**를 선택합니다.

**IS(Integration Services)**

- [catalog].[event_messagea]에서 [execution_path]가 Scale Out에서 패키지 실행에 대해 올바르지 않습니다. [execution_path]는 패키지 실행 파일의 개체 이름 대신 "\Package"로 시작합니다. SSMS에서 패키지 실행의 개요 보고서를 볼 때 실행 개요에서 "실행 경로"의 링크는 작동하지 않습니다. 해결 방법은 개요 보고서에서 "메시지 보기"를 클릭하여 모든 이벤트 메시지를 확인하는 것입니다.


## <a name="downloadssdtmediadownloadpng-ssms-172httpsgomicrosoftcomfwlinklinkid854085"></a>[SSMS 17.2](https://go.microsoft.com/fwlink/?linkid=854085) ![다운로드](../ssdt/media/download.png)
일반 공급 | 빌드 번호: 14.0.17177.0

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

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
또한 모든 스크립팅 옵션이 자체 섹션인 *버전 옵션*으로 이동하였습니다. 따라서 더 이상 *일반 스크립팅 옵션* 아래에 없습니다.

- “URL에서 복원”에서 국가 클라우드에 대한 지원 추가
- 이제 QueryStoreUI 보고서는 sys.query_store_runtime_stats에서 추가 메트릭(RowCount, DOP, CLR Time 등)을 지원합니다.
- Azure SQL Database에 IntelliSense 지원 https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
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
- SSMS UI의 SPID가 부실하고 동기화되지 않는 문제 해결. https://connect.microsoft.com/SQLServer/feedback/details/1898875
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
- Always Encrypted: 새 CMK 대화 상자에서 AKV 권한 상태에 대한 메시징 기능 개선. 긴 이름을 가진 CEK를 보다 쉽게 구분할 수 있도록 CEK 드롭다운에 도구 설명 추가. 일부 CNG 키 저장소 공급자가 Always Encrypted를 위한 [새 열 마스터 키] 대화 상자에 표시되지 않는 문제 해결.
- SSMS 연결에 대해 일관성 없는 “응용 프로그램 이름” 해결. http://connect.microsoft.com/SQLServer/feedback/details/3135115
- SSMS가 SQL Azure에 대한 정확한 스크립트(DATA_COMPRESSIONS 옵션을 포함한 테이블 및 인덱스)를 생성하지 않았던 문제 해결. https://connect.microsoft.com/SQLServer/feedback/details/3133148
- 사용자가 빠른 실행을 위해 CTRL+Q 바로 가기를 사용할 수 없었던 문제 해결(참고: 이제 쿼리 편집기에서 "IntelliSense 사용" 옵션을 설정/해제하기 위한 새 키 바인딩은 CTRL+B, CTRL+I). https://connect.microsoft.com/SQLServer/feedback/details/3131968
- "데이터베이스 복원"에서 사용자 지정 도메인이 정의된 계정을 가진 구독에서 저장소 계정을 선택하려고 할 때 SSMS가 예외를 throw했던 문제 해결
- "데이터베이스 다이어그램"에서 SSMS가 “인덱스가 배열의 범위 밖에 있습니다.” 오류를 throw하고 사용자가 "테이블 보기"를 표준이 아닌 것으로 변경할 수 없었던 문제 해결. https://connect.microsoft.com/SQLServer/feedback/details/3133792 및 http://connect.microsoft.com/SQLServer/feedback/details/3135326
- "URL에 백업/복원"에서 SSMS가 클래식 저장소 계정을 열거하지 않았던 문제 해결.
- 스키마 바운드 보안 개체를 DB 역할에 추가하려고 할 때 예외가 throw되었던 문제 해결. https://connect.microsoft.com/SQLServer/feedback/details/3118143
- SSMS에서 다음 오류가 간헐적으로 표시되는 문제를 해결했습니다. “데이터가 Null입니다. 이 메서드 또는 속성은 Null 값에 호출될 수 없습니다." 테이블 노드를 확장하는 경우 http://connect.microsoft.com/SQLServer/feedback/details/3136283
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

## <a name="downloadssdtmediadownloadpng-ssms-171httpsgomicrosoftcomfwlinklinkid849819"></a>[SSMS 17.1](https://go.microsoft.com/fwlink/?linkid=849819) ![다운로드](../ssdt/media/download.png)
출시 | 빌드 번호: 14.0.17119.0

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40a)

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

## <a name="downloadssdtmediadownloadpng-ssms-170httpgomicrosoftcomfwlinklinkid847722"></a>[SSMS 17.0](http://go.microsoft.com/fwlink/?LinkID=847722) ![다운로드](../ssdt/media/download.png)
출시 | 빌드 번호: 14.0.17099.0

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x40a)

### <a name="enhancements"></a>개선 사항 

- 업그레이드 패키지 및 WSUS(Windows Software Update Services). 향후 17.X 릴리스에는 더 작은 누적 업데이트 패키지가 포함됨 
  - 업데이트 패키지는 WSUS 카탈로그에도 게시됨  
- 아이콘 업데이트. 아이콘이 VS Shell 제공 아이콘과 일치하고 높은 DPI 해상도를 지원하도록 업데이트됨. 16.X 및 17.X 버전을 구분하는 새 SSMS 및 Profiler 프로그램 아이콘
- SQL PowerShell 모듈
  - SQL Server PowerShell 모듈이 SSMS에서 제거되고 이제 PowerShell 갤러리를 통해 제공(모듈 버전 관리를 지원하려면 이제 PowerShell 5.0 필요)
  - 일부 SMO 개체의 프레젠테이션(형식) 관련 기타 개선 사항(예: 이제 데이터베이스에 크기와 사용 가능한 공간이 표시되고 테이블에 행 수와 공간 사용량 표시)
  - OE의 “PowerShell 시작” 메뉴에서 PowerShell 명령 프롬프트를 호출할 때 색 지정을 추가함
  - AG cmdlet(New-SqlAvailabilityGroup, Join-SqlAvailabilityGroup 및 Set-SqlAvailabilityGroup cmdlet)에 -ClusterType 및 -RequiredCopiesToCommit 매개 변수를 추가함
  - Add-SqlAzureAuthenticationContext cmdlet에 -ActiveDirectoryAuthority 및 -AzureKeyVaultResourceId 매개 변수를 추가함
  - Revoke-SqlAvailabilityGroupCreateAnyDatabase, Grant-SqlAvailabilityGroupCreateAnyDatabase 및 Set-SqlAvailabilityReplicaRoleToSecondary cmdlet을 추가함
  - Set-SqlAvailabilityReplica 및 New-SqlAvailabilityReplica cmdlet에 -SeedingMode 매개 변수를 추가함
  - Get-SqlDatabase에 -ConnectionString 매개 변수를 추가함
- Linux의 SQL Server. 일반 개선 사항 및 로그 전달에 대한 수정
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
- 실행 계획. 경과된 시간의 속성 창에서 전체 스레드의 합계 대신 최댓값 표시. 새로운 메모리 부여 연산자 속성 노출. 활성 쿼리 통계에서 “쿼리 편집” 단추를 사용하도록 설정함. 인터리브 실행 지원
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
  - 새 클러스터 유형에 대한 지원 추가: EXTERNAL 및 NONE. Linux에서 SQL Server에 대한 지원 추가. 초기 데이터 동기화에 대한 옵션으로 자동 시드를 추가. 일부 결함을 수정함(예: 엔드포인트 URL 처리, DB 새로 고침, UI 레이아웃). Azure 복제본 관련 기능을 제거함
  - 여러 가용성 그룹 키워드에 대한 IntelliSense를 개선함
- 작업 모니터
  - SSMS 출력 창에 새 “작업 모니터” 창을 추가함
  - 팝업 메시지를 표시하지 않고 정보를 출력 창에 기록하도록 연결 오류/시간 초과 메시지를 변경함
  - 개요 섹션에서 빈 차트(5번째 차트)를 제거함
  - 작업 모니터 데이터 수집이 일시 중지된 경우 개요 제목에 “(일시 중지됨)”을 추가함
  - SQL Server에 대한 그래프 확장. 그래프 노드와 에지 테이블에 대한 새 아이콘. 그래프 노드 및 에지 테이블이 그래프 테이블 폴더에 표시됨. 그래프 노드와 에지 테이블을 만드는 템플릿을 사용할 수 있음
- 프레젠테이션 모드. 빠른 실행(Ctr-Q)을 통해 사용할 수 있는 새 작업 3개. PresentOn - 프레젠테이션 모드 켜기. PresentEdit - 프레젠테이션 모드에 대한 프레젠테이션 글꼴 크기 편집.  쿼리 편집기의 경우 "텍스트 편집기 글꼴".  다른 구성 요소의 경우 "환경 글꼴"
RestoreDefaultFonts - 기본 설정으로 되돌리기
*참고: 현재 PresentOff 명령이 없습니다.  프레젠테이션 모드를 끄려면 RestoreDefaultFonts를 사용 하세요.*

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
- Always Encrypted. SQL 2016 RTM Standard Edition 또는 SQL 2014 이하 서버를 대상으로 할 경우 “Always Encrypted” 메뉴가 잘못 사용하도록 설정됨. CREATE 또는 ALTER 구문을 사용할 때 IntelliSense가 오류를 보고하는 문제를 해결함. CMK/CEK에 이스케이프(즉, 괄호로 묶음)해야 하는 문자가 포함된 경우 암호화가 실패하는 문제를 해결함. SSMS에서 메모리 부족 예외가 발생하는 경우 네이티브(64비트) PowerShell을 대신 사용하도록 제안하는 오류가 표시됨.
사용자가 클래식 Azure 구독 대신 리소스 그룹 관리자 구독을 사용하는 경우 AE 마법사가 실패하는 문제를 해결함. 사용자가 구독에 사용 권한이 없거나 Azure Key Vault가 없는 경우 AE 마법사에 잘못된 오류가 표시되는 문제를 해결함.
AAD가 여럿인 경우 Azure Key Vault 로그인 페이지에 Azure 구독이 표시되지 않는 AE 마법사의 문제를 해결함. Azure Key Vault 로그인 페이지에 사용자에게 읽기 권한이 있는 Azure 구독이 표시되지 않는 AE 마법사의 문제를 해결함
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
- [Generate Tasks]\(작업 생성) 스크립트에서 Azure SQL DB에 대한 [데이터베이스 만들기] 스크립트를 생성하지 않음.
- 뷰 디자이너의 스크롤 막대가 사용하지 않도록 설정된 것으로 보임.
- Always Encrypted AVK 키 경로에 버전 ID가 포함되지 않음.
- 쿼리 창의 엔진 버전 쿼리 수 줄임. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3113387)
- 암호화가 잘못 처리된 후 모듈을 새로 고치지 못하는 Always Encrypted 오류.
- OLTP 및 OLAP에 대한 기본 연결 제한 시간을 15초에서 30초로 변경하여 무시된 연결 실패의 클래스를 수정함. 
- 사용자 지정 보고서가 시작될 때 SSMS 작동이 중단되는 문제를 해결함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3118856)
- Azure SQL Database의 “스크립트 생성...”이 실패하는 문제를 해결했습니다.
- 저장 프로시저와 같은 개체를 스크립팅할 때 줄 바꿈이 추가되지 않도록 "스크립팅" 및 "스크립트 생성 마법사"를 수정함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3115850)
- SQLAS PowerShell 공급자: Dimension 및 MeasureGroup 폴더에 LastProcessed 속성을 추가함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3111879)
- 활성 쿼리 통계: 배치에 있는 첫 번째 쿼리만 표시하던 문제를 해결함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3114221)  
- 실행 계획: 속성 창에서 전체 스레드의 합계 대신 최대값을 표시함.
- 쿼리 저장소: 실행 변형이 높은 쿼리에 대해 새 보고서를 추가함.
- 개체 탐색기 성능 문제: [연결 항목](http://connect.microsoft.com/SQLServer/feedback/details/3114074). 테이블의 상황에 맞는 메뉴가 잠시 중단됨. 원격(인터넷) 연결을 통해 테이블의 인덱스를 마우스 오른쪽 단추로 클릭할 경우 SSMS가 느려짐. 서버에서 정렬되는 테이블 쿼리 실행 차단
- SSMS에서 Azure 배포 마법사를 제거함(Azure VM에 데이터베이스 배포)
- SSMS에서 실행 계획에 누락된 인덱스가 표시되지 않았던 문제를 해결함 [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3114194)
- SSMS에서 종료 시 발생하는 일반적인 작동 중단 문제를 해결함
- Polybase|규모 확장 그룹 노드에서 상황에 맞는 메뉴를 표시할 때 오류가 발생하는 개체 탐색기의 문제를 해결함 [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3115128)
- 데이터베이스에 대한 사용 권한을 표시하려고 할 때 SSMS의 작동이 중단되는 문제를 해결함
- 쿼리 저장소: 쿼리 저장소 보고서의 결과 표에 대한 상황에 맞는 메뉴 항목의 일반적인 개선 사항
- 기존 테이블에 대한 Always Encrypted 구성이 관련 없는 개체에 대한 오류와 함께 실패함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3103181)
- 여러 스키마가 포함된 기존 데이터베이스에 대한 Always Encrypted 구성이 작동하지 않음. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3109591)
- Always Encrypted, 암호화된 열 마법사가 시스템 뷰를 참조하는 뷰를 포함하는 데이터베이스로 인해 실패함. [Connect 항목](http://connect.microsoft.com/SQLServer/feedback/details/3111925)
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


## <a name="downloadssdtmediadownloadpng-ssms-1653httpgomicrosoftcomfwlinklinkid840946"></a>[SSMS 16.5.3](http://go.microsoft.com/fwlink/?LinkID=840946) ![다운로드](../ssdt/media/download.png)
일반 공급 | 빌드 번호: 13.0.16106.4

[중국어(간체)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804) | [중국어(번체)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404) | [영어(미국)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409) | [프랑스어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c) | [독일어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407) | [이탈리아어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410) | [일본어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411) | [한국어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412) | [포르투갈어(브라질)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416) | [러시아어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419) | [스페인어](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)

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


## <a name="uninstall-and-reinstall-ssms-17x"></a>SSMS 17.x 제거 및 다시 설치

SSMS 설치에 문제가 있고, 표준 제거 및 다시 설치로 해결되지 않는 경우 먼저 Visual Studio 2015 IsoShell을 [복구](https://support.microsoft.com/help/4028054/windows-10-repair-or-remove-programs)해 볼 수 있습니다. Visual Studio 2015 IsoShell을 복구해도 문제가 해결되지 않으면 다음 단계에서 여러 가지 해결해야 할 임의의 문제를 발견합니다.

1.  응용 프로그램을 제거한 것과 동일한 방식으로 SSMS를 제거합니다(사용자의 Windows 버전에 따라 *앱 및 기능*, *프로그램 및 기능* 등 사용).

2.  **관리자 권한 cmd 프롬프트에서** Visual Studio 2015 IsoShell을 제거합니다.
   
    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```

    ```vs_isoshell.exe /Uninstall /Force /PromptRestart```

3.  응용 프로그램을 제거하는 것과 동일한 방식으로 Microsoft Visual C++ 2015 재배포 가능 패키지를 제거합니다. x86 및 x64 버전이 컴퓨터에 설치되어 있으면 모두 제거합니다.

4.  **관리자 권한 cmd 프롬프트에서** Visual Studio 2015 IsoShell을 다시 설치합니다.  

    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```  
 
    ```vs_isoshell.exe /PromptRestart```

5.  SSMS를 다시 설치합니다.

6.  현재 최신 상태가 아닌 경우 [최신 버전의 Visual C++ 2015 재배포 가능 패키지](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)로 업그레이드합니다.


## <a name="additional-downloads"></a>추가 다운로드  
모든 SQL Server Management Studio 다운로드의 전체 목록은 [Microsoft 다운로드 센터](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending)를 검색하세요.  
  
최신 SQL Server Management Studio에 대해서는 [SQL Server Management Studio 다운로드&#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)를 참조하세요.  
