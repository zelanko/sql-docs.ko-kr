---
title: SAP ASE 용 SSMA의 새로운 기능 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 4da3fa07c4cdcdf2f3666c3bf85ba3669eb7e5bf
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68632059"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>SAP ASE 용 SSMA의 새로운 기능 (SybaseToSQL)
이 문서에서는 각 릴리스의 SAP ASE (이전에는 Sybase 용 SSMA) 변경 내용에 대 한 SSMA (SQL Server Migration Assistant)를 나열 합니다.

## <a name="ssma-v83"></a>SSMA v 8.3

SAP ASE 용 SSMA의 v2.0 릴리스는 품질 및 변환 메트릭을 향상 시 키도 록 설계 된 대상 수정 기능으로 향상 되었습니다. 또한이 SAP ASE 용 SSMA 릴리스는 다음과 같은 수정 사항을 제공 합니다.

* 접근성 문제 해결
* SQL Server에서 ' hierarchyid ' 형식에 대 한 기본 지원 추가

> [!IMPORTANT]
> SSMA v 7.4 이상 버전을 사용 하는 경우 .Net 4.5.2는 설치 필수 구성 요소입니다.

## <a name="ssma-v82"></a>SSMA v8.2

SAP ASE 용 SSMA의 v 8.2 릴리스는 품질 및 변환 메트릭을 개선 하 고에 대 한 수정 사항을 위해 디자인 된 수정 사항 집합을 사용 하 여 향상 되었습니다.

* 데이터 마이그레이션 후 사용 하지 않도록 설정 된 비클러스터형 인덱스에 문제가 있습니다.
* 자동 설치 중에 .NET Framework를 검색 합니다.
* 새 버전이 다운로드 될 때 발생 하는 일시적인 충돌입니다.

> [!NOTE]
> 자동 업데이트의 알려진 문제로 인해 SSMA v 8.1에서 v 8.2로 업데이트 하지 못할 수 있습니다. 이 오류가 발생 하는 경우 새 버전을 다운로드 하 고 수동으로 설치 하세요.

> [!IMPORTANT]
> SSMA v 7.4 이상 버전을 사용 하는 경우 .Net 4.5.2는 설치 필수 구성 요소입니다.

## <a name="ssma-v81"></a>SSMA v8.1

SAP ASE 용 SSMA의 v 8.1 릴리스는 품질 및 변환 메트릭을 향상 시 키도 록 설계 된 대상 수정 기능으로 향상 되었습니다.

> [!NOTE]
> 자동 업데이트의 알려진 문제로 인해 SSMA v 8.0에서 v 8.1로의 업데이트가 실패할 수 있습니다. 이 오류가 발생 하는 경우 새 버전을 다운로드 하 고 수동으로 설치 하세요.

## <a name="ssma-v80"></a>SSMA v8.0

SAP ASE 용 SSMA의 v 8.0 릴리스는 품질 및 변환 메트릭을 개선 하기 위해 설계 된 대상 수정 기능을 통해 향상 되었습니다. 또한이 릴리스에서는 다음과 같은 새로운 기능을 제공 합니다.

* 대상으로 **Azure SQL Database Managed Instance** 지원. 이제 Azure SQL Database Managed Instance를 대상으로 하는 새 프로젝트를 만들 수 있습니다.

  ![SQL DB MI 프로젝트](../media/ssma-newproject-sqldbmi.png)

* 변환 후 **수정 관리자**입니다. [여기](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)에서 자세히 알아보세요.

