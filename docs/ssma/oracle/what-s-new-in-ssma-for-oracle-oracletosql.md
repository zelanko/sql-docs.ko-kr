---
title: (OracleToSQL) Oracle 용 SSMA의 새로운 기능 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 09/22/2018
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
ms.openlocfilehash: 78f1615e375dfeafbcf25a8b0466ed92fbcc16ea
ms.sourcegitcommit: 7076fcb854c033a5dbeac7fcb22c5e15cf8528fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2018
ms.locfileid: "46362047"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>(OracleToSQL) Oracle 용 SSMA의 새로운 기능
이 문서에서는 Oracle 각 릴리스의 변경 내용에 대 한 SSMA를 나열 합니다.  

## <a name="ssma-v710"></a>SSMA v7.10
Oracle 용 SSMA의 v7.10 릴리스에는 다음 변경 내용이 포함 됩니다.
- 대상된 수정 사항을 추가 보안 및 글로벌 요구 사항 변화에에서 맞게 개인 정보 보호를 제공 하도록 설계 되었습니다.
- 계층적 쿼리와 관련 된 변환 향상 되었습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수입니다.

## <a name="ssma-v79"></a>SSMA v7.9
Oracle 용 SSMA의 v7.9 릴리스에는 다음 변경 내용이 포함 됩니다.
- 품질 및 변환 메트릭을 개선 하는 대상된 수정 되었습니다.
- Oracle에서 SQL Server로 마이그레이션 "계속" 문 지원 합니다.
- 데이터 형식 매핑 및 프로젝트 기본 설정을 변경 하려면 SSMA 명령줄에서 지원 합니다.
- 마이그레이션에 대 한 지원 SQL Server Integration Services (SSIS)를 사용 하 여 데이터입니다. 스키마를 변환한 후 마우스 오른쪽 단추 클릭 상황에 맞는 메뉴 옵션을 사용 하 여 SSIS 패키지를 만들 수는 있습니다.
- 정규화 된 서버 이름을 지정 하려면 SSMA에서 Azure SQL Database 연결 대화 상자도 변경 되었습니다. SSMA의 이전 버전에서는 Azure SQL Database 접두사 프로젝트 설정 내에서 명시적으로 언급 해야 했습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수입니다.

## <a name="ssma-v78"></a>SSMA v 7.8
Oracle 용 SSMA의 v 7.8 릴리스는 다음 변경 내용을 포함 되어 있습니다.
-   에 대 한 지원이 추가 되었습니다.
    - IN 절에 대 한 행 식입니다.
    - 암시적 캐스트입니다.
    - Azure SQL Database에 대 한 변환 UID입니다.
- 프로젝트 설정에서 강조 표시 된 변경 형식 매핑입니다.
- 사용자가 원격 분석을 사용 하지 않도록 설정 하는 기능을 제공 합니다.

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수입니다.

## <a name="ssma-v77"></a>SSMA v7.7
Oracle 용 SSMA의 v7.7 릴리스에는 다음 변경 내용이 포함 됩니다.
- Oracle 용 SSMA 품질 및 변환 메트릭을 개선 하는 대상된 수정 사항을 사용 하 여 향상 되었습니다.
- Oracle 용 SSMA의 32 비트 버전 다시은 인기 있는 필요에 따라입니다. (이전 v7.4) 이전 구현에 비해, 두 개의 설치 관리자 패키지 있지만 나란히 설치할 수 없습니다. 결과적으로, 해야 연결 구성 요소에 따라 가장 적합 한 버전을 선택 해야 합니다. 항상 가능한 경우 64 비트 버전을 사용 하는 것이 좋습니다.
- SQL Server 2017 지원은 이제 공식 Oracle 확장 팩도 Linux 지원 (새 원격 설치 옵션)입니다. 확장 팩 기능은 제한 된 테스터의 Linux에 설치 하면 및 서버 쪽 데이터 마이그레이션 기능이 지원 되지 않습니다.
- Oracle 용 SSMA를 사용 하면 일반 테이블로 구체화 된 뷰를 마이그레이션할 수 있습니다 (에서 설정을 구성할 수 있습니다 **프로젝트 설정** -> **동기화**  ->  **구체화 된 뷰에 대 한 백업 테이블 검색**).

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수입니다.

