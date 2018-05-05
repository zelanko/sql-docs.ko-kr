---
title: SSMA for d b 2의에서 새로운 기능 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
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
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ddfcf888930c5667d815783d3a0c7052b7c11c0a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>SSMA for d b 2의에서 새로운 기능 (DB2ToSQL)
이 항목에서는 각 릴리스의 DB2 변경에 대 한 SSMA를 나열 합니다.  

## <a name="ssma-v77"></a>SSMA v7.7
D b 2 용 SSMA의 v7.7 릴리스에서 다음 변경 내용이 포함 되어 있습니다.
- D b 2 용 SSMA 품질 및 변환 메트릭을 향상 된 대상으로 지정 된 수정 사항으로 향상 되었습니다.
- 많은 요청에 따라, 32 비트 버전의 SSMA for d b 2 ´ ù. 이전 구현을 v7.4) (이전에 비해, 두 개의 설치 관리자 패키지 있지만 나란히 설치할 수 없습니다. 결과적으로,가지고 연결 구성 요소에 따라 가장 적합 한 버전을 선택 해야 합니다. 항상 가능한 경우 64 비트 버전을 사용 하는 것이 좋습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수 구성 요소입니다.

## <a name="ssma-v76"></a>SSMA v7.6
D b 2 용 SSMA의 v7.6 릴리스 품질 및 변환 메트릭을 향상 된 대상으로 지정 된 수정 사항 및 SQL Server 2017 (공개 미리 보기)에 대 한 지원이 향상 되었습니다. Windows 및 Linux에서 SQL Server 2017에 대 한 지원을 공개 미리 보기 이므로 프로덕션 마이그레이션에 사용할 수 없습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이상 버전을 사용 하 여.Net 4.5.2는 설치 필수 구성 요소 이며 도구의 32 비트 버전도 않습니다.

## <a name="ssma-v75"></a>SSMA v7.5
장애가 있는 사용자에 대 한 큰 액세스 가능성을 확인 하려면 몇 가지 향상 된 d b 2 용 SSMA의 v7.5 릴리스에서 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.5 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA는 되 고 중단 되었습니다.

## <a name="ssma-v74"></a>SSMA v7.4
D b 2 용 SSMA의 v7.4 릴리스에서 다음 변경 내용이 포함 되어 있습니다.
- **쿼리 제한 시간** 옵션은 원본 및 대상에서 스키마 개체 검색 하는 동안 이제 사용할 수 있습니다.
![쿼리 제한 시간 옵션](../media/query-timeout_red.png)

- 품질 및 변환 메트릭은 고객 의견에 따라 대상된 수정 프로그램으로 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.4 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA는 되 고 중단 되었습니다.

## <a name="ssma-v73"></a>SSMA v7.3
D b 2 용 SSMA의 v7.3 릴리스에서 다음 변경 내용이 포함 되어 있습니다.
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
D b 2 용 SSMA의 v 7.2가 사전 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
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
D b 2 용 SSMA의 2016 년 5 월 릴리스에서 다음과 같은 변경 내용이 포함 되어 있습니다.  

-  SQL Server 2016에 대 한 지원이 추가 되었습니다.
-  추가 된 SQL Server 메모리 내 모드 및 hekaton 기능으로 DB2 메모리 내 모드와 일반 테이블 변환 합니다.
-  SQL Server 정책 개체가 (d b 2에 대 한 행 수준 보안)을 DB2 액세스 제어의 추가 된 변환 합니다.
-  SQL Server 임시 테이블에 DB2 시스템 버전 테이블의 추가 된 변환 합니다.
-  향상 된 DB2 파서 및 확인자입니다.
-  .NET 2.0에 대 한 설치 관리자 검사를 제거 합니다.
-  Db2 설치 관리자에서 불필요 한 *.dll을 제거 합니다.
-  프로젝트"저장" 고정 및 SSMA 콘솔에 대 한 프로젝트 열기 명령입니다.
-  SSMA 콘솔에 대 한 고정된 "securepassword" 명령입니다.
-  고정 되는 초기 로드에 대 한 개체의 수를 계산 합니다.
-  전역 설정에서 수정 된 버그입니다.
  
## <a name="march-2016"></a>2016 년 3 월  
D b 2 용 SSMA의 2016 년 3 월 미리 보기 릴리스에서 다음과 같은 변경을 포함 되어 있습니다.  
  
-  SQL Server 2016으로 마이그레이션에 대 한 지원이 추가 되었습니다.  
  
## <a name="january-2016"></a>2016 년 1 월  
D b 2 용 SSMA의 2016 년 1 월 유지 보수 릴리스는 다음과 같은 변경을 포함 되어 있습니다.  
  
-  다양 한 표준 함수에 대 한 지원이 추가 되었습니다.  
-  DB2 파서 오류를 수정 했습니다.  
-  고정된 DB2 v9 zOS (RFC 5690920)를 지원 합니다.  
-  고정된 DB2 식별자 오류를 확인할 수 없는 변환 중입니다.  
-  SSMA (RFC 5706203)에 추가 된 보기 로그의 메뉴 항목입니다.  
-  추가 된 원격 분석 합니다.
  
## <a name="november-2014"></a>2014 년 11 월  
D b 2 용 SSMA의 2014 년 11 월 릴리스에서 초기 릴리스가 했습니다.
