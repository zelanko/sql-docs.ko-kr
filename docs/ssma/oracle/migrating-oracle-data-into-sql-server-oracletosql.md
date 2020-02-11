---
title: Oracle 데이터를 SQL Server로 마이그레이션 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Oracle Data Migration, Client-Side Migration
- Oracle Data Migration,Server-Side Migration
ms.assetid: e23c5268-41ed-4e55-9fe7-a11376202a13
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: c37f9c8e39a8a9dd87eabecba445b5ce7cef9028
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68264683"
---
# <a name="migrating-oracle-data-into-sql-server-oracletosql"></a>Oracle 데이터를 SQL Server로 마이그레이션(OracleToSQL)
로 변환 된 개체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 성공적으로 동기화 한 후에는 Oracle에서로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터를 마이그레이션할 수 있습니다.  
  
> [!IMPORTANT]  
> 사용 중인 엔진이 서버 쪽 데이터 마이그레이션 엔진이 면 데이터를 마이그레이션하기 전에 ssma를 실행 하는 컴퓨터에 oracle 용 SSMA 확장 팩 및 Oracle 공급자를 설치 해야 합니다. SQL Server 에이전트 서비스도 실행 중 이어야 합니다. 확장 팩을 설치 하는 방법에 대 한 자세한 내용은 [서버 구성 요소 설치 (OracleToSQL)](https://msdn.microsoft.com/33070e5f-4e39-4b70-ae81-b8af6e4983c5) 를 참조 하십시오.  
  
## <a name="setting-migration-options"></a>마이그레이션 옵션 설정  
로 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]마이그레이션하기 전에 **프로젝트 설정** 대화 상자에서 프로젝트 마이그레이션 옵션을 검토 하십시오.  
  
