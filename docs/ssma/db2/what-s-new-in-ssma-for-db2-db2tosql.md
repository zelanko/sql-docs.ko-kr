---
title: DB2 (DB2ToSQL)에 대한 SSMA의 새로운 소식 | 마이크로 소프트 문서
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
ms.author: jtoland;alexiva
ms.openlocfilehash: 53a159627750a5ec66b5aa0b3fd6510c647e26a5
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625520"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>DB2 (DB2ToSQL)에 대한 SSMA의 새로운 내용

이 문서에서는 각 릴리스의 DB2 변경 사항에 대한 SQL 서버 마이그레이션 도우미(SSMA)를 나열합니다.

## <a name="ssma-v88"></a>SSMA v8.8

DB2용 SSMA의 v8.8 릴리스에는 다음이 포함됩니다.

* SQL Server 개체 동기화 안정성 향상
* 평가 및 변환 중 GUI 성능 향상
* 데이터 마이그레이션을 `varbinary(40)` 용이하게 하기 위해 매핑을 에서 업데이트했습니다. `ROWID`
* `SELECT ... FROM NEW/OLD TABLE` 문 변환 개선
* 프로시저 `ALTER` 및 함수에 대한 명령문의 새로운 변환
* 파괴 할당의 새로운 변환

## <a name="ssma-v87"></a>SSMA v8.7

DB2용 SSMA의 v8.7 릴리스에는 새로운 DB2 구문 파서뿐만 아니라 그래픽 사용자 인터페이스의 사소한 수정 및 성능 향상이 포함되어 있습니다.

또한 DB2용 SSMA는 이제 다음을 제공합니다.

* LUW에서 DB2에서 마이그레이션할 때 외래 키 를 검색하기 위한 수정 사항입니다.
* 명령문의 `SELECT ... FOR UPDATE` 변환이 개선되었습니다.
* MQ `COUNT` 테이블의 함수변환이 개선되었습니다.
* 명령문의 `SAVEPOINT` 변환.
* 절의 값에 대한 DB2의 `NULL` 동작을 에뮬레이트하는 변환입니다. `ORDER BY`
* 동료 결과 집합 문에 대 한 구문 분석 지원입니다.

