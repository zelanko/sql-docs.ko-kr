---
title: D b 2 용 SSMA의 새로운 기능 (DB2ToSQL) | Microsoft Docs
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/27/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
ms.author: jtoland;alexiva
ms.openlocfilehash: 3b3fca46fb5e30cfa446e0ca9de8dc0324d2f7f8
ms.sourcegitcommit: 9afb612c5303d24b514cb8dba941d05c88f0ca90
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82220090"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>D b 2 용 SSMA의 새로운 기능 (DB2ToSQL)

이 문서에서는 각 릴리스의 DB2 변경에 대 한 SSMA (SQL Server Migration Assistant)를 나열 합니다.

## <a name="ssma-v89"></a>SSMA v 8.9

D b 2 용 SSMA의 v 8.9 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 함수 변환에 대 한 수정 `TIMESTAMPDIFF`
* 분할 된 인덱스가 있을 때 인덱스 검색에 대 한 수정
* 기본 인덱스가 다른 스키마에 정의 되어 있는 경우 외래 키 검색 수정
* 기본 제공 함수 이름과 일치 하는 열에 대 한 변환 향상
* 프로젝트 이름에서 특수 문자를 사용 하 여 문제 해결

## <a name="ssma-v88"></a>SSMA v 8.8

D b 2 용 SSMA의 v 8.8 릴리스에는 다음이 포함 됩니다.

* SQL Server 개체 동기화 안정성 향상
* 평가 및 변환 중 GUI 성능 향상
* `ROWID` `varbinary(40)` 데이터 마이그레이션을 용이 하 게 하기 위해에서로의 매핑을 업데이트 했습니다.
* 문의 변환 향상 `SELECT ... FROM NEW/OLD TABLE`
* `ALTER`프로시저 및 함수에 대 한 문의 새로운 변환
* 구조 파괴 할당의 새 변환

## <a name="ssma-v87"></a>SSMA v 8.7

D b 2 용 SSMA의 v2.0 릴리스에는 새 DB2 구문 파서 뿐만 아니라 그래픽 사용자 인터페이스의 사소한 수정 및 성능 향상이 포함 되어 있습니다.

또한 d b 2 용 SSMA는 이제 다음을 제공 합니다.

* LUW의 DB2에서 마이그레이션할 때 외래 키 검색에 대 한 수정 사항입니다.
* 문의 변환이 개선 `SELECT ... FOR UPDATE` 되었습니다.
* MQ 테이블의 함수에 대 한 변환 기능이 향상 `COUNT` 되었습니다.
* 문을 변환 `SAVEPOINT` 합니다.
* 절에서 값에 대 한 DB2's 동작을 에뮬레이트하는 변환입니다 `NULL` `ORDER BY` .
* RESULT SET 문 연결에 대 한 구문 분석 지원.

