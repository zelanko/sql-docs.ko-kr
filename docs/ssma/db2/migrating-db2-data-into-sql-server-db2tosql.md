---
title: DB2 데이터를 SQL Server로 마이그레이션 (DB2ToSQL) | Microsoft Docs
description: 변환 된 개체를 동기화 한 후 DB2 데이터베이스에서 SQL Server 또는 Azure SQL Database로 데이터를 마이그레이션하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 86cbd39f-6dac-409a-9ce1-7dd54403f84b
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 2f3ca5b9f222e52b7913d5688b6e8c6adfbd526d
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869731"
---
# <a name="migrating-db2-data-into-sql-server-db2tosql"></a>DB2 데이터를 SQL Server로 마이그레이션 (DB2ToSQL)
변환 된 개체를에 성공적으로 동기화 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB2에서로 데이터를 마이그레이션할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
> 사용 중인 엔진이 서버 쪽 데이터 마이그레이션 엔진 인 경우 데이터를 마이그레이션하려면 먼저 ssma를 실행 하는 컴퓨터에 DB2 용 SSMA 확장 팩과 DB2 공급자를 설치 해야 합니다. SQL Server 에이전트 서비스도 실행 중 이어야 합니다. 확장 팩을 설치 하는 방법에 대 한 자세한 내용은 [SQL Server에 SSMA 구성 요소 설치](./installing-ssma-components-on-sql-server-db2tosql.md) 를 참조 하세요.  
  
## <a name="setting-migration-options"></a>마이그레이션 옵션 설정  
로 데이터를 마이그레이션하기 전에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **프로젝트 설정** 대화 상자에서 프로젝트 마이그레이션 옵션을 검토 하십시오.  
  
-   이 대화 상자를 사용 하 여 마이그레이션 일괄 처리 크기, 테이블 잠금, 제약 조건 확인, null 값 처리, id 값 처리 등의 옵션을 설정할 수 있습니다. 프로젝트 마이그레이션 설정에 대 한 자세한 내용은 [프로젝트 설정 (마이그레이션)](./project-settings-migration-db2tosql.md)을 참조 하세요.  
  
-   사용자는 **프로젝트 설정** 대화 상자의 **마이그레이션 엔진** 을 사용 하 여 다음과 같은 두 가지 유형의 데이터 마이그레이션 엔진을 사용 하 여 마이그레이션 프로세스를 수행할 수 있습니다.  
  
    1.  클라이언트 쪽 데이터 마이그레이션 엔진  
  
    2.  서버 쪽 데이터 마이그레이션 엔진  
  
**클라이언트 쪽 데이터 마이그레이션:**  
  
-   클라이언트 쪽에서 데이터 마이그레이션을 시작 하려면 **프로젝트 설정** 대화 상자에서 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션을 선택 합니다.  
  
-   **프로젝트 설정** 에서 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션이 설정 되어 있습니다.  
  
    > [!NOTE]  
    > **클라이언트 쪽 데이터 마이그레이션 엔진** 은 ssma 응용 프로그램 내에 상주 하므로 확장 팩의 가용성에 따라 달라 집니다.  
  
**서버 쪽 데이터 마이그레이션:**  
  
-   서버 쪽 데이터 마이그레이션 중에 엔진은 대상 데이터베이스에 상주 합니다. 확장 팩을 통해 설치 됩니다. 확장 팩을 설치 하는 방법에 대 한 자세한 내용은 [SQL Server에 SSMA 구성 요소 설치](./installing-ssma-components-on-sql-server-db2tosql.md) 를 참조 하세요.  
  
-   서버 쪽에서 마이그레이션을 시작 하려면 **프로젝트 설정** 대화 상자에서 **서버 쪽 데이터 마이그레이션 엔진** 옵션을 선택 합니다.  
  
## <a name="migrating-data-to-sql-server"></a>SQL Server로 데이터 마이그레이션  
데이터 마이그레이션은 DB2 테이블의 데이터 행을 트랜잭션의 테이블로 이동 하는 대량 로드 작업입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 각 트랜잭션에 로드 되는 행 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로젝트 설정에서 구성 됩니다.  
  
마이그레이션 메시지를 보려면 출력 창이 표시 되는지 확인 합니다. 그렇지 않으면 **보기** 메뉴에서 **출력** 을 선택 합니다.  
  
