---
title: "Access(AccessToSQL) 용 SSMA의 새로운 기능 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 09/22/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: a24d3fc0-6911-4bfa-828a-197abf222e02
caps.latest.revision: "37"
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3b159377cfa3ff160d9be60dba91af5561649c4a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="whats-new-in-ssma-for-access-accesstosql"></a>(AccessToSQL) Access 용 SSMA의 새로운 기능
이 항목에서는 각 릴리스에 대 한 액세스 변경에 대 한 SSMA를 나열 합니다.  

## <a name="ssma-v76"></a>SSMA v7.6
Access 용 SSMA v7.6 릴리스의 품질 및 변환 메트릭을 향상 된 대상으로 지정 된 수정 사항 및 SQL Server 2017 (공개 미리 보기)에 대 한 지원이 향상 되었습니다. Windows 및 Linux에서 SQL Server 2017에 대 한 지원을 공개 미리 보기 이므로 프로덕션 마이그레이션에 사용할 수 없습니다.

> [!IMPORTANT]
> SSMA v7.4 및 이상 버전을 사용 하 여.Net 4.5.2는 설치 필수 구성 요소 이며 도구의 32 비트 버전도 않습니다.

## <a name="ssma-v75"></a>SSMA v7.5
장애가 있는 사용자에 대 한 큰 액세스 가능성을 확인 하려면 몇 가지 향상 된 Access 용 SSMA v7.5 릴리스의 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.5 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA는 되 고 중단 되었습니다.

## <a name="ssma-v74"></a>SSMA v7.4
Access 용 SSMA의 v7.4 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
- **쿼리 제한 시간** 옵션은 원본 및 대상에서 스키마 개체 검색 하는 동안 이제 사용할 수 있습니다.
![쿼리 제한 시간 옵션](../media/query-timeout_red.png)

- 품질 및 변환 메트릭은 고객 의견에 따라 대상된 수정 프로그램으로 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.4 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA는 되 고 중단 되었습니다.

## <a name="ssma-v73"></a>SSMA v7.3
Access 용 SSMA의 v7.3 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
- 향상 된 품질 및 변환 메트릭을 고객 의견에 따라 수정 프로그램을 대상된으로 합니다.
- 다음 항목을 통해 노출 SSMA 확장성 프레임 워크:
  - SQL Server Data Tools (SSDT) 프로젝트에 내보내기 기능.
    -   SSDT 프로젝트에 SSMA에서 스키마 스크립트를 내보낼 수 있습니다. 추가 스키마를 변경 하 여 데이터베이스를 배포 하는 스키마 스크립트를 사용할 수 있습니다.
![SSDT 프로젝트 명령으로 저장](../media/export-schema-scripts_red.png)

  - SSMA 사용자 지정 변환을 수행 하는 데 사용할 수 있는 라이브러리입니다.
    - 이제 사용자 지정 구문 변환 및 SSMA 이전에 처리 되지 않은 변환 처리할 수 있는 코드를 생성할 수 있습니다.
      - 이 블로그 게시물에서 사용할 수 있는 사용자 지정 변환기를 생성 하는 방법에 대 한 지침 [확장 SQL Server Migration Assistant의 변환 기능](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)합니다.
      - 이 변환에 대 한 샘플 프로젝트를 다운로드할 수 수 [블로그 게시물](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)합니다.

## <a name="ssma-v72"></a>SSMA v 7.2가 사전
Access 용 SSMA의 v 7.2가 사전 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
- 향상 된 품질 및 변환 메트릭을 고객 의견에 따라 수정 프로그램을 대상된으로 합니다.
- 원격 분석의 향상 된 기능 고객 문제를 해결 하 고 SSMA의 변환율 향상에 더 나은 데이터 요소를 제공 합니다.