* 예비 데이터베이스/스키마 선택.

  원본에 연결할 때 사용자는 이제 원하는 데이터베이스/스키마를 선택할 수 있습니다. 마이그레이션하려는 스키마만 선택 하면 초기 연결 중에 시간이 절약 되 고 전체 SSMA 성능이 향상 됩니다.

  ![SSMA 필터 개체](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

SAP ASE 용 SSMA의 v 7.10 릴리스는 글로벌 요구 사항에 대 한 추가 보안 및 개인 정보 보호를 제공 하도록 설계 된 대상 수정 기능을 통해 향상 되었습니다.

## <a name="ssma-v79"></a>SSMA v7.9

SAP ASE 용 SSMA의 v 7.9 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 품질 및 변환 메트릭을 개선 하는 대상 수정
* SSMA 명령줄에서 데이터 형식 매핑 및 프로젝트 기본 설정을 변경 하는 기능을 지원 합니다.
* SQL Server Integration Services (SSIS)를 사용 하 여 데이터 마이그레이션을 지원 합니다. 스키마를 변환한 후에는 마우스 오른쪽 단추를 클릭 하 여 상황에 맞는 메뉴 옵션을 사용 하 여 SSIS 패키지를 만들 수 있습니다.
* 또한 SSMA의 Azure SQL Database 연결 대화 상자가 정규화 된 서버 이름을 지정 하도록 변경 되었습니다. 이전 버전의 SSMA에서는 Azure SQL Database 접두사가 프로젝트 설정 내에서 명시적으로 언급 되어야 했습니다.

## <a name="ssma-v78"></a>SSMA v7.8

SAP ASE 용 SSMA의 v 7.8 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 프로젝트 설정에서 강조 표시 된 형식 매핑을 변경 합니다.
* 사용자가 원격 분석을 사용 하지 않도록 설정할 수 있는 기능입니다.

## <a name="ssma-v77"></a>SSMA v7.7

SAP ASE 용 SSMA의 v 7.7 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* SAP ASE 용 SSMA는 품질 및 변환 메트릭을 개선 하는 대상 수정 기능으로 향상 되었습니다.
* 인기 있는 요구 사항에 따라 SAP ASE 용 SSMA의 32 비트 버전이 다시 있습니다. 이전 구현과 비교할 때 (v 7.4 이전)에는 두 개의 설치 관리자 패키지가 있지만 함께 설치할 수는 없습니다. 따라서 사용 중인 연결 구성 요소에 따라 가장 적합 한 버전을 선택 해야 합니다. 가능 하면 항상 64 비트 버전을 사용 하는 것이 좋습니다.

## <a name="ssma-v76"></a>SSMA v7.6

SAP ASE 용 SSMA의 v 7.6 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 품질 및 변환 메트릭과 SQL Server 2017 (공개 미리 보기)에 대 한 지원을 제공 하는 대상 수정 Windows 및 Linux에서 SQL Server 2017에 대 한 지원은 공개 미리 보기 상태 이며 프로덕션 마이그레이션에 사용할 수 없습니다.
* Sybase 함수 변환을 지원 합니다.

## <a name="ssma-v75"></a>SSMA v7.5

SAP ASE 용 SSMA의 v2.0 릴리스 (이전에는 Sybase 용 SSMA)에는 다음 변경 내용이 포함 되어 있습니다.

* 장애가 있는 사용자에 게 더 많은 접근성을 보장 하기 위해 몇 가지 기능이 향상 되었습니다.
* CREATE 또는 REPLACE 구문을 지원 합니다.

## <a name="ssma-v74"></a>SSMA v7.4

Sybase 용 SSMA의 v 7.4 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 이제 원본 및 대상에서 스키마 개체를 검색 하는 동안 **쿼리 제한 시간** 옵션을 사용할 수 있습니다.

  ![쿼리 제한 시간 옵션](../media/query-timeout_red.png)
* 사용자 의견에 따라 대상 수정으로 품질 및 변환 메트릭이 개선 되었습니다.

  > [!IMPORTANT]
  > .Net 4.5.2은 SSMA v 7.4를 설치 하기 위한 필수 구성 요소입니다. 또한 v 7.4부터 SSMA의 32 비트 버전이 중단 됩니다.  

## <a name="ssma-v73"></a>SSMA v7.3

Sybase 용 SSMA의 v 7.3 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 고객 의견을 기반으로 하는 대상 픽스로 품질 및 변환 메트릭이 개선 되었습니다.
* SSMA 확장성 프레임 워크는 다음 항목을 통해 노출 됩니다.
  * SQL Server Data Tools (SSDT) 프로젝트로 기능을 내보냅니다.
    * 이제 SSMA에서 SSDT 프로젝트로 스키마 스크립트를 내보낼 수 있습니다. 스키마 스크립트를 사용 하 여 추가 스키마 변경을 수행 하 고 데이터베이스를 배포할 수 있습니다.

        ![SSDT 프로젝트로 저장 명령](../media/export-schema-scripts_red.png)
  * 사용자 지정 변환을 수행 하기 위해 SSMA에서 사용할 수 있는 라이브러리입니다.
    * 이제 SSMA에서 이전에 처리 되지 않은 사용자 지정 구문 변환과 변환을 처리할 수 있는 코드를 생성할 수 있습니다.
      * 사용자 지정 변환기를 구성 하는 방법에 대 한 지침은이 블로그 게시물에서 [SQL Server Migration Assistant의 변환 기능을 확장](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)하는 데 사용할 수 있습니다.
      * 이 [블로그 게시물](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)에서 변환할 샘플 프로젝트를 다운로드 합니다.

## <a name="ssma-v72"></a>SSMA v7.2

Sybase 용 SSMA의 v 7.2 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 고객 의견을 기반으로 하는 대상 픽스로 품질 및 변환 메트릭이 개선 되었습니다.
* 향상 된 원격 분석을 통해 고객 문제를 해결 하 고 SSMA의 변환 속도를 개선할 수 있는 더 나은 데이터 요소를 제공 합니다.

## <a name="ssma-v71"></a>SSMA v7.1

Sybase 용 SSMA의 v 7.1 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 이제 Windows 및 Linux CTP1의 SQL Server 2017는 마이그레이션에 지원 되는 대상 플랫폼입니다. 이 기능은 technical preview에 있으며 SQL server를 대상으로 하는 스키마 및 데이터 이동을 지원 합니다.
* 최신 버전의 SSMA를 사용할 수 있는 즉시 다운로드 하는 자동 업데이트 지원.
* 이제 Windows installer 패키지 파일 (.msi)을 통해 SSMA를 설치할 수 있는 이진 파일이 제공 됩니다.

## <a name="may-2016"></a>2016 년 5 월

Sybase 용 SSMA의 2016 년 5 월 릴리스에서는 다음과 같은 변경 내용이 포함 되어 있습니다.  

* SQL Server 2016에 대 한 지원이 추가 되었습니다.
* .Net 2.0에 대 한 설치 관리자 검사가 제거 되었습니다.
* .Net 3.5에서 .Net 4.0으로 확장 팩 종속성을 업데이트 했습니다.
* SSMA 콘솔에 대 한 "프로젝트 저장" 및 "프로젝트 열기" 명령을 수정 했습니다.
* SSMA 콘솔에 대 한 "securepassword" 명령을 수정 했습니다.
* 초기 로드에 대 한 개체 계산을 수정 했습니다.
* 전역 설정에서 버그가 수정 되었습니다.

## <a name="march-2016"></a>3 월 2016

Sybase 용 SSMA의 2016 년 3 월 preview 릴리스는 SQL Server 2016로 마이그레이션에 대 한 지원을 추가 합니다.  
  
## <a name="january-2016"></a>1 월 2016

Sybase 용 SSMA의 1 월 2016 유지 관리 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
* SSMA에 보기 로그 메뉴 항목을 추가 했습니다 (RFC 5706203).  
* 원격 분석 추가.

## <a name="july-2014"></a>7 월 2014

Sybase 용 SSMA의 7 월 2014 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
* Azure SQL DB 코드 변환을 개선 했습니다.  
* 확장 팩 기능을 스키마로 이동 하 여 Azure SQL DB를 지원 합니다.  
* 10k가 넘는 개체가 포함 된 데이터베이스에 대해 테스트 된 성능 향상 기능이 추가 되었습니다.  
* 많은 수의 개체를 처리 하기 위한 UI 개선 기능이 추가 되었습니다.  
* "잘 알려진" LOB 스키마를 강조 표시 하는 기능이 추가 되어 변환 시 무시 될 수 있습니다.  
* 변환 속도 개선 기능이 추가 되었습니다.  
* UI에서 개체 개수를 표시 하는 기능이 추가 되었습니다.
* 20%를 초과 하 여 보고서 크기를 줄였습니다.  
* 구문 분석 되지 않은 구문에 대 한 오류 메시지가 개선 되었습니다.  
  
## <a name="april-2014"></a>4 월 2014

Sybase 용 SSMA의 4 월 2014 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
* MS SQL Server 2014에 대 한 지원이 추가 되었습니다.  
* Azure로의 변환과 관련 된 버그가 수정 되었습니다.  
* IE 10의 보이지 않는 보고서 페이지와 관련 된 버그가 수정 되었습니다.  
  
## <a name="january-2012"></a>1 월 2012

Sybase 용 SSMA의 1 월 2012 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
* 롤백 트리거 변환에 대 한 지원이 추가 되었습니다.
* 동일한 SET 문에서 @@ROWCOUNT 및 @@ERROR 를 변환 하기 위한 수정이 제공 되었습니다.  
  
## <a name="july-2011"></a>7 월 2011

Sybase 용 SSMA의 7 월 2011 릴리스는 데이터 마이그레이션 중에 향상 된 오류 보고 기능을 제공 합니다.  
  
## <a name="april-2011"></a>4 월 2011

Sybase 용 SSMA의 4 월 2011 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
* 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 ,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" 및 Azure SQL을 지 원하는 통합 된 "Sybase 용 ssma" 제품입니다.  
* "Denali"에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 하 고 마이그레이션하는 데 대 한 지원이 추가 되었습니다.  
* Sybase 데이터베이스를 Azure SQL로 변환 하 고 마이그레이션하는 새 기능이 추가 되었습니다.  
* 데이터의 병렬 마이그레이션을 지 원하는 향상 된 클라이언트 쪽 데이터 마이그레이션 엔진.  
* 단순 및 대량 로그 복구 모델로 데이터 마이그레이션 성능이 개선 되었습니다.
* 대/소문자를 구분 하는 Sybase 데이터베이스를 대/소문자를 구분 하는 SQL Server으로 올바르게 변환 하 고 마이그레이션하는 기능이 추가 되었습니다.  
* SQL Server ANSI join 문이 DELETE 및 UPDATE 문으로 확장 되었으므로 Sybase ASE 비 ANSI 조인 문 변환에 대 한 지원이 추가 되었습니다.  
* Sybase ASE ODBC 공급자 및 Sybase ASE ADO.Net 공급자를 사용 하 여 Sybase ASE 서버에 연결 하기 위한 추가 연결 옵션을 제공 했습니다.
* Sybase 에뮬레이션 함수 (확장 팩의 일부로 설치 됨)를 포함 하는 **Sysdb**라는 별도의 데이터베이스에 대 한 종속성이 제거 되었습니다.
* 클러스터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sybase 확장 팩용 ssma를 설치 하는 기능이 추가 되었습니다.
* 이전 버전의 SSMA (v 4.0 및 v 4.2)에서 만든 프로젝트의 이전 버전과의 호환성이 추가 되었습니다.  
* 이전 버전의 SSMA (v 4.0 및 v 4.2)와 함께 Sybase v 5.0 용 SSMA 제품을 함께 설치 하는 기능이 추가 되었습니다.  
  
## <a name="july-2010"></a>7 월 2010

Sybase 용 SSMA의 7 월 2010 릴리스를 추가 했습니다.

* SQL Server 2008 R2로의 마이그레이션을 지원 합니다.  
* 명령줄 실행을 위한 새 SSMA 콘솔 응용 프로그램입니다.  
* 서버 쪽 및 클라이언트 쪽 데이터 마이그레이션 엔진을 모두 사용 하 여 데이터 마이그레이션을 지원 합니다.  
* 데이터 마이그레이션에서 "Custom SELECT" 문을 지원 합니다.  
* Sybase ASE 15.0.3 및 15.5에서의 마이그레이션 지원.  
  
## <a name="june-2008"></a>6 월 2008

Sybase 용 SSMA의 6 월 2008 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
* Ssma에서 수행한 데이터베이스 개체 변환과 데이터 마이그레이션을 자동으로 테스트 하는 SSMA 테스터를 추가 했습니다. 모든 SSMA 마이그레이션 단계를 완료 한 후 SSMA 테스터를 사용 하 여 변환 된 개체가 동일한 방식으로 작동 하 고 모든 데이터가 제대로 전송 되었는지 확인 합니다.
* SQL 이전 변환을 추가 했습니다. 이제 사용자는 변환에 사용할 각 소스 프로시저에 대 한 임시 테이블 (및 기타 개체) 선언을 지정할 수 있습니다.
* 개체 변환에 향상 된 기능이 추가 되었습니다.  
  * 조인 변환이 수정 되었습니다.  
  * Having/group by 절 없이 집계 및 비 집계  
  * SELECT INTO 문을 사용 하는 ID 함수  
  * 데이터 전용의 클러스터형 제약 조건 및 인덱스-잠김  
  * SELECT INTO에서 만든 임시 테이블  
  * 임시 테이블에 대 한 제약 조건/인덱스.  
  * 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 datetime 형식이 지원 됩니다.  
  * Sybase 15.0 연결 및 데이터 형식 지원.  
  
## <a name="may-2007"></a>2007 년 5 월

Sybase의 SSMA 릴리스 2007 년 5 월 릴리스를 추가 했습니다.  
  
* 프로젝트를 저장할 때 데이터베이스 콘텐츠를 더 빠르게 로드할 수 있습니다.  
* SQL Server 형식의 SQL 모드에서 사용자가 입력 한 주석을 지원 합니다.  
* 개체 변환의 향상 된 기능.  

## <a name="november-2006"></a>11 월 2006

Sybase 용 SSMA의 11 월 2006 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
* 새 전역 설정이 추가 됨:  
  * 편집기 창에 줄 번호를 표시 하도록 선택할 수 있습니다.  
  * 중복 된 개체를 바꿀지 묻는 메시지를 표시 하도록 SSMA를 구성 하거나 스키마를 변환 하는 동안 중복 개체를 항상 또는 절대 바꾸지 않도록 구성할 수 있습니다.  
* SSMA에서 다음과 같은 상황을 처리 하는 방법을 구성할 수 있는 새로운 변환 옵션이 추가 되었습니다.  
  * 이진 문자열을 포함 하는 CAST 또는 CONVERT 문입니다.  
  * 같음 식에서 null 값을 확인 합니다.  
  * 프록시 테이블  
  * RAISERROR의 사용자 메시지 오류 번호입니다.  
  * 확인 되지 않은 식별자를 포함 하는 UPDATE 문입니다.  
* 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 날짜 범위 밖에 있는 날짜를 처리 하는 방법을 지정할 수 있는 새로운 마이그레이션 옵션을 추가 했습니다.  
* 가독성 향상을 위해 코드의 형식을 지정 하는 **sql** 탭에 **형식이 지정 된 sql** 설정이 추가 되었습니다.  
* 다음을 포함 한 버그 수정
  * SSMA는 이제 {SHARED |의 잠금 테이블 *테이블* 을 변환 합니다. EXCLUSIVE} 모드 문에서 테이블의 후속 SELECT 쿼리에 TABLOCK 또는 TABLOCKX 힌트를 추가 합니다.  
  * 이제 문자 식에서 이진 형식을 사용 하는 경우 필요한 캐스팅이 추가 됩니다.  
  * 메모리 및 성능 향상.  
  
## <a name="july-2006"></a>7 월 2006

SSMA for Sybase의 2006년 7월 릴리스가 첫 버전입니다.  
  
## <a name="see-also"></a>참조

[Sybase &#40;sybasetosql 용 Ssma 시작&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
