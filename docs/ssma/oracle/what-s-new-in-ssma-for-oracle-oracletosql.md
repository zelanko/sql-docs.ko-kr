---
title: Oracle 용 SSMA의 새로운 기능 (OracleToSQL) | Microsoft Docs
description: 각 릴리스에 대 한 Oracle (OracleToSQL)에 대 한 변경 SQL Server Migration Assistant 내용에 대해 알아봅니다.
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 6/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
ms.author: alexiva
ms.openlocfilehash: 5d1a12d41d7d25154998f39be136266631b6d421
ms.sourcegitcommit: e572f1642f588b8c4c75bc9ea6adf4ccd48a353b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84779560"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>Oracle 용 SSMA의 새로운 기능 (OracleToSQL)

이 문서에서는 각 릴리스의 Oracle 변경 내용에 대 한 SSMA (SQL Server Migration Assistant)를 나열 합니다.

## <a name="ssma-v810"></a>SSMA v 8.10

Oracle 용 SSMA의 v 8.10 릴리스에는 다음과 같은 변경 내용 뿐만 아니라 약간의 성능 향상이 포함 되어 있습니다.

* 인덱스 구성 테이블의 테스터 문제에 대 한 수정
* 확장 팩의 확장 저장 프로시저 이름에 대 한 수정

## <a name="ssma-v89"></a>SSMA v 8.9

Oracle 용 SSMA 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 동적 SQL 문자열 리터럴 변환
* `LAG`, `FIRST_VALUE` 및 `LAST_VALUE` 분석 함수 변환
* 기본 DDL에 대 한 지원 추가 `ALTER TRIGGER` / `ALTER INDEX` (설정/해제 등)
* 기본 제공 함수 이름과 일치 하는 열에 대 한 변환 향상
* 사용할 수 있는 열에 대 한 필터링 된 고유 인덱스 생성 `NULL`
* Azure SQL Data Warehouse에 대 한 변수 선언 변환 향상
* 프로젝트 이름에서 특수 문자를 사용 하 여 문제 해결

## <a name="ssma-v88"></a>SSMA v 8.8

Oracle 용 SSMA의 v 8.8 릴리스에는 다음이 포함 됩니다.

* SQL Server 개체 동기화 안정성 향상
* 평가 및 변환 중 GUI 성능 향상
* 분석 절의 변환 개선 `OVER PARTITION`
* 분석 함수에 대 한 새 변환 `LEAD`
* 하위 쿼리 팩터링 절의 새 변환
* `REPLICATE`Azure SQL Data Warehouse에 대 한 새 배포 옵션
* 변환 성능을 향상 시키기 위해 새로운 Oracle 구문 파서

## <a name="ssma-v87"></a>SSMA v 8.7

Oracle 용 SSMA의 v2.0 릴리스에는 그래픽 사용자 인터페이스의 일부 수정 및 성능 향상 기능이 있습니다.

또한 이제 Oracle 용 SSMA는 ' 고급 개체 선택 ' 대화 상자에서 유효성 상태를 기준으로 개체를 필터링 할 수 있습니다.