## <a name="ssma-v71"></a>SSMA v7.1
Access 용 SSMA의 v7.1 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
- Windows 및 Linux c t p 1에서 SQL Server 2017 마이그레이션에 지원 되는 대상 플랫폼 되었습니다. 이 기능은 기술 미리 보기 중 이며은 스키마 및 데이터 이동 대상 SQL server 지원 합니다.
- SSMA는 이제 자동으로 업데이트 되는 사용 가능한 즉시 최신 버전의 SSMA 다운로드를 지원 합니다.
- SSMA 설치할 수 있는 이진 파일은 이제 Windows installer 패키지 파일 (.msi)을 통해 배달 됩니다.

**리소스**

[SQL Server Migration Assistant의 변환 기능을 확장합니다.](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)
  
## <a name="may-2016"></a>2016 년 5 월  
Access 용 SSMA의 2016 년 5 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-  SQL Server 2016에 대 한 공식 지원 추가
-  .NET 2.0에 대 한 설치 관리자 검사를 제거 합니다.
-  프로젝트"저장" 고정 및 SSMA 콘솔에 대 한 프로젝트 열기 명령입니다.
-  SSMA 콘솔에 대 한 고정된 "securepassword" 명령입니다.
-  고정 되는 초기 로드에 대 한 개체의 수를 계산 합니다.
-  테이블 데이터 액세스를 위해 UI 탭에 대 한 로드를 고정 합니다.
-  전역 설정에서 수정 된 버그입니다. 
   
## <a name="march-2016"></a>2016 년 3 월  
Access 용 SSMA의 2016 년 3 월 미리 보기 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-  SQL Server 2016으로 마이그레이션에 대 한 지원이 추가 되었습니다.  
   
## <a name="january-2016"></a>2016 년 1 월  
Access 용 SSMA의 2016 년 1 월 유지 보수 릴리스는 다음과 같은 변경을 포함 되어 있습니다.  
  
-  기본값은 GUID 필드 (RFC 3894811)에 대 한 잘못 된 함수를 고정된 합니다.  
-  SQL 데이터베이스 (Azure) (RFC 4919573)에 레코드 가져오기에 대 한 고정된 중단 됩니다.  
-  SSMA (RFC 5706203)에 추가 된 보기 로그의 메뉴 항목입니다.  
-  추가 된 원격 분석 합니다.  
  
## <a name="july-2014"></a>2014 년 7 월  
Access 용 SSMA의 2014 년 7 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   향상 된 Azure SQL DB 코드 변환 합니다.  
-   Azure SQL DB를 지원 하도록 스키마 확장 팩 기능을 이동 합니다.  
-   10 개 k 개체가 포함 된 데이터베이스에 대 한 테스트 거친된 성능이 개선 되었습니다.  
-   많은 수의 개체를 처리 하기 위한 향상 된 UI가 추가 되었습니다.  
-   (되므로 변환 과정에서 무시) "잘 알려진" LOB 스키마의 강조 표시에 대 한 지원이 추가 되었습니다.  
-   변환 속도 향상을 추가 합니다.
-   UI에 표시 개체에 대 한 지원 추가 계산 합니다.
-   25%를 초과 하 여 축소 된 보고서 크기입니다.
-   구문 분석 되지 않은 구문에 대 한 향상 된 오류 메시지입니다.  
  
## <a name="april-2014"></a>2014 년 4 월  
Access 용 SSMA의 2014 년 4 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   MS SQL Server 2014에 대 한 지원이 추가 되었습니다.  
-   Azure에 변환에 대 한 수정 된 버그입니다.  
-   IE 10에서 보이지 않는 보고서 페이지에 대 한 수정 된 버그입니다.  
  
## <a name="january-2012"></a>2012 년 1 월  
Access 용 SSMA의 2012 년 1 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   마이그레이션 후 MS 액세스: 연결 된 테이블에 대 한 사용자 이름 및 암호를 저장 하지 하는 옵션을 제공 합니다.  
-   No Action에 대 한 순환 참조에 대 한 연계 동작을 설정 합니다.  
-   No Action에 대 한 순환 참조가 cascade 동작을 나타내는 적절 한 메시지 설정 되었습니다 제공.  
  
