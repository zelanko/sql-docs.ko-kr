---
title: SAP ASE를 위한 SSMA의 새로운 점 (SybaseToSQL) | 마이크로 소프트 문서
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
ms.author: jtoland;alexiva
ms.openlocfilehash: 7f23c7e1c676b4ade42b43cf963e0fa6956f93c6
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625592"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>SAP ASE를 위한 SSMA의 새로운 내용 (SybaseToSQL)

이 문서에서는 각 릴리스의 SAP ASE(이전 SsMA for Sybase)에 대한 SQL 서버 마이그레이션 도우미(SSMA)를 나열합니다.

## <a name="ssma-v88"></a>SSMA v8.8

SAP ASE용 SSMA의 v8.8 릴리스에는 다음이 포함됩니다.

* SQL Server 개체 동기화 안정성 향상
* 평가 및 변환 중 GUI 성능 향상
* 개체에 대 한 SQL 정의에서 누락 된 문자와 문제에 대 한 수정

## <a name="ssma-v87"></a>SSMA v8.7

SAP ASE용 SSMA의 v8.7 릴리스에는 그래픽 사용자 인터페이스에서 사소한 수정 및 성능 향상이 있습니다.

> [!IMPORTANT]
> SSMA v8.5 이상에서는 .NET 4.7.2가 설치 필수 조건입니다. 이 버전을 설치해야 하는 경우 여기에서 런타임 파일을 다운로드할 수 [있습니다.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v86"></a>SSMA v8.6

유용성과 성능을 향상시키기 위해 설계된 대상 수정 사항 집합 외에도 사용자가 변환된 코드에서 SSMA 확장 속성을 생략할 수 있는 설정을 추가하여 SAP ASE용 SSMA의 v8.6 릴리스가 향상되었습니다.

이 설정을 활용하려면 SAP ASE용 SSMA에서 **도구** > **프로젝트 설정** > **일반** > **변환으로**이동한 다음 기타 에서 **[Omit** **확장 속성]** 설정의 값을 **예로**업데이트합니다.

![확장 속성 설정 생략](../sybase/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> SSMA v8.5 이상에서는 .NET 4.7.2가 설치 필수 조건입니다. 이 버전을 설치해야 하는 경우 여기에서 런타임 파일을 다운로드할 수 [있습니다.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v85"></a>SSMA v8.5

SAP ASE용 SSMA의 v8.5 릴리스는 사용성과 성능을 향상시키기 위해 설계된 대상 수정 사항 집합과 함께 Azure Active Directory 인증 및 SQL 서버의 JSON 기능에 대한 기본 지원으로 향상되었습니다.

또한 SAP ASE용 SSMA를 사용하면 시스템 테이블과 뷰를 숨길 수 있습니다(변환에서 제외).

> [!IMPORTANT]
> SSMA v8.5에서는 .NET 4.7.2가 설치 전제 조건입니다. 이 버전을 설치해야 하는 경우 여기에서 런타임 파일을 다운로드할 수 [있습니다.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v84"></a>SSMA v8.4

SAP ASE용 SSMA의 v8.4 릴리스는 접근성 문제를 해결하고 SQL Server 2016 및 이후 버전에 대해 최대 인덱스 열(16개 대신 32개)과 관련된 버그를 수정하도록 설계된 대상 수정 사항으로 향상되었습니다.

> [!IMPORTANT]
> SSMA 버전 7.4 ~ 8.4를 사용하면 .NET 4.5.2가 설치 필수 조건입니다.

## <a name="ssma-v83"></a>SSMA v8.3

SAP ASE용 SSMA의 v8.3 릴리스는 품질 및 변환 메트릭을 개선하도록 설계된 대상 수정 사항으로 향상되었습니다. 또한 SAP ASE용 SSMA 릴리스에서는 다음과 같은 수정 사항을 제공합니다.

* 접근성 문제 해결
* SQL Server에서 `hierarchyid` 형식에 대한 기본 지원 추가

## <a name="ssma-v82"></a>SSMA v8.2

SAP ASE용 SSMA의 v8.2 릴리스는 품질 및 변환 메트릭을 개선하도록 설계된 대상 수정 사항 집합과 다음에 대한 수정 사항으로 향상되었습니다.

* 데이터 마이그레이션 후 클러스터되지 않은 인덱스가 비활성화된 문제입니다.
* 자동 설치 중 .NET 프레임워크 를 검색합니다.
* 새 버전을 다운로드할 때 발생하는 간헐적인 충돌입니다.

> [!NOTE]
> 자동 업데이트로 인해 SSMA v8.1에서 v8.2로 업데이트가 실패할 수 있습니다. 이 오류가 발생하면 새 버전을 다운로드하고 수동으로 설치하십시오.

## <a name="ssma-v81"></a>SSMA v8.1

SAP ASE용 SSMA의 v8.1 릴리스는 품질 및 변환 메트릭을 개선하도록 설계된 대상 수정 사항으로 향상되었습니다.

> [!NOTE]
> 자동 업데이트로 인해 SSMA v8.0에서 v8.1로 업데이트가 실패할 수 있습니다. 이 오류가 발생하면 새 버전을 다운로드하고 수동으로 설치하십시오.

## <a name="ssma-v80"></a>SSMA v8.0

SAP ASE용 SSMA의 v8.0 릴리스는 품질 및 변환 메트릭을 개선하도록 설계된 대상 수정 사항으로 향상되었습니다. 또한 이 릴리스에서는 다음과 같은 새로운 기능을 제공합니다.

* Azure **SQL 데이터베이스 관리 인스턴스를** 대상으로 지원합니다. 이제 Azure SQL Database 관리 인스턴스를 대상으로 하는 새 프로젝트를 만들 수 있습니다.

  ![SQL DB MI 프로젝트](../media/ssma-newproject-sqldbmi.png)

* 변환 후 **수정 고문**. 자세한 내용은 [여기를 참조하십시오.](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 예비 데이터베이스/스키마 선택.

  소스에 연결할 때 사용자는 이제 관심 있는 데이터베이스/스키마를 선택할 수 있습니다. 마이그레이션하려는 스키마만 선택하면 초기 연결 시 시간을 절약하고 전반적인 SSMA 성능을 향상시킬 수 있습니다.

  ![SSMA 필터 개체](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

SAP ASE용 SSMA의 v7.10 릴리스는 글로벌 요구 사항의 변화를 충족하기 위해 추가보안 및 개인 정보 보호를 제공하도록 설계된 대상 수정 사항으로 향상되었습니다.

## <a name="ssma-v79"></a>SSMA v7.9

SAP ASE용 SSMA의 v7.9 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 품질 및 전환 측정항목을 개선하는 타겟팅된 수정사항입니다.
* SSMA 명령줄에서 지원하여 데이터 유형 매핑 및 프로젝트 기본 설정을 변경합니다.
* SQL 서버 통합 서비스(SSIS)를 사용하여 데이터 마이그레이션을 지원합니다. 스키마를 변환한 후 오른쪽 클릭 컨텍스트 메뉴 옵션을 사용하여 SSIS 패키지를 만들 수 있습니다.
* SSMA의 Azure SQL Database 연결 대화 상자도 완전히 정규화된 서버 이름을 지정하도록 변경되었습니다. 이전 버전의 SSMA에서는 프로젝트 설정 내에서 Azure SQL Database 접두사를 명시적으로 언급해야 했습니다.

## <a name="ssma-v78"></a>SSMA v7.8

SAP ASE용 SSMA의 v7.8 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* **프로젝트 설정에서**강조 표시된 유형 매핑 변경.
* 사용자가 원격 분석을 사용하지 않도록 설정하는 기능입니다.

## <a name="ssma-v77"></a>SSMA v7.7

SAP ASE용 SSMA의 v7.7 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* SAP ASE용 SSMA는 품질 및 변환 메트릭을 개선하는 대상 수정 사항으로 개선되었습니다.
* 인기 있는 수요에 따라 SAP ASE용 SSMA의 32비트 버전이 돌아왔습니다. 이전 구현(v7.4 이전)과 비교하여 두 개의 설치 관리자 패키지가 있지만 나란히 설치할 수는 없습니다. 따라서 사용 가능한 연결 구성 요소에 따라 가장 적합한 버전을 선택해야 합니다. 가능하면 항상 64비트 버전을 사용하는 것이 좋습니다.

## <a name="ssma-v76"></a>SSMA v7.6

SAP ASE용 SSMA의 v7.6 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 품질 및 변환 메트릭을 개선하고 SQL Server 2017(공개 미리 보기)을 지원하는 대상 수정 프로그램입니다. Windows 및 Linux에서 SQL Server 2017에 대한 지원은 공개 미리 보기중이며 프로덕션 마이그레이션에 사용해서는 안 됩니다.
* Sybase 함수 변환 지원.

## <a name="ssma-v75"></a>SSMA v7.5

SAP ASE용 SSMA의 v7.5 릴리스(이전 Sybase용 SSMA)에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 장애가 있는 사용자에게 더 큰 접근성을 보장하기 위한 몇 가지 개선 사항.
* 구문에 `CREATE OR REPLACE` 대 한 지원입니다.

## <a name="ssma-v74"></a>SSMA v7.4

Sybase용 SSMA의 v7.4 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 이제 소스 및 대상에서 스키마 개체 검색 중에 **쿼리 시간 지정** 옵션을 사용할 수 있습니다.

  ![쿼리 시간 시간 변경 옵션](../media/query-timeout_red.png)
* 고객 피드백을 기반으로 타겟팅된 수정을 통해 품질 및 전환 지표가 개선되었습니다.

  > [!IMPORTANT]
  > .NET 4.5.2는 SSMA v7.4를 설치하기 위한 필수 조건입니다. 또한 v7.4부터 는 SSMA의 32비트 버전이 단종됩니다.

## <a name="ssma-v73"></a>SSMA v7.3

Sybase용 SSMA의 v7.3 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

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

Sybase용 SSMA의 v7.2 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 고객 피드백을 기반으로 타겟팅된 수정을 통해 품질 및 전환 지표를 개선했습니다.
* 원격 분석 개선으로 고객 문제를 해결하고 SSMA의 전환율을 개선하기 위해 더 나은 데이터 포인트를 제공합니다.

## <a name="ssma-v71"></a>SSMA v7.1

Sybase용 SSMA의 v7.1 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* Windows 및 Linux CTP1의 SQL Server 2017은 이제 마이그레이션을 위해 지원되는 대상 플랫폼입니다. 이 기능은 기술 미리 보기에 있으며 SQL 서버를 대상으로 하는 스키마 및 데이터 이동을 지원합니다.
* 사용 가능한 즉시 최신 버전의 SSMA를 다운로드할 수 있는 자동 업데이트 지원.
* 이제 SSMA 설치 가능 바이너리가 Windows Installer 패키지 파일(.msi)을 통해 배달됩니다.

## <a name="may-2016"></a>2016년 5월

Sybase용 SSMA 2016년 5월 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* SQL Server 2016에 대한 지원이 추가되었습니다.
* .NET 2.0에 대한 설치 관리자 검사를 제거했습니다.
* 확장 팩 종속성을 .NET 3.5에서 .NET 4.0으로 업데이트했습니다.
* SSMA 콘솔에 대한 수정 `save-project` 및 `open-project` 명령.
* SSMA 콘솔에 대한 `securepassword` 고정 명령.
* 초기 로드를 위한 객체 수를 고정했습니다.
* 전역 설정에서 버그를 수정했습니다.

## <a name="march-2016"></a>2016년 3월

Sybase용 SSMA의 2016년 3월 미리 보기 릴리스는 SQL Server 2016으로의 마이그레이션에 대한 지원을 추가합니다.

## <a name="january-2016"></a>2016년 1월

Sybase용 SSMA의 2016년 1월 유지 관리 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* SSMA(RFC 5706203)에 보기 로그 메뉴 항목이 추가되었습니다.
* 원격 분석이 추가되었습니다.

## <a name="july-2014"></a>2014 년 7 월

Sybase용 SSMA 의 2014년 7월 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 향상된 Azure SQL DB 코드 변환.
* Azure SQL DB를 지원하도록 확장 팩 기능을 스키마로 이동했습니다.
* 10k 이상의 개체가 있는 데이터베이스에 대해 테스트된 성능 향상이 추가되었습니다.
* 많은 수의 개체를 처리하기 위한 UI 개선 사항이 추가되었습니다.
* 잘 알려진 LOB 스키마를 강조 표시하는 기능이 추가되어 변환시 무시할 수 있습니다.
* 전환 속도 개선이 추가되었습니다.
* UI에서 개체 수를 표시하는 기능을 추가했습니다.
* 보고서 크기를 25% 이상 줄였습니다.
* 구문 분석되지 않은 구문에 대한 오류 메시지가 개선되었습니다.

## <a name="april-2014"></a>2014년 4월

Sybase용 SSMA 의 2014년 4월 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* MS SQL Server 2014의 지원이 추가되었습니다.
* Azure로의 변환과 관련된 버그를 수정했습니다.
* IE 10의 보이지 않는 보고서 페이지와 관련된 버그를 수정했습니다.

## <a name="january-2012"></a>2012년 1월

Sybase용 SSMA 의 2012년 1월 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 롤백 트리거 변환에 대한 지원이 추가되었습니다.
* 변환 `@@ROWCOUNT` 및 `@@ERROR` 동일한 `SET` 명령문에 대한 수정 프로그램을 제공했습니다.

## <a name="july-2011"></a>2011년 7월

Sybase용 SSMA의 2011년 7월 릴리스는 데이터 마이그레이션 중에 향상된 오류 보고를 제공합니다.

## <a name="april-2011"></a>2011년 4월

Sybase용 SSMA 의 2011년 4월 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)][ [!INCLUDE [ssSQL11](../../includes/ssSQL11-md.md)] 및 Azure SQL을 지원하는 [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)]통합된 "Sybase용 SSMA" 제품입니다.
* 로 연결 및 마이그레이션에 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]대한 지원이 추가되었습니다.
* Sybase 데이터베이스를 Azure SQL로 변환하고 마이그레이션하는 새 기능을 추가했습니다.
* 향상된 클라이언트 측 데이터 마이그레이션 엔진으로 데이터의 병렬 마이그레이션을 지원합니다.
* 단순 및 대량 기록 복구 모델로 데이터 마이그레이션 성능이 향상되었습니다.
* 대/소문자 구분 Sybase 데이터베이스를 대/소문자 구분 SQL Server로 올바르게 변환하고 마이그레이션하는 기능을 추가했습니다.
* SQL Server ANSI 조인 문에 Sybase ASE 비 ANSI 조인 문을 변환하기 위한 추가 지원이 DELETE 및 UPDATE 문으로 확장되었습니다.
* Sybase ASE ODBC 공급자 및 Sybase ASE ADO.NET 공급자를 사용하여 Sybase ASE 서버에 연결하기 위한 추가 연결 옵션을 제공했습니다.
* 확장 팩의 일부로 설치되는 Sybase 에뮬레이션 함수를 포함하는 별도의 데이터베이스(확장 `SysDB`팩)에 대한 종속성을 제거했습니다.
* [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] 클러스터에 Sybase 확장 팩에 SSMA를 설치하는 기능이 추가되었습니다.
* 이전 버전의 SSMA(v4.0 및 v4.2)에서 만든 프로젝트의 이전 버전 호환성이 추가되었습니다.
* 이전 버전의 SSMA(v4.0 및 v4.2)와 함께 Sybase v5.0 제품(SxS)에 대한 SSMA를 설치하는 기능이 추가되었습니다.

## <a name="july-2010"></a>2010년 7월

7 월 2010 Sybase에 대 한 SSMA의 릴리스 추가:

* SQL Server 2008 R2로 마이그레이션하기 위한 지원.
* 명령줄 실행을 위한 새로운 SSMA 콘솔 응용 프로그램입니다.
* 서버 측 및 클라이언트 측 데이터 마이그레이션 엔진을 모두 사용하여 데이터 마이그레이션을 지원합니다.
* 데이터 마이그레이션에서 "사용자 지정 SELECT" 문을 지원합니다.
* Sybase ASE 15.0.3 및 15.5에서 마이그레이션을 지원합니다.

## <a name="june-2008"></a>2008년 6월

Sybase용 SSMA 의 2008년 6월 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 데이터베이스 개체 변환 및 SSMA에서 만든 데이터 마이그레이션을 자동으로 테스트하는 SSMA 테스터를 추가했습니다. 모든 SSMA 마이그레이션 단계가 완료되면 SSMA Tester를 사용하여 변환된 개체가 동일한 방식으로 작동하고 모든 데이터가 제대로 전송되었는지 확인합니다.
* SQL 이전 변환을 추가했습니다. 이제 사용자는 변환에 사용할 각 소스 프로시저에 대한 임시 테이블(및 기타 개체) 선언을 지정할 수 있습니다.
* 개체 변환이 추가되었습니다.
  * 조인 변환이 수정되었습니다.
  * 절별로/그룹화하지 않고 집계 및 비집계.
  * 문이 `IDENTITY` 있는 `SELECT INTO` 함수입니다.
  * 데이터 전용 잠긴 데이터 제약 조건 및 인덱스입니다.
  * 에서 `SELECT INTO`만든 임시 테이블
  * 임시 테이블에 대한 제약 조건 / 인덱스.
  * 새 [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] 날짜 시간 형식이 지원됩니다.
  * Sybase 15.0 연결 및 데이터 형식이 지원됩니다.

## <a name="may-2007"></a>2007년 5월

Sybase에 대 한 SSMA의 5 월 2007 릴리스 추가:

* 프로젝트를 저장할 때 데이터베이스 콘텐츠를 더 빠르게 로드할 수 있는 기능입니다.
* SQL Server 형식의 SQL 모드에서 사용자가 입력한 주석에 대한 지원입니다.
* 개체 변환의 개선.

## <a name="november-2006"></a>2006년 11월

Sybase용 SSMA의 2006년 11월 릴리스에는 다음과 같은 변경 사항이 포함되어 있습니다.

* 새 전역 설정이 추가되었습니다.
  * 편집기 창에 줄 번호를 표시하도록 선택할 수 있습니다.
  * SSMA를 구성하여 중복 개체를 바꾸라는 메시지를 표시하거나 스키마 변환 중에 중복 개체를 항상 또는 교체하지 않을 수 있습니다.
* SSMA가 다음 상황을 처리하는 방법을 구성할 수 있는 새 변환 옵션이 추가되었습니다.
  * 이진 문자열을 포함하는 `CAST` 또는 `CONVERT` 문입니다.
  * 같음 식에서 null 값을 확인합니다.
  * 프록시 테이블입니다.
  * 에 대한 `RAISERROR`사용자 메시지 오류 번호
  * `UPDATE`확인되지 않은 식별자를 포함하는 문입니다.
* SSMA가 [!INCLUDE [ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 범위를 벗어난 날짜를 처리하는 방법을 지정할 수 있는 새 마이그레이션 옵션을 추가했습니다.
* 가독성을 향상하기 위해 코드의 서식을 지정하는 **SQL** 탭에 **서식이 지정된 SQL** 설정을 추가했습니다.
* 다음과 같은 버그 수정 사항:
  * 이제 SSMA는 `LOCK TABLE <table> IN { SHARED | EXCLUSIVE } MODE` 테이블의 `TABLOCK` 후속 `TABLOCKX` `SELECT` 쿼리에 a 또는 힌트를 추가하여 문을 변환합니다.
  * 이제 문자 식에 이진 형식을 사용할 때 필요한 캐스트가 추가됩니다.
  * 메모리 및 성능 향상.

## <a name="july-2006"></a>2006년 7월

SSMA for Sybase의 2006년 7월 릴리스가 첫 버전입니다.

## <a name="see-also"></a>참고 항목

[Sybase&#40;SybaseToSQL&#41;대한 SSMA를 시작하기](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
