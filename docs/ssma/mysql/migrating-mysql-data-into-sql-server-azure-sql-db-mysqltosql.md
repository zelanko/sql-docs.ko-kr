---
title: 마이그레이션 MySQL 데이터를 SQL Server-Azure SQL DB (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Data Migration, server side data migration
- Data Migration,client side data migration
ms.assetid: a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 83a4a2d1bea5074cc268590d4074bde631f28694
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908831"
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-db-mysqltosql"></a>마이그레이션 MySQL 데이터를 SQL Server-Azure SQL DB (MySQLToSQL)
사용 하 여 변환된 된 개체를 성공적으로 동기화 한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure MySQL에서 데이터를 마이그레이션할 수 있습니다 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다.  
  
> [!IMPORTANT]  
> 엔진이 사용 중인 된 경우 서버 쪽 데이터 마이그레이션 엔진으로, 그런 다음 마이그레이션을 수행 하기 전에 데이터를 MySQL 확장 팩 및 SSMA를 실행 하는 컴퓨터에서 MySQL 공급자 용 SSMA를 설치 해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 실행 해야 합니다. 확장 팩을 설치 하는 방법에 대 한 자세한 내용은 참조 하세요. [(MySQL to SQL) SQL Server에 SSMA 구성 요소 설치](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
## <a name="setting-migration-options"></a>마이그레이션 옵션 설정  
마이그레이션하기 전에 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 프로젝트 마이그레이션 옵션을 검토 합니다 **프로젝트 설정을** 대화 상자.  
  
-   이 대화 상자를 사용 하 여 마이그레이션 일괄 처리 크기, 테이블 잠금, 제약 조건 검사, null 값 처리 및 id 값 처리 등의 옵션을 설정할 수 있습니다. 프로젝트 마이그레이션 설정에 대 한 자세한 내용은 참조 하세요. [프로젝트 설정 (마이그레이션)](https://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9)합니다.  
  
    에 대 한 자세한 **데이터 마이그레이션 설정 확장**를 참조 하세요 [데이터 마이그레이션 설정](data-migration-settings-mysqltosql.md)  
  
-   합니다 **마이그레이션 엔진** 에 **프로젝트 설정을** 대화 상자에서 두 가지 유형의 데이터 마이그레이션 엔진을 사용 하 여 마이그레이션 프로세스를 수행할 수 있습니다:  
  
    1.  클라이언트 쪽 데이터 마이그레이션 엔진  
  
    2.  서버 쪽 데이터 마이그레이션 엔진  
  
**클라이언트 쪽 데이터 마이그레이션:**  
  
-   클라이언트 쪽에서 데이터 마이그레이션을 시작 하려면 선택 합니다 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션을 **프로젝트 설정을** 대화 상자.  
  
-   **프로젝트 설정**의 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션을 설정 합니다.  
  
    > [!NOTE]  
    > 합니다 **클라이언트 쪽 데이터 마이그레이션 엔진** SSMA 응용 프로그램 내에 있고 따라서 확장 팩의 가용성에 종속 되지 않습니다.  
  
**서버 쪽 데이터 마이그레이션:**  
  
-   서버 쪽 데이터 마이그레이션 중에 엔진은 대상 데이터베이스에 상주합니다. 확장 팩을 통해 설치 됩니다. 확장 팩을 설치 하는 방법에 대 한 자세한 내용은 참조 하세요. [(MySQL to SQL) SQL Server에 SSMA 구성 요소 설치](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
-   서버 쪽에서 마이그레이션을 시작 하려면 선택 합니다 **서버 쪽 데이터 마이그레이션 엔진** 옵션을 **프로젝트 설정** 대화 상자.  
  
> [!IMPORTANT]  
> **클라이언트 쪽 데이터 마이그레이션** 옵션은 SQL Azure 사용할 수 있습니다.  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>SQL Server 또는 SQL Azure 데이터 마이그레이션  
마이그레이션에 대 한 MySQL 테이블에서 행의 데이터를 이동 하는 대량 로드 작업을 데이터가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 테이블에서 트랜잭션. 행 수가 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 각 트랜잭션에서 프로젝트 설정에서 구성 됩니다.  
  
마이그레이션 메시지를 보려면 출력 창 표시 되는지 확인 합니다. 이 고, 그렇지 합니다 **뷰** 메뉴에서 **출력**합니다.  
  
**데이터를 마이그레이션**  
  
1.  다음 사항을 확인합니다.  
  
    -   MySQL 공급자 SSMA를 실행 하는 컴퓨터에 설치 됩니다.  
  
    -   대상 데이터베이스를 사용 하 여 변환된 된 개체를 동기화 해야 (SQL Server / SQL Azure).  
  
2.  MySQL 메타 데이터 탐색기에서 마이그레이션할 데이터가 포함 된 개체를 선택 합니다.  
  
    -   모든 스키마에 대 한 데이터를 마이그레이션하려면 선택 확인란 옆 **스키마**합니다.  
  
    -   데이터 마이그레이션 또는 개별 테이블을 생략 하려면 먼저 스키마를 확장 **테이블**, 다음을 선택 하거나 표 옆의 확인란의 선택을 취소 합니다.  
  
3.  데이터를 마이그레이션하려면 두 가지 경우 발생 합니다.  
  
    **클라이언트 쪽 데이터 마이그레이션:**  
  
    -   수행 하는 데 **클라이언트 쪽 데이터 마이그레이션**를 선택 합니다 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션를 **프로젝트 설정** 대화 상자.  
  
    **서버 쪽 데이터 마이그레이션:**  
  
    -   서버 쪽 데이터 마이그레이션을 수행 하기 전에 다음을 확인 합니다.  
  
        1.  SSMA MySQL 확장 팩에 대 한 SQL Server 인스턴스에 설치 됩니다.  
  
        2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 SQL Server 인스턴스에서 실행 되 고  
  
    -   수행 하는 데 **서버 쪽 데이터 마이그레이션**를 선택 합니다 **서버 쪽 데이터 마이그레이션 엔진** 옵션를 **프로젝트 설정** 대화 상자.  
  
4.  마우스 오른쪽 단추로 클릭 **스키마** MySQL 메타 데이터 탐색기에서를 클릭 한 다음 **데이터 마이그레이션**합니다. 또한 개별 개체 또는 개체의 범주에 대 한 데이터를 마이그레이션할 수 있습니다. 개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 선택 된 **데이터 마이그레이션** 옵션입니다.  
  
    > [!NOTE]  
    > SSMA MySQL 확장 팩에 대 한 SQL Server 인스턴스에 설치 되어 있지 않으면 한 경우 **서버 쪽 데이터 마이그레이션 엔진** 을 선택한 경우 데이터베이스에서 대상 데이터베이스로 데이터를 마이그레이션하는 동안 다음 오류가 발생 합니다. ' SQL Server에 SSMA 데이터 마이그레이션 구성 요소를 찾을 수 없습니다, 가능한 서버 쪽 데이터 마이그레이션 설정 되지 것입니다. 확장 팩 올바르게 설치 되어 있는지를 확인 하세요. '. 클릭 **취소** 데이터 마이그레이션이 종료 합니다.  
  
5.  에 **MySQL에 연결** 대화 상자에서 연결 자격 증명을 입력 한 다음 클릭 **Connect**합니다. MySQL에 연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [MySQL에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
    데이터베이스에서 대상 데이터베이스로 SQL Server 인 경우 다음의 연결 자격 증명을 입력 합니다 **SQL Server에 연결** 대화 상자를 클릭 **Connect**. SQL Server에 연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [SQL Server에 연결](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    SQL Azure 데이터베이스에서 대상 데이터베이스로 사용 하는 경우 다음의 연결 자격 증명을 입력 합니다 **SQL Azure 연결** 대화 상자를 클릭 **Connect**합니다. SQL Azure 연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [Azure SQL DB에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md)  
  
    메시지에 표시 됩니다는 **출력** 창입니다. 마이그레이션이 완료 되 면 합니다 **데이터 마이그레이션 보고서** 나타납니다. 모든 데이터 마이그레이션하지 않은 경우 오류를 포함 하는 행을 클릭 한 다음 클릭 **세부 정보**합니다. 보고서를 사용 하 여 완료 되 면 **닫기**합니다. 데이터 마이그레이션 보고서에 대 한 자세한 내용은 참조 하세요. [데이터 마이그레이션 보고서 (SSMA 공통)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> SQL Express edition으로 대상 데이터베이스를 사용 하면 클라이언트 쪽 데이터 마이그레이션에만 허용 됩니다 및 서버 쪽 데이터 마이그레이션이 지원 되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server-Azure SQL DB로 마이그레이션 MySQL 데이터베이스 &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