> [!IMPORTANT]
> SSMA v8.5 이상에서는 .NET 4.7.2가 설치 필수 조건입니다. 이 버전을 설치해야 하는 경우 여기에서 런타임 파일을 다운로드할 수 [있습니다.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v86"></a>SSMA v8.6

유용성과 성능을 향상시키기 위해 설계된 대상 수정 사항 집합 외에도 사용자가 변환된 코드에서 SSMA 확장 속성을 생략할 수 있는 설정을 추가하여 DB2용 SSMA의 v8.6 릴리스가 향상되었습니다.

이 설정을 활용하려면 DB2용 SSMA에서 **도구** > **프로젝트 설정** > **일반** > **변환으로**이동한 다음 **기타 에서 [Omit** **확장 속성]** 설정의 값을 **예로**업데이트합니다.

![확장 속성 설정 생략](../db2/media/ssma-omit-extended-properties.png)

또한 DB2용 SSMA는 이제 다음을 제공합니다.

* 기본 인수 값을 사용하는 함수 변환에 대한 수정 사항입니다.
* 함수에 `PARAMETER` 대한 절의 구문 분석이 개선되었습니다.
* 문을 변환하는 `LEAVE` 기능입니다.

> [!IMPORTANT]
> SSMA v8.5 이상에서는 .NET 4.7.2가 설치 필수 조건입니다. 이 버전을 설치해야 하는 경우 여기에서 런타임 파일을 다운로드할 수 [있습니다.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v85"></a>SSMA v8.5

DB2용 SSMA의 v8.5 릴리스는 사용성과 성능을 향상시키기 위해 설계된 대상 수정 사항 집합과 함께 Azure Active Directory 인증 및 SQL 서버의 JSON 기능에 대한 기본 지원으로 향상되었습니다.

또한 DB2용 SSMA가 다음과 함께 향상되었습니다.

* 을 통해 명령문에 대한 변환 추가 지원 `GET DIAGNOSTICS` `ROW_NUMBER`
* 개체 이름 의 시작 부분에 있는 공백과 관련된 버그에 대한 수정 프로그램이 적용되지 않습니다.

> [!IMPORTANT]
> SSMA v8.5에서는 .NET 4.7.2가 설치 전제 조건입니다. 이 버전을 설치해야 하는 경우 여기에서 런타임 파일을 다운로드할 수 [있습니다.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v84"></a>SSMA v8.4

DB2용 SSMA의 v8.4 릴리스는 접근성 문제를 해결하고 SQL Server 2016 및 이후 버전에 대해 최대 인덱스 열(16개 대신 32개)과 관련된 버그를 수정하도록 설계된 대상 수정 사항으로 향상되었습니다.

> [!IMPORTANT]
> SSMA 버전 7.4에서는 8.4이지만 .NET 4.5.2는 설치 필수 조건입니다.

## <a name="ssma-v83"></a>SSMA v8.3

DB2용 SSMA의 v8.3 릴리스는 품질 및 변환 메트릭을 개선하도록 설계된 대상 수정 사항으로 향상되었습니다. 또한 DB2용 SSMA 릴리스는 다음과 같은 수정 프로그램을 제공합니다.

* 내게 필요한 옵션 문제를 해결합니다.
* SQL Server에서 `hierarchyid` 형식에 대한 기본 지원을 추가합니다.
* z/OS 검색 쿼리에서 TRIM 함수 `RTRIM` / `LTRIM`사용량을 .로 바꿉꿉입니다.
* 사용자가 '표준 모드'(기본값에서)로 연결할 때 `NULLID`패키지 컬렉션을 지정할 수 있도록 허용합니다.
* 에 대한 `CREATE TABLE AS SELECT`변환추가
* 전역 임시 테이블에 대한 변환을 개선합니다.
* 개체 고유성 검사 순서로 문제를 해결하여 이름이 충돌하는 경우 제약 조건보다 테이블의 우선 순위를 지정합니다.
* z/OS에 대한 기본 열 `DATE` `TIMESTAMP` 값을 로드하는 문제를 해결합니다.
* 유니코드 줄 피드 문자(일명)를 `NEL`지원합니다.
* 누락된 `RETURN TO` 절을 사용 하 고 커서 변환 문제를 해결 합니다.
* 레이블 및 `GOTO`에 대한 지원을 추가합니다.

## <a name="ssma-v82"></a>SSMA v8.2

DB2용 SSMA의 v8.2 릴리스는 SSMA 콘솔 도구에서 Azure SQL Database에 대한 연결 및 변환 중에 뷰 선언에서 COUNT_BIG 열이 누락된 문제를 해결하기 위해 향상되었습니다. 또한 이 버전에는 품질 및 전환 메트릭을 개선하기 위해 설계된 대상 수정 사항 집합과 다음에 대한 수정 사항이 포함되어 있습니다.

* 데이터 마이그레이션 후 클러스터되지 않은 인덱스가 비활성화된 문제입니다.
* 자동 설치 중 .NET 프레임워크 를 검색합니다.
* 새 버전을 다운로드할 때 발생하는 간헐적인 충돌입니다.

> [!NOTE]
> 자동 업데이트로 인해 SSMA v8.1에서 v8.2로 업데이트가 실패할 수 있습니다. 이 오류가 발생하면 새 버전을 다운로드하고 수동으로 설치하십시오.

## <a name="ssma-v81"></a>SSMA v8.1

DB2용 SSMA의 v8.1 릴리스는 품질 및 변환 메트릭을 개선하도록 설계된 대상 수정 프로그램을 제공하도록 향상되었습니다.

> [!NOTE]
> 자동 업데이트로 인해 SSMA v8.0에서 v8.1로 업데이트가 실패할 수 있습니다. 이 오류가 발생하면 새 버전을 다운로드하고 수동으로 설치하십시오.

## <a name="ssma-v80"></a>SSMA v8.0

DB2용 SSMA의 v8.0 릴리스는 품질 및 변환 메트릭을 개선하도록 설계된 대상 수정 프로그램을 제공하도록 향상되었습니다. 이 릴리스는 다음과 같은 새로운 기능도 제공합니다.

* Azure **SQL 데이터베이스 관리 인스턴스를** 대상으로 지원합니다. 이제 Azure SQL Database 관리 인스턴스를 대상으로 하는 새 프로젝트를 만들 수 있습니다.

  ![SQL DB MI 프로젝트](../media/ssma-newproject-sqldbmi.png)

* 변환 후 **수정 고문**. 자세한 내용은 [여기를 참조하십시오.](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 예비 데이터베이스/스키마 선택.

  소스에 연결할 때 사용자는 이제 관심 있는 데이터베이스/스키마를 선택할 수 있습니다. 마이그레이션하려는 스키마만 선택하면 초기 연결 시 시간을 절약하고 전반적인 SSMA 성능을 향상시킬 수 있습니다.

  ![SSMA 필터 개체](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

DB2용 SSMA의 v7.10 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 글로벌 요구 사항의 변화를 충족하기 위해 추가 보안 및 개인 정보 보호를 제공하도록 설계된 대상 수정 사항입니다.
* `BEGIN-END` 블록 변환을 위한 수정 사항입니다.

## <a name="ssma-v79"></a>SSMA v7.9

DB2용 SSMA의 v7.9 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 품질 및 전환 측정항목을 개선하는 타겟팅된 수정사항입니다.
* SSMA 명령줄에서 지원하여 데이터 유형 매핑 및 프로젝트 기본 설정을 변경합니다.
* SQL 서버 통합 서비스(SSIS)를 사용하여 데이터 마이그레이션을 지원합니다. 스키마를 변환한 후 오른쪽 클릭 컨텍스트 메뉴 옵션을 사용하여 SSIS 패키지를 만들 수 있습니다.
* SSMA의 Azure SQL Database 연결 대화 상자도 완전히 정규화된 서버 이름을 지정하도록 변경되었습니다. 이전 버전의 SSMA에서는 프로젝트 설정 내에서 Azure SQL Database 접두사를 명시적으로 언급해야 했습니다.

## <a name="ssma-v78"></a>SSMA v7.8

DB2용 SSMA의 v7.8 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* *프로젝트 설정에서*강조 표시된 유형 매핑 변경.
* 사용자가 원격 분석을 사용하지 않도록 설정하는 기능입니다.

## <a name="ssma-v77"></a>SSMA v7.7

DB2용 SSMA의 v7.7 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 품질 및 전환 측정항목을 개선하는 타겟팅된 수정사항입니다.
* 인기 있는 수요에 따라 DB2용 SSMA의 32비트 버전이 돌아왔습니다. 이전 구현(v7.4 이전)과 비교하여 두 개의 설치 관리자 패키지가 있지만 나란히 설치할 수는 없습니다. 따라서 사용 가능한 연결 구성 요소에 따라 가장 적합한 버전을 선택해야 합니다. 가능하면 항상 64비트 버전을 사용하는 것이 좋습니다.

## <a name="ssma-v76"></a>SSMA v7.6

DB2용 SSMA의 v7.6 릴리스는 품질 및 변환 메트릭을 개선하는 대상 수정 사항과 SQL Server 2017(공개 미리 보기)에 대한 지원으로 향상되었습니다. Windows 및 Linux에서 SQL Server 2017에 대한 지원은 공개 미리 보기중이며 프로덕션 마이그레이션에 사용해서는 안 됩니다.

## <a name="ssma-v75"></a>SSMA v7.5

DB2용 SSMA의 v7.5 릴리스는 장애가 있는 사용자에게 더 큰 접근성을 보장하기 위해 몇 가지 개선 사항으로 개선되었습니다.

## <a name="ssma-v74"></a>SSMA v7.4

DB2용 SSMA의 v7.4 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 이제 소스 및 대상에서 스키마 개체 검색 중에 **쿼리 시간 지정** 옵션을 사용할 수 있습니다.

  ![쿼리 시간 시간 변경 옵션](../media/query-timeout_red.png)

* 고객 피드백을 기반으로 타겟팅된 수정을 통해 품질 및 전환 지표가 개선되었습니다.

  > [!IMPORTANT]
  > .NET 4.5.2는 SSMA v7.4를 설치하기 위한 필수 조건입니다. 또한 v7.4부터 SSMA의 32비트 버전이 단종되었습니다.

## <a name="ssma-v73"></a>SSMA v7.3

DB2용 SSMA의 v7.3 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 고객 피드백을 기반으로 타겟팅된 수정을 통해 품질 및 전환 지표를 개선했습니다.
* 다음 항목을 통해 노출된 SSMA 확장성 프레임워크:
  * 기능을 SQL 서버 데이터 도구(SSDT) 프로젝트로 내보냅니다.
    * 이제 SSMA에서 SSDT 프로젝트로 스키마 스크립트를 내보낼 수 있습니다. 스키마 스크립트를 사용하여 스키마를 추가로 변경하고 데이터베이스를 배포할 수 있습니다.

      ![SSDT 프로젝트 명령으로 저장](../media/export-schema-scripts_red.png)
  * 사용자 지정 변환을 수행하기 위해 SSMA에서 사용할 수 있는 라이브러리입니다.
    * 이제 이전에 SSMA에서 처리하지 않았던 사용자 지정 구문 변환 및 변환을 처리할 수 있는 코드를 생성할 수 있습니다.
      * 사용자 지정 변환기를 구성하는 방법에 대한 지침은 [SQL Server 마이그레이션 도우미의 변환 기능 확장,](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)이 블로그 게시물에서 사용할 수 있습니다.
      * 이 블로그 게시물에서 변환을 위한 샘플 [프로젝트를 다운로드합니다.](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)

## <a name="ssma-v72"></a>SSMA v7.2

DB2용 SSMA의 v7.2 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 고객 피드백을 기반으로 타겟팅된 수정을 통해 품질 및 전환 지표를 개선했습니다.
* 원격 분석 개선으로 고객 문제를 해결하고 SSMA의 전환율을 개선하기 위해 더 나은 데이터 포인트를 제공합니다.

## <a name="ssma-v71"></a>SSMA v7.1

DB2용 SSMA의 v7.1 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* Windows 및 Linux CTP1의 SQL Server 2017은 이제 마이그레이션을 위해 지원되는 대상 플랫폼입니다. 이 기능은 기술 미리 보기에 있으며 스키마 및 데이터 이동을 사용하여 SQL 서버를 대상으로 할 수 있습니다.
* 사용 가능한 즉시 최신 버전의 SSMA를 다운로드할 수 있는 자동 업데이트 지원.
* 이제 SSMA 설치 가능 바이너리가 Windows Installer 패키지 파일(.msi)을 통해 배달됩니다.

## <a name="may-2016"></a>2016년 5월

DB2용 SSMA 2016년 5월 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* SQL Server 2016에 대한 지원이 추가되었습니다.
* SQL Server 인메모리 및 헤카톤 기능에 DB2 인메모리 및 일반 테이블을 추가했습니다.
* SQL Server 정책 개체에 대한 DB2 액세스 컨트롤의 변환을 추가했습니다(DB2의 행 수준 보안).
* SQL Server 임시 테이블에 DB2 시스템 버전 테이블을 추가했습니다.
* DB2 파서 및 해결새를 개선했습니다.
* .NET 2.0에 대한 설치 관리자 검사를 제거했습니다.
* Db2 \*설치 관리자에서 불필요한 .dll을 제거했습니다.
* SSMA 콘솔에 대한 수정 `save-project` 및 `open-project` 명령.
* SSMA 콘솔에 대한 `securepassword` 고정 명령.
* 초기 로드를 위한 객체 수를 고정했습니다.
* 전역 설정에서 버그를 수정했습니다.
  
## <a name="march-2016"></a>2016년 3월

DB2용 SSMA의 2016년 3월 미리 보기 릴리스는 SQL Server 2016으로의 마이그레이션에 대한 지원을 추가합니다.

## <a name="january-2016"></a>2016년 1월

DB2용 SSMA의 2016년 1월 유지 관리 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.
  
* 여러 표준 기능에 대한 지원이 추가되었습니다.
* DB2 파서 오류를 수정했습니다.
* DB2 v9 zOS 지원(RFC 5690920)을 수정했습니다.
* 변환 하는 동안 DB2 해결 되지 않은 식별자 오류를 수정 했습니다.
* SSMA(RFC 5706203)에 보기 로그 메뉴 항목이 추가되었습니다.
* 원격 분석이 추가되었습니다.
  
## <a name="november-2014"></a>2014년 11월

DB2용 SSMA의 2014년 11월 릴리스는 초기 릴리스였습니다.
