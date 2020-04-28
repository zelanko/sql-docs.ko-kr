---
title: Sybase ASE 데이터베이스 개체 변환 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 507ac2a61043260435a18c90fb473130988e7f35
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67948517"
---
# <a name="converting-sap-ase-database-objects-sybasetosql"></a>SAP ASE 데이터베이스 개체 변환 (SybaseToSQL)
SAP 적응 서버 엔터프라이즈 (ASE)에 연결 하 고, 또는 Azure SQL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결 하 고, 프로젝트 및 데이터 매핑 옵션을 설정한 후에는 Sap 적응 서버 엔터프라이즈 (ase) 데이터베이스 개체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 또는 azure sql database 개체로 변환할 수 있습니다.  
  
## <a name="the-conversion-process"></a>변환 프로세스  
데이터베이스 개체를 변환 하면 ASE에서 개체 정의를 사용 하 여 유사 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 SQL Azure 개체로 변환한 다음이 정보를 ssma 메타 데이터로 로드 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL 인스턴스에 정보를 로드 하지 않습니다. 그런 다음 또는 Azure SQL 메타 데이터 탐색기를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여 개체 및 해당 속성을 볼 수 있습니다.
  
변환 하는 동안 SSMA는 출력 창에 출력 메시지를 인쇄 하 고 **오류 목록** 창에 오류 메시지를 출력 합니다. 출력 및 오류 정보를 사용 하 여 ASE 데이터베이스를 수정 하거나 변환 프로세스를 수정 하 여 원하는 변환 결과를 가져와야 하는지 여부를 결정할 수 있습니다.  
  
