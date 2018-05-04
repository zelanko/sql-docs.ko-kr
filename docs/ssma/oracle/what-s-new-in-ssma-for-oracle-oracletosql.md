---
title: SSMA for Oracle (OracleToSQL)의 새로운 기능 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 03/01/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3071e64cfeb6abac76f223407899100b4e8d31a0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>SSMA for Oracle (OracleToSQL)의 새로운 기능
이 항목에서는 각 릴리스의 Oracle 변경에 대 한 SSMA를 나열 합니다.  

## <a name="ssma-v77"></a>SSMA v7.7
Oracle 용 SSMA의 v7.7 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
- Oracle 용 SSMA 품질 및 변환 메트릭을 향상 된 대상으로 지정 된 수정 사항으로 향상 되었습니다.
- 많은 요청에 따라, 32 비트 버전의 Oracle 용 SSMA ´ ù. 이전 구현을 v7.4) (이전에 비해, 두 개의 설치 관리자 패키지 있지만 나란히 설치할 수 없습니다. 결과적으로,가지고 연결 구성 요소에 따라 가장 적합 한 버전을 선택 해야 합니다. 항상 가능한 경우 64 비트 버전을 사용 하는 것이 좋습니다.
- SQL Server 2017 지원은 이제 공식 Oracle 확장 팩에도 Linux에서 지원 (새 원격 설치 옵션) 합니다. Linux 테스터에 설치 된 경우 확장 팩 기능 제한 됩니다 및 서버 쪽 데이터 마이그레이션 기능은 지원 되지 않습니다. 
- SSMA for Oracle 사용 하면 일반 테이블로 구체화 된 뷰를 마이그레이션할 수 있습니다 (에서 설정을 통해 구성 가능 **프로젝트 설정** -> **동기화**  ->  **구체화 된 뷰에 대 한 백업 테이블 검색**).

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수 구성 요소입니다.

## <a name="ssma-v76"></a>SSMA v7.6
Oracle 용 SSMA v7.6 릴리스의 품질 및 변환 메트릭을 향상 된 대상으로 지정 된 수정 사항 및 SQL Server 2017 (공개 미리 보기)에 대 한 지원이 향상 되었습니다. Windows 및 Linux에서 SQL Server 2017에 대 한 지원을 공개 미리 보기 이므로 프로덕션 마이그레이션에 사용할 수 없습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이상 버전을 사용 하 여.Net 4.5.2는 설치 필수 구성 요소 이며 도구의 32 비트 버전도 않습니다.

## <a name="ssma-v75"></a>SSMA v7.5
Oracle 용 SSMA의 v7.5 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
- 장애가 있는 사용자에 대 한 큰 액세스 가능성을 확인 하려면 몇 가지 향상 된 버전으로 향상 되었습니다.
- 업데이트 대상된의 수정 된 품질 및 변환 메트릭이 개선 하기 위해 같은 고객 의견에 따라, 데이터 마이그레이션 중에 날짜 및 float 데이터 형식 처리가 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.5 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA는 되 고 중단 되었습니다.

## <a name="ssma-v74"></a>SSMA v7.4
Oracle 용 SSMA의 v7.4 릴리스는 다음과 같은 변경을 포함 되어 있습니다.

- 이제 Oracle 용 SSMA는 마이그레이션에 대 한 대상 플랫폼으로 Azure SQL 데이터 웨어하우스를 지원합니다.

    ![새 프로젝트 창](../media/new-project.png)
  - 다음 그림에 나와 있는 것 처럼 데이터 웨어하우스 저장소 옵션을 지원 합니다.

    ![데이터 웨어하우스에 대 한 저장소 옵션](../media/storage-options_red.png)
  - 다음 그림에 표시 된 것과 같이 데이터 분포 옵션을 지원 합니다.

    ![데이터 웨어하우스에 대 한 데이터 분산](../media/data-distribution_red.png)

- **쿼리 제한 시간** 옵션은 원본 및 대상에서 스키마 개체 검색 하는 동안 이제 사용할 수 있습니다.

    ![쿼리 제한 시간 옵션](../media/query-timeout_red.png)

- 품질 및 변환 메트릭은 고객 의견에 따라 대상된 수정 프로그램으로 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.4 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA는 되 고 중단 되었습니다.

## <a name="ssma-v73"></a>SSMA v7.3
Oracle 용 SSMA의 v7.3 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
- 향상 된 품질 및 변환 메트릭을 고객 의견에 따라 수정 프로그램을 대상된으로 합니다.
- 다음 항목을 통해 노출 SSMA 확장성 프레임 워크:
  - SQL Server Data Tools (SSDT) 프로젝트에 내보내기 기능.
    -   SSDT 프로젝트에 SSMA에서 스키마 스크립트를 내보낼 수 있습니다. 추가 스키마를 변경 하 여 데이터베이스를 배포 하는 스키마 스크립트를 사용할 수 있습니다.
![SSDT 프로젝트 명령으로 저장](../media/export-schema-scripts_red.png)
  - SSMA 사용자 지정 변환을 수행 하는 데 사용할 수 있는 라이브러리입니다.
    - 이제 사용자 지정 구문 변환 및 SSMA 이전에 처리 되지 않은 변환 처리할 수 있는 코드를 생성할 수 있습니다.
      - 이 블로그 게시물에서 사용할 수 있는 사용자 지정 변환기를 생성 하는 방법에 대 한 지침 [확장 SQL Server Migration Assistant의 변환 기능](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)합니다.
      - 이 변환에 대 한 샘플 프로젝트를 다운로드할 수 수 [블로그 게시물](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)합니다.


## <a name="ssma-v72"></a>SSMA v7.2
Oracle 용 SSMA의 v 7.2가 사전 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
- 향상 된 품질 및 변환 메트릭을 고객 의견에 따라 수정 프로그램을 대상된으로 합니다.
- 원격 분석의 향상 된 기능 고객 문제를 해결 하 고 SSMA의 변환율 향상에 더 나은 데이터 요소를 제공 합니다.

## <a name="ssma-v71"></a>SSMA v7.1
Oracle 용 SSMA의 v7.1 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
- Windows 및 Linux c t p 1에서 SQL Server 2017 마이그레이션에 지원 되는 대상 플랫폼 되었습니다. 이 기능은 기술 미리 보기 상태에서 이며 대상 SQL 서버에 스키마 및 데이터를 이동할 수 있습니다.
- SSMA는 이제 자동으로 업데이트 되는 사용 가능한 즉시 최신 버전의 SSMA 다운로드를 지원 합니다.
- SSMA 설치할 수 있는 이진 파일은 이제 Windows installer 패키지 파일 (.msi)을 통해 배달 됩니다.

**리소스**

[SQL Server Migration Assistant의 변환 기능을 확장합니다.](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[평가 하 고 SQL Server에 Microsoft 이외의 데이터 플랫폼에서 데이터를 마이그레이션할 *(예: Oracle) 있음*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 년 5 월  
Oracle 용 SSMA의 2016 년 5 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  

-   SQL Server 2016에 대 한 지원이 추가 되었습니다.
-   추가 된 SQL Server 임시 테이블에 Oracle 플래시 백 보관 테이블로 변환 합니다.
-   SQL Server 정책 개체가 (Oracle에 대 한 행 수준 보안)를 변환 하는 Oracle VPD 정책으로 추가 된 변환 됩니다.
-   Oracle에 대 한 초기 로드의 저하 시간입니다.
-   향상 된 파서 및 확인자입니다.
-   .NET 2.0에 대 한 설치 관리자 검사를 제거 합니다.
-   업데이트 된 확장 팩 종속성.Net 3.5에서에서.Net 4.0 합니다.
-   프로젝트"저장" 고정 및 SSMA 콘솔에 대 한 프로젝트 열기 명령입니다.
-   SSMA 콘솔에 대 한 고정된 "securepassword" 명령입니다.
-   고정 되는 초기 로드에 대 한 개체의 수를 계산 합니다.
-   Oracle에 대 한 문자 데이터 형식 변환 문제를 수정 했습니다.
-   전역 설정에서 수정 된 버그입니다.
  
## <a name="march-2016"></a>2016 년 3 월  
Oracle 용 SSMA의 2016 년 3 월 미리 보기 릴리스는 다음과 같은 변경을 포함 되어 있습니다.  
  
-   SQL Server 2016으로 마이그레이션에 대 한 지원이 추가 되었습니다.  
-   마이그레이션 Oracle 행 수준 보안 (을 몇 가지 제한 사항이)에 대 한 지원이 추가 되었습니다.  
-   마이그레이션에 대 한 지원을 추가 메모리에는 Oracle SQL Server 열 저장소 테이블입니다.  
  
## <a name="january-2016"></a>2016 년 1 월  
2014 년 1 월 Oracle 용 SSMA의 유지 관리 릴리스에 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   클러스터형 인덱스에 대 한 지원이 추가 되었습니다.  
-   느린 Oracle 스키마 쿼리 (RFC 5076207) 수정 했습니다.  
-   고정 콘솔에서 Azure에 연결 합니다.  
-   SSMA (RFC 5706203)에 추가 된 보기 로그의 메뉴 항목입니다. 
-   추가 된 원격 분석 합니다.  
  
## <a name="july-2014"></a>2014 년 7 월  
Oracle 용 SSMA의 2014 년 7 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   Azure SQL DB에 대 한 지원이 추가 되었습니다.  
-   Azure SQL DB를 지원 하기 위해 확장 팩 기능 스키마로 이동 합니다.  
-   Oracle 구체화 된 뷰에 대 한 지원이 추가 되었습니다.  
-   지원이 추가 되었습니다. SQL Server 2014 메모리 액세스에 최적화 된 테이블입니다.  
-   포함 된 성능 향상 10k 사용 하 여 데이터베이스에 대 한 개체를 테스트합니다.  
-   많은 수의 개체를 처리 하기 위한 향상 된 UI가 추가 되었습니다.  
-   "잘 알려진" LOB 스키마의 강조 표시를 추가 합니다.  
-   변환 속도 향상을 포함 합니다.  
-   UI에 표시 개체에 대 한 지원 추가 계산 합니다.  
-   25%를 초과 하 여 축소 된 보고서 크기입니다.
-   구문 분석 되지 않은 구문에 대 한 향상 된 오류 메시지입니다.  
  
## <a name="april-2014"></a>2014 년 4 월  
Oracle 용 SSMA의 2014 년 4 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   MS SQL Server 2014의 지원이 추가 되었습니다.  
-   Oracle 12 및 쿼리 최적화의 지원이 추가 되었습니다.  
-   Azure에 변환에 대 한 수정 된 버그입니다.  
-   IE 10에서 보이지 않는 보고서 페이지에 대 한 수정 된 버그입니다.  
  
## <a name="january-2012"></a>2012 년 1 월  
Oracle 용 SSMA의 2012 년 1 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   NULL로 RowType 및 RecordType 입력된 매개 변수에 대 한 지원 추가 기본값입니다.  
  
## <a name="july-2011"></a>2011 년 7 월  
Oracle 용 SSMA의 2011 년 7 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   에 대 한 Oracle 시퀀스는 변환에 대 한 지원을 추가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" 시퀀스 생성기입니다.  
-   향상 된 오류 데이터 마이그레이션 중에 보고 합니다.  
-   예약 된 단어를 사용 하 여 문의 향상 된 변환 합니다.  
-   향상 된 함수에서 날짜 값의 암시적 변환입니다.  
  
## <a name="april-2011"></a>2011 년 4 월  
Oracle 용 SSMA의 2011 년 4 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   지 원하는 통합된 "SSMA에 대 한 Oracle" 제품 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 년 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"로 지정 합니다.  
-   연결 하 고로 마이그레이션에 대 한 지원을 추가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"로 지정 합니다.  
-   데이터의 병렬 마이그레이션을 지 원하는 향상 된 클라이언트 쪽 데이터 마이그레이션 엔진입니다.  
-   향상 된 데이터 마이그레이션 성능 단순 및 대량 로그 복구 모델.  
-   SSMA (v4.0 및 v4.2)의 이전 버전에서 만든 프로젝트의 이전 버전과 호환성에 대 한 지원이 추가 되었습니다.  
-   SSMA 제품에 대 한 Oracle v5.0 나란히 (SxS) SSMA (v4.0 및 v4.2)의 이전 버전으로 설치 하는 기능을 추가 합니다.  
-   사용자 정의 형식 (하위 유형, VARRAY, 중첩 테이블, 개체 테이블 및 개체 보기 포함) 및 특수 한 오류 메시지와 함께 PL/SQL 블록에서 사용법을 보고에 대 한 지원이 추가 되었습니다.  

## <a name="july-2010"></a>2010 년 7 월  
Oracle 용 SSMA의 2010 년 7 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   SQL Server 2008 r 2로 마이그레이션에 대 한 지원이 추가 되었습니다.  
-   명령줄 실행에 대 한 새 SSMA 콘솔 응용 프로그램을 추가 합니다.  
-   서버 쪽 및 클라이언트 쪽 데이터 마이그레이션 엔진 둘 다 사용 하 여 데이터 마이그레이션에 대 한 지원이 추가 되었습니다.  
-   "사용자 지정 선택" 문에 데이터 마이그레이션에 대 한 지원이 추가 되었습니다.  
-   Oracle 11g R2 마이그레이션에 대 한 지원이 추가 되었습니다.  
  
## <a name="june-2008"></a>2008 년 6 월  
Oracle 용 SSMA의 2008 년 6 월 릴리스는 다음과 같은 변경을 포함 되어 있습니다.  
  
-   동의어에 대 한 추가 정보, 개체를 구문 분석할 수 없습니다, 패널 및 SQL Server 로고 제거 및 레이아웃 지 속성에 대 한 원시 소스를 포함 하 여 평가 보고서에 추가 된 개선 되었습니다.  
-   개체 변환에서 추가 된 향상 된 기능:  
    -   패키지 DBMS_LOB, DBMS_SQL 변환을 추가 합니다.  
    -   조인 수정 변환 합니다.  
    -   컬렉션 및 레코드 변환, 대부분의 경우 각 필드에 대 한 별도 변수를 통해 릴리스 레코드의 변환 지금 수정 합니다.  
    -   레코드 및 컬렉션 구현의 개선 되었습니다.  
    -   기간 이동 집계 함수를 추가 합니다.  
    -   롤업/큐브 절을 추가 합니다.  
    -   NEXTVAL/CURVAL 성능이 향상 됩니다.  
    -   SET 절에서 그룹화 열 집합을 그룹화 하 고 ID 그룹화 추가 되었습니다.  
    -   MERGE 문 추가 합니다.  
    -   새 날짜/시간 형식 및 추가 된 CLR 데이터 형식으로 변환 레코드와 컬렉션을 지원 합니다.  
-   테스터의 추가 된 새로운 기능입니다. 테스터를 사용 하 여 개체로 테스트할 수 이제 테이블, 테스트 사례에 몇 가지 테스트 가능한 개체의 호출 순서를 변경할 수 있습니다, 그리고 사용자 절차와 레코드 및 컬렉션 매개 변수로 사용 하 여 함수를 테스트 하 고 반환 값 및 분석기 확인에 추가 된 종속성 테이블에만 사용 합니다.  
  
## <a name="august-2007"></a>2007 년 8 월  
Oracle 용 SSMA의 2007 년 8 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   새 테스터 구성 요소를 사용 하면 생성, 관리 및 변환 된 SQL 코드를 확인 하는 테스트 사례를 실행을 추가 합니다.  
-   Oracle 하위 유형, 컬렉션 및 로컬 모듈의 변환에 대 한 지원 추가 SQL 변환기에 추가 되었습니다.  
-   새로운 동기화 기능을 사용 하면 특정 개체를 SQL Server 데이터베이스와 동기화를 추가 합니다.  
-   추가 된 새 변환 옵션입니다.  
  
## <a name="april-2007"></a>2007 년 4 월  
Oracle 용 SSMA의 2007 년 4 월 릴리스가 첫 버전입니다.
