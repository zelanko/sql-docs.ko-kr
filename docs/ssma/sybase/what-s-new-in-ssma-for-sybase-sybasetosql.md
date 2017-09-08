---
title: "기능 &#39; SSMA for Sybase (SybaseToSQL)의 새로운 s | Microsoft Docs"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
caps.latest.revision: 21
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 80642503480add90fc75573338760ab86139694c
ms.openlocfilehash: 1054c9279039eda01320e1afd9745b6a53200b3f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/21/2017

---
# <a name="what39s-new-in-ssma--for-sybase-sybasetosql"></a>기능 &#39;의 새로운 SSMA for Sybase (SybaseToSQL)
이 항목에서는 각 릴리스의 Sybase 변경에 대 한 SSMA를 나열 합니다. 

## <a name="ssma-v74"></a>SSMA v7.4
SSMA for Sybase v7.4 출시 다음과 같은 변경 내용이 포함 되어 있습니다.
- **쿼리 제한 시간** 옵션은 원본 및 대상에서 스키마 개체 검색 하는 동안 이제 사용할 수 있습니다.
![쿼리 제한 시간 옵션](../media/query-timeout_red.png)
- 품질 및 변환 메트릭은 고객 의견에 따라 대상된 수정 프로그램으로 향상 되었습니다.

> [!IMPORTANT]
> .NET 4.5.2 v7.4 SSMA를 설치 하기 위한 필수 조건입니다. 또한 v7.4 부터는 32 비트 버전의 SSMA는 되 고 중단 되었습니다.  

## <a name="ssma-v73"></a>SSMA v7.3
SSMA for Sybase v7.3 출시 다음과 같은 변경 내용이 포함 되어 있습니다.
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
Sybase 용 SSMA의 v 7.2가 사전 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
- 향상 된 품질 및 변환 메트릭을 고객 의견에 따라 수정 프로그램을 대상된으로 합니다.
- 원격 분석의 향상 된 기능 고객 문제를 해결 하 고 SSMA의 변환율 향상에 더 나은 데이터 요소를 제공 합니다.

## <a name="ssma-v71"></a>SSMA v7.1
Access 용 SSMA의 v7.1 릴리스는 다음과 같은 변경을 포함 되어 있습니다.
- Windows 및 Linux c t p 1에서 SQL Server 2017 마이그레이션에 지원 되는 대상 플랫폼 되었습니다. 이 기능은 기술 미리 보기 중 이며은 스키마 및 데이터 이동 대상 SQL server 지원 합니다.
- SSMA는 이제 자동으로 업데이트 되는 사용 가능한 즉시 최신 버전의 SSMA 다운로드를 지원 합니다.
- SSMA 설치할 수 있는 이진 파일은 이제 Windows installer 패키지 파일 (.msi)을 통해 배달 됩니다.

**리소스**