> [!IMPORTANT]
> SSMA v 8.5 이상에서 .NET 4.7.2는 설치 필수 구성 요소입니다. 이 버전을 설치 해야 하는 경우 [여기](https://dotnet.microsoft.com/download/dotnet-framework/net472)에서 런타임 파일을 다운로드할 수 있습니다.

## <a name="ssma-v86"></a>SSMA v 8.6

사용자가 변환 된 코드에서 SSMA 확장 속성을 생략할 수 있도록 하는 설정을 추가 하 여 d b 2 용 SSMA의 v 8.6 릴리스를 향상 시켰습니다.

이 설정을 활용 하려면 d b 2 용 ssma에서 **도구**  >  **프로젝트 설정**  >  **일반**  >  **변환**으로 이동한 다음 **기타**에서 **확장 속성 생략** 설정의 값을 **예**로 업데이트 합니다.

![확장 속성 설정 생략](../db2/media/ssma-omit-extended-properties.png)

또한 d b 2 용 SSMA는 이제 다음을 제공 합니다.

* 기본 인수 값을 사용 하는 함수 변환에 대 한 수정입니다.
* 함수의 절 구문 분석 기능이 향상 `PARAMETER` 되었습니다.
* 문을 변환 하는 기능 `LEAVE` 입니다.

> [!IMPORTANT]
> SSMA v 8.5 이상에서 .NET 4.7.2는 설치 필수 구성 요소입니다. 이 버전을 설치 해야 하는 경우 [여기](https://dotnet.microsoft.com/download/dotnet-framework/net472)에서 런타임 파일을 다운로드할 수 있습니다.

## <a name="ssma-v85"></a>SSMA v 8.5

D b 2 용 SSMA의 v 8.5 릴리스는 유용성 및 성능을 향상 시 키도 록 설계 된 대상 수정 집합과 함께 Azure Active Directory 인증 및 SQL server의 JSON 기능에 대 한 기본 지원을 지원 하 여 향상 되었습니다.

또한 DB2 용 SSMA는 다음과 같이 향상 되었습니다.

* `GET DIAGNOSTICS`문을 사용 하 여 변환 추가를 지원 `ROW_NUMBER` 합니다.
* 개체 이름 시작 부분에 있는 공백과 관련 된 버그에 대 한 수정 사항이 적용 되지 않습니다.

> [!IMPORTANT]
> SSMA v 8.5를 사용 하는 경우 .NET 4.7.2 설치 필수 구성 요소입니다. 이 버전을 설치 해야 하는 경우 [여기](https://dotnet.microsoft.com/download/dotnet-framework/net472)에서 런타임 파일을 다운로드할 수 있습니다.

## <a name="ssma-v84"></a>SSMA v 8.4

D b 2 용 SSMA 릴리스는 SQL Server 2016 이상 버전에 대 한 액세스 가능성 문제를 해결 하 고 max index 열 (16 대신 32을 허용 하도록)과 관련 된 버그를 수정 하도록 설계 된 대상 수정으로 향상 되었습니다.

> [!IMPORTANT]
> SSMA 버전 7.4 (8.4)을 사용 하 여 .NET 4.5.2는 설치 필수 구성 요소입니다.

## <a name="ssma-v83"></a>SSMA v 8.3

D b 2 용 SSMA의 v2.0 릴리스는 품질 및 변환 메트릭을 향상 시 키도 록 설계 된 대상 수정 기능으로 향상 되었습니다. 또한 d b 2 용 SSMA 릴리스는 다음과 같은 수정 사항을 제공 합니다.

* 접근성 문제를 해결 합니다.
* SQL Server 형식에 대 한 기본 지원을 추가 `hierarchyid` 합니다.
* Z/OS 검색 쿼리에서 TRIM 함수 사용을로 바꿉니다 `RTRIM` / `LTRIM` .
* 사용자가 ' 표준 모드 '에서 연결할 때 패키지 컬렉션을 지정할 수 있도록 허용 `NULLID` 합니다 (기본값).
* 에 대 한 변환을 추가 `CREATE TABLE AS SELECT` 합니다.
* 전역 임시 테이블의 변환을 향상 시킵니다.
* 이름이 충돌 하는 경우 제약 조건에 대 한 테이블의 우선 순위를 지정 하기 위해 개체 고유성 검사의 문제를 해결 합니다.
* `DATE`Z/OS의 및에 대 한 기본 열 값 로드 문제를 해결 `TIMESTAMP` 합니다.
* 유니코드 줄 바꿈 문자 (라고도 함)를 지원 `NEL` 합니다.
* 누락 된 절이 있는 커서 변환 문제를 해결 `RETURN TO` 합니다.
* 레이블 및에 대 한 지원을 추가 `GOTO` 합니다.

## <a name="ssma-v82"></a>SSMA v 8.2

D b 2 용 SSMA의 v 8.2 릴리스는로 향상 되어, SSMA 콘솔 도구에서 Azure SQL Database에 대 한 연결 문제를 해결 하 고, 변환 하는 동안 보기 선언에 COUNT_BIG 열이 누락 되었습니다. 또한이 버전에는 품질 및 변환 메트릭을 개선 하기 위해 설계 된 수정 내용 집합 뿐만 아니라에 대 한 수정 프로그램도 포함 됩니다.

* 데이터 마이그레이션 후 사용 하지 않도록 설정 된 비클러스터형 인덱스에 문제가 있습니다.
* 자동 설치 중에 .NET Framework를 검색 합니다.
* 새 버전이 다운로드 될 때 발생 하는 일시적인 충돌입니다.

> [!NOTE]
> 자동 업데이트의 알려진 문제로 인해 SSMA v 8.1에서 v 8.2로 업데이트 하지 못할 수 있습니다. 이 오류가 발생 하는 경우 새 버전을 다운로드 하 고 수동으로 설치 하세요.

## <a name="ssma-v81"></a>SSMA v 8.1

D b 2 용 SSMA의 v 8.1 릴리스는 품질 및 변환 메트릭을 개선 하기 위해 설계 된 대상 수정 프로그램을 제공 하도록 향상 되었습니다.

> [!NOTE]
> 자동 업데이트의 알려진 문제로 인해 SSMA v 8.0에서 v 8.1로의 업데이트가 실패할 수 있습니다. 이 오류가 발생 하는 경우 새 버전을 다운로드 하 고 수동으로 설치 하세요.

## <a name="ssma-v80"></a>SSMA v 8.0

D b 2 용 SSMA 릴리스는 품질 및 변환 메트릭을 개선 하기 위해 설계 된 대상 수정 기능을 제공 하도록 향상 되었습니다. 또한이 릴리스는 다음과 같은 새로운 기능을 제공 합니다.

* 대상으로 **Azure SQL Database Managed Instance** 지원. 이제 Azure SQL Database Managed Instance를 대상으로 하는 새 프로젝트를 만들 수 있습니다.

  ![SQL DB MI 프로젝트](../media/ssma-newproject-sqldbmi.png)

* 변환 후 **수정 관리자**입니다. [여기](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)에서 자세히 알아보세요.

* 예비 데이터베이스/스키마 선택.

  원본에 연결할 때 사용자는 이제 원하는 데이터베이스/스키마를 선택할 수 있습니다. 마이그레이션하려는 스키마만 선택 하면 초기 연결 중에 시간이 절약 되 고 전체 SSMA 성능이 향상 됩니다.

  ![SSMA 필터 개체](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

D b 2 용 SSMA의 v 7.10 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 글로벌 요구 사항에 대 한 변경 내용을 충족 하기 위해 추가 보안 및 개인 정보 보호를 제공 하도록 설계 된 대상 수정
* 블록의 변환에 대 한 수정 `BEGIN-END` 입니다.

## <a name="ssma-v79"></a>SSMA v 7.9

D b 2 용 SSMA의 v 7.9 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 품질 및 변환 메트릭을 개선 하는 대상 수정
* SSMA 명령줄에서 데이터 형식 매핑 및 프로젝트 기본 설정을 변경 하는 기능을 지원 합니다.
* SQL Server Integration Services (SSIS)를 사용 하 여 데이터 마이그레이션을 지원 합니다. 스키마를 변환한 후에는 마우스 오른쪽 단추를 클릭 하 여 상황에 맞는 메뉴 옵션을 사용 하 여 SSIS 패키지를 만들 수 있습니다.
* 또한 SSMA의 Azure SQL Database 연결 대화 상자가 정규화 된 서버 이름을 지정 하도록 변경 되었습니다. 이전 버전의 SSMA에서는 Azure SQL Database 접두사가 프로젝트 설정 내에서 명시적으로 언급 되어야 했습니다.

## <a name="ssma-v78"></a>SSMA v 7.8

D b 2 용 SSMA의 v 7.8 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* *프로젝트 설정*에서 강조 표시 된 형식 매핑을 변경 합니다.
* 사용자가 원격 분석을 사용 하지 않도록 설정할 수 있는 기능입니다.

## <a name="ssma-v77"></a>SSMA v 7.7

D b 2 용 SSMA의 v 7.7 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 품질 및 변환 메트릭을 개선 하는 대상 수정
* 인기 있는 수요에 따라 d b 2 용 SSMA의 32 비트 버전이 다시 사용 됩니다. 이전 구현과 비교할 때 (v 7.4 이전)에는 두 개의 설치 관리자 패키지가 있지만 함께 설치할 수는 없습니다. 따라서 사용 중인 연결 구성 요소에 따라 가장 적합 한 버전을 선택 해야 합니다. 가능 하면 항상 64 비트 버전을 사용 하는 것이 좋습니다.

## <a name="ssma-v76"></a>SSMA v 7.6

D b 2 용 SSMA 릴리스는 품질 및 변환 메트릭과 SQL Server 2017 (공개 미리 보기)에 대 한 지원을 제공 하는 대상 수정으로 향상 되었습니다. Windows 및 Linux에서 SQL Server 2017에 대 한 지원은 공개 미리 보기 상태 이며 프로덕션 마이그레이션에 사용할 수 없습니다.

## <a name="ssma-v75"></a>SSMA v 7.5

장애가 있는 사용자에 게 더 많은 액세스 가능성을 보장 하기 위해 d b 2 용 SSMA 릴리스는 여러 가지 향상 된 기능으로 향상 되었습니다.

## <a name="ssma-v74"></a>SSMA v 7.4

D b 2 용 SSMA의 v 7.4 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 이제 원본 및 대상에서 스키마 개체를 검색 하는 동안 **쿼리 제한 시간** 옵션을 사용할 수 있습니다.

  ![쿼리 제한 시간 옵션](../media/query-timeout_red.png)

* 사용자 의견에 따라 대상 수정으로 품질 및 변환 메트릭이 개선 되었습니다.

  > [!IMPORTANT]
  > .NET 4.5.2은 SSMA v 7.4를 설치 하기 위한 필수 구성 요소입니다. 또한 v 7.4부터 SSMA의 32 비트 버전이 더 이상 사용 되지 않습니다.

## <a name="ssma-v73"></a>SSMA v 7.3

D b 2 용 SSMA의 v 7.3 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

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

D b 2 용 SSMA의 v 7.2 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 고객 의견을 기반으로 하는 대상 픽스로 품질 및 변환 메트릭이 개선 되었습니다.
* 향상 된 원격 분석을 통해 고객 문제를 해결 하 고 SSMA의 변환 속도를 개선할 수 있는 더 나은 데이터 요소를 제공 합니다.

## <a name="ssma-v71"></a>SSMA v 7.1

D b 2 용 SSMA의 v 7.1 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 이제 Windows 및 Linux CTP1의 SQL Server 2017는 마이그레이션에 지원 되는 대상 플랫폼입니다. 이 기능은 technical preview 이며 SQL server를 대상으로 하는 스키마 및 데이터 이동을 허용 합니다.
* 최신 버전의 SSMA를 사용할 수 있는 즉시 다운로드 하는 자동 업데이트 지원.
* 이제 Windows Installer 패키지 파일 (.msi)을 통해 SSMA를 설치할 수 있는 이진 파일이 제공 됩니다.

## <a name="may-2016"></a>2016년 5월

D b 2 용 SSMA 릴리스 2016 릴리스는 다음과 같은 변경 내용을 포함 하 고 있습니다.

* SQL Server 2016에 대 한 지원이 추가 되었습니다.
* DB2 메모리 내 및 일반 테이블의 변환이 추가 되어 메모리 내 및 hekaton 기능을 SQL Server.
* Db2 액세스 제어를 SQL Server 정책 개체 (DB2 용 행 수준 보안)로 변환 했습니다.
* DB2 시스템 버전 관리 테이블을 SQL Server 임시 테이블로 변환 했습니다.
* DB2 파서 및 해결 프로그램을 개선 했습니다.
* .NET 2.0에 대 한 설치 관리자 검사가 제거 되었습니다.
* \*Db2 설치 관리자에서 불필요 한 .dll을 제거 했습니다.
* `save-project` `open-project` Ssma 콘솔에 대 한 및 명령이 수정 되었습니다.
* `securepassword`SSMA 콘솔에 대 한 고정 명령입니다.
* 초기 로드에 대 한 개체 계산을 수정 했습니다.
* 전역 설정에서 버그가 수정 되었습니다.
  
## <a name="march-2016"></a>2016년 3월

D b 2 용 SSMA의 2016 preview 릴리스는 SQL Server 2016로 마이그레이션에 대 한 지원을 추가 합니다.

## <a name="january-2016"></a>2016년 1월

D b 2 용 SSMA의 1 월 2016 유지 관리 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.
  
* 여러 표준 함수에 대 한 지원이 추가 되었습니다.
* DB2 파서 오류가 수정 되었습니다.
* DB2 v9 zOS 지원 (RFC 5690920)을 수정 했습니다.
* 변환 하는 동안 d b 2의 확인 되지 않은 식별자 오류가 수정 되었습니다.
* SSMA에 보기 로그 메뉴 항목을 추가 했습니다 (RFC 5706203).
* 원격 분석 추가.
  
## <a name="november-2014"></a>2014년 11월

D b 2 용 SSMA의 11 월 2014 릴리스는 초기 릴리스입니다.