## <a name="ssma-v76"></a>SSMA v7.6
Oracle 용 SSMA v7.6 릴리스의 품질 및 변환 메트릭을 개선 하는 대상된 수정 사항을 SQL Server 2017 (공개 미리 보기)에 대 한 지원이 향상 되었습니다. Windows 및 Linux에서 SQL Server 2017에 대 한 지원을 공개 미리 보기로 제공 않으며 프로덕션 마이그레이션에 사용할 수 없습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는 사용 하 여.Net 4.5.2는 설치 필수 이며 도구의 32 비트 버전은 지원 되지 않습니다.

## <a name="ssma-v75"></a>SSMA v7.5
Oracle 용 SSMA의 v7.5 릴리스에는 다음 변경 내용이 포함 됩니다.
- 장애가 있는 사용자에 큰 액세스 가능성을 보장 하기 위해 여러 향상 된 기능을 사용 하 여 향상 되었습니다.
- 향상 된 데이터 마이그레이션 중에 고객 피드백에 따라 날짜 및 float 데이터 형식의 처리와 같은 대상된 수정 사항 사용 하 여 품질 및 변환 메트릭을 개선 하기 위해 업데이트 합니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.5 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA이 이제 중단 됩니다.

## <a name="ssma-v74"></a>SSMA v7.4
Oracle 용 SSMA의 v7.4 릴리스에는 다음 변경 내용이 포함 됩니다.

- 이제 Oracle 용 SSMA는 마이그레이션에 대 한 대상 플랫폼으로 Azure SQL Data Warehouse를 지원합니다.

    ![새 프로젝트 창](../media/new-project.png)
  - 다음 그림에 나와 있는 것 처럼 데이터 웨어하우스 저장소 옵션을 지원 합니다.

    ![데이터 웨어하우스에 대 한 저장소 옵션](../media/storage-options_red.png)
  - 다음 이미지와 같이 데이터 분포 옵션을 지원 합니다.

    ![데이터 웨어하우스에 대 한 데이터 배포](../media/data-distribution_red.png)

- 합니다 **쿼리 제한 시간** 옵션을 원본 및 대상 스키마 개체 검색 하는 동안 제공 됩니다.

    ![쿼리 제한 시간 옵션](../media/query-timeout_red.png)

- 품질 및 변환 메트릭, 고객 피드백에 따라 대상된 수정 사항을 사용 하 여 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.4 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA이 이제 중단 됩니다.

## <a name="ssma-v73"></a>SSMA v7.3
Oracle 용 SSMA의 v7.3 릴리스에는 다음 변경 내용이 포함 됩니다.
- 향상 된 품질 및 변환 메트릭 고객 피드백에 따라 대상된 수정 사항 사용 하 여입니다.
- SSMA 확장성 프레임 워크는 다음 항목을 통해 노출 합니다.
  - SQL Server Data Tools (SSDT) 프로젝트에 기능을 내보냅니다.
    -   이제 SSDT 프로젝트 SSMA에서 스키마 스크립트를 내보낼 수 있습니다. 추가 스키마 변경을 수행 하 여 데이터베이스를 배포 하는 스키마 스크립트를 사용할 수 있습니다.
![SSDT 프로젝트 명령으로 저장](../media/export-schema-scripts_red.png)
  - SSMA 사용자 지정 변환을 수행 하는 데 사용할 수 있는 라이브러리입니다.
    - 이제 사용자 지정 구문 변환 및 SSMA 이전에 처리 되지 않은 변환을 처리할 수 있는 코드를 생성할 수 있습니다.
      - 이 블로그 게시물에서는 사용자 지정 변환기를 생성 하는 방법에 사용할 [확장 SQL Server Migration Assistant의 변환 기능](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)합니다.
      - 이 변환에 대 한 샘플 프로젝트를 다운로드 [블로그 게시물](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)합니다.


