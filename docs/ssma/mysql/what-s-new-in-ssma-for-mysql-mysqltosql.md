---
title: MySQL (MySQLToSql) 용 SSMA의 새로운 기능 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 03/01/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
caps.latest.revision: 21
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d818a1ce31d752898d5d1ebde5a27addbedd91ad
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776679"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>MySQL (MySQLToSql) 용 SSMA의 새로운 기능
이 항목에서는 각 릴리스의 MySQL 변경에 대 한 SSMA를 나열 합니다. 

## <a name="ssma-v77"></a>SSMA v7.7
MySQL 용 SSMA의 v7.7 릴리스에서 다음 변경 내용이 포함 되어 있습니다.
- MySQL 용 SSMA 품질 및 변환 메트릭을 향상 된 대상으로 지정 된 수정 사항으로 향상 되었습니다.
- 많은 요청에 따라, 32 비트 버전의 MySQL 용 SSMA ´ ù. 이전 구현을 v7.4) (이전에 비해, 두 개의 설치 관리자 패키지 있지만 나란히 설치할 수 없습니다. 결과적으로,가지고 연결 구성 요소에 따라 가장 적합 한 버전을 선택 해야 합니다. 항상 가능한 경우 64 비트 버전을 사용 하는 것이 좋습니다.
- MySQL 용 SSMA MySQL 호환 되는 제 3 자 ODBC 드라이버를 사용할 수 있는 ODBC 연결 문자열 연결 모드를 있습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수 구성 요소입니다.

## <a name="ssma-v76"></a>SSMA v7.6
MySQL 용 SSMA의 v7.6 릴리스 품질 및 변환 메트릭을 향상 된 대상으로 지정 된 수정 사항 및 SQL Server 2017 (공개 미리 보기)에 대 한 지원이 향상 되었습니다. Windows 및 Linux에서 SQL Server 2017에 대 한 지원을 공개 미리 보기 이므로 프로덕션 마이그레이션에 사용할 수 없습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이상 버전을 사용 하 여.Net 4.5.2는 설치 필수 구성 요소 이며 도구의 32 비트 버전도 않습니다.

## <a name="ssma-v75"></a>SSMA v7.5
장애가 있는 사용자에 대 한 큰 액세스 가능성을 확인 하려면 몇 가지 향상 된 MySQL 용 SSMA의 v7.5 릴리스에서 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.5 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA는 되 고 중단 되었습니다.

## <a name="ssma-v74"></a>SSMA v7.4
MySQL 용 SSMA의 v7.4 릴리스에서 다음 변경 내용이 포함 되어 있습니다.
- **쿼리 제한 시간** 옵션은 원본 및 대상에서 스키마 개체 검색 하는 동안 이제 사용할 수 있습니다.
![쿼리 제한 시간 옵션](../media/query-timeout_red.png)
- 품질 및 변환 메트릭은 고객 의견에 따라 대상된 수정 프로그램으로 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.4 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA는 되 고 중단 되었습니다. 

## <a name="ssma-v73"></a>SSMA v7.3
MySQL 용 SSMA의 v7.3 릴리스에서 다음 변경 내용이 포함 되어 있습니다.
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
MySQL 용 SSMA의 v 7.2가 사전 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.
- 향상 된 품질 및 변환 메트릭을 고객 의견에 따라 수정 프로그램을 대상된으로 합니다.
- 원격 분석의 향상 된 기능 고객 문제를 해결 하 고 SSMA의 변환율 향상에 더 나은 데이터 요소를 제공 합니다.

## <a name="ssma-v71"></a>SSMA v7.1
Access 용 SSMA의 v7.1 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
- Windows 및 Linux c t p 1에서 SQL Server 2017 마이그레이션에 지원 되는 대상 플랫폼 되었습니다. 이 기능은 기술 미리 보기 상태에서 이며 대상 SQL 서버에 스키마 및 데이터를 이동할 수 있습니다.
- SSMA는 이제 자동으로 업데이트 되는 사용 가능한 즉시 최신 버전의 SSMA 다운로드를 지원 합니다.
- SSMA 설치할 수 있는 이진 파일은 이제 Windows installer 패키지 파일 (.msi)을 통해 배달 됩니다.

**리소스**

[SQL Server Migration Assistant의 변환 기능을 확장합니다.](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[평가 하 고 SQL Server에 Microsoft 이외의 데이터 플랫폼에서 데이터를 마이그레이션할 *(예: Oracle) 있음*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 년 5 월  
MySQL 용 SSMA의 2016 년 5 월 릴리스에서 다음 변경 내용이 들어: 합니다.

-  SQL Server 2016에 대 한 지원이 추가 되었습니다.
-  향상 된 파서 및 확인자입니다.
-  .NET 2.0에 대 한 설치 관리자 검사를 제거 합니다.
-  업데이트 된 확장 팩 종속성.Net 3.5에서에서.Net 4.0 합니다.
-  MySql에 대 한 수정 된 기본 BigInt typemapping 합니다.
-  프로젝트"저장" 고정 및 SSMA 콘솔에 대 한 프로젝트 열기 명령입니다.
-  SSMA 콘솔에 대 한 고정된 "securepassword" 명령입니다.
-  고정 되는 초기 로드에 대 한 개체의 수를 계산 합니다.
-  고정된 MsSql 개체를 로드 합니다.
-  전역 설정에서 수정 된 버그입니다.
 
## <a name="march-2016"></a>2016 년 3 월  
MySQL 용 SSMA의 2016 년 3 월 미리 보기 릴리스에서 다음과 같은 변경을 포함 되어 있습니다.  
  
-  SQL Server 2016으로 마이그레이션에 대 한 지원이 추가 되었습니다. 
  
## <a name="january-2016"></a>2016 년 1 월  
MySQL 용 SSMA의 2016 년 1 월 유지 보수 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-  SSMA (RFC 5706203)에 추가 된 보기 로그의 메뉴 항목입니다.  
-  추가 된 원격 분석 합니다.  
  
## <a name="july-2014"></a>2014 년 7 월  
MySQL 용 SSMA의 2014 년 7 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-  향상 된 Azure SQL DB 코드 변환 합니다. 
-  Azure SQL DB를 지원 하기 위해 확장 팩 기능 스키마로 이동 합니다.  
-  성능 향상 10k 사용 하 여 데이터베이스에 대 한 개체를 테스트합니다.  
-  많은 수의 개체를 처리 하기 위한 UI 개선 되었습니다.  
-  (되므로 변환 과정에서 무시)의 "알려진" LOB 스키마 강조 표시 합니다.  
-  변환 속도 향상 합니다.  
-  UI에서 개체 수를 표시 합니다.  
-  25%를 초과 하 여 크기 감소를 보고 합니다.  
-  구문 분석 되지 않은 구문에 대 한 향상 된 오류 메시지입니다.  
  
## <a name="april-2014"></a>2014 년 4 월  
MySQL 용 SSMA의 2011 년 7 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-  MS SQL Server 2014의 지원이 추가 되었습니다.  
-  Azure에 변환에 대 한 수정 된 버그  
-  IE 10에서 보이지 않는 보고서 페이지에 대 한 수정 된 버그입니다.  
  
## <a name="july-2011"></a>2011 년 7 월  
MySQL 용 SSMA의 2011 년 7 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   제한으로의 변환이 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"에서 오프셋 합니다.  
-   향상 된 오류 데이터 마이그레이션 중에 보고 합니다.  
  
## <a name="april-2011"></a>2011 년 4 월  
MySQL 용 SSMA의 2011 년 4 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   설치 가능 "SSMA에 대 한 MySQL의" 수 있도록 지 원하는 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 년 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"와 Azure SQL 합니다.  
-   연결 하는 기능 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"로 지정 합니다.  
-   데이터의 병렬 마이그레이션을 지 원하는 향상 된 클라이언트 쪽 데이터 마이그레이션 엔진입니다.  
-   향상 된 데이터 마이그레이션 성능 단순 및 대량 로그 복구 모델.  
-   SSMA 콘솔 MySQL 버전에 대 한 이전 버전과 호환성을 지원합니다. SSMA v5.0 이전 버전에서 만든 프로젝트를 열 수 있습니다.  
-   V5.0 제품 수 있습니다. MySQL 용 SSMA SSMA 제품의 이전 버전으로 나란히 (SxS)를 설치 합니다.  
  
## <a name="july-2010"></a>2010 년 7 월  
MySQL 용 SSMA의 2010 년 7 월 릴리스는 다음과 같은 기능이 포함 되어 있습니다.  
  
1.  **사용자 인터페이스 개선:**  
  
    -   MySQL 데이터베이스 개체에 대 한 ' SQL 모드 ' 탭  
    -   MySQL 데이터베이스 개체에 대 한 [설정] 탭  
    -   MySQL 테이블에 대 한 '데이터' 탭  
    -   변환 및 마이그레이션 페이지에서 업데이트 된 프로젝트 설정  
    -   테이블 수준에서 ' 데이터 마이그레이션 설정 '  
  
2.  **MySQL 및 SQL Server에 연결 하는 개선:**  
  
    -   MySQL에서 SSL 연결  
    -   SQL Server에서 암호화 된 연결  
  
3.  **MySQL 메타 베이스 탐색기 개선 사항:**  
  
    -   모든 MySQL 데이터베이스 개체 및 해당 탭을 로드 합니다.  
  
4.  **개체의 변환 개선:**  
  
    -   MySQL 메타 베이스 개체 – 프로시저, 함수, 뷰, 트리거 및 문을으로 변환 됩니다.  
    -   테이블의 공간 데이터 형식에 대 한 제한적된으로 지원 합니다.  
    -   SQL Server 저장 프로시저에 MySQL 함수를 변환 하는 옵션  
    -   옵션 개체를 변환 하는 동안 SQL 모드 및 Charset 매핑을 적용 하려면  
  
5.  **데이터 마이그레이션에 대 한 개선:**  
  
    -   서버 쪽 및 클라이언트 쪽 데이터 마이그레이션 엔진 둘 다 사용 하 여 데이터 마이그레이션에 대 한 지원  
    -   공간 데이터 마이그레이션에 대 한 지원  
    -   테이블에 대 한 데이터 마이그레이션에 대 한 사용자 지정 SQL  
  
6.  **MySQL 콘솔 용 SSMA:**  
  
    -   MySQL 용 SSMA 콘솔 기능 지원  
    -   스크립트 수준 상호 작용에 대 한 지원  
  
## <a name="january-2010"></a>2010년 1월  
MySQL 용 SSMA의 2010 년 1 월 릴리스에서 초기 릴리스가 했습니다. 이 다음과 같은 기능이 포함 되어 있습니다.  
  
-   둘 다에 마이그레이션에 대 한 지원 추가 온-프레미스 SQL Server 및 Azure SQL 합니다.  
  
-   **기능 스냅숏:** 스키마 및 데이터 마이그레이션을의 MySQL 테이블/인덱스/제약 조건입니다.
