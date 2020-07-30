---
title: Oracle 스키마 변환 (OracleToSQL) | Microsoft Docs
description: 옵션을 설정 하 고 Oracle 및 SQL Server에 연결한 후 oracle 데이터베이스 개체를 Oracle 용 SSMA와 SQL Server 데이터베이스 개체로 변환 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 844d602168c063c90034469466ade816431481d4
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87395168"
---
# <a name="converting-oracle-schemas-oracletosql"></a>Oracle 스키마 변환(OracleToSQL)
Oracle에 연결 하 고,에 연결 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고, 프로젝트 및 데이터 매핑 옵션을 설정한 후에는 oracle 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체로 변환할 수 있습니다.  
  
## <a name="the-conversion-process"></a>변환 프로세스  
데이터베이스 개체를 변환 하면 Oracle의 개체 정의를 사용 하 여 유사한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체로 변환한 다음이 정보를 SSMA 메타 데이터로 로드 합니다. 인스턴스에 정보를 로드 하지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 그런 다음 메타 데이터 탐색기를 사용 하 여 개체 및 해당 속성을 볼 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
변환 하는 동안 SSMA는 출력 창에 출력 메시지를 인쇄 하 고 오류 목록 창에 오류 메시지를 출력 합니다. 출력 및 오류 정보를 사용 하 여 원하는 변환 결과를 얻기 위해 Oracle 데이터베이스 또는 변환 프로세스를 수정 해야 하는지 여부를 결정할 수 있습니다.  
  
