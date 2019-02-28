---
title: Access(AccessToSQL) 용 SSMA의 새로운 기능 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 02/27/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 40d5daaaef68d4355a95fb6cef2c55628cdf4008
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955924"
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>SSMA for Access (AccessToSQL)의 새로운 기능
이 문서는 각 릴리스에 대 한 액세스 변경에 대 한 SQL Server Migration Assistant (SSMA)를 나열합니다.  

## <a name="ssma-v80"></a>SSMA v8.0
품질 및 변환 메트릭을 개선 하기 위한 대상된 수정 사항을 제공 하려면 SSMA for Access v8.0 릴리스의 향상 되었습니다. 이 릴리스에 또한 다음과 같은 새로운 기능을 제공합니다.

* 에 대 한 지원 **Azure SQL Database Managed Instance** 대상으로 합니다. 이제 Azure SQL Database Managed Instance를 대상으로 하는 새 프로젝트를 만들 수 있습니다.

  ![SQL DB MI 프로젝트](../media/ssma-newproject-sqldbmi.png)

*   변환 후 **수정 advisor**합니다. 자세한 내용을 알아보세요 [여기](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)합니다.

* 임시 데이터베이스/스키마 선택 합니다.

    원본에 연결할 때 사용자가 데이터베이스/스키마 관심 이제 선택할 수 있습니다. 마이그레이션하려는 스키마만 선택 하면 초기 연결 중 시간이 절약 되 고 전반적인 SSMA 성능을 개선 합니다.

    ![SSMA 필터 개체](../media/ssma-filter-objects.png)

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수입니다.


## <a name="ssma-v710"></a>SSMA v7.10
SSMA for Access v7.10 릴리스의 추가 보안 및 글로벌 요구 사항 변화에에서 맞게 개인 정보 보호를 제공 하도록 설계 하는 대상된 수정 사항을 사용 하 여 향상 되었습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수입니다.

## <a name="ssma-v79"></a>SSMA v7.9
SSMA for Access v7.9 릴리스는 다음 변경 내용을 포함 되어 있습니다.
- 품질 및 변환 메트릭을 개선 하는 대상된 수정 되었습니다.
- 데이터 형식 매핑 및 프로젝트 기본 설정을 변경 하려면 SSMA 명령줄에서 지원 합니다.
- 정규화 된 서버 이름을 지정 하려면 SSMA에서 Azure SQL Database 연결 대화 상자도 변경 되었습니다. SSMA의 이전 버전에서는 Azure SQL Database 접두사 프로젝트 설정 내에서 명시적으로 언급 해야 했습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수입니다.

## <a name="ssma-v78"></a>SSMA v7.8
SSMA for Access v 7.8 릴리스는 다음 변경 내용을 포함 되어 있습니다.
- 프로젝트 설정에서 강조 표시 된 변경 형식 매핑입니다.
- 사용자가 원격 분석을 사용 하지 않도록 설정 하는 기능을 제공 합니다.

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수입니다.

## <a name="ssma-v77"></a>SSMA v7.7
SSMA for Access v7.7 릴리스는 다음 변경 내용을 포함 되어 있습니다.
- Access 용 SSMA 품질 및 변환 메트릭을 개선 하는 대상된 수정 사항을 사용 하 여 향상 되었습니다.
- Access 용 SSMA의 32 비트 버전 다시은 인기 있는 필요에 따라입니다. (이전 v7.4) 이전 구현에 비해, 두 개의 설치 관리자 패키지 있지만 나란히 설치할 수 없습니다. 결과적으로, 해야 연결 구성 요소에 따라 가장 적합 한 버전을 선택 해야 합니다. 항상 가능한 경우 64 비트 버전을 사용 하는 것이 좋습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는.Net 4.5.2는 설치 필수입니다.

## <a name="ssma-v76"></a>SSMA v7.6
SSMA for Access v7.6 릴리스의 품질 및 변환 메트릭을 개선 하는 대상된 수정 사항을 SQL Server 2017 (공개 미리 보기)에 대 한 지원이 향상 되었습니다. Windows 및 Linux에서 SQL Server 2017에 대 한 지원을 공개 미리 보기로 제공 되며 프로덕션 마이그레이션에 사용할 수 없습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이후 버전에서는 사용 하 여.Net 4.5.2는 설치 필수 이며 도구의 32 비트 버전은 지원 되지 않습니다.

