---
title: (MySQLToSql) MySQL 용 SSMA의 새로운 기능 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 06/11/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
author: HJToland3
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 5f3ea9905f0a44e7863154b93283ea8ef2f49f7b
ms.sourcegitcommit: 40e55e55a73e39d447da87d9178f2b6067f39c6f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2019
ms.locfileid: "66841069"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>MySQL용 SSMA의 새로운 기능(MySQLToSql)

이 문서에서는 MySQL 각 릴리스의 변경 내용에 대 한 SQL Server Migration Assistant (SSMA)를 나열 합니다.

## <a name="ssma-v82"></a>SSMA v8.2

MySQL 용 SSMA의 v8.1 릴리스에서 품질 및 변환 메트릭 뿐만 아니라 수정에 대 한 개선 하기 위한 수정의 대상된 집합을 사용 하 여 향상 되었습니다.

* 데이터 마이그레이션 후 비활성화 된 비클러스터형 인덱스를 사용 하 여에 문제가 있습니다.
* 자동 설치 중.NET Framework의 검색 합니다.
* 새 버전 다운로드 될 때 발생 하는 일시적인 충돌 합니다.

> [!NOTE]
> 자동 업데이트를 사용 하 여 알려진된 문제 v8.2를 SSMA v8.1에서 업데이트 오류가 발생할 수 있습니다. 이 오류가 발생 하면 새 버전을 다운로드 하 고 수동으로 설치 하세요.

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수입니다.

## <a name="ssma-v81"></a>SSMA v8.1

MySQL 용 SSMA의 v8.1 릴리스에서 품질 및 변환 메트릭을 향상 하도록 설계 된 대상된 수정 사항을 향상 되었습니다.

> [!NOTE]
> 자동 업데이트를 사용 하 여 알려진된 문제 v8.1를 SSMA v8.0에서 업데이트 오류가 발생할 수 있습니다. 이 오류가 발생 하면 새 버전을 다운로드 하 고 수동으로 설치 하세요.

## <a name="ssma-v80"></a>SSMA v8.0

MySQL 용 SSMA의 v8.0 릴리스에서 품질 및 변환 메트릭을 개선 하기 위한 대상된 수정 사항을 향상 되었습니다. 이 릴리스에 또한 다음과 같은 새로운 기능을 제공합니다.

* 에 대 한 지원 **Azure SQL Database Managed Instance** 대상으로 합니다. 이제 Azure SQL Database Managed Instance를 대상으로 하는 새 프로젝트를 만들 수 있습니다.

  ![SQL DB MI 프로젝트](../media/ssma-newproject-sqldbmi.png)

* 변환 후 **수정 advisor**합니다. 자세한 내용을 알아보세요 [여기](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)합니다.

