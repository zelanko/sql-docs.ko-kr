---
title: Sybase ASE 데이터를 SQL Server-SQL Azure DB로 마이그레이션 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Migrating data,Client Side Data Migration
- Migrating data,Server Side Data Migration
ms.assetid: 54a39f5e-9250-4387-a3ae-eae47c799811
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0d942e0cbf5aed745d58541ef348647a7d727665
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34779089"
---
# <a name="migrating-sybase-ase-data-into-sql-server---azure-sql-db--sybasetosql"></a>Sybase ASE 데이터를 Azure SQL DB (SybaseToSQL)-SQL Server로 마이그레이션
Sybase 적응형 Server Enterprise (ASE) 데이터베이스 개체를 성공적으로 로드 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Azure SQL DB를 ASE에서 데이터를 마이그레이션할 수 있습니다 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB입니다.  
  
> [!IMPORTANT]  
> 서버 쪽 데이터 마이그레이션 엔진으로 사용 하 고 엔진을 사용 하는 경우 데이터를 마이그레이션하기 전에 설치 해야 합니다 SSMA는 Sybase ASE 확장 팩 및 SSMA를 실행 하는 컴퓨터의 Sybase ASE 공급자에 대 한 합니다. 도 SQL Server 에이전트 서비스를 실행 해야 합니다. 확장 팩을 설치 하는 방법에 대 한 자세한 내용은 참조 [SQL server (SybaseToSQL) SSMA 구성 요소 설치](http://msdn.microsoft.com/en-us/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
## <a name="setting-migration-options"></a>마이그레이션 옵션 설정  
마이그레이션을 수행 하기 전에 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB에 프로젝트 마이그레이션 옵션을 검토 하는 **프로젝트 설정** 대화 상자.  
  
-   이 대화 상자를 사용 하 여 마이그레이션 일괄 처리 크기, 테이블 잠금, 제약 조건 검사, null 값 처리 및 id 값 처리 등의 옵션을 설정할 수 있습니다. 프로젝트 마이그레이션 설정에 대 한 자세한 내용은 참조 [프로젝트 설정 (마이그레이션) (Sybase)](http://msdn.microsoft.com/en-us/82f8857f-7ab1-4738-ab6e-b1e95ea94924)합니다.  
  
    대 한 자세한 내용은 **확장 데이터 마이그레이션 설정**, 참조 [데이터 마이그레이션 설정](http://msdn.microsoft.com/en-us/94d7a083-2dbc-4e3d-94dd-92b7ff9d0c2d)  
  
-   **마이그레이션 엔진** 에 **프로젝트 설정** 대화 상자의 viz 두 가지 유형의 데이터 마이그레이션 엔진을 사용 하 여 마이그레이션 프로세스를 수행할 수 있습니다.:  
  
    1.  클라이언트 쪽 데이터 마이그레이션 엔진  
  
    2.  서버 쪽 데이터 마이그레이션 엔진  
  
**클라이언트 쪽 데이터 마이그레이션:**  
  
-   클라이언트 쪽에서 데이터 마이그레이션을 시작 하려면 옵션을 선택 **클라이언트 쪽 데이터 마이그레이션 엔진** 에 **프로젝트 설정** 대화 상자.  
  
-   **프로젝트 설정**, **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션은 기본적으로 설정 됩니다.  
  
    > [!NOTE]  
    > 클라이언트 쪽 데이터 마이그레이션 엔진 SSMA 응용 프로그램 내에 상주 하 고 따라서 확장 팩의 가용성에 종속 되지 않습니다.  
  
**서버 쪽 데이터 마이그레이션:**  
  
-   서버 쪽 데이터 마이그레이션 중에 엔진은 대상 데이터베이스에 상주합니다. 확장 팩을 통해 설치 됩니다. 확장 팩을 설치 하는 방법에 대 한 자세한 내용은 참조 하세요. [SQL server (SybaseToSQL) SSMA 구성 요소 설치](http://msdn.microsoft.com/en-us/5ad9e12c-2cdb-4dd2-8703-05a23242d19d)  
  
-   서버 쪽에서 마이그레이션을 시작 하려면 선택은 **서버 쪽 데이터 마이그레이션 엔진** 옵션에 **프로젝트 설정** 대화입니다.  
  
> [!NOTE]  
> 대상 데이터베이스와 Azure SQL DB 사용 되는 경우 **클라이언트 쪽 데이터 마이그레이션** 허용 되는 서버 쪽 데이터 마이그레이션 지원 되지 않습니다.  
  
## <a name="migrating-data-to-sql-server-or-azure-sql-db"></a>SQL Server 또는 Azure SQL DB로 데이터 마이그레이션  
마이그레이션 데이터는 트랜잭션에 대 한 SQL Server 테이블로 ASE 테이블에서 행의 데이터를 이동 하는 대량 로드 작업입니다. 각 트랜잭션에서 SQL Server 또는 Azure SQL DB에 로드 하는 행 수가 프로젝트 설정에서 구성 됩니다.  
  
마이그레이션 메시지를 보려면 출력 창이 표시 되는지 확인 합니다. 그렇지 않은 경우 선택 **출력** 에서 **보기** 메뉴.  
  
**데이터를 마이그레이션**  
  
1.  다음을 확인합니다.  
  
    -   ASE 공급자 SSMA를 실행 하는 컴퓨터에 설치 됩니다.  
  
    -   변환된 된 개체 (SQL Server 또는 Azure SQL DB) 대상 데이터베이스와 동기화 해야 합니다.  
  
2.  Sybase 메타 데이터 탐색기에서 마이그레이션할 데이터가 포함 된 개체를 선택 합니다.  
  
    -   모든 스키마에 대 한 데이터를 마이그레이션하려면 확인란을 옆에 선택 **스키마**합니다.  
  
    -   데이터를 마이그레이션하거나 생략 개별 테이블을 먼저 스키마를 확장 하 고 **테이블**, 다음을 선택 하거나 테이블 옆 확인란의 선택을 취소 합니다.  
  
3.  데이터를 마이그레이션하려면 두 가지 경우 발생 합니다.  
  
    **클라이언트 쪽 데이터 마이그레이션:**  
  
    수행 하기 위한 **클라이언트 쪽 데이터 마이그레이션**을 선택는 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션에 **프로젝트 설정** 대화 상자.  
  
    **서버 쪽 데이터 마이그레이션:**  
  
    -   서버 쪽 데이터 마이그레이션을 수행 하기 전에 다음을 확인 합니다.  
  
        1.  SSMA for Sybase 확장 팩은 SQL Server의 인스턴스에 설치 됩니다.  
  
        2.  SQL Server 에이전트 서비스가 SQL Server의 인스턴스에서 실행 되  
  
    -   수행 하기 위한 **서버 쪽 데이터 마이그레이션**을 선택는 **서버 쪽 데이터 마이그레이션 엔진** 옵션에 **프로젝트 설정** 대화 상자.  
  
4.  마우스 오른쪽 단추로 클릭 **스키마** Sybase 메타 데이터 탐색기에서를 클릭 한 다음 **데이터 마이그레이션**합니다. 개별 개체 또는 개체의 범주에 대 한 데이터를 마이그레이션할 수도 있습니다: 개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 된 **데이터 마이그레이션** 옵션입니다.  
  
    > [!NOTE]  
    > SSMA for Sybase 확장 팩 SQL Server의 인스턴스에 설치 되어 있지 않으면 및 경우 **서버 쪽 데이터 마이그레이션 엔진** 을 선택 하면 데이터베이스에서 대상 데이터베이스로 데이터를 마이그레이션하는 동안 다음 오류가 발생 한 후: ' SSMA 데이터 마이그레이션 구성 요소를 찾을 수 없습니다 SQL Server, 서버 쪽 데이터 마이그레이션 지원 되지 것입니다. 확장 팩 올바르게 설치 되어 있는지를 확인 하십시오. '. 클릭 **취소** 데이터 마이그레이션을 종료 하 합니다.  
  
5.  에 **Sybase ASE에 연결** 대화 상자에서 연결 자격 증명을 입력 한 다음 클릭 **연결**합니다. Sybase ASE에 연결 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Sybase 연결할 &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)  
  
    대상 데이터베이스가 SQL Server 인 경우에 연결 자격 증명을 입력 한 다음,는 **SQL Server에 연결** 대화 상자와 클릭 **연결**합니다. SQL Server에 연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [SQL Server(SybaseToSQL)에 연결](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606)  
  
    대상 데이터베이스가 Azure SQL DB 인 경우에 연결 자격 증명을 입력 한 다음는 **Azure SQL DB에 연결** 대화 상자와 클릭 **연결**합니다. Azure SQL DB에 연결 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure SQL DB에 연결 &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
    메시지에 표시 됩니다는 **출력** 창. 마이그레이션이 완료 되는 **데이터 마이그레이션 보고서** 나타납니다. 모든 데이터 마이그레이션하지 않은 경우 오류를 포함 하는 행을 클릭 한 다음 클릭 **세부 정보**합니다. 보고서와 함께 완료 했으면 클릭 **닫기**합니다. 데이터 마이그레이션 보고서에 대 한 자세한 내용은 참조 하십시오. [(SSMA 공통) 데이터 마이그레이션 보고서](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> SQL Express edition으로 대상 데이터베이스를 사용 하면 클라이언트 쪽 데이터 마이그레이션에만 사용할 수 및 서버 쪽 데이터 마이그레이션이 지원 되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server-Azure SQL DB Sybase ASE 데이터베이스 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