## <a name="ssma-v72"></a>SSMA v7.2
Oracle 용 SSMA의 v 7.2가 사전 릴리스는 다음 변경 내용을 포함 되어 있습니다.
- 향상 된 품질 및 변환 메트릭 고객 피드백에 따라 대상된 수정 사항 사용 하 여입니다.
- 더 나은 데이터 요소를 고객 문제를 해결 하 여 SSMA의 전환율을 향상 시킬 수 있도록 원격 분석 향상 된 기능입니다.

## <a name="ssma-v71"></a>SSMA v7.1
Oracle 용 SSMA의 v7.1 릴리스는 다음 변경 내용을 포함 되어 있습니다.
- Windows 및 Linux CTP1에서 SQL Server 2017 마이그레이션에 대 한 지원 되는 대상 플랫폼 되었습니다. 이 기능은 기술 미리 보기로 제공 되며 대상 SQL server에 스키마 및 데이터 이동할 수 있습니다.
- SSMA는 이제 사용 가능한 즉시 최신 버전의 SSMA 다운로드 하려면 자동 업데이트를 지원 합니다.
- SSMA 설치 가능 이진 파일은 이제 Windows installer 패키지 파일 (.msi)를 통해 전달 됩니다.

**리소스**

[SQL Server Migration Assistant의 변환 기능 확장](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[평가 및 비 Microsoft 데이터 플랫폼에서 데이터를 SQL Server로 마이그레이션 *(사용 하 여 Oracle 예제)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 년 5 월  
Oracle 용 SSMA의 2016 년 5 월 릴리스는 다음 변경 내용이 포함 되어 있습니다.  

- SQL Server 2016에 대 한 지원이 추가 되었습니다.
- 추가 SQL Server의 temporal 테이블에 Oracle 못하실지도 보관 테이블 변환 합니다.

    **참고** -SSMA Oracle 플래시 백 데이터 보관 테이블에서 기록 데이터를 복사 하지 않습니다. 결과적으로, 기록 데이터 마이그레이션 프로세스 중에 수동으로 복사 해야 합니다. 또한 SSMA 시스템 테이블로 처리 되기 때문에 SQL Server 메타 데이터 탐색기에서 기록 테이블을 표시 하지 않습니다, SQL Server Management Studio에서 기록 테이블을 볼 수 있습니다.
    SQL Server 2016 등 여러 Oracle 플래시 백 기능을 지원 하지 않습니다.
    - Oracle 못하실지도 트랜잭션 쿼리
    - DBMS_FLASHBACK 패키지
    - 플래시 백 트랜잭션
    - 플래시 백 데이터 보관
    - 플래시 백 테이블
    - 플래시 백 놓기
    - 플래시 백 데이터베이스
- SQL Server 정책 개체 (Oracle에 대 한 행 수준 보안)에 Oracle VPD 정책의 추가 변환입니다.
- Oracle에 대 한 초기 로드의 감소 시간입니다.
- 향상 된 파서 및 확인자입니다.
- .NET 2.0에 대 한 설치 관리자 검사를 제거 합니다.
- 업데이트 된 확장 팩 종속성.Net 3.5에서에서.net 4.0입니다.
- "저장"프로젝트 수정 및 SSMA 콘솔에 대 한 프로젝트 열기 명령입니다.
- SSMA 콘솔에 대 한 고정된 "securepassword" 명령입니다.
- 초기 로드에 대 한 개체의 계산을 고정 합니다.
- Oracle에 대 한 문자 데이터 형식 변환 수정 되었습니다.
- 전역 설정에 대 한 버그가 수정 되었습니다.
  
## <a name="march-2016"></a>2016 년 3 월  
Oracle 용 SSMA의 2016 년 3 월 미리 보기 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-   SQL Server 2016으로 마이그레이션에 대 한 지원이 추가 되었습니다.  
-   (사용 하 여 몇 가지 제한 사항이) 마이그레이션 Oracle 행 수준 보안에 대 한 지원이 추가 되었습니다.  
-   마이그레이션에 대 한 지원 추가 메모리에서 Oracle SQL Server 열 저장소 테이블입니다.  
  
## <a name="january-2016"></a>2016 년 1 월  
2014 년 1 월 Oracle 용 SSMA의 유지 관리 릴리스에 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   클러스터형 인덱스에 대 한 지원이 추가 되었습니다.  
-   느린 Oracle 스키마 쿼리를 (RFC 5076207) 수정 했습니다.  
-   고정 콘솔에서 Azure에 연결 합니다.  
-   추가 뷰는 메뉴 항목을 로그 하 SSMA (RFC 5706203)입니다. 
-   추가 원격 분석입니다.  
  
## <a name="july-2014"></a>2014 년 7 월  
Oracle 용 SSMA의 2014 년 7 월 릴리스는 다음 변경 내용이 포함 되어 있습니다.  
  
-   Azure SQL DB에 대 한 지원이 추가 되었습니다.  
-   Azure SQL DB를 지원 하도록 확장 팩 기능 스키마로 이동 합니다.  
-   Oracle 구체화 된 뷰에 대 한 지원이 추가 되었습니다.  
-   최적화 된 테이블을 SQL Server 2014 메모리에 대 한 지원이 추가 되었습니다.  
-   포함 된 성능 향상 10k를 사용 하 여 데이터베이스에 대 한 개체를 테스트합니다.  
-   많은 수의 개체를 처리 하기 위한 향상 된 UI가 추가 되었습니다.  
-   "알려진" LOB 스키마의 강조 표시를 추가 합니다.  
-   변환 속도 향상을 포함 합니다.  
-   UI에서 개체를 표시 하기 위한 추가 지원 계산 합니다.  
-   25% 이상 감소 보고서 크기입니다.
-   구문 분석 되지 않은 구문에 대 한 향상 된 오류 메시지입니다.  
  
## <a name="april-2014"></a>2014 년 4 월  
Oracle 용 SSMA의 2014 년 4 월 릴리스는 다음 변경 내용이 포함 되어 있습니다.  
  
-   MS SQL Server 2014 지원이 추가 되었습니다.  
-   Oracle 12 및 쿼리 최적화에 대 한 지원이 추가 되었습니다.  
-   Azure에 변환에 대 한 수정 된 버그입니다.  
-   IE 10에서 보이지 않는 보고서 페이지에 대 한 수정 된 버그입니다.  
  
## <a name="january-2012"></a>2012 년 1 월  
Oracle 용 SSMA의 2012 년 1 월 릴리스는 다음 변경 내용이 포함 되어 있습니다.  
  
-   NULL이 기본값으로 RowType과 RecordType 입력된 매개 변수에 대 한 지원이 추가 되었습니다.  
  
## <a name="july-2011"></a>2011 년 7 월  
Oracle 용 SSMA의 2011 년 7 월 릴리스는 다음 변경 내용이 포함 되어 있습니다.  
  
-   에 대 한 Oracle 시퀀스는 변환에 대 한 지원이 추가 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" 시퀀스 생성기입니다.  
-   데이터 마이그레이션 중에 보고 기능 향상 된 오류입니다.  
-   향상 된 예약어를 사용 하 여 문 변환 합니다.  
-   함수에서 날짜 값의 향상 된 암시적 변환입니다.  
  
## <a name="april-2011"></a>2011 년 4 월  
Oracle 용 SSMA의 2011 년 4 월 릴리스는 다음 변경 내용이 포함 되어 있습니다.  
  
-   지 원하는 통합 된 "Oracle SSMA" 제품 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali"로 지정 합니다.  
-   연결 및 마이그레이션에 대 한 지원이 추가 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali"로 지정 합니다.  
-   데이터의 병렬 마이그레이션을 지 원하는 향상 된 클라이언트 쪽 데이터 마이그레이션 엔진입니다.  
-   향상 된 데이터 마이그레이션 성능을 단순 및 대량 로그 복구 모델.  
-   SSMA (v4.0 및 v4.2)의 이전 버전에서 만든 프로젝트의 이전 버전과 호환성에 대 한 지원이 추가 되었습니다.  
-   SSMA 제품에 대 한 Oracle v5.0 나란히 (SxS) 이전 버전의 SSMA (v4.0 및 v4.2)를 사용 하 여 설치 하는 기능을 추가 합니다.  
-   사용자 정의 형식 (하위 형식, VARRAY, 중첩 테이블, 개체 테이블 및 개체 뷰 포함) 및 특수 한 오류 메시지를 사용 하 여 PL/SQL 블록의 사용법을 보고에 대 한 지원이 추가 되었습니다.  

## <a name="july-2010"></a>2010 년 7 월  
Oracle 용 SSMA의 2010 년 7 월 릴리스는 다음 변경 내용이 포함 되어 있습니다.  
  
-   SQL Server 2008 R2로 마이그레이션에 대 한 지원이 추가 되었습니다.  
-   명령줄 실행에 대 한 새 SSMA 콘솔 응용 프로그램을 추가 합니다.  
-   서버 쪽 및 클라이언트 쪽 데이터 마이그레이션 엔진을 사용 하 여 데이터 마이그레이션에 대 한 지원이 추가 되었습니다.  
-   데이터 마이그레이션에 대 한 "사용자 지정 선택" 문에 대 한 지원이 추가 되었습니다.  
-   Oracle에서 11g R2 마이그레이션에 대 한 지원이 추가 되었습니다.  
  
## <a name="june-2008"></a>2008 년 6 월  
Oracle 용 SSMA의 2008 년 6 월 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-   동의어에 대 한 추가 정보를 구문 분석할 개체, 패널 및 SQL Server 로고 제거 레이아웃 지 속성에 대 한 원시 소스를 포함 하 여 평가 보고서에 추가 된 개선 사항입니다.  
-   개체 변환에 추가 된 향상 된 기능:  
    -   패키지 DBMS_LOB, DBMS_SQL 변환을 추가 합니다.  
    -   조인 수정 변환 합니다.  
    -   컬렉션 및 레코드 변환, 이제 각 필드에 대 한 별도 변수를 통해 출시 대부분의 레코드를 수정 합니다.  
    -   레코드 및 컬렉션 구현의 개선 사항입니다.  
    -   기간 이동 집계 함수를 추가 합니다.  
    -   롤업/큐브 절을 추가 합니다.  
    -   NEXTVAL/CURVAL 개선 합니다.  
    -   SET 절에서 그룹화 열, 집합, 그룹화 및 ID 그룹화 추가 되었습니다.  
    -   MERGE 문 추가 합니다.  
    -   새 날짜/시간 형식 및 레코드 컬렉션을 추가 하는 CLR 데이터 형식으로 변환 지원 합니다.  
-   테스터의 새 기능이 추가 되었습니다. 테스터를 사용 하 여 개체로 테스트할 수 이제 테이블, 테스트 사례에서 여러 테스트 가능 개체의 호출 순서를 변경할 수 있습니다, 사용자 매개 변수 및 반환 값으로 프로시저 및 레코드 및 컬렉션을 사용 하 여 함수를 테스트할 수 있으며 종속성 분석기를 확인 하려면 추가 된 사용 된 테이블만 합니다.  
  
## <a name="august-2007"></a>2007 년 8 월  
Oracle 용 SSMA의 2007 년 8 월 릴리스는 다음 변경 내용이 포함 되어 있습니다.  
  
-   새 테스터 구성 요소를 사용 하면 생성, 관리 및 변환 된 SQL 코드를 확인 하려면 테스트 사례를 실행을 추가 합니다.  
-   Oracle 하위 형식, 컬렉션 및 로컬 모듈의 변환에 대 한 지원이 추가 되었습니다 SQL 변환기에 추가 되었습니다.  
-   새 동기화 기능을 SQL Server 데이터베이스를 사용 하 여 특정 개체를 동기화 할 수를 추가 합니다.  
-   추가 된 새 변환 옵션 됩니다.  
  
## <a name="april-2007"></a>2007 년 4 월  
Oracle 용 SSMA의 2007 년 4 월 릴리스는 초기 릴리스가 였습니다.