## <a name="setting-conversion-options"></a>변환 옵션 설정  
개체를 변환 하기 전에 **프로젝트 설정** 대화 상자에서 프로젝트 변환 옵션을 검토 합니다. 이 대화 상자를 사용 하 여 SSMA에서 함수 및 전역 변수를 변환 하는 방법을 설정할 수 있습니다. 자세한 내용은 [프로젝트 설정 &#40;변환&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)을 참조 하세요.  
  
## <a name="conversion-results"></a>변환 결과  
다음 표에서는 변환 된 Oracle 개체 및 결과 개체를 보여 줍니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Oracle 개체|결과 SQL Server 개체|  
|-|-|  
|Functions|함수를로 직접 변환할 수 있는 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] ssma는 함수를 만듭니다.<br /><br />경우에 따라 함수를 저장 프로시저로 변환 해야 합니다. 이 경우 SSMA는 저장 프로시저와 저장 프로시저를 호출 하는 함수를 만듭니다.|  
|절차|프로시저를로 직접 변환할 수 있으면 [!INCLUDE[tsql](../../includes/tsql-md.md)] ssma에서 저장 프로시저를 만듭니다.<br /><br />경우에 따라 저장 프로시저를 자치 트랜잭션에서 호출 해야 합니다. 이 경우 SSMA는 두 개의 저장 프로시저를 만듭니다. 하나는 프로시저를 구현 하 고 다른 하나는 구현 하는 저장 프로시저를 호출 하는 데 사용 됩니다.|  
|패키지|SSMA는 비슷한 개체 이름으로 통합 되는 저장 프로시저 및 함수 집합을 만듭니다.|  
|시퀀스|SSMA는 시퀀스 개체 (SQL Server 2012 또는 SQL Server 2014)를 만들거나 Oracle 시퀀스를 에뮬레이트합니다.|  
|인덱스 및 트리거와 같은 종속 개체가 있는 테이블|SSMA는 종속 개체가 있는 테이블을 만듭니다.|  
|트리거와 같은 종속 개체를 사용 하 여 보기|SSMA는 종속 개체를 포함 하는 뷰를 만듭니다.|  
|구체화된 뷰|**SSMA는 일부 예외를 제외 하 고 SQL server에 인덱싱된 뷰를 만듭니다. 구체화 된 뷰에 다음 구문 중 하나 이상이 포함 되어 있으면 변환이 실패 합니다.**<br /><br />사용자 정의 함수<br /><br />SELECT, WHERE 또는 GROUP BY 절의 비 결정적인 필드/함수/식<br /><br />SELECT *, WHERE 또는 GROUP BY 절의 Float 열 사용 (이전 문제의 특수 한 경우)<br /><br />사용자 지정 데이터 형식 (포함 테이블)<br /><br />COUNT (고유 &lt; 필드 &gt; )<br /><br />FETCH<br /><br />OUTER 조인(LEFT, RIGHT 또는 FULL)<br /><br />하위 쿼리, 기타 뷰<br /><br />초과, 순위, 잠재 고객, 로그<br /><br />MIN, MAX<br /><br />UNION, 빼기, INTERSECT<br /><br />HAVING|  
|트리거|**SSMA는 다음 규칙에 따라 트리거를 만듭니다.**<br /><br />Instead of 트리거는 INSTEAD OF 트리거로 변환 됩니다.<br /><br />AFTER 트리거는 AFTER 트리거로 변환 됩니다.<br /><br />Instead of 트리거는 instead of 트리거로 변환 됩니다. 동일한 작업에 정의 된 INSTEAD OF 트리거는 여러 개의 트리거로 결합 됩니다.<br /><br />행 수준 트리거는 커서를 사용 하 여 에뮬레이션 됩니다.<br /><br />연계 트리거는 여러 개별 트리거로 변환 됩니다.|  
|동의어|**다음 개체 유형에 대해 동의어가 생성 됩니다.**<br /><br />테이블 및 개체 테이블<br /><br />뷰 및 개체 뷰<br /><br />저장 프로시저<br /><br />Functions<br /><br />**다음 개체의 동의어가 확인 되 고 직접 개체 참조로 대체 됩니다.**<br /><br />시퀀스<br /><br />패키지<br /><br />Java 클래스 스키마 개체<br /><br />사용자 정의 개체 유형<br /><br />다른 동의어에 대 한 동의어는 마이그레이션할 수 없으며 오류로 표시 됩니다.<br /><br />구체화 된 뷰에 대해서는 동의어가 생성 되지 않습니다.|  
|사용자 정의 형식|**SSMA는 사용자 정의 형식 변환에 대 한 지원을 제공 하지 않습니다. PL/SQL 프로그램에서 사용 하는 사용자 정의 형식은 다음 규칙에 따라 특수 변환 오류로 표시 됩니다.**<br /><br />사용자 정의 형식의 테이블 열은 VARCHAR (8000)로 변환 됩니다.<br /><br />저장 프로시저나 함수에 대 한 사용자 정의 형식의 인수는 VARCHAR (8000)로 변환 됩니다.<br /><br />PL/SQL 블록에서 사용자 정의 형식의 변수가 VARCHAR (8000)로 변환 됩니다.<br /><br />개체 테이블은 표준 테이블로 변환 됩니다.<br /><br />개체 뷰가 표준 뷰로 변환 됩니다.|  
  
## <a name="converting-oracle-database-objects"></a>Oracle Database 개체 변환  
Oracle 데이터베이스 개체를 변환 하려면 먼저 변환할 개체를 선택 하 고 SSMA에서 변환을 수행 하도록 합니다. 변환 하는 동안 출력 메시지를 보려면 **보기** 메뉴에서 **출력**을 선택 합니다.  
  
**Oracle 개체를 SQL Server 구문으로 변환 하려면**  
  
1.  Oracle 메타 데이터 탐색기에서 Oracle 서버를 확장 한 다음 **스키마**를 확장 합니다.  
  
2.  변환할 개체 선택:  
  
    -   모든 스키마를 변환 하려면 **스키마**옆의 확인란을 선택 합니다.  
  
    -   데이터베이스를 변환 하거나 생략 하려면 스키마 이름 옆의 확인란을 선택 합니다.  
  
    -   개체의 범주를 변환 하거나 생략 하려면 스키마를 확장 한 다음 범주 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
    -   개별 개체를 변환 하거나 생략 하려면 category 폴더를 확장 한 다음 개체 옆의 확인란을 선택 하거나 선택 취소 합니다.  
  