> [!IMPORTANT]
> SSMA v 8.5 이상에서 .NET 4.7.2는 설치 필수 구성 요소입니다. 이 버전을 설치 해야 하는 경우 [여기](https://dotnet.microsoft.com/download/dotnet-framework/net472)에서 런타임 파일을 다운로드할 수 있습니다.

## <a name="ssma-v86"></a>SSMA v 8.6

사용자가 변환 된 코드에서 SSMA 확장 속성을 생략할 수 있도록 하는 설정을 추가 하 여 Oracle 용 SSMA의 hyper-v 8.6 릴리스를 향상 시켰습니다.

이 설정을 활용 하려면 Oracle 용 ssma에서 **도구**  >  **프로젝트 설정**  >  **일반**  >  **변환**으로 이동한 다음 **기타**에서 **확장 속성 생략** 설정의 값을 **예**로 업데이트 합니다.

![확장 속성 설정 생략](../oracle/media/ssma-omit-extended-properties.png)

또한 Oracle 용 SSMA는 이제 절의 구문 분석을 향상 시킵니다 `XMLTABLE` .

> [!IMPORTANT]
> SSMA v 8.5 이상에서 .NET 4.7.2는 설치 필수 구성 요소입니다. 이 버전을 설치 해야 하는 경우 [여기](https://dotnet.microsoft.com/download/dotnet-framework/net472)에서 런타임 파일을 다운로드할 수 있습니다.

## <a name="ssma-v85"></a>SSMA v 8.5

Oracle 용 SSMA의 v 8.5 릴리스는 유용성 및 성능을 향상 시 키도 록 설계 된 대상 수정 집합과 함께 Azure Active Directory 인증 및 SQL server의 JSON 기능에 대 한 기본 지원을 지원 하 여 향상 되었습니다.

또한 Oracle 용 SSMA는 다음에 대 한 지원으로 향상 되었습니다.

* 검색을 위해 선택 된 개체 수를 990으로 제한 (Oracle의 `WHERE .. IN (..)` 절 제한은 1000 항목).
* 에서로 데이터 `RAW` 마이그레이션 `UNIQUEIDENTIFIER`
* 절을 구문 분석 하는 중 `PARALLEL_ENABLE` 입니다.

마지막으로, Oracle 용 SSMA의 v 8.5 릴리스는 이제 다음을 제공 합니다.

* 변환 된 패키지 상수의 성능이 개선 되었습니다.
* .NET의 Oracle Data Provider 버전 19.5.0에 대 한 업데이트입니다.

> [!IMPORTANT]
> SSMA v 8.5를 사용 하는 경우 .NET 4.7.2 설치 필수 구성 요소입니다. 이 버전을 설치 해야 하는 경우 [여기](https://dotnet.microsoft.com/download/dotnet-framework/net472)에서 런타임 파일을 다운로드할 수 있습니다.

## <a name="ssma-v84"></a>SSMA v 8.4

Oracle 용 SSMA의 v 8.4 릴리스는 SQL Server 2016 이상 버전에 대 한 액세스 가능성 문제를 해결 하 고 max index 열 (16 대신 32을 허용 하도록)과 관련 된 버그를 수정 하도록 설계 된 대상 수정 기능을 사용 하 여 향상 되었습니다.

또한 Oracle 용 SSMA 릴리스는 `SYS_REFCURSOR` 저장 프로시저 매개 변수로의 변환을 추가 `OUT` 합니다.

> [!IMPORTANT]
> SSMA 버전 7.4 ~ 8.4을 사용 하 여 .NET 4.5.2는 설치 필수 구성 요소입니다.

## <a name="ssma-v83"></a>SSMA v 8.3

Oracle 용 SSMA의 v2.0 릴리스는 품질 및 변환 메트릭을 향상 시 키도 록 설계 된 대상 수정 기능으로 향상 되었습니다. 또한 Oracle 용 SSMA 릴리스는 다음과 같은 수정 사항을 제공 합니다.

* 접근성 문제를 해결 합니다.
* SQL Server 형식에 대 한 기본 지원을 추가 `hierarchyid` 합니다.
* 동의어를 통해 호출 되는 함수에 대 한 알 수 없는 반환 형식 문제를 해결 합니다.
* ODP.NET을 v 19.3로 업데이트 합니다.

## <a name="ssma-v82"></a>SSMA v 8.2

Oracle 용 SSMA의 v 8.2 릴리스는 다음과 같이 향상 되었습니다.

* 에 대 한 지원을 추가 `DBMS_OUTPUT.ENABLE` / `DISABLE` 합니다.
* `CAST AS FLOAT` `BINARY_FLOAT` `BINARY_DOUBLE` 기본 데이터 마이그레이션 쿼리에서 및 열을 제거 합니다.
* 현재 값이 변경 된 경우 시퀀스 새로 고침을 수정 합니다.
* 이름이 같은 열이 있는 경우 의사 열 (등)의 잘못 해석 관련 된 버그를 수정 `ROWNUM` 합니다.
* 모호 하지 않은 식별자로 루프를 변환 하는 동안 발생 하는 충돌을 해결 `FOR` 합니다.

또한이 버전에는 품질 및 변환 메트릭을 개선 하기 위해 설계 된 수정 내용 집합 뿐만 아니라에 대 한 수정 프로그램도 포함 됩니다.

* 데이터 마이그레이션 후 사용 하지 않도록 설정 된 비클러스터형 인덱스에 문제가 있습니다.
* 자동 설치 중에 .NET Framework를 검색 합니다.
* 새 버전이 다운로드 될 때 발생 하는 일시적인 충돌입니다.

> [!NOTE]
> 자동 업데이트의 알려진 문제로 인해 SSMA v 8.1에서 v 8.2로 업데이트 하지 못할 수 있습니다. 이 오류가 발생 하는 경우 새 버전을 다운로드 하 고 수동으로 설치 하세요.

## <a name="ssma-v81"></a>SSMA v 8.1

Oracle 용 SSMA의 v2.0 릴리스는 품질 및 변환 메트릭을 향상 시 키도 록 설계 된 대상 수정 기능으로 향상 되었습니다.

> [!NOTE]
> 자동 업데이트의 알려진 문제로 인해 SSMA v 8.0에서 v 8.1로의 업데이트가 실패할 수 있습니다. 이 오류가 발생 하는 경우 새 버전을 다운로드 하 고 수동으로 설치 하세요.

## <a name="ssma-v80"></a>SSMA v 8.0

Oracle 용 SSMA의 v 8.0 릴리스는 품질 및 변환 메트릭을 개선 하기 위해 설계 된 대상 수정 기능으로 향상 되었습니다. 또한이 릴리스는 다음과 같은 새로운 기능을 제공 합니다.

* 대상으로 **Azure SQL Database Managed Instance** 지원. 이제 Azure SQL Database Managed Instance를 대상으로 하는 새 프로젝트를 만들 수 있습니다.

  ![SQL DB MI 프로젝트](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > Oracle 용 SSMA 확장 팩도 Azure SQL Database Managed Instance에서 원격 설치를 허용 하도록 업데이트 되었습니다.
  >
  > ![Oracle 용 SSMA 확장 팩](../media/ssma-oracle-ext-pack.png)

  Azure SQL Database Managed Instance를 대상으로 지정 하는 경우 테스터 및 서버 쪽 데이터 마이그레이션을 비롯 한 일부 기능이 지원 되지 않습니다. 자세한 내용은 [여기](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/)서 확인할 수 있습니다.

* 변환 후 **수정 관리자**입니다. [여기](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)에서 자세히 알아보세요.

* 예비 데이터베이스/스키마 선택.

  원본에 연결할 때 사용자는 이제 원하는 데이터베이스/스키마를 선택할 수 있습니다. 마이그레이션하려는 스키마만 선택 하면 초기 연결 중에 시간이 절약 되 고 전체 SSMA 성능이 향상 됩니다.

  ![SSMA 필터 개체](../media/ssma-filter-objects.png)

* 관리 되는 공식 .NET 드라이버를 사용 하 여 Oracle에 연결 하는 기능입니다. OCI 드라이버는 더 이상 Oracle 용 SQL Server Migration Assistant를 사용 하기 위한 필수 구성 요소가 아닙니다.

* `ROWID` `UROWID` 기본적으로 및에 매핑할 수 `VARCHAR` 있습니다. `uniqueidentifier`명시적 열에 대 한 데이터 마이그레이션을 수용 하기 위해에서로 변경 되었습니다 `ROWID` .

## <a name="ssma-v710"></a>SSMA v 7.10

Oracle 용 SSMA 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 글로벌 요구 사항에 대 한 변경 내용을 충족 하기 위해 추가 보안 및 개인 정보 보호를 제공 하도록 설계 된 대상 수정
* 계층적 쿼리와 관련 된 변환 향상

## <a name="ssma-v79"></a>SSMA v 7.9

Oracle 용 SSMA 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 품질 및 변환 메트릭을 개선 하는 대상 수정
* Oracle에서 SQL Server로 "Continue" 문을 마이그레이션할 수 있도록 지원 합니다.
* SSMA 명령줄에서 데이터 형식 매핑 및 프로젝트 기본 설정을 변경 하는 기능을 지원 합니다.
* SQL Server Integration Services (SSIS)를 사용 하 여 데이터 마이그레이션을 지원 합니다. 스키마를 변환한 후에는 마우스 오른쪽 단추를 클릭 하 여 상황에 맞는 메뉴 옵션을 사용 하 여 SSIS 패키지를 만들 수 있습니다.
* 또한 SSMA의 Azure SQL Database 연결 대화 상자가 정규화 된 서버 이름을 지정 하도록 변경 되었습니다. 이전 버전의 SSMA에서는 Azure SQL Database 접두사가 프로젝트 설정 내에서 명시적으로 언급 되어야 했습니다.

## <a name="ssma-v78"></a>SSMA v 7.8

Oracle 용 SSMA의 v 7.8 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 지원:
  * 절에 대 한 행 식 `IN` 입니다.
  * 암시적 형식 캐스트입니다.
  * `UID`Azure SQL Database에 대 한 변환입니다.
* **프로젝트 설정**에서 강조 표시 된 형식 매핑을 변경 합니다.
* 사용자가 원격 분석을 사용 하지 않도록 설정할 수 있는 기능입니다.

## <a name="ssma-v77"></a>SSMA v 7.7

Oracle 용 SSMA 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* Oracle 용 SSMA는 품질 및 변환 메트릭을 개선 하는 대상 수정 기능으로 향상 되었습니다.
* 인기 있는 수요에 따라 Oracle 용 SSMA의 32 비트 버전이 다시 사용 됩니다. 이전 구현에 비해 (v 7.4 이전)에는 두 개의 설치 관리자 패키지가 있지만 함께 설치할 수는 없습니다. 따라서 사용 중인 연결 구성 요소에 따라 가장 적합 한 버전을 선택 해야 합니다. 가능 하면 항상 64 비트 버전을 사용 하는 것이 좋습니다.
* SQL Server 2017 지원은 이제 Linux에서 지원 되는 Oracle 확장 팩 (새 원격 설치 옵션)을 사용 하 여 공식적으로 지원 됩니다. 테스터 및 서버 쪽 데이터 마이그레이션 기능이 지원 되지 않으므로 Linux에 설치 된 경우 확장 팩 기능이 제한 됩니다.
* Oracle 용 ssma를 사용 하면 구체화 된 뷰를 일반 테이블로 마이그레이션할 수 있습니다 ( **프로젝트 설정**동기화의 설정을 통해 구성 가능,  ->  **Synchronization**  ->  **구체화 된 뷰에 대 한 지원 테이블 검색**).

## <a name="ssma-v76"></a>SSMA v 7.6

Oracle 용 SSMA의 v 7.6 릴리스는 품질 및 변환 메트릭과 SQL Server 2017 (공개 미리 보기)에 대 한 지원을 제공 하는 대상 수정 기능으로 개선 되었습니다. Windows 및 Linux에서 SQL Server 2017에 대 한 지원은 공개 미리 보기 상태 이며 프로덕션 마이그레이션에 사용할 수 없습니다.

## <a name="ssma-v75"></a>SSMA v 7.5

Oracle 용 SSMA 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 장애가 있는 사용자에 게 더 많은 접근성을 보장 하기 위해 몇 가지 향상 된 기능으로 향상 되었습니다.
* 고객 의견을 바탕으로 데이터 마이그레이션 중에 날짜 및 부동 데이터 형식의 처리를 개선 하는 등의 대상 수정 사항으로 품질 및 변환 메트릭을 개선 하도록 업데이트 되었습니다.

## <a name="ssma-v74"></a>SSMA v 7.4

Oracle 용 SSMA의 v 7.4 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 이제 Oracle 용 SSMA는 Azure SQL Data Warehouse를 마이그레이션하기 위한 대상 플랫폼으로 지원 합니다.

  ![새 프로젝트 창](../media/new-project.png)
  * 에서는 다음 이미지에 표시 된 것 처럼 데이터 웨어하우스 저장소 옵션을 지원 합니다.

  ![데이터 웨어하우스의 저장소 옵션](../media/storage-options_red.png)
  * 에서는 다음 이미지에 표시 된 것 처럼 데이터 배포 옵션을 지원 합니다.

  ![데이터 웨어하우스의 데이터 배포](../media/data-distribution_red.png)

* 이제 원본 및 대상에서 스키마 개체를 검색 하는 동안 **쿼리 제한 시간** 옵션을 사용할 수 있습니다.

  ![쿼리 제한 시간 옵션](../media/query-timeout_red.png)

* 사용자 의견에 따라 대상 수정으로 품질 및 변환 메트릭이 개선 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2은 SSMA v 7.4를 설치 하기 위한 필수 구성 요소입니다. 또한 v 7.4부터 SSMA의 32 비트 버전이 중단 됩니다.

## <a name="ssma-v73"></a>SSMA v 7.3

Oracle 용 SSMA 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 고객 의견을 기반으로 하는 대상 픽스로 품질 및 변환 메트릭이 개선 되었습니다.
* SSMA 확장성 프레임 워크는 다음 항목을 통해 노출 됩니다.
  * SQL Server Data Tools (SSDT) 프로젝트로 기능을 내보냅니다.
    * 이제 SSMA에서 SSDT 프로젝트로 스키마 스크립트를 내보낼 수 있습니다. 스키마 스크립트를 사용 하 여 추가 스키마 변경을 수행 하 고 데이터베이스를 배포할 수 있습니다.

      ![SSDT 프로젝트로 저장 명령](../media/export-schema-scripts_red.png)
  * 사용자 지정 변환을 수행 하기 위해 SSMA에서 사용할 수 있는 라이브러리입니다.
    * 이제 SSMA에서 이전에 처리 되지 않은 사용자 지정 구문 변환과 변환을 처리할 수 있는 코드를 생성할 수 있습니다.
      * 사용자 지정 변환기를 구성 하는 방법에 대 한 지침은이 블로그 게시물에서 [SQL Server Migration Assistant의 변환 기능을 확장](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)하는 데 사용할 수 있습니다.
      * 이 [블로그 게시물](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)에서 변환할 샘플 프로젝트를 다운로드 합니다.

## <a name="ssma-v72"></a>SSMA v 7.2

Oracle 용 SSMA 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 고객 의견을 기반으로 하는 대상 픽스로 품질 및 변환 메트릭이 개선 되었습니다.
* 향상 된 원격 분석을 통해 고객 문제를 해결 하 고 SSMA의 변환 속도를 개선할 수 있는 더 나은 데이터 요소를 제공 합니다.

## <a name="ssma-v71"></a>SSMA v 7.1

Oracle 용 SSMA의 v 7.1 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 이제 Windows 및 Linux CTP1의 SQL Server 2017는 마이그레이션에 지원 되는 대상 플랫폼입니다. 이 기능은 technical preview 이며 SQL server를 대상으로 하는 스키마 및 데이터 이동을 허용 합니다.
* 이제 SSMA가 자동 업데이트를 지원 하 여 최신 버전의 SSMA를 사용할 수 있는 즉시 다운로드 합니다.
* 이제 Windows Installer 패키지 파일 (.msi)을 통해 SSMA를 설치할 수 있는 이진 파일이 제공 됩니다.

## <a name="may-2016"></a>2016년 5월

Oracle의 SSMA 릴리스 2016에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* SQL Server 2016에 대 한 지원이 추가 되었습니다.
* Oracle 플래시 백 archive 테이블을 SQL Server 임시 테이블로 변환 했습니다.

  > [!NOTE]
  > SSMA는 Oracle 플래시 백 데이터 보관 테이블의 기록 데이터를 복사 하지 않습니다. 따라서 마이그레이션 프로세스 중에 기록 데이터를 수동으로 복사 해야 합니다. 또한 시스템 테이블로 처리 되기 때문에 SSMA가 SQL Server 메타 데이터 탐색기에 기록 테이블을 표시 하지 않지만 SQL Server Management Studio에서 기록 테이블을 볼 수 있습니다.
  >
  > SQL Server 2016은 다음을 비롯 한 몇 가지 Oracle 플래시 백 기능을 지원 하지 않습니다.
  >
  >   * Oracle 플래시 백 트랜잭션 쿼리
  >   * `DBMS_FLASHBACK`패키지
  >   * 플래시 백 트랜잭션
  >   * 플래시 백 데이터 보관
  >   * 플래시 백 테이블
  >   * 플래시 백 Drop
  >   * 플래시 백 데이터베이스

* Oracle VPD 정책을 SQL Server 정책 개체 (Oracle 용 행 수준 보안)로 변환 했습니다.
* Oracle의 초기 로드 시간을 줄였습니다.
* 파서 및 확인자를 개선 했습니다.
* .NET 2.0에 대 한 설치 관리자 검사가 제거 되었습니다.
* .NET 3.5에서 .NET 4.0으로 확장 팩 종속성을 업데이트 했습니다.
* `save-project` `open-project` Ssma 콘솔에 대 한 및 명령이 수정 되었습니다.
* `securepassword`SSMA 콘솔에 대 한 고정 명령입니다.
* 초기 로드에 대 한 개체 계산을 수정 했습니다.
* Oracle에 대 한 문자 데이터 형식의 변환을 수정 했습니다.
* 전역 설정에서 버그가 수정 되었습니다.

## <a name="march-2016"></a>2016년 3월

Oracle 용 SSMA의 3 월 2016 preview 릴리스는 다음에 대 한 지원을 추가 했습니다.

* SQL Server 2016로의 마이그레이션.
* Oracle 행 수준 보안 마이그레이션 (몇 가지 제한 사항이 있음).
* 메모리 테이블의 Oracle을 SQL Server 열 저장소로 마이그레이션

## <a name="january-2016"></a>2016년 1월

Oracle 용 SSMA의 1 월 2014 유지 관리 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 클러스터형 인덱스에 대 한 지원이 추가 되었습니다.
* 저속 Oracle 스키마 쿼리 (RFC 5076207)를 수정 했습니다.
* 콘솔에서 Azure에 연결을 수정 했습니다.
* SSMA에 보기 로그 메뉴 항목을 추가 했습니다 (RFC 5706203).
* 원격 분석 추가.

## <a name="july-2014"></a>2014 년 7 월

Oracle 용 SSMA의 7 월 2014 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* Azure SQL DB에 대 한 지원이 추가 되었습니다.
* 확장 팩 기능을 스키마로 이동 하 여 Azure SQL DB를 지원 합니다.
* Oracle 구체화 뷰에 대 한 지원이 추가 되었습니다.
* SQL Server 2014 메모리 최적화 테이블에 대 한 지원이 추가 되었습니다.
* 과도 한 개체가 포함 된 데이터베이스에 대 한 성능 향상 기능이 테스트 되었습니다.
* 많은 수의 개체를 처리 하기 위한 UI 개선 기능이 추가 되었습니다.
* 잘 알려진 LOB 스키마의 강조 표시를 추가 했습니다.
* 포함 된 변환 속도 향상.
* UI의 개체 수를 표시 하기 위한 지원이 추가 되었습니다.
* 20%를 초과 하 여 보고서 크기를 줄였습니다.
* 구문 분석 되지 않은 구문에 대 한 오류 메시지가 개선 되었습니다.

## <a name="april-2014"></a>2014년 4월

Oracle 용 SSMA의 4 월 2014 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* MS SQL Server 2014에 대 한 지원이 추가 되었습니다.
* Oracle 12 및 쿼리 최적화에 대 한 지원이 추가 되었습니다.
* Azure로의 변환과 관련 된 버그가 수정 되었습니다.
* IE 10의 보이지 않는 보고서 페이지와 관련 된 버그가 수정 되었습니다.

## <a name="january-2012"></a>2012년 1월

Oracle 용 SSMA의 1 월 2012 릴리스는 `RowType` 및 입력 매개 변수에 대 한 지원을에 추가 `RecordType` `NULL` 합니다.

## <a name="july-2011"></a>2011년 7월

Oracle 용 SSMA의 7 월 2011 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* Oracle 시퀀스에서 시퀀스 생성기로의 변환에 대 한 지원이 추가 되었습니다 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] .
* 데이터 마이그레이션 중에 향상 된 오류 보고
* 예약어를 사용 하 여 문의 변환을 개선 했습니다.
* 함수에서 날짜 값의 암시적 변환이 향상 되었습니다.

## <a name="april-2011"></a>4 월 2011

Oracle 용 SSMA의 4 월 2011 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 및를 지 원하는 통합 된 "Oracle 용 SSMA" 제품입니다 [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] .
* 에 연결 및 마이그레이션에 대 한 지원이 추가 되었습니다 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] .
* 데이터의 병렬 마이그레이션을 지 원하는 향상 된 클라이언트 쪽 데이터 마이그레이션 엔진.
* `Simple`및 로그 복구 모델을 사용 하 여 데이터 마이그레이션 성능이 개선 `Bulk` 되었습니다.
* 이전 버전의 SSMA (v 4.0 및 v 4.2)에서 만든 프로젝트의 이전 버전과의 호환성에 대 한 지원이 추가 되었습니다.
* 이전 버전의 SSMA (v 4.0 및 v 4.2)와 함께 Oracle v 5.0 용 SSMA 제품을 함께 설치 하는 기능이 추가 되었습니다.
* 사용자 정의 형식 (하위 형식, `VARRAY` , `NESTED TABLE` , 개체 테이블 및 개체 뷰 포함)과 특수 오류 메시지를 포함 하는 PL/SQL 블록의 용도에 대 한 지원이 추가 되었습니다.

## <a name="july-2010"></a>2010년 7월

Oracle 용 SSMA의 7 월 2010 릴리스 추가 됨:

* SQL Server 2008 R2로의 마이그레이션을 지원 합니다.
* 명령줄 실행을 위한 새 SSMA 콘솔 응용 프로그램입니다.
* 서버 쪽 및 클라이언트 쪽 데이터 마이그레이션 엔진을 모두 사용 하 여 데이터 마이그레이션을 지원 합니다.
* 데이터 마이그레이션에서 "Custom SELECT" 문을 지원 합니다.
* Oracle 11g r 2에서의 마이그레이션 지원.

## <a name="june-2008"></a>6 월 2008

Oracle 용 SSMA의 6 월 2008 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 동의어에 대 한 추가 정보, 구문 분석 된 개체에 대 한 원시 원본, 패널 및 SQL Server 로고 제거 및 레이아웃 지 속성을 비롯 하 여 평가 보고서에 향상 된 기능이 추가 되었습니다.
* 개체 변환에 향상 된 기능이 추가 되었습니다.
  * 패키지 `DBMS_LOB` , `DBMS_SQL` 변환 추가
  * 조인 변환이 수정 되었습니다.
  * 각 필드에 대 한 별도의 변수를 통해 릴리스된 간단한 사례에서 레코드 변환, 컬렉션 및 레코드 변환의 수정
  * 레코드 및 컬렉션 구현의 향상 된 기능.
  * 창 고 집계 함수를 추가 했습니다.
  * `ROLLUP`/`CUBE`절이 추가 되었습니다.
  * 개선 `NEXTVAL` / `CURVAL` .
  * `SET`절, 그룹화 집합 및 그룹화 ID의 열 그룹화가 추가 되었습니다.
  * `MERGE`문이 추가 되었습니다.
  * CLR 데이터 형식이 추가 된 새 datetime 형식 및 레코드와 컬렉션의 변환을 지원 합니다.
* 테스터의 새 기능을 추가 했습니다. 이제 테스터를 사용 하 여 테이블을 개체로 테스트할 수 있습니다. 테스트 사례에서 여러 테스트 가능한 개체의 호출 순서를 변경할 수 있으며, 사용자는 매개 변수 및 반환 값으로 레코드 및 컬렉션을 사용 하 여 프로시저와 함수를 테스트 하 고 사용 된 테이블만 검사 하도록 종속성 분석기를 추가할 수 있습니다.
  
## <a name="august-2007"></a>8 월 2007

Oracle 용 SSMA의 8 월 2007 릴리스 추가 됨:

* 새 테스터 구성 요소를 사용 하 여 변환 된 SQL 코드를 확인 하는 테스트 사례를 만들고 관리 하 고 실행할 수 있습니다.
* Oracle 하위 형식, 컬렉션 및 로컬 모듈의 변환에 대 한 지원이 SQL 변환기에 추가 되었습니다.
* 새 동기화 기능을 사용 하면 SQL Server 데이터베이스와 특정 개체를 동기화 할 수 있습니다.
* 새 변환 옵션입니다.
  
## <a name="april-2007"></a>4 월 2007

Oracle 용 SSMA의 4 월 2007 릴리스는 초기 릴리스입니다.