## <a name="setting-conversion-options"></a>변환 옵션 설정  
개체를 변환 하기 전에 **프로젝트 설정** 대화 상자에서 프로젝트 변환 옵션을 검토 합니다. 이 대화 상자를 사용 하 여 SSMA에서 함수 및 전역 변수를 변환 하는 방법을 설정할 수 있습니다. 자세한 내용은 [프로젝트 설정 &#40;변환&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)을 참조 하세요.  
  
## <a name="converting-ase-database-objects"></a>ASE 데이터베이스 개체 변환  
ASE 데이터베이스 개체를 변환 하려면 먼저 변환할 개체를 선택 하 고 SSMA에서 변환을 수행 하도록 합니다. 변환 하는 동안 출력 메시지를 보려면 **보기** 메뉴에서 **출력**을 선택 합니다.  
  
**ASE 개체를 SQL Server 또는 SQL Azure 구문으로 변환 하려면**  
  
1.  Sybase 메타 데이터 탐색기에서 ASE 서버를 확장 한 다음 **데이터베이스**를 확장 합니다.  
  
2.  변환할 개체 선택:  
  
    -   모든 데이터베이스를 변환 하려면 **데이터베이스**옆의 확인란을 선택 합니다.  
  
    -   데이터베이스를 변환 하거나 생략 하려면 데이터베이스 이름 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
    -   개별 스키마를 변환 하거나 생략 하려면 데이터베이스를 확장 하 고 **스키마**를 확장 한 다음 스키마 옆에 있는 확인란을 선택 하거나 선택 취소 합니다.  
  
    -   개체의 범주를 변환 하거나 생략 하려면 스키마를 확장 한 다음 범주 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
    -   개별 개체를 변환 하거나 생략 하려면 category 폴더를 확장 한 다음 개체 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
3.  선택한 모든 개체를 변환 하려면 **데이터베이스**를 마우스 오른쪽 단추로 클릭 한 다음 **스키마 변환**을 선택 합니다.  
  
    개체 또는 포함 하는 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **스키마 변환**을 선택 하 여 개별 개체 또는 개체 범주를 변환할 수도 있습니다.  
  
> [!NOTE]  
> 일부 SAP ASE 시스템 함수는 동작의 해당 SQL Server 시스템 함수와 정확히 일치 하지 않습니다. SAP ASE 동작을 에뮬레이트하기 위해 SSMA는 변환 된 SQL Server 데이터베이스에서 2ss ' 이라는 스키마를 사용 하 여 사용자 정의 함수를 생성 합니다. 프로젝트 설정에 따라 일부 SQL Server 시스템 함수는 이러한 에뮬레이트된 함수로 바뀝니다. SSMA는 다음과 같은 사용자 정의 함수를 만듭니다.  
  
||||  
|-|-|-|  
|**char_length_nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_varchar**|**inttohex**|**substring_nvarchar**|  
|**charindex_nvarchar**|**ssma_datediff**|**substring_varbinary**|  
|**charindex_varchar**|**hextoint**|**substring_varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-azure-sql"></a>Azure SQL에서 지원 되지 않는 개체  
다음 T-sql 키워드는 SQL Server 온-프레미스로 변환 하는 동안 SAP ASE 용 SSMA에서 사용 되지만 이러한 키워드는 SQL Azure T-sql 구문에서 지원 되지 않습니다.  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|GRANT/REVOKE/DENY ALL|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>변환 문제 보기  
일부 SAP ASE 개체는 변환 되지 않을 수 있습니다. 요약 변환 보고서를 보면 변환 성공률을 확인할 수 있습니다.  
  
**요약 보고서를 보려면**  
  
1.  Sybase 메타 데이터 탐색기에서 **데이터베이스**를 선택 합니다.  
  
2.  오른쪽 창에서 **보고서** 탭을 선택 합니다.  
  
    이 보고서는 평가 또는 변환 된 모든 데이터베이스 개체에 대 한 요약 평가 보고서를 표시 합니다. 또한 개별 개체에 대 한 요약 보고서를 볼 수 있습니다.  
  
    -   개별 데이터베이스에 대 한 보고서를 보려면 Sybase 메타 데이터 탐색기에서 데이터베이스를 선택 합니다.  
  
    -   개별 데이터베이스 개체에 대 한 보고서를 보려면 Sybase 메타 데이터 탐색기에서 개체를 선택 합니다. 변환 문제가 있는 개체에는 빨간색 오류 아이콘이 있습니다.  
  
변환이 실패 한 개체의 경우 변환 실패를 일으킨 구문을 볼 수 있습니다.  
  
**개별 변환 문제를 보려면**  
  
1.  Sybase 메타 데이터 탐색기에서 **데이터베이스**를 확장 합니다.  
  
2.  빨간색 오류 아이콘이 표시 된 데이터베이스를 확장 합니다.  
  
3.  **스키마** 폴더를 확장 한 다음 빨간색 오류 아이콘이 표시 된 스키마를 확장 합니다.  
  
4.  스키마 아래에서 빨간색 오류 아이콘이 있는 폴더를 확장 합니다.  
  
5.  빨간색 오류 아이콘이 있는 개체를 선택 합니다.  
  
6.  오른쪽 창에서 **보고서** 탭을 선택 합니다.  
  
7.  **보고서** 탭의 맨 위에는 드롭다운 목록이 있습니다. 목록에 **통계가**표시 되 면 선택 항목을 **원본**으로 변경 합니다.  
  
    SSMA는 소스 코드와 코드 바로 위에 몇 개의 단추를 표시 합니다.  
  
8.  오른쪽을 가리키는 화살표가 있는 빨간색 오류 아이콘을 선택 하 여 **다음 문제**를 선택 합니다.  
  
    SAP ASE 용 SSMA는 현재 개체에서 발견 된 첫 번째 문제 소스 코드를 강조 표시 합니다.  
  
변환할 수 없는 각 항목에 대해 해당 개체를 사용 하 여 수행할 작업을 결정 해야 합니다.  
  
-   **SQL** 탭에서 프로시저 및 트리거에 대 한 소스 코드를 편집할 수 있습니다.  
  
-   SAP ASE 개체를 변경 하 여 문제가 있는 코드를 제거 하거나 수정할 수 있습니다. 업데이트 된 코드를 SSMA에 로드 하려면 메타 데이터를 업데이트 해야 합니다. 자세한 내용은 [SAP ASE에 연결 &#40;SybaseToSQL&#41;을 ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)참조 하세요.  
  
-   마이그레이션할 때 개체를 제외할 수 있습니다. 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure Sql 메타 데이터 탐색기 및 Sybase 메타 데이터 탐색기에서 또는 azure sql로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 로드 하기 전에 항목 옆에 있는 확인란의 선택을 취소 하 고 SAP ASE에서 데이터를 마이그레이션합니다.  
  
## <a name="next-steps"></a>다음 단계  
마이그레이션 프로세스의 다음 단계에서는 변환 된 [데이터베이스 개체를 SQL Server/SQL Azure (SybaseToSQL)로 로드](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06)합니다.  
  
## <a name="see-also"></a>참고 항목  
[SAP ASE 데이터베이스를 SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;로 마이그레이션](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
