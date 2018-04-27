---
title: Sybase ASE 데이터베이스 개체 (SybaseToSQL) 변환 | Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 94dd2dd9d2c7dab4e8c29c1bc109c5fbb7c5313c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="converting-sap-ase-database-objects-sybasetosql"></a>SAP ASE 데이터베이스 개체 (SybaseToSQL) 변환
에 연결 하려면 SAP 적응형 Server Enterprise (ASE)에 연결한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SAP 적응형 Server Enterprise (ASE) 데이터베이스 개체를 Azure SQL 및 집합 프로젝트 및 데이터 매핑 옵션을 변환할 수 있습니다 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 데이터베이스 개체입니다.  
  
## <a name="the-conversion-process"></a>변환 프로세스  
ASE에서 개체 정의 가져와 데이터베이스 개체를 변환, 유사로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체, 및 SSMA 메타 데이터를이 정보를 로드 합니다. 인스턴스로 정보를 로드 하지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 합니다. 사용 하 여 개체 및 해당 속성을 볼 다음는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL 메타 데이터 탐색기입니다.
  
SSMA 변환 중에 출력 창 및 오류 메시지를 출력 메시지를 인쇄는 **오류 목록** 창. 출력 및 오류 정보를 사용 하 여 ASE 데이터베이스 또는 원하는 변환 결과를 얻으려면 변환 프로세스를 수정할 수 있는지 확인 합니다.  
  