-   이 대화 상자를 사용 하 여 마이그레이션 일괄 처리 크기, 테이블 잠금, 제약 조건 확인, null 값 처리, id 값 처리 등의 옵션을 설정할 수 있습니다. 프로젝트 마이그레이션 설정에 대 한 자세한 내용은 [프로젝트 설정 (마이그레이션) (OracleToSQL)](https://msdn.microsoft.com/fcd6b988-633b-4b2b-9f36-6368b5e86b60)을 참조 하십시오.  
  
-   사용자는 **프로젝트 설정** 대화 상자의 **마이그레이션 엔진** 을 사용 하 여 다음과 같은 두 가지 유형의 데이터 마이그레이션 엔진을 사용 하 여 마이그레이션 프로세스를 수행할 수 있습니다.  
  
    1.  클라이언트 쪽 데이터 마이그레이션 엔진  
  
    2.  서버 쪽 데이터 마이그레이션 엔진  
  
**클라이언트 쪽 데이터 마이그레이션:**  
  
-   클라이언트 쪽에서 데이터 마이그레이션을 시작 하려면 **프로젝트 설정** 대화 상자에서 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션을 선택 합니다.  
  
-   **프로젝트 설정**에서 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션이 설정 되어 있습니다.  
  
    > [!NOTE]  
    > **클라이언트 쪽 데이터 마이그레이션 엔진** 은 ssma 응용 프로그램 내에 상주 하므로 확장 팩의 가용성에 따라 달라 집니다.  
  
**서버 쪽 데이터 마이그레이션:**  
  
-   서버 쪽 데이터 마이그레이션 중에 엔진은 대상 데이터베이스에 상주 합니다. 확장 팩을 통해 설치 됩니다. 확장 팩을 설치 하는 방법에 대 한 자세한 내용은 [SQL Server에 서버 구성 요소 설치](installing-ssma-components-on-sql-server-oracletosql.md) 를 참조 하세요.  
  
-   서버 쪽에서 마이그레이션을 시작 하려면 **프로젝트 설정** 대화 상자에서 **서버 쪽 데이터 마이그레이션 엔진** 옵션을 선택 합니다.  
  
## <a name="migrating-data-to-sql-server"></a>SQL Server로 데이터 마이그레이션  
데이터 마이그레이션은 Oracle 테이블의 데이터 행을 트랜잭션의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블로 이동 하는 대량 로드 작업입니다. 각 트랜잭션에 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 되는 행 수는 프로젝트 설정에서 구성 됩니다.  
  
마이그레이션 메시지를 보려면 출력 창이 표시 되는지 확인 합니다. 그렇지 않으면 **보기** 메뉴에서 **출력**을 선택 합니다.  
  
**데이터를 마이그레이션하려면**  
  
1.  다음 사항을 확인합니다.  
  
    -   Oracle 공급자는 SSMA를 실행 하는 컴퓨터에 설치 됩니다.  
  
    -   변환 된 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 동기화 했습니다.  
  
2.  Oracle 메타 데이터 탐색기에서 마이그레이션할 데이터가 포함 된 개체를 선택 합니다.  
  
    -   모든 스키마에 대 한 데이터를 마이그레이션하려면 **스키마**옆의 확인란을 선택 합니다.  
  
    -   데이터를 마이그레이션하거나 개별 테이블을 생략 하려면 먼저 스키마를 확장 하 고 **테이블**을 확장 한 다음 테이블 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
3.  데이터를 마이그레이션하기 위해 다음 두 가지 경우가 발생 합니다.  
  
    **클라이언트 쪽 데이터 마이그레이션:**  
  
    -   **클라이언트 쪽 데이터 마이그레이션을**수행 하려면 **프로젝트 설정** 대화 상자에서 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션을 선택 합니다.  
  
    **서버 쪽 데이터 마이그레이션:**  
  
    -   서버 쪽에서 데이터 마이그레이션을 수행 하기 전에 다음을 확인 하십시오.  
  
        1.  Oracle 용 SSMA 확장 팩은 인스턴스에 설치 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
        2.  SQL Server 인스턴스에서 SQL Server 에이전트 서비스가 실행 중입니다.  
  
    -   **서버 쪽 데이터 마이그레이션을**수행 하려면 **프로젝트 설정** 대화 상자에서 **서버 쪽 데이터 마이그레이션 엔진** 옵션을 선택 합니다.  
  
4.  Oracle 메타 데이터 탐색기에서 **스키마** 를 마우스 오른쪽 단추로 클릭 한 다음 **데이터 마이그레이션**을 클릭 합니다. 개별 개체 또는 개체의 범주에 대 한 데이터를 마이그레이션할 수도 있습니다. 개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 합니다. **데이터 마이그레이션** 옵션을 선택 합니다.  
  
    > [!NOTE]  
    > Oracle 용 SSMA 확장 팩이 인스턴스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]설치 되지 않은 경우 및 **서버 쪽 데이터 마이그레이션 엔진** 을 선택한 경우 데이터를 대상 데이터베이스로 마이그레이션하는 동안 다음 오류가 발생 합니다. ' ssma 데이터 마이그레이션 구성 요소를 SQL Server에서 찾을 수 없습니다. 서버 쪽 데이터 마이그레이션은 가능 하지 않습니다. 확장 팩이 올바르게 설치 되어 있는지 확인 하세요. ' **취소** 를 클릭 하 여 데이터 마이그레이션을 종료 합니다.  
  
5.  **Oracle에 연결** 대화 상자에서 연결 자격 증명을 입력 한 다음 **연결**을 클릭 합니다. Oracle에 연결 하는 방법에 대 한 자세한 내용은 [Connect To oracle &#40;OracleToSQL를](../../ssma/oracle/connect-to-oracle-oracletosql.md) 참조 하세요&#41;  
  
    대상 데이터베이스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결 하려면 **SQL Server** 연결 대화 상자에 연결 자격 증명을 입력 하 고 **연결**을 클릭 합니다. 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결 하는 방법에 대 한 자세한 내용은 [SQL Server에 연결](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536) 을 참조 하세요.  
  
    메시지가 **출력** 창에 표시 됩니다. 마이그레이션이 완료 되 면 **데이터 마이그레이션 보고서** 가 나타납니다. 데이터를 마이그레이션하지 않은 경우 오류가 포함 된 행을 클릭 한 다음 **세부 정보**를 클릭 합니다. 보고서가 완료 되 면 **닫기**를 클릭 합니다. 데이터 마이그레이션 보고서에 대 한 자세한 내용은 [SSMA Common (데이터 마이그레이션 보고서)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241) 를 참조 하세요.  
  
> [!NOTE]  
> SQL Express edition을 대상 데이터베이스로 사용 하는 경우 클라이언트 쪽 데이터 마이그레이션만 허용 되며 서버 쪽 데이터 마이그레이션은 지원 되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
[Oracle 데이터베이스를 SQL Server &#40;OracleToSQL&#41;로 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