## <a name="ssma-v75"></a>SSMA v7.5
SSMA for Access v7.5 릴리스의 장애가 있는 사용자에 큰 액세스 가능성을 보장 하기 위해 여러 향상 된 기능을 사용 하 여 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.5 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA이 이제 중단 됩니다.

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for Access v7.4 릴리스는 다음 변경 내용을 포함 되어 있습니다.
- 합니다 **쿼리 제한 시간** 옵션을 원본 및 대상 스키마 개체 검색 하는 동안 제공 됩니다.
![쿼리 제한 시간 옵션](../media/query-timeout_red.png)

- 품질 및 변환 메트릭, 고객 피드백에 따라 대상된 수정 사항을 사용 하 여 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.4 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA이 이제 중단 됩니다.

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for Access v7.3 릴리스는 다음 변경 내용을 포함 되어 있습니다.
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
SSMA for Access v 7.2가 사전 릴리스는 다음 변경 내용을 포함 되어 있습니다.
- 향상 된 품질 및 변환 메트릭 고객 피드백에 따라 대상된 수정 사항 사용 하 여입니다.
- 더 나은 데이터 요소를 고객 문제를 해결 하 여 SSMA의 전환율을 향상 시킬 수 있도록 원격 분석 향상 된 기능입니다.

## <a name="ssma-v71"></a>SSMA v7.1
SSMA for Access v7.1 릴리스는 다음 변경 내용을 포함 되어 있습니다.
- Windows 및 Linux CTP1에서 SQL Server 2017 마이그레이션에 대 한 지원 되는 대상 플랫폼 되었습니다. 이 기능은 기술 미리 보기 상태에서 이며 대상 SQL server에 스키마 및 데이터 이동을 지원 합니다.
- SSMA는 이제 사용 가능한 즉시 최신 버전의 SSMA 다운로드 하려면 자동 업데이트를 지원 합니다.
- SSMA 설치 가능 이진 파일은 이제 Windows installer 패키지 파일 (.msi)를 통해 전달 됩니다.

**리소스**

[SQL Server Migration Assistant의 변환 기능 확장](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)
  
## <a name="may-2016"></a>2016 년 5 월  
Access 용 SSMA의 2016 년 5 월 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-  SQL Server 2016에 대 한 공식 지원 추가
-  .NET 2.0에 대 한 설치 관리자 검사를 제거 합니다.
-  "저장"프로젝트 수정 및 SSMA 콘솔에 대 한 프로젝트 열기 명령입니다.
-  SSMA 콘솔에 대 한 고정된 "securepassword" 명령입니다.
-  초기 로드에 대 한 개체의 계산을 고정 합니다.
-  테이블 데이터 액세스에 대 한 UI 탭에 대 한 로드를 고정 합니다.
-  전역 설정에 대 한 버그가 수정 되었습니다. 
   
## <a name="march-2016"></a>2016 년 3 월  
Access 용 SSMA의 2016 년 3 월 미리 보기 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-  SQL Server 2016으로 마이그레이션에 대 한 지원이 추가 되었습니다.  
   
## <a name="january-2016"></a>2016 년 1 월  
Access 용 SSMA의 2016 년 1 월 유지 관리 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-  GUID 필드 (RFC 3894811)의 기본값에 대 한 잘못 된 함수를 고정된 합니다.  
-  SQL Database (Azure) (RFC 4919573)로 레코드 가져오기에 대 한 고정된 중단 됩니다.  
-  추가 뷰는 메뉴 항목을 로그 하 SSMA (RFC 5706203)입니다.  
-  추가 원격 분석입니다.  
  
## <a name="july-2014"></a>2014 년 7 월  
Access 용 SSMA의 2014 년 7 월 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-   향상 된 Azure SQL DB 코드 변환 합니다.  
-   Azure SQL DB를 지원 하도록 스키마를 확장 팩 기능을 이동 합니다.  
-   10 개의 개체를 사용 하 여 데이터베이스에 대 한 테스트 성능이 향상 되었습니다.  
-   많은 수의 개체를 처리 하기 위한 향상 된 UI가 추가 되었습니다.  
-   (따라서 변환에서 무시)의 "알려진" LOB 스키마 강조 표시에 대 한 지원이 추가 되었습니다.  
-   변환 속도 향상을 추가 합니다.
-   UI에서 개체를 표시 하기 위한 추가 지원 계산 합니다.
-   25% 이상 감소 보고서 크기입니다.
-   구문 분석 되지 않은 구문에 대 한 향상 된 오류 메시지입니다.  
  
## <a name="april-2014"></a>2014 년 4 월  
Access 용 SSMA의 2014 년 4 월 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-   MS SQL Server 2014에 대 한 지원이 추가 되었습니다.  
-   Azure에 변환에 대 한 수정 된 버그입니다.  
-   IE 10에서 보이지 않는 보고서 페이지에 대 한 수정 된 버그입니다.  
  
