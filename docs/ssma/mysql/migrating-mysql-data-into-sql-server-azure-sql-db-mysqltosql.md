---
title: SQL Server로 MySQL 데이터 마이그레이션-Azure SQL DB (MySQLToSQL) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67908831"
---
# <a name="migrating-mysql-data-into-sql-server---azure-sql-db-mysqltosql"></a>MySQL 데이터를 SQL Server로 마이그레이션-Azure SQL DB (MySQLToSQL)
변환 된 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 성공적으로 동기화 한 후에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 MySQL에서 또는 SQL Azure로 데이터를 마이그레이션할 수 있습니다.  
  
> [!IMPORTANT]  
> 사용 중인 엔진이 서버 쪽 데이터 마이그레이션 엔진 인 경우 데이터를 마이그레이션하기 전에 ssma를 실행 하는 컴퓨터에 mysql 확장 팩과 MySQL 공급자를 설치 해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스도 실행 중 이어야 합니다. 확장 팩을 설치 하는 방법에 대 한 자세한 내용은 [SQL Server에 SSMA 구성 요소 설치 (MySQL TO SQL)](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1) 를 참조 하세요.  
  
## <a name="setting-migration-options"></a>마이그레이션 옵션 설정  
데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 마이그레이션하기 전에 **프로젝트 설정** 대화 상자에서 프로젝트 마이그레이션 옵션을 검토 하십시오.  
  