* 임시 데이터베이스/스키마 선택 합니다.

  원본에 연결할 때 사용자가 데이터베이스/스키마 관심 이제 선택할 수 있습니다. 마이그레이션하려는 스키마만 선택 하면 초기 연결 중 시간이 절약 되 고 전반적인 SSMA 성능을 개선 합니다.

  ![SSMA 필터 개체](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

MySQL 용 SSMA의 v7.10 릴리스에서 다음 변경 내용을 포함 되어 있습니다.

* 대상된 수정 사항을 추가 보안 및 글로벌 요구 사항 변화에에서 맞게 개인 정보 보호를 제공 하도록 설계 되었습니다.
* 함수 이름과 인수 목록 사이 공백이의 변환에 대 한 수정 합니다.

## <a name="ssma-v79"></a>SSMA v7.9

MySQL 용 SSMA의 v7.9 릴리스에서 다음 변경 내용을 포함 되어 있습니다.

* 품질 및 변환 메트릭을 개선 하는 대상된 수정 되었습니다.
* MySQL에서 Azure SQL Database 마이그레이션 공간 데이터 형식에 대 한 부분 지원.
* 데이터 형식 매핑 및 프로젝트 기본 설정을 변경 하려면 SSMA 명령줄에서 지원 합니다.
* 마이그레이션에 대 한 지원 SQL Server Integration Services (SSIS)를 사용 하 여 데이터입니다. 스키마를 변환한 후 마우스 오른쪽 단추 클릭 상황에 맞는 메뉴 옵션을 사용 하 여 SSIS 패키지를 만들 수는 있습니다.
* 정규화 된 서버 이름을 지정 하려면 SSMA에서 Azure SQL Database 연결 대화 상자도 변경 되었습니다. SSMA의 이전 버전에서는 Azure SQL Database 접두사 프로젝트 설정 내에서 명시적으로 언급 해야 했습니다.

## <a name="ssma-v78"></a>SSMA v7.8

MySQL 용 SSMA의 v 7.8 릴리스에서 다음 변경 내용을 포함 되어 있습니다.

* 프로젝트 설정에서 강조 표시 하는 형식 매핑을 변경 합니다.
* 원격 분석을 사용 하지 않도록 설정 하는 작업을 할 수 있습니다.

## <a name="ssma-v77"></a>SSMA v7.7

MySQL 용 SSMA의 v7.7 릴리스에서 다음 변경 내용을 포함 되어 있습니다.

* 품질 및 변환 메트릭을 개선 하는 대상된 수정 사항을 사용 하 여 MySQL 용 SSMA 향상 되었습니다.
* MySQL 용 SSMA의 32 비트 버전 다시은 인기 있는 필요에 따라입니다. (이전 v7.4) 이전 구현에 비해, 두 개의 설치 관리자 패키지 있지만 나란히 설치할 수 없습니다. 결과적으로, 해야 연결 구성 요소에 따라 가장 적합 한 버전을 선택 해야 합니다. 항상 가능한 경우 64 비트 버전을 사용 하는 것이 좋습니다.
* MySQL 용 SSMA MySQL과 호환 되는 모든 타사 ODBC 드라이버를 사용할 수 있는 ODBC 연결 문자열 연결 모드를 얻었습니다.

## <a name="ssma-v76"></a>SSMA v7.6

MySQL 용 SSMA의 v7.6 릴리스에서 품질 및 변환 메트릭을 개선 하는 대상된 수정 사항을 SQL Server 2017 (공개 미리 보기)에 대 한 지원이 향상 되었습니다. Windows 및 Linux에서 SQL Server 2017에 대 한 지원을 공개 미리 보기로 제공 않으며 프로덕션 마이그레이션에 사용할 수 없습니다.

## <a name="ssma-v75"></a>SSMA v7.5

장애가 있는 사용자에 큰 액세스 가능성을 보장 하기 위해 여러 향상 된 기능을 사용 하 여 MySQL 용 SSMA의 v7.5 릴리스에서 향상 되었습니다.

## <a name="ssma-v74"></a>SSMA v7.4

MySQL 용 SSMA의 v7.4 릴리스에서 다음 변경 내용을 포함 되어 있습니다.

* 합니다 **쿼리 제한 시간** 옵션을 원본 및 대상 스키마 개체 검색 하는 동안 제공 됩니다.

    ![쿼리 제한 시간 옵션](../media/query-timeout_red.png)
* 품질 및 변환 메트릭, 고객 피드백에 따라 대상된 수정 사항을 사용 하 여 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.4 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA이 이제 중단 됩니다.

## <a name="ssma-v73"></a>SSMA v7.3

MySQL 용 SSMA의 v7.3 릴리스에서 다음 변경 내용을 포함 되어 있습니다.

* 향상 된 품질 및 변환 메트릭 고객 피드백에 따라 대상된 수정 사항 사용 하 여입니다.
* SSMA 확장성 프레임 워크는 다음 항목을 통해 노출 합니다.
  * SQL Server Data Tools (SSDT) 프로젝트에 기능을 내보냅니다.
    * 이제 SSDT 프로젝트 SSMA에서 스키마 스크립트를 내보낼 수 있습니다. 추가 스키마 변경을 수행 하 여 데이터베이스를 배포 하는 스키마 스크립트를 사용할 수 있습니다.

      ![SSDT 프로젝트 명령으로 저장](../media/export-schema-scripts_red.png)
  * SSMA 사용자 지정 변환을 수행 하는 데 사용할 수 있는 라이브러리입니다.
    * 이제 사용자 지정 구문 변환 및 SSMA 이전에 처리 되지 않은 변환을 처리할 수 있는 코드를 생성할 수 있습니다.
      * 이 블로그 게시물에서는 사용자 지정 변환기를 생성 하는 방법에 사용할 [확장 SQL Server Migration Assistant의 변환 기능](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)합니다.
      * 이 변환에 대 한 샘플 프로젝트를 다운로드 [블로그 게시물](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)합니다.

## <a name="ssma-v72"></a>SSMA v7.2

MySQL 용 SSMA의 v 7.2가 사전 릴리스는 다음 변경 내용이 포함 되어 있습니다.

* 향상 된 품질 및 변환 메트릭 고객 피드백에 따라 대상된 수정 사항 사용 하 여입니다.
* 더 나은 데이터 요소를 고객 문제를 해결 하 여 SSMA의 전환율을 향상 시킬 수 있도록 원격 분석 향상 된 기능입니다.

## <a name="ssma-v71"></a>SSMA v7.1

MySQL 용 SSMA의 v7.1 릴리스에서 다음 변경 내용을 포함 되어 있습니다.

* Windows 및 Linux CTP1에서 SQL Server 2017 마이그레이션에 대 한 지원 되는 대상 플랫폼 되었습니다. 이 기능은 기술 미리 보기로 제공 되며 대상 SQL server에 스키마 및 데이터 이동할 수 있습니다.
* SSMA는 이제 사용 가능한 즉시 최신 버전의 SSMA 다운로드 하려면 자동 업데이트를 지원 합니다.
* SSMA 설치 가능 이진 파일은 이제 Windows installer 패키지 파일 (.msi)를 통해 전달 됩니다.

## <a name="may-2016"></a>2016 년 5 월  
MySQL 용 SSMA의 2016 년 5 월 릴리스에서 다음 변경 내용을 포함 되어 있습니다.

* SQL Server 2016에 대 한 지원이 추가 되었습니다.
* 향상 된 파서 및 확인자입니다.
* .NET 2.0에 대 한 설치 관리자 검사를 제거 합니다.
* 업데이트 된 확장 팩 종속성.Net 3.5에서에서.net 4.0입니다.
* MySql에 대 한 수정 된 기본 BigInt 형식 매핑입니다.
* "저장"프로젝트 수정 및 SSMA 콘솔에 대 한 프로젝트 열기 명령입니다.
* SSMA 콘솔에 대 한 고정된 "securepassword" 명령입니다.
* 초기 로드에 대 한 개체의 계산을 고정 합니다.
* 고정된 MsSql 개체를 로드 합니다.
* 전역 설정에 대 한 버그가 수정 되었습니다.

## <a name="march-2016"></a>2016 년 3 월

MySQL 용 SSMA의 2016 년 3 월 미리 보기 릴리스의 SQL Server 2016으로 마이그레이션에 대 한 지원을 추가합니다. 
  
## <a name="january-2016"></a>2016 년 1 월

MySQL 용 SSMA의 2016 년 1 월 유지 관리 릴리스는 다음 변경 내용을 포함 되어 있습니다.  

* 추가 뷰는 메뉴 항목을 로그 하 SSMA (RFC 5706203)입니다.  
* 추가 원격 분석입니다.  
  
## <a name="july-2014"></a>2014 년 7 월

MySQL 용 SSMA의 2014 년 7 월 릴리스에서 다음 변경 내용을 포함 되어 있습니다.  
  
* 향상 된 Azure SQL DB 코드 변환 합니다. 
* Azure SQL DB를 지원 하도록 확장 팩 기능 스키마로 이동 합니다.  
* 성능 향상 10k를 사용 하 여 데이터베이스에 대 한 개체를 테스트 합니다.  
* 많은 수의 개체를 처리 하기 위한 UI 개선 사항.  
* (따라서 변환에서 무시)의 "알려진" LOB 스키마 강조 표시 합니다.  
* 변환 속도 향상 되었습니다.  
* UI에서 개체 수를 표시 합니다.  
* 25% 이상 크기 감소를 보고 합니다.  
* 구문 분석 되지 않은 구문에 대 한 향상 된 오류 메시지입니다.  
  
## <a name="april-2014"></a>2014 년 4 월

MySQL 용 SSMA의 2014 년 4 월 릴리스에서 다음 변경 내용을 포함 되어 있습니다.  
  
* MS SQL Server 2014 지원이 추가 되었습니다.  
* Azure에 변환에 대 한 수정 된 버그  
* IE 10에서 보이지 않는 보고서 페이지에 대 한 수정 된 버그입니다.  
  
## <a name="july-2011"></a>2011 년 7 월

MySQL 용 SSMA의 2011 년 7 월 릴리스에서 다음 변경 내용을 포함 되어 있습니다.  
  
* 제한의 변환이 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali"에서 오프셋입니다.  
* 데이터 마이그레이션 중에 보고 기능 향상 된 오류입니다.  
  
## <a name="april-2011"></a>2011 년 4 월

MySQL 용 SSMA의 2011 년 4 월 릴리스에서 다음 변경 내용을 포함 되어 있습니다.  
  
* "SSMA for MySQL"에 지의 설치 가능한 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" 및 Azure SQL입니다.  
* 연결 하는 기능 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali"로 지정 합니다.  
* 데이터의 병렬 마이그레이션을 지 원하는 향상 된 클라이언트 쪽 데이터 마이그레이션 엔진입니다.  
* 향상 된 데이터 마이그레이션 성능을 단순 및 대량 로그 복구 모델.  
* SSMA MySQL 콘솔 버전에 대 한 이전 버전과 호환성을 지원합니다. SSMA v5.0 이전 버전에서 만든 프로젝트를 열 수 있습니다.  
* V5.0 제품 수는 MySQL 용 SSMA SSMA 제품의 이전 버전과 나란히 (SxS)를 설치 합니다.  
  
## <a name="july-2010"></a>2010 년 7 월

MySQL 용 SSMA의 2010 년 7 월 릴리스에서 다음과 같은 기능이 포함 되어 있습니다.  
  
1. **사용자 인터페이스 개선:**  
  
    * MySQL 데이터베이스 개체에 대 한 ' SQL 모드 ' 탭  
    * MySQL 데이터베이스 개체에 대 한 '설정' 탭  
    * MySQL 테이블에 대 한 '데이터' 탭  
    * 변환 및 마이그레이션 페이지에서 업데이트 된 프로젝트 설정  
    * 테이블 수준에서 ' 데이터 마이그레이션 설정 '  
  
2. **MySQL 및 SQL Server에 연결할 개선:**  
  
    * MySQL에 SSL 연결  
    * SQL Server에서 암호화 된 연결  
  
3. **MySQL Metabase Explorer 기능 개선:**  
  
    * 모든 MySQL 데이터베이스 개체와 해당 개별 탭을 로드 합니다.  
  
4. **개체 변환 기능 개선:**
  
    * 프로시저, 함수, 뷰, 트리거 및 문을 MySQL 메타 베이스 개체의 변환입니다.  
    * 테이블의 공간 데이터 형식에 대 한 제한적으로 지원 합니다.
    * SQL Server 저장 프로시저에 MySQL 함수를 변환 하는 옵션  
    * 개체 변환 하는 동안 SQL 모드 및 문자 집합 매핑을 적용 하는 옵션  
  
5. **데이터 마이그레이션 기능 개선:**  
  
    * 서버 쪽 및 클라이언트 쪽 데이터 마이그레이션 엔진을 사용 하 여 데이터 마이그레이션에 대 한 지원  
    * 공간 데이터 마이그레이션에 대 한 지원  
    * 테이블에 대 한 데이터 마이그레이션에 대 한 사용자 지정 SQL  
  
6. **SSMA MySQL 콘솔에 대 한 합니다.**  
  
    * MySQL 용 SSMA 콘솔 기능 지원  
    * 스크립트 수준 상호 작용에 대 한 지원  
  
## <a name="january-2010"></a>2010년 1월

MySQL 용 SSMA의 2010 년 1 월 릴리스에서 초기 릴리스가 였습니다. 다음 기능은 포함 합니다. 
  
* 둘 다로 마이그레이션에 대 한 지원이 추가 되었습니다 온-프레미스 SQL Server 및 Azure SQL입니다.  
  
* **스냅숏 기능:** 스키마 및 데이터 마이그레이션의 MySQL 테이블/인덱스/제약 조건입니다.