## <a name="july-2011"></a>2011 년 7 월  
Access 용 SSMA의 2011 년 7 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   향상 된 오류 데이터 마이그레이션 중에 보고 합니다.  
  
## <a name="april-2011"></a>2011 년 4 월  
Access 용 SSMA의 2011 년 4 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   추가 "SSMA에 대 한 액세스"를 지 원하는 설치 가능한 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 년 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"와 Azure SQL 합니다.  
-   연결 하는 기능을 추가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"로 지정 합니다.  
-   이전 버전과 호환성에 대 한 액세스 콘솔 버전에 대 한 추가 SSMA 지원 합니다. SSMA v5.0 이전 버전에서 만든 프로젝트를 열 수 있습니다.
-   SSMA 제품의 이전 버전으로 SSMA v5.0 제품 나란히 (SxS)를 설치 하는 기능을 추가 합니다.  
  
## <a name="july-2010"></a>2010 년 7 월  
Access 용 SSMA의 2010 년 7 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   SQL Server 2008 R2 및 SQL Azure로 마이그레이션하기 위한 지원이 추가 되었습니다.
-   SQL Server 및 Azure SQL 모두에 보안 연결을 추가 합니다.  
-   Access 2010 데이터베이스에 대 한 지원이 추가 되었습니다.
-   명령줄 실행에 대 한 새 SSMA 콘솔 응용 프로그램을 추가 합니다.
-   SQL Server DateTime2 데이터 형식에 대 한 지원이 추가 되었습니다.
  
## <a name="june-2008"></a>2008 년 6 월  
Access 용 SSMA의 2008 년 6 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   Access 2007 데이터베이스에 대 한 지원이 추가 되었습니다.  
  
## <a name="may-2007"></a>2007 년 5 월  
Access 용 SSMA의 2007 년 5 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   작업 그룹 정책을 사용 하는 Access 데이터베이스에 대 한 지원이 추가 되었습니다.  
-   SQL Server 메타 데이터 탐색기에서 변환 된 개체를 삭제 하는 기능을 제공 합니다.  
-   SQL Server에서 사용자가 입력 한 주석에 대 한 지원 추가 형식의 SQL 모드입니다.  
-   개체 변환에서 추가 된 향상 된 기능입니다.  
  
## <a name="november-2006"></a>2006 년 11 월  
Access 용 SSMA의 2006 년 11 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   에 대 한 액세스에서 단일 데이터베이스의 마이그레이션을 통해 안내해 주는 새 데이터베이스 마이그레이션 마법사 추가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
-   새 변환, 로드, 추가 및 Access 데이터베이스를 변환 하는 마이그레이션 명령으로 변환된 된 개체를 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 고 데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 한꺼번에 합니다.  
-   향상 된 쿼리 마이그레이션입니다. 변환에는 더 쿼리 뷰를 선택 하는 이제 마이그레이션을 쿼리 합니다. 자세한 내용은 참조 [Access 데이터베이스 개체가 변환](http://msdn.microsoft.com/en-us/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)합니다.  
-   테이블 및 인덱스 속성을 편집 하는 기능을 추가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **테이블** 탭 합니다.  
-   새 전역 설정에 추가 되었습니다.  
    -   편집기 창에서 줄 번호를 표시 하도록 선택할 수 있습니다.  
    -   SSMA 중복 개체를 바꿀 것인지 묻는 메시지를 구성 하거나 항상 또는 never 스키마 변환 하는 동안 중복 된 개체를 바꿀 수 있습니다.  
-   SSMA는 복잡 한 쿼리는 와일드 카드를 포함 하는 경우 경고 표시 되는지 여부를 지정할 수 있는 새 변환 옵션이 추가 되었습니다.  
  
## <a name="july-2006"></a>2006 년 7 월  
Access 용 SSMA의 2006 년 7 월 릴리스가 첫 버전입니다.