## <a name="setting-conversion-options"></a>변환 옵션 설정  
개체를 변환 하기 전에 프로젝트 변환 옵션을 검토는 **프로젝트 설정** 대화 상자. 이 대화 상자를 사용 하 여 SSMA 함수 및 전역 변수를 변환 하는 방법을 설정할 수 있습니다. 자세한 내용은 참조 [프로젝트 설정 &#40;변환&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)합니다.  
  
## <a name="converting-ase-database-objects"></a>ASE 데이터베이스 개체를 변환합니다.  
ASE 데이터베이스 개체를 변환 하려면 먼저, 변환할 개체를 선택 한 다음 SSMA는 변환을 수행 합니다. 변환 중에 출력 메시지를 볼 수는 **보기** 메뉴 선택 **출력**합니다.  
  
**ASE 개체 SQL Server 또는 SQL Azure 구문으로 변환 하려면**  
  
1.  메타 데이터 탐색기 Sybase ASE 서버를 확장 한 다음 확장 **데이터베이스**합니다.  
  
2.  변환할 개체를 선택 합니다.  
  
    -   모든 데이터베이스를 변환 하려면 확인란을 옆에 선택 **데이터베이스**합니다.  
  
    -   변환 하거나 생략 데이터베이스를 선택 하거나 데이터베이스 이름 옆에 있는 확인란의 선택을 취소 합니다.  
  
    -   를 변환 하거나 개별 스키마를 생략 하려면 데이터베이스를 확장 하 고 **스키마**, 다음을 선택 하거나 스키마 옆에 있는 확인란의 선택을 취소 합니다.  
  
    -   를 변환 하거나 개체의 범주를 생략 하려면 스키마를 확장 한 다음 선택 하거나 범주 옆의 확인란의 선택을 취소 합니다.  
  
    -   를 변환 하거나 개별 개체를 생략 하려면 범주 폴더를 확장 한 다음 선택 하거나 개체 옆에 있는 확인란의 선택을 취소 합니다.  
  
3.  선택한 모든 개체를 변환 하려면 마우스 오른쪽 단추로 클릭 **데이터베이스**를 선택한 후 **변환 스키마**합니다.  
  
    개체 또는 해당 포함 된 폴더를 마우스 오른쪽 단추로 클릭 한 다음 선택 하 여 개별 개체 또는 개체 범주의 변환할 수도 **변환 스키마**합니다.  
  
> [!NOTE]  
> SAP ASE 시스템 함수 중 일부 일치 하지 않습니다 동작에 해당 하는 SQL Server 시스템 함수입니다. SAP ASE 동작을 에뮬레이션 하려면 SSMA 's2ss' 라는 스키마에서 변환 된 SQL Server 데이터베이스에 사용자 정의 함수를 생성 합니다. 프로젝트 설정에 따라이 SQL Server 시스템 함수 중 몇 가지은 에뮬레이트된 이러한 기능으로 대체 됩니다. SSMA는 다음 사용자 정의 함수를 만듭니다.  
  
||||  
|-|-|-|  
|**char_length_nvarchar**|**index_colorder**|**ssma_datepart**|  
|**char_length_varchar**|**inttohex**|**substring_nvarchar**|  
|**charindex_nvarchar**|**ssma_datediff**|**substring_varbinary**|  
|**charindex_varchar**|**hextoint**|**substring_varchar**|  
|**ulowsurr**|**to_unichar**|**ssma_current_time**|  
|**uhighsurr**|||  
  
## <a name="objects-not-supported-in-azure-sql"></a>Azure SQL에서 지원 되지 않는 개체  
다음 T-SQL 키워드는 사용 SSMA 하 여 SAP ASE SQL Server 온-프레미스를 변환 하는 동안 되지만 SQL Azure T-SQL 구문을 사용 하 여 이러한 키워드를 사용할 수 없습니다.  
  
||||  
|-|-|-|  
|CHECKPOINT|CREATE/ALTER/DROP DEFAULT|CREATE/DROP RULE|  
|DBCC TRACEOFF|DBCC TRACEON|GRANT/REVOKE/DENY ALL|  
|KILL|READTEXT|SELECT INTO|  
|SET OFFSETS|SETUSER|SHUTDOWN|  
|WRITETEXT|||  
  
## <a name="viewing-conversion-problems"></a>변환 문제 보기  
일부 SAP ASE 개체 변환 하지 않을 수 있습니다. 변환 요약 보고서를 확인 하 여 변환 성공률을 확인할 수 있습니다.  
  
**요약 보고서를 보려면**  
  
1.  Sybase 메타 데이터 탐색기에서 선택 **데이터베이스**합니다.  
  
2.  오른쪽 창에서 선택 된 **보고서** 탭 합니다.  
  
    이 보고서는 평가 되거나 변환 된 모든 데이터베이스 개체에 대 한 요약 평가 보고서를 표시 합니다. 개별 개체에 대 한 요약 보고서를 볼 수 있습니다.  
  
    -   개별 데이터베이스에 대 한 보고서를 보려면 Sybase 메타 데이터 탐색기에서 데이터베이스를 선택 합니다.  
  
    -   개별 데이터베이스 개체에 대 한 보고서를 보려면 Sybase 메타 데이터 탐색기에서 개체를 선택 합니다. 빨간색 오류 아이콘이 변환 문제가 발생 하는 개체.  
  
개체의 변환에 실패 한 경우 변환 실패 시 발생 하는 구문을 볼 수 있습니다.  
  
**개별 변환 문제를 보려면**  
  
1.  Sybase 메타 데이터 탐색기에서 확장 **데이터베이스**합니다.  
  
2.  빨간색 오류 아이콘을 보여 주는 데이터베이스를 확장 합니다.  
  
3.  확장 된 **스키마** 폴더를 다음 빨간색 오류 아이콘을 보여 주는 스키마를 확장 합니다.  
  
4.  스키마에서 빨간색 오류 아이콘을가지고 있는 폴더를 확장 합니다.  
  
5.  빨간색 오류 아이콘을 가진 개체를 선택 합니다.  
  
6.  오른쪽 창에서 선택 된 **보고서** 탭 합니다.  
  
7.  맨 위에 있는 **보고서** 탭은 드롭 다운 목록입니다. 목록에 표시 하는 경우 **통계**, 선택 영역을 변경 **소스**합니다.  
  
    SSMA는 소스 코드 및 코드 바로 위의 여러 개의 단추가 표시 됩니다.  
  
8.  선택 **다음 문제점**, 오른쪽을 가리키는 화살표가 있는 빨간색 오류 아이콘입니다.  
  
    SAP ASE 용 SSMA는 현재 개체에서 찾은 첫 번째 문제가 있는 소스 코드를 강조 표시 합니다.  
  
변환 될 수 있는 각 항목에 대 한 해당 개체를 사용 하 여 수행할를 결정 해야 합니다.  
  
-   프로시저와 트리거의 원본 코드를 편집할 수는 **SQL** 탭 합니다.  
  
-   제거 하거나 문제가 있는 코드를 수정 하려면 SAP ASE 개체를 변경할 수 있습니다. SSMA에 업데이트 된 코드를 로드 하려면 메타 데이터를 업데이트 해야 합니다. 자세한 내용은 참조 [SAP ASE 연결할 &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)합니다.  
  
-   마이그레이션에서 개체를 제외할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Azure SQL 메타 데이터 탐색기와 Sybase 메타 데이터 탐색기가 개체를 로드 하기 전에 항목 옆에 있는 확인란의 선택을 취소 하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Azure SQL 및 SAP ASE에서 데이터를 마이그레이션 또는 합니다.  
  
## <a name="next-steps"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [를 SQL Server로 변환 된 데이터베이스 개체를 로드 / SQL Azure (SybaseToSQL)](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06)합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server-Azure SQL 데이터베이스에 SAP ASE 데이터베이스 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
