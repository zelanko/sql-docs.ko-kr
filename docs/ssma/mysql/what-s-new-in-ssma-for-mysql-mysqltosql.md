---
title: MySQL 용 SSMA의 새로운 기능 (MySQLToSql) | Microsoft Docs
description: 각 릴리스에 대 한 MySQL (MySQLToSQL)에 대 한 변경 SQL Server Migration Assistant 내용에 대해 알아봅니다.
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 6/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
ms.author: alexiva
ms.openlocfilehash: ce77e0e9a3421fab7f1fc031bbf55e8a84c235df
ms.sourcegitcommit: e572f1642f588b8c4c75bc9ea6adf4ccd48a353b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2020
ms.locfileid: "84778065"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>MySQL용 SSMA의 새로운 기능(MySQLToSql)

이 문서에서는 각 릴리스의 MySQL 변경 내용에 대 한 SSMA (SQL Server Migration Assistant)를 나열 합니다.

## <a name="ssma-v810"></a>SSMA v 8.10

MySQL 용 SSMA의 v 8.10 릴리스에는 약간의 성능 향상 및 버그 수정이 포함 되어 있습니다.

## <a name="ssma-v89"></a>SSMA v 8.9

MySQL 용 SSMA 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 공간 형식의 데이터 마이그레이션에 대 한 수정
* 프로젝트 이름에서 특수 문자를 사용 하 여 문제 해결

## <a name="ssma-v88"></a>SSMA v 8.8

MySQL 용 SSMA의 v 8.8 릴리스에는 다음이 포함 됩니다.

* SQL Server 개체 동기화 안정성 향상
* 평가 및 변환 중 GUI 성능 향상

## <a name="ssma-v87"></a>SSMA v 8.7

MySQL 용 SSMA의 v2.0 릴리스에는 그래픽 사용자 인터페이스의 약간 수정 및 성능 향상 기능이 있습니다.

또한 Azure SQL을 대상으로 하는 경우에는 이제 MySQL 용 SSMA가 변환 절을 제공 합니다 `LIMIT` .