-   이 대화 상자를 사용 하 여 마이그레이션 일괄 처리 크기, 테이블 잠금, 제약 조건 확인, null 값 처리 및 id 값 처리 등의 옵션을 설정할 수 있습니다. 프로젝트 마이그레이션 설정에 대 한 자세한 내용은 [프로젝트 설정 (마이그레이션)](https://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9)을 참조 하세요.  
  
    **확장 데이터 마이그레이션 설정**에 대 한 자세한 내용은 [데이터 마이그레이션 설정](data-migration-settings-mysqltosql.md) 을 참조 하세요.  
  
-   사용자는 **프로젝트 설정** 대화 상자의 **마이그레이션 엔진** 을 사용 하 여 다음과 같은 두 가지 유형의 데이터 마이그레이션 엔진을 사용 하 여 마이그레이션 프로세스를 수행할 수 있습니다.  
  
    1.  클라이언트 쪽 데이터 마이그레이션 엔진  
  
    2.  서버 쪽 데이터 마이그레이션 엔진  
  
**클라이언트 쪽 데이터 마이그레이션:**  
  
-   클라이언트 쪽에서 데이터 마이그레이션을 시작 하려면 **프로젝트 설정** 대화 상자에서 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션을 선택 합니다.  
  
-   **프로젝트 설정**에서 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션이 설정 되어 있습니다.  
  
    > [!NOTE]  
    > **클라이언트 쪽 데이터 마이그레이션 엔진** 은 ssma 응용 프로그램 내에 상주 하므로 확장 팩의 가용성에 따라 달라 집니다.  
  
**서버 쪽 데이터 마이그레이션:**  
  
-   서버 쪽 데이터 마이그레이션 중에 엔진은 대상 데이터베이스에 상주 합니다. 확장 팩을 통해 설치 됩니다. 확장 팩을 설치 하는 방법에 대 한 자세한 내용은 [SQL Server에 SSMA 구성 요소 설치 (MySQL TO SQL)](https://msdn.microsoft.com/6772d0c5-258f-4d7b-afb0-b5f810e71af1) 를 참조 하세요.  
  
-   서버 쪽에서 마이그레이션을 시작 하려면 **프로젝트 설정** 대화 상자에서 **서버 쪽 데이터 마이그레이션 엔진** 옵션을 선택 합니다.  
  
> [!IMPORTANT]  
> **클라이언트 쪽 데이터 마이그레이션** 옵션은 SQL Azure에만 사용할 수 있습니다.  
  
## <a name="migrating-data-to-sql-server-or-sql-azure"></a>SQL Server 또는 SQL Azure로 데이터 마이그레이션  
데이터 마이그레이션은 MySQL 테이블의 데이터 행을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 트랜잭션의 SQL Azure 테이블로 이동 하는 대량 로드 작업입니다. 각 트랜잭션에 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 되는 행 수는 프로젝트 설정에서 구성 됩니다.  
  
마이그레이션 메시지를 보려면 출력 창이 표시 되는지 확인 합니다. 그렇지 않으면 **보기** 메뉴에서 **출력**을 선택 합니다.  
  
**데이터를 마이그레이션하려면**  
  
1.  다음 사항을 확인합니다.  
  
    -   MySQL 공급자는 SSMA를 실행 하는 컴퓨터에 설치 됩니다.  
  
    -   변환 된 개체를 대상 데이터베이스 (SQL Server/SQL Azure)와 동기화 했습니다.  
  
2.  MySQL 메타 데이터 탐색기에서 마이그레이션할 데이터가 포함 된 개체를 선택 합니다.  
  
    -   모든 스키마에 대 한 데이터를 마이그레이션하려면 **스키마**옆의 확인란을 선택 합니다.  
  
    -   데이터를 마이그레이션하거나 개별 테이블을 생략 하려면 먼저 스키마를 확장 하 고 **테이블**을 확장 한 다음 테이블 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
3.  데이터를 마이그레이션하기 위해 다음 두 가지 경우가 발생 합니다.  
  
    **클라이언트 쪽 데이터 마이그레이션:**  
  
    -   **클라이언트 쪽 데이터 마이그레이션을**수행 하려면 **프로젝트 설정** 대화 상자에서 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션을 선택 합니다.  
  
    **서버 쪽 데이터 마이그레이션:**  
  
    -   서버 쪽에서 데이터 마이그레이션을 수행 하기 전에 다음을 확인 하십시오.  
  
        1.  MySQL 용 SSMA 확장 팩은 SQL Server 인스턴스에 설치 됩니다.  
  
        2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가의 인스턴스에서 실행 되 고 SQL Server  
  
    -   **서버 쪽 데이터 마이그레이션을**수행 하려면 **프로젝트 설정** 대화 상자에서 **서버 쪽 데이터 마이그레이션 엔진** 옵션을 선택 합니다.  
  
4.  MySQL 메타 데이터 탐색기에서 **스키마** 를 마우스 오른쪽 단추로 클릭 한 다음 **데이터 마이그레이션**을 클릭 합니다. 개별 개체 또는 개체의 범주에 대 한 데이터를 마이그레이션할 수도 있습니다. 개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 합니다. **데이터 마이그레이션** 옵션을 선택 합니다.  
  
    > [!NOTE]  
    > SQL Server 인스턴스에 MySQL 용 SSMA 확장 팩이 설치 되어 있지 않은 경우 및 **서버 쪽 데이터 마이그레이션 엔진** 을 선택한 경우 데이터를 대상 데이터베이스로 마이그레이션하는 동안 다음 오류가 발생 합니다. ' Ssma 데이터 마이그레이션 구성 요소를 SQL Server에서 찾을 수 없습니다. 서버 쪽 데이터 마이그레이션은 가능 하지 않습니다. 확장 팩이 올바르게 설치 되어 있는지 확인 하세요. ' **취소** 를 클릭 하 여 데이터 마이그레이션을 종료 합니다.  
  
5.  **MySQL에 연결** 대화 상자에서 연결 자격 증명을 입력 한 다음 **연결**을 클릭 합니다. MySQL에 연결 하는 방법에 대 한 자세한 내용은 [mysql에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md) 을 참조 하세요.  
  
    대상 데이터베이스가 SQL Server 경우 **SQL Server에 연결** 대화 상자에 연결 자격 증명을 입력 하 고 **연결**을 클릭 합니다. SQL Server에 연결 하는 방법에 대 한 자세한 내용은 [SQL Server에 연결](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536) 을 참조 하세요.  
  
    대상 데이터베이스를 SQL Azure 하는 경우 **SQL Azure에 연결** 대화 상자에 연결 자격 증명을 입력 하 고 **연결**을 클릭 합니다. SQL Azure에 연결 하는 방법에 대 한 자세한 내용은 [AZURE SQL DB &#40;MySQLToSQL에 연결](../../ssma/mysql/connect-to-azure-sql-db-mysqltosql.md) 을 참조 하세요&#41;  
  
    메시지가 **출력** 창에 표시 됩니다. 마이그레이션이 완료 되 면 **데이터 마이그레이션 보고서** 가 나타납니다. 데이터를 마이그레이션하지 않은 경우 오류가 포함 된 행을 클릭 한 다음 **세부 정보**를 클릭 합니다. 보고서가 완료 되 면 **닫기**를 클릭 합니다. 데이터 마이그레이션 보고서에 대 한 자세한 내용은 [SSMA Common (데이터 마이그레이션 보고서)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241) 를 참조 하세요.  
  
> [!NOTE]  
> SQL Express edition을 대상 데이터베이스로 사용 하는 경우 클라이언트 쪽 데이터 마이그레이션만 허용 되며 서버 쪽 데이터 마이그레이션은 지원 되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
[MySQL 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