**데이터를 마이그레이션하려면**  
  
1.  다음을 확인합니다.  
  
    -   DB2 공급자는 SSMA를 실행 하는 컴퓨터에 설치 됩니다.  
  
    -   변환 된 개체를 데이터베이스와 동기화 했습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  DB2 메타 데이터 탐색기에서 마이그레이션할 데이터가 포함 된 개체를 선택 합니다.  
  
    -   모든 스키마에 대 한 데이터를 마이그레이션하려면 **스키마** 옆의 확인란을 선택 합니다.  
  
    -   데이터를 마이그레이션하거나 개별 테이블을 생략 하려면 먼저 스키마를 확장 하 고 **테이블** 을 확장 한 다음 테이블 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
3.  데이터를 마이그레이션하기 위해 다음 두 가지 경우가 발생 합니다.  
  
    **클라이언트 쪽 데이터 마이그레이션:**  
  
    -   **클라이언트 쪽 데이터 마이그레이션을** 수행 하려면 **프로젝트 설정** 대화 상자에서 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션을 선택 합니다.  
  
    **서버 쪽 데이터 마이그레이션:**  
  
    -   서버 쪽에서 데이터 마이그레이션을 수행 하기 전에 다음을 확인 하십시오.  
  
        1.  D b 2 용 SSMA 확장 팩은 인스턴스에 설치 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
        2.  SQL Server 인스턴스에서 SQL Server 에이전트 서비스가 실행 중입니다.  
  
    -   **서버 쪽 데이터 마이그레이션을** 수행 하려면 **프로젝트 설정** 대화 상자에서 **서버 쪽 데이터 마이그레이션 엔진** 옵션을 선택 합니다.  
  
4.  DB2 메타 데이터 탐색기에서 **스키마** 를 마우스 오른쪽 단추로 클릭 한 다음 **데이터 마이그레이션** 을 클릭 합니다. 개별 개체 또는 개체의 범주에 대 한 데이터를 마이그레이션할 수도 있습니다. 개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 합니다. **데이터 마이그레이션** 옵션을 선택 합니다.  
  
    > [!NOTE]  
    > D b 2 용 SSMA 확장 팩이 인스턴스에 설치 되지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 **서버 쪽 데이터 마이그레이션 엔진** 을 선택한 경우 데이터를 대상 데이터베이스로 마이그레이션하는 동안 다음 오류가 발생 합니다. ' ssma 데이터 마이그레이션 구성 요소를 SQL Server에서 찾을 수 없습니다. 서버 쪽 데이터 마이그레이션은 가능 하지 않습니다. 확장 팩이 올바르게 설치 되어 있는지 확인 하세요. ' **취소** 를 클릭 하 여 데이터 마이그레이션을 종료 합니다.  
  
5.  **DB2에 연결** 대화 상자에서 연결 자격 증명을 입력 한 다음 **연결** 을 클릭 합니다. D b 2에 연결 하는 방법에 대 한 자세한 내용은 [Db2 데이터베이스에 연결 &#40;DB2ToSQL를](../../ssma/db2/connecting-to-db2-database-db2tosql.md) 참조 하세요&#41;  
  
    대상 데이터베이스에 연결 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Server** 연결 대화 상자에 연결 자격 증명을 입력 하 고 **연결** 을 클릭 합니다. 에 연결 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server에 연결](./connecting-to-sql-server-db2tosql.md) 을 참조 하세요.  
  
    메시지가 **출력** 창에 표시 됩니다. 마이그레이션이 완료 되 면 **데이터 마이그레이션 보고서** 가 나타납니다. 데이터를 마이그레이션하지 않은 경우 오류가 포함 된 행을 클릭 한 다음 **세부 정보** 를 클릭 합니다. 보고서가 완료 되 면 **닫기** 를 클릭 합니다. 데이터 마이그레이션 보고서에 대 한 자세한 내용은 [SSMA Common (데이터 마이그레이션 보고서)](../sybase/data-migration-report-sybasetosql.md) 를 참조 하세요.  
  
> [!NOTE]  
> SQL Express edition을 대상 데이터베이스로 사용 하는 경우 클라이언트 쪽 데이터 마이그레이션만 허용 되며 서버 쪽 데이터 마이그레이션은 지원 되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
[DB2 데이터를 SQL Server &#40;DB2ToSQL&#41;로 마이그레이션 ](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