> [!IMPORTANT]
> SSMA v 8.5 이상에서 .NET 4.7.2는 설치 필수 구성 요소입니다. 이 버전을 설치 해야 하는 경우 [여기](https://dotnet.microsoft.com/download/dotnet-framework/net472)에서 런타임 파일을 다운로드할 수 있습니다.

## <a name="ssma-v86"></a>SSMA v 8.6

사용자가 변환 된 코드에서 SSMA 확장 속성을 생략할 수 있도록 하는 설정을 추가 하 여 MySQL 용 SSMA의 v 8.6 릴리스가 향상 되었습니다.

이 설정을 활용 하려면 MySQL 용 ssma에서 **도구**  >  **프로젝트 설정**  >  **일반**  >  **변환**으로 이동한 다음 **기타**에서 **확장 속성 생략** 설정의 값을 **예**로 업데이트 합니다.

![확장 속성 설정 생략](../mysql/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> SSMA v 8.5 이상에서 .NET 4.7.2는 설치 필수 구성 요소입니다. 이 버전을 설치 해야 하는 경우 [여기](https://dotnet.microsoft.com/download/dotnet-framework/net472)에서 런타임 파일을 다운로드할 수 있습니다.

## <a name="ssma-v85"></a>SSMA v 8.5

MySQL 용 SSMA의 v 8.5 릴리스는 유용성 및 성능을 향상 시 키도 록 설계 된 대상 수정 집합과 함께 Azure Active Directory 인증 및 SQL server의 JSON 기능에 대 한 기본 지원을 지원 하 여 향상 되었습니다.

> [!IMPORTANT]
> SSMA v 8.5를 사용 하는 경우 .NET 4.7.2 설치 필수 구성 요소입니다. 이 버전을 설치 해야 하는 경우 [여기](https://dotnet.microsoft.com/download/dotnet-framework/net472)에서 런타임 파일을 다운로드할 수 있습니다.

## <a name="ssma-v84"></a>SSMA v 8.4

MySQL 용 SSMA의 v 8.4 릴리스는 SQL Server 2016 이상 버전에 대 한 액세스 가능성 문제를 해결 하 고 max index 열 (16이 아닌 32을 허용 하도록)과 관련 된 버그를 수정 하도록 설계 된 대상 수정 기능을 사용 하 여 향상 되었습니다.

> [!IMPORTANT]
> SSMA 버전 7.4 (8.4)을 사용 하 여 .NET 4.5.2는 설치 필수 구성 요소입니다.

## <a name="ssma-v83"></a>SSMA v 8.3

MySQL 용 SSMA의 v2.0 릴리스는 품질 및 변환 메트릭을 향상 시 키도 록 설계 된 대상 수정 기능으로 향상 되었습니다. 또한이 MySQL 용 SSMA 릴리스는 다음과 같은 수정 사항을 제공 합니다.

* 접근성 문제를 해결 합니다.
* SQL Server 형식에 대 한 기본 지원을 추가 `hierarchyid` 합니다.

## <a name="ssma-v82"></a>SSMA v 8.2

MySQL 용 SSMA의 v 8.2 릴리스는 품질 및 변환 메트릭을 개선 하 고에 대 한 수정 사항을 위해 디자인 된 수정 사항 집합을 사용 하 여 향상 되었습니다.

* 데이터 마이그레이션 후 사용 하지 않도록 설정 된 비클러스터형 인덱스에 문제가 있습니다.
* 자동 설치 중에 .NET Framework를 검색 합니다.
* 새 버전이 다운로드 될 때 발생 하는 일시적인 충돌입니다.

> [!NOTE]
> 자동 업데이트의 알려진 문제로 인해 SSMA v 8.1에서 v 8.2로 업데이트 하지 못할 수 있습니다. 이 오류가 발생 하는 경우 새 버전을 다운로드 하 고 수동으로 설치 하세요.

## <a name="ssma-v81"></a>SSMA v 8.1

MySQL 용 SSMA의 v 8.1 릴리스는 품질 및 변환 메트릭을 향상 시 키도 록 설계 된 대상 수정 기능으로 향상 되었습니다.

> [!NOTE]
> 자동 업데이트의 알려진 문제로 인해 SSMA v 8.0에서 v 8.1로의 업데이트가 실패할 수 있습니다. 이 오류가 발생 하는 경우 새 버전을 다운로드 하 고 수동으로 설치 하세요.

## <a name="ssma-v80"></a>SSMA v 8.0

MySQL 용 SSMA의 v 8.0 릴리스는 품질 및 변환 메트릭을 개선 하기 위해 설계 된 대상 수정 기능으로 향상 되었습니다. 또한이 릴리스는 다음과 같은 새로운 기능을 제공 합니다.

* 대상으로 **Azure SQL Database Managed Instance** 지원. 이제 Azure SQL Database Managed Instance를 대상으로 하는 새 프로젝트를 만들 수 있습니다.

  ![SQL DB MI 프로젝트](../media/ssma-newproject-sqldbmi.png)

* 변환 후 **수정 관리자**입니다. [여기](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)에서 자세히 알아보세요.

* 예비 데이터베이스/스키마 선택.

  원본에 연결할 때 사용자는 이제 원하는 데이터베이스/스키마를 선택할 수 있습니다. 마이그레이션하려는 스키마만 선택 하면 초기 연결 중에 시간이 절약 되 고 전체 SSMA 성능이 향상 됩니다.

  ![SSMA 필터 개체](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

MySQL 용 SSMA의 v 7.10 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 글로벌 요구 사항에 대 한 변경 내용을 충족 하기 위해 추가 보안 및 개인 정보 보호를 제공 하도록 설계 된 대상 수정
* 함수 이름과 인수 목록 간의 공백 변환에 대 한 수정입니다.

## <a name="ssma-v79"></a>SSMA v 7.9

MySQL 용 SSMA의 v 7.9 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 품질 및 변환 메트릭을 개선 하는 대상 수정
* MySQL에서 Azure SQL Database로 공간 데이터 형식을 마이그레이션하기 위한 부분 지원.
* SSMA 명령줄에서 데이터 형식 매핑 및 프로젝트 기본 설정을 변경 하는 기능을 지원 합니다.
* SQL Server Integration Services (SSIS)를 사용 하 여 데이터 마이그레이션을 지원 합니다. 스키마를 변환한 후에는 마우스 오른쪽 단추를 클릭 하 여 상황에 맞는 메뉴 옵션을 사용 하 여 SSIS 패키지를 만들 수 있습니다.
* 또한 SSMA의 Azure SQL Database 연결 대화 상자가 정규화 된 서버 이름을 지정 하도록 변경 되었습니다. 이전 버전의 SSMA에서는 Azure SQL Database 접두사가 프로젝트 설정 내에서 명시적으로 언급 되어야 했습니다.

## <a name="ssma-v78"></a>SSMA v 7.8

MySQL 용 SSMA의 v 7.8 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 프로젝트 설정에서 강조 표시 된 형식 매핑을 변경 합니다.
* 사용자가 원격 분석을 사용 하지 않도록 설정할 수 있는 기능입니다.

## <a name="ssma-v77"></a>SSMA v 7.7

MySQL 용 SSMA의 v 7.7 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* MySQL 용 SSMA는 품질 및 변환 메트릭을 개선 하는 대상 수정 기능으로 향상 되었습니다.
* 널리 사용 되는 요구 사항에 따라 MySQL 용 SSMA의 32 비트 버전이 다시 사용 됩니다. 이전 구현에 비해 (v 7.4 이전)에는 두 개의 설치 관리자 패키지가 있지만 함께 설치할 수는 없습니다. 따라서 사용 중인 연결 구성 요소에 따라 가장 적합 한 버전을 선택 해야 합니다. 가능 하면 항상 64 비트 버전을 사용 하는 것이 좋습니다.
* 이제 MySQL 용 SSMA에는 MySQL과 호환 되는 타사 ODBC 드라이버를 사용할 수 있는 ODBC 연결 문자열 연결 모드가 있습니다.

## <a name="ssma-v76"></a>SSMA v 7.6

MySQL 용 SSMA의 v 7.6 릴리스는 품질 및 변환 메트릭을 개선 하 고 SQL Server 2017 (공개 미리 보기)에 대 한 지원으로 향상 되었습니다. Windows 및 Linux에서 SQL Server 2017에 대 한 지원은 공개 미리 보기 상태 이며 프로덕션 마이그레이션에 사용할 수 없습니다.

## <a name="ssma-v75"></a>SSMA v 7.5

장애가 있는 사용자에 게 더 많은 액세스 가능성을 보장 하기 위해 몇 가지 향상 된 기능을 통해 MySQL 용 SSMA의 v 7.5 릴리스가 향상 되었습니다.

## <a name="ssma-v74"></a>SSMA v 7.4

MySQL 용 SSMA의 v 7.4 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 이제 원본 및 대상에서 스키마 개체를 검색 하는 동안 **쿼리 제한 시간** 옵션을 사용할 수 있습니다.

    ![쿼리 제한 시간 옵션](../media/query-timeout_red.png)
* 사용자 의견에 따라 대상 수정으로 품질 및 변환 메트릭이 개선 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2은 SSMA v 7.4를 설치 하기 위한 필수 구성 요소입니다. 또한 v 7.4부터 SSMA의 32 비트 버전이 중단 됩니다.

## <a name="ssma-v73"></a>SSMA v 7.3

MySQL 용 SSMA의 v 7.3 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

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

MySQL 용 SSMA의 v 7.2 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 고객 의견을 기반으로 하는 대상 픽스로 품질 및 변환 메트릭이 개선 되었습니다.
* 향상 된 원격 분석을 통해 고객 문제를 해결 하 고 SSMA의 변환 속도를 개선할 수 있는 더 나은 데이터 요소를 제공 합니다.

## <a name="ssma-v71"></a>SSMA v 7.1

MySQL 용 SSMA의 v 7.1 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* 이제 Windows 및 Linux CTP1의 SQL Server 2017는 마이그레이션에 지원 되는 대상 플랫폼입니다. 이 기능은 technical preview 이며 SQL server를 대상으로 하는 스키마 및 데이터 이동을 허용 합니다.
* 이제 SSMA가 자동 업데이트를 지원 하 여 최신 버전의 SSMA를 사용할 수 있는 즉시 다운로드 합니다.
* 이제 Windows Installer 패키지 파일 (.msi)을 통해 SSMA를 설치할 수 있는 이진 파일이 제공 됩니다.

## <a name="may-2016"></a>2016년 5월

MySQL 용 SSMA의 2016 년 5 월 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* SQL Server 2016에 대 한 지원이 추가 되었습니다.
* 파서 및 확인자를 개선 했습니다.
* .NET 2.0에 대 한 설치 관리자 검사가 제거 되었습니다.
* .NET 3.5에서 .NET 4.0으로 확장 팩 종속성을 업데이트 했습니다.
* MySql에 대 한 기본 BigInt 형식 매핑을 수정 했습니다.
* `save-project` `open-project` Ssma 콘솔에 대 한 및 명령이 수정 되었습니다.
* `securepassword`SSMA 콘솔에 대 한 고정 명령입니다.
* 초기 로드에 대 한 개체 계산을 수정 했습니다.
* MsSql 개체 로드를 수정 했습니다.
* 전역 설정에서 버그가 수정 되었습니다.

## <a name="march-2016"></a>2016년 3월

MySQL 용 SSMA의 2016 년 3 월 preview 릴리스는 SQL Server 2016로 마이그레이션에 대 한 지원을 추가 합니다.
  
## <a name="january-2016"></a>2016년 1월

MySQL 용 SSMA의 1 월 2016 유지 관리 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.

* SSMA에 보기 로그 메뉴 항목을 추가 했습니다 (RFC 5706203).
* 원격 분석 추가.
  
## <a name="july-2014"></a>2014 년 7 월

MySQL 용 SSMA의 7 월 2014 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.
  
* Azure SQL DB 코드 변환을 개선 했습니다.
* 확장 팩 기능을 스키마로 이동 하 여 Azure SQL DB를 지원 합니다.
* 10k가 넘는 개체가 포함 된 데이터베이스에 대 한 성능 향상이 테스트 되었습니다.
* 많은 수의 개체를 처리 하기 위한 UI 개선
* 잘 알려진 LOB 스키마를 강조 표시 합니다 (변환 시 무시 될 수 있음).
* 변환 속도 향상.
* UI의 개체 수를 표시 합니다.
* 보고서 크기는 25% 이상 감소 합니다.
* 구문 분석 되지 않은 구문에 대 한 오류 메시지가 개선 되었습니다.
  
## <a name="april-2014"></a>2014년 4월

MySQL 용 SSMA의 4 월 2014 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.
  
* SQL Server 2014에 대 한 지원이 추가 되었습니다.
* Azure로의 변환과 관련 된 버그가 수정 되었습니다.
* IE 10의 보이지 않는 보고서 페이지와 관련 된 버그가 수정 되었습니다.
  
## <a name="july-2011"></a>2011년 7월

MySQL 용 SSMA의 7 월 2011 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.
  
* 에서로의 변환을 `LIMIT` 지원 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] `OFFSET` 합니다.
* 데이터 마이그레이션 중에 향상 된 오류 보고
  
## <a name="april-2011"></a>4 월 2011

MySQL 용 SSMA의 4 월 2011 릴리스에는 다음과 같은 변경 내용이 포함 되어 있습니다.
  
* [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] 및 Azure SQL을 지 원하는 "ssma for MySQL"의 단일 설치 가능 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] .
* 연결할 수 있는 권한 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 입니다.
* 데이터의 병렬 마이그레이션을 지 원하는 향상 된 클라이언트 쪽 데이터 마이그레이션 엔진.
* 단순 및 대량 로그 복구 모델로 데이터 마이그레이션 성능이 개선 되었습니다.
* MySQL 용 SSMA 콘솔 버전은 이전 버전과의 호환성을 지원 합니다. 이전 버전에서 만든 프로젝트를 SSMA v 5.0으로 열 수 있습니다.
* MySQL 용 SSMA 제품 제품을 이전 버전의 SSMA 제품과 함께 (SxS) 설치할 수 있습니다.
  
## <a name="july-2010"></a>2010년 7월

MySQL 용 SSMA의 7 월 2010 릴리스에는 다음과 같은 기능이 포함 되어 있습니다.
  
**1. 사용자 인터페이스에 대 한 향상 된 기능:**

* MySQL 데이터베이스 개체에 대 한 ' SQL 모드 ' 탭
* MySQL 데이터베이스 개체에 대 한 ' 설정 ' 탭
* MySQL 테이블의 ' 데이터 ' 탭
* 변환 및 마이그레이션 페이지에서 업데이트 된 프로젝트 설정
* 테이블 수준에서 ' 데이터 마이그레이션 설정 '
  
**2. MySQL 및 SQL Server에 연결 하기 위한 향상 된 기능:**
  
* MySQL의 SSL 연결
* SQL Server 암호화 된 연결
  
**3. MySQL 메타 베이스 탐색기의 향상 된 기능:**
  
* 모든 MySQL 데이터베이스 개체와 해당 탭을 로드 합니다.
  
**4. 향상 된 개체 변환:**
  
* MySQL 메타 베이스 개체 변환 (프로시저, 함수, 뷰, 트리거 및 문).
* 테이블의 공간 데이터 형식에 대 한 제한 된 지원.
* MySQL 함수를 SQL Server 저장 프로시저로 변환 하는 옵션
* 개체를 변환 하는 동안 SQL 모드 및 문자 집합 매핑을 적용 하는 옵션
  
**5. 데이터 마이그레이션에 대 한 향상 된 기능:**  
  
* 서버 쪽 및 클라이언트 쪽 데이터 마이그레이션 엔진을 모두 사용 하 여 데이터 마이그레이션 지원
* 공간 데이터 마이그레이션에 대 한 지원
* 테이블에 대 한 데이터 마이그레이션에 대 한 사용자 지정 SQL
  
**6. MySQL 용 SSMA 콘솔:**  
  
* MySQL 용 SSMA의 지원 콘솔 기능  
* 스크립트 수준 상호 작용에 대 한 지원  
  
## <a name="january-2010"></a>2010년 1월

MySQL 용 SSMA의 1 월 2010 릴리스는 초기 릴리스입니다. 여기에는 다음과 같은 기능이 포함 되어 있습니다.
  
* 온-프레미스 SQL Server 및 Azure SQL 모두로의 마이그레이션에 대 한 지원이 추가 되었습니다.  
  
* **기능 스냅숏:** MySQL 테이블/인덱스/제약 조건에 대 한 스키마 및 데이터 마이그레이션