[SQL Server Migration Assistant의 변환 기능을 확장합니다.](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[평가 하 고 SQL Server에 Microsoft 이외의 데이터 플랫폼에서 데이터를 마이그레이션할 *(예: Oracle) 있음*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>2016 년 5 월  
Sybase 용 SSMA의 2016 년 5 월 릴리스에서 다음과 같은 변경 내용이 포함 되어 있습니다.  

-  SQL Server 2016에 대 한 지원이 추가 되었습니다.
-  .NET 2.0에 대 한 설치 관리자 검사를 제거 합니다.
-  업데이트 된 확장 팩 종속성.Net 3.5에서에서.Net 4.0 합니다.
-  프로젝트"저장" 고정 및 SSMA 콘솔에 대 한 프로젝트 열기 명령입니다.
-  SSMA 콘솔에 대 한 고정된 "securepassword" 명령입니다.
-  고정 되는 초기 로드에 대 한 개체의 수를 계산 합니다.
-  전역 설정에서 수정 된 버그입니다.

## <a name="march-2016"></a>2016 년 3 월  
Sybase 용 SSMA의 2016 년 3 월 미리 보기 릴리스에서 다음과 같은 변경을 포함 되어 있습니다.  
  
-  SQL Server 2016으로 마이그레이션에 대 한 지원이 추가 되었습니다.  
  
## <a name="january-2016"></a>2016 년 1 월  
Sybase 용 SSMA의 2016 년 1 월 유지 보수 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-  SSMA (RFC 5706203)에 추가 된 보기 로그의 메뉴 항목입니다.  
-  추가 된 원격 분석 합니다. 
  
## <a name="july-2014"></a>2014 년 7 월  
Sybase 용 SSMA의 2014 년 7 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-  향상 된 Azure SQL DB 코드 변환 합니다.  
-  Azure SQL DB를 지원 하도록 스키마 확장 팩 기능을 이동 합니다.  
-  추가 된 성능 향상 10k 사용 하 여 데이터베이스에 대 한 개체를 테스트합니다.  
-  많은 수의 개체를 처리 하기 위한 향상 된 UI가 추가 되었습니다.  
-  (되므로 변환 과정에서 무시) "잘 알려진" LOB 스키마를 강조 표시 기능이 추가 되었습니다.  
-  변환 속도 향상을 추가 합니다.  
-  UI에 설명 된 개체 수를 표시 하는 기능을 추가 합니다. 
-  25%를 초과 하 여 축소 된 보고서 크기입니다.  
-  구문 분석 되지 않은 구문에 대 한 향상 된 오류 메시지입니다.  
  
## <a name="april-2014"></a>2014 년 4 월  
Sybase 용 SSMA의 2014 년 4 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   MS SQL Server 2014의 지원이 추가 되었습니다.  
-   Azure에 변환에 대 한 수정 된 버그입니다.  
-   IE 10에서 보이지 않는 보고서 페이지에 대 한 수정 된 버그입니다.  
  
## <a name="january-2012"></a>2012 년 1 월  
Sybase 용 SSMA의 2012 년 1 월 릴리스에서 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   롤백 트리거 변환에 대 한 지원이 추가 되었습니다.  
-   변환 하기 위한 수정 제공@ROWCOUNT 및 @@ERROR 동일한 SET 문의 합니다.  
  
## <a name="july-2011"></a>2011 년 7 월  
Sybase 용 SSMA의 2011 년 7 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   향상 된 오류 데이터 마이그레이션 중에 보고 합니다.  
  
## <a name="april-2011"></a>2011 년 4 월  
Sybase 용 SSMA의 2011 년 4 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   지 원하는 통합된 "Sybase SSMA" 제품 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 년 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"와 Azure SQL 합니다.  
-   연결 하 고로 마이그레이션에 대 한 지원을 추가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali"로 지정 합니다.  
-   변환한 다음 Sybase 데이터베이스를 Azure SQL 마이그레이션 새 기능이 추가 되었습니다.  
-   데이터의 병렬 마이그레이션을 지 원하는 향상 된 클라이언트 쪽 데이터 마이그레이션 엔진입니다.  
-   향상 된 데이터 마이그레이션 성능 단순 및 대량 로그 복구 모델.  
-   제대로 변환 하 고 대/소문자 구분 SQL Server에 대/소문자 구분 Sybase 데이터베이스를 마이그레이션할 기능이 추가 되었습니다.  
-   SQL Server ANSI 조인 문이 Sybase ASE ANSI가 아닌 조인 문 변환에 대 한 지원 추가 삭제 하 고 UPDATE 문을 확장 되었습니다.  
-   Sybase ASE ODBC 공급자 및 Sybase ASE ADO.Net 공급자를 사용 하 여 Sybase ASE 서버에 연결 하기 위한 추가 연결 옵션을 제공 합니다.  
-   라고 하는 별도 데이터베이스에 대 한 종속성을 제거 **SysDB**, Sybase 에뮬레이션 함수 (확장 팩의 일부로 설치 됨)를 포함 하 합니다.  
-   에 SSMA for Sybase 확장 팩 설치 하는 기능이 추가 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 클러스터입니다.  
-   SSMA (v4.0 및 v4.2)의 이전 버전에서 만든 프로젝트의 이전 버전과 호환성을 추가 합니다.  
-   SSMA (v4.0 및 v4.2)의 이전 버전으로 Sybase v5.0 제품-side-by-side (SxS) 용 SSMA를 설치 하는 기능을 추가 합니다.  
  
## <a name="july-2010"></a>2010 년 7 월  
Sybase 용 SSMA의 2010 년 7 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   SQL Server 2008 r 2로 마이그레이션에 대 한 지원이 추가 되었습니다.  
-   명령줄 실행에 대 한 새 SSMA 콘솔 응용 프로그램을 추가 합니다.  
-   서버 쪽 및 클라이언트 쪽 데이터 마이그레이션 엔진 둘 다 사용 하 여 데이터 마이그레이션에 대 한 지원이 추가 되었습니다.  
-   "사용자 지정 선택" 문에 데이터 마이그레이션에 대 한 지원이 추가 되었습니다.  
-   Sybase ASE 15.0.3 및 15.5에서에서 마이그레이션에 대 한 지원이 추가 되었습니다.  
  
## <a name="june-2008"></a>2008 년 6 월  
Sybase 용 SSMA의 2008 년 6 월 릴리스는 다음과 같은 변경을 포함 되어 있습니다.  
  
-   데이터베이스 개체 변환 및 SSMA 수행한 데이터 마이그레이션에 자동으로 테스트 하는 추가 된 SSMA 테스터. 모든 SSMA 마이그레이션 단계가 완료 되 면 SSMA 테스터를 사용 하 여 변환 된 개체가 같은 방식으로 작동 하는지 되 고 모든 데이터가 제대로 전송 되었습니다.  
-   추가 된 이전 SQL 변환 합니다. 사용자 이제 지정할 수 있습니다 임시 테이블 (및 다른 개체) 변환에 사용할 각 소스 프로시저에 대 한 선언이 있습니다.  
-   개체 변환에서 추가 된 향상 된 기능:  
    -   조인 수정 변환 합니다.  
    -   집계 및 없이 비 집계 필요/그룹 절.  
    -   SELECT INTO 문 사용 하 여 IDENTITY 함수입니다.  
    -   클러스터형된 제약 조건 및 인덱스 데이터에만 잠금이 설정 합니다.  
    -   SELECT INTO 의해 생성 된 임시 테이블입니다.  
    -   제약 조건 / 임시 테이블의 인덱스입니다.  
    -   새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 날짜/시간 형식이 지원 됩니다.  
    -   Sybase 15.0 연결 및 데이터 형식을 지원 합니다.  
  
## <a name="may-2007"></a>2007 년 5 월  
Sybase 용 SSMA의 2007 년 5 월 릴리스는 다음과 같은 변경 내용이 포함 되어 있습니다.  
  
-   프로젝트를 저장할 때 데이터베이스 콘텐츠를 더 빠르게 로드 기능이 추가 되었습니다.  
-   SQL Server에서 사용자가 입력 한 주석에 대 한 지원 추가 형식의 SQL 모드입니다.  
-   개체 변환에서 추가 된 향상 된 기능입니다.  
  
이 릴리스에 대 한 도움말 파일이 업데이트 되지 않았습니다. 자세한 내용은이 항목의 뒷부분에 나오는 설명서 참고 사항 섹션을 참조 합니다.  
  
## <a name="november-2006"></a>2006 년 11 월  
Sybase 용 SSMA의 2006 년 11 월 릴리스에서 다음과 같은 변경을 포함 되어 있습니다.  
  
-   새 전역 설정에 추가 되었습니다.  
    -   편집기 창에서 줄 번호를 표시 하도록 선택할 수 있습니다.  
    -   SSMA 중복 개체를 바꿀 것인지 묻는 메시지를 구성 하거나 항상 또는 never 스키마 변환 하는 동안 중복 된 개체를 바꿀 수 있습니다.  
-   SSMA 다음과 같은 경우를 처리 하는 방법을 구성할 수 있는 새로운 변환 옵션을 추가 합니다.  
    -   CAST 또는 CONVERT 문의 이진 문자열을 포함 합니다.  
    -   같음 식의 null 값을 확인 합니다.  
    -   프록시 테이블입니다.  
    -   RAISERROR에 대 한 사용자 메시지의 오류 번호입니다.  
    -   확인 되지 않은 식별자를 포함 하는 UPDATE 문입니다.  
-   SSMA를 외부에 있는 날짜를 처리 하는 방법을 지정할 수 있는 마이그레이션 새 옵션이 추가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 날짜 범위입니다.  
-   추가 **서식이 지정 된 SQL** 에 설정 된 **SQL** 가독성 향상된을 위해 코드를 포맷 하는 탭 합니다.  
-   다음을 포함 하는 버그 수정:  
    -   SSMA는 이제 잠금이 테이블 변환 *테이블* IN {SHARED | (를) 단독 모드 문을 후속에 TABLOCK 또는 TABLOCKX 힌트를 추가 하 여 테이블에 대 한 쿼리를 선택 합니다.  
    -   이진 형식의 문자 식에 사용 되는 필요한 캐스트 이제 추가 됩니다.  
    -   메모리 및 성능 향상  
  
## <a name="july-2006"></a>2006 년 7 월  
SSMA for Sybase의 2006년 7월 릴리스가 첫 버전입니다.  
  
## <a name="see-also"></a>관련 항목:  
[SSMA for Sybase &#40; 시작 SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