## <a name="january-2012"></a>2012 년 1 월  
Access 용 SSMA의 2012 년 1 월 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-   마이그레이션 후 연결 된 테이블을 MS Access에 대 한 사용자 이름 및 암호를 유지 하지 하는 옵션을 제공 합니다.  
-   No Action을 순환 참조 연계 동작을 설정 합니다.  
-   No Action을 순환 참조 연계 동작을 나타내는 적절 한 메시지 설정 되었습니다 제공.  
  
## <a name="july-2011"></a>2011 년 7 월  
Access 용 SSMA의 2011 년 7 월 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-   데이터 마이그레이션 중에 보고 기능 향상 된 오류입니다.  
  
## <a name="april-2011"></a>2011 년 4 월  
Access 용 SSMA의 2011 년 4 월 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-   추가 "SSMA에 대 한 액세스"를 지 원하는 설치 가능한 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" 및 Azure SQL입니다.  
-   연결 하는 기능을 추가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali"로 지정 합니다.  
-   이전 버전과 호환성에 대 한 액세스 콘솔 버전에 대 한 추가 SSMA 지원 합니다. SSMA v5.0 이전 버전에서 만든 프로젝트를 열 수 있습니다.
-   SSMA 제품의 이전 버전을 사용 하 여 SSMA v5.0 제품 나란히 (SxS)를 설치 하는 기능을 추가 합니다.  
  
## <a name="july-2010"></a>2010 년 7 월  
SSMA for Access 2010 년 7 월 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-   SQL Server 2008 R2 및 Azure SQL로 마이그레이션에 대 한 지원이 추가 되었습니다.
-   SQL Server와 Azure SQL에 보안 연결을 추가 합니다.  
-   Access 2010 데이터베이스에 대 한 지원이 추가 되었습니다.
-   명령줄 실행에 대 한 새 SSMA 콘솔 응용 프로그램을 추가 합니다.
-   SQL Server DateTime2 데이터 형식에 대 한 지원이 추가 되었습니다.
  
## <a name="june-2008"></a>2008 년 6 월  
Access 용 SSMA의 2008 년 6 월 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-   Access 2007 데이터베이스에 대 한 지원이 추가 되었습니다.  
  
## <a name="may-2007"></a>2007 년 5 월  
Access 용 SSMA의 2007 년 5 월 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-   작업 그룹 정책을 사용 하는 Access 데이터베이스에 대 한 지원이 추가 되었습니다.  
-   SQL Server 메타 데이터 탐색기에서 변환 된 개체를 삭제 하는 기능을 제공 합니다.  
-   SQL 모드를 포맷 하는 SQL Server에서 사용자가 입력 한 주석에 대 한 지원이 추가 되었습니다.  
-   개체 변환에 추가 된 개선 사항입니다.  
  
## <a name="november-2006"></a>2006 년 11 월  
Access 용 SSMA의 2006 년 11 월 릴리스는 다음 변경 내용을 포함 되어 있습니다.  
  
-   에 대 한 액세스에서 단일 데이터베이스의 마이그레이션을 단계별로 안내 하는 새 Database Migration Wizard 추가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
-   새 변환, 로드를 추가 하 고 Access 데이터베이스를 변환 하는 마이그레이션 명령으로 변환된 된 개체를 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 하 고 데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 한꺼번에 합니다.  
-   향상 된 쿼리 마이그레이션입니다. 변환에는 더 쿼리 뷰를 선택 하는 이제 마이그레이션을 쿼리 합니다. 자세한 내용은 [Access 데이터베이스 개체 변환](converting-access-database-objects-accesstosql.md)합니다.  
-   테이블 및 인덱스 속성을 편집 하는 기능을 추가 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **테이블** 탭 합니다.  
-   새 전역 설정을 추가 합니다.  
    -   편집기 창에서 줄 번호를 표시 하도록 선택할 수 있습니다.  
    -   SSMA 중복 개체를 바꿀 것인지 묻는 메시지를 구성 하거나 항상 하지 않았거나 전혀 스키마 변환 하는 동안 중복 된 개체를 바꿀 수 있습니다.  
-   SSMA 복잡 한 쿼리를 와일드 카드를 포함 하는 경우 경고 메시지가 표시 되는지 여부를 지정할 수 있는 새 변환 옵션을 추가 합니다.  
  
## <a name="july-2006"></a>2006 년 7 월  
SSMA for Access는 2006 년 7 월 릴리스의 초기 릴리스가 였습니다.