3.  선택한 모든 개체를 변환 하려면 **스키마** 를 마우스 오른쪽 단추로 클릭 하 고 **스키마 변환**을 선택 합니다.  
  
    개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **스키마 변환**을 선택 하 여 개별 개체 또는 개체 범주를 변환할 수도 있습니다.  
  
## <a name="viewing-conversion-problems"></a>변환 문제 보기  
일부 Oracle 개체는 변환 되지 않을 수 있습니다. 요약 변환 보고서를 보면 변환 성공률을 확인할 수 있습니다.  
  
**요약 보고서를 보려면**  
  
1.  Oracle 메타 데이터 탐색기에서 **스키마**를 선택 합니다.  
  
2.  오른쪽 창에서 **보고서** 탭을 선택 합니다.  
  
    이 보고서는 평가 또는 변환 된 모든 데이터베이스 개체에 대 한 요약 평가 보고서를 표시 합니다. 또한 개별 개체에 대 한 요약 보고서를 볼 수 있습니다.  
  
    -   개별 스키마에 대 한 보고서를 보려면 Oracle 메타 데이터 탐색기에서 스키마를 선택 합니다.  
  
    -   개별 개체에 대 한 보고서를 보려면 Oracle 메타 데이터 탐색기에서 개체를 선택 합니다. 변환 문제가 있는 개체에는 빨간색 오류 아이콘이 있습니다.  
  
변환이 실패 한 개체의 경우 변환 실패를 일으킨 구문을 볼 수 있습니다.  
  
**개별 변환 문제를 보려면**  
  
1.  Oracle 메타 데이터 탐색기에서 **스키마**를 확장 합니다.  
  
2.  빨간색 오류 아이콘을 표시 하는 스키마를 확장 합니다.  
  
3.  스키마 아래에서 빨간색 오류 아이콘이 있는 폴더를 확장 합니다.  
  
4.  빨간색 오류 아이콘이 있는 개체를 선택 합니다.  
  
5.  오른쪽 창에서 **보고서** 탭을 클릭 합니다.  
  
6.  **보고서** 탭의 맨 위에는 드롭다운 목록이 있습니다. 목록에 **통계가**표시 되 면 선택 항목을 **원본**으로 변경 합니다.  
  
    SSMA는 소스 코드와 코드 바로 위에 몇 개의 단추를 표시 합니다.  
  
7.  **다음 문제** 단추를 클릭 합니다. 오른쪽을 가리키는 화살표가 있는 빨간색 오류 아이콘입니다.  
  
    SSMA는 현재 개체에서 발견 된 첫 번째 문제 소스 코드를 강조 표시 합니다.  
  
변환할 수 없는 각 항목에 대해 해당 개체를 사용 하 여 수행할 작업을 결정 해야 합니다.  
  
-   **SQL** 탭에서 프로시저에 대 한 소스 코드를 수정할 수 있습니다.  
  
-   Oracle 데이터베이스에서 개체를 수정 하 여 문제가 있는 코드를 제거 하거나 수정할 수 있습니다. 업데이트 된 코드를 SSMA에 로드 하려면 메타 데이터를 업데이트 해야 합니다. 자세한 내용은 [Oracle Database &#40;OracleToSQL&#41;에 연결 ](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)을 참조 하세요.  
  
-   마이그레이션할 때 개체를 제외할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]메타 데이터 탐색기 및 Oracle 메타 데이터 탐색기에서 개체를 로드 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 oracle에서 데이터를 마이그레이션하기 전에 항목 옆에 있는 확인란의 선택을 취소 합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [변환 된 개체를 SQL Server 로드](loading-converted-database-objects-into-sql-server-oracletosql.md)하는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
[Oracle 데이터베이스를 SQL Server &#40;OracleToSQL&#41;로 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
