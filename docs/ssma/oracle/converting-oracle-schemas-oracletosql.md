---
title: Oracle 스키마 (OracleToSQL) 변환 | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Conversion Results
ms.assetid: e021182d-31da-443d-b110-937f5db27272
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: 208378f2be9ad4eea080df758616e554c1262905
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="converting-oracle-schemas-oracletosql"></a>Oracle 스키마 (OracleToSQL) 변환
Oracle에 연결한 후에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 프로젝트 설정 및 데이터 매핑 옵션에는 Oracle 데이터베이스 개체를 변환할 수 있습니다 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스 개체입니다.  
  
## <a name="the-conversion-process"></a>변환 프로세스  
Oracle에서 개체 정의 가져와 데이터베이스 개체를 변환, 유사로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체, 및 SSMA 메타 데이터를이 정보를 로드 합니다. 인스턴스로 정보를 로드 하지 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 사용 하 여 개체 및 해당 속성을 볼 다음는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기입니다.  
  
SSMA는 변환 중 출력 창에 출력 메시지 및 오류 목록 창에 오류 메시지를 인쇄합니다. 출력 및 오류 정보를 사용 하 여 Oracle 데이터베이스 또는 원하는 변환 결과를 얻으려면 변환 프로세스를 수정할 수 있는지 확인 합니다.  
  
## <a name="setting-conversion-options"></a>변환 옵션 설정  
개체를 변환 하기 전에 프로젝트 변환 옵션을 검토는 **프로젝트 설정** 대화 상자. 이 대화 상자를 사용 하 여 SSMA 함수 및 전역 변수를 변환 하는 방법을 설정할 수 있습니다. 자세한 내용은 참조 [프로젝트 설정 &#40; 변환 &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
## <a name="conversion-results"></a>변환 결과  
다음 표에 나와 있는 Oracle 개체 변환 되 고 그 결과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 개체:  
  
|||  
|-|-|  
|Oracle 개체|결과 SQL Server 개체|  
|함수|함수를 직접 변환할 수 있는 경우 [!INCLUDE[tsql](../../includes/tsql_md.md)], SSMA는 함수를 만듭니다.<br /><br />경우에 따라 저장된 프로시저에 함수를 변환 합니다. 이 경우 SSMA는 저장된 프로시저와 저장된 프로시저를 호출 하는 함수를 만듭니다.|  
|절차|프로시저를 직접 변환할 수 있는 경우 [!INCLUDE[tsql](../../includes/tsql_md.md)], SSMA 저장된 프로시저를 만듭니다.<br /><br />경우에 따라 자치 트랜잭션을에서 저장된 프로시저를 호출 해야 합니다. 이 경우 SSMA 두 개의 저장된 프로시저를 만듭니다: 저장 프로시저는 프로시저와 구현 하는 호출에 사용 되는 다른 저장 프로시저를 구현 합니다.|  
|패키지|SSMA는 저장된 프로시저 및 비슷한 개체 이름으로 통합 하는 함수 집합을 만듭니다.|  
|시퀀스|SSMA (SQL Server 2012 또는 SQL Server 2014) 시퀀스 개체를 만들거나 Oracle 시퀀스를 에뮬레이션 합니다.|  
|인덱스 및 트리거가 같은 종속 개체가 있는 테이블|SSMA는 종속 개체와 테이블을 만듭니다.|  
|트리거 등의 종속 개체와 보기|SSMA는 종속 개체와 뷰를 만듭니다.|  
|구체화 된 뷰|**SSMA는 몇 가지 예외가 SQL server에서 인덱싱된 뷰를 만듭니다. 구체화 된 뷰는 다음 구문 중 하나 이상 포함 하는 경우 변환이 실패 합니다.**<br /><br />사용자 정의 함수<br /><br />명확 하지 않은 필드 / 함수 / 식은 SELECT, 위치 또는 GROUP BY 절<br /><br />Float 열에 SELECT *의 사용 위치 또는 GROUP BY 절 (이전 문제의 특수 한 경우)<br /><br />사용자 지정 데이터 형식 (중첩 시 테이블)<br /><br />COUNT (distinct &lt;필드&gt;)<br /><br />FETCH<br /><br />OUTER 조인(LEFT, RIGHT 또는 FULL)<br /><br />하위 쿼리, 보기<br /><br />과다, RANK, 잠재 고객, 로그<br /><br />MIN, MAX<br /><br />UNION, 빼기, 교차<br /><br />HAVING|  
|트리거|**SSMA는 다음 규칙에 따라 트리거를 만듭니다.**<br /><br />전에 트리거는 INSTEAD of 트리거도 변환 됩니다.<br /><br />다음 트리거는 AFTER 트리거도 변환 됩니다.<br /><br />INSTEAD OF 트리거는 INSTEAD of 트리거도 변환 됩니다. 동일한 작업에 정의 된 여러 INSTEAD OF 트리거는 트리거를 하나에 결합 됩니다.<br /><br />행 수준 트리거가 커서를 사용 하 여 에뮬레이션 합니다.<br /><br />연계 트리거는 여러 개의 개별 트리거도 변환 됩니다.|  
|동의어|**동의어는 다음 개체 유형에 대해 생성 됩니다.**<br /><br />테이블 및 개체 테이블<br /><br />뷰 및 개체 보기<br /><br />저장 프로시저<br /><br />함수<br /><br />**다음 개체에 대 한 동의어 해결 되 고 직접 개체 참조로 대체 합니다.**<br /><br />시퀀스<br /><br />패키지<br /><br />Java 클래스 스키마 개체<br /><br />사용자 정의 개체 유형<br /><br />다른 동의어에 대 한 동의어를 마이그레이션할 수 없습니다 및 오류로 표시 됩니다.<br /><br />동의어는 Materialized 보기에 대해 생성 되지 않습니다.|  
|사용자 정의 형식|**SSMA는 사용자 정의 형식 변환에 대 한 지원을 제공 하지 않습니다. PL/SQL 프로그램에서의 사용법을 포함 하 여 사용자 정의 형식 특수 변환 오류는 다음과 같은 규칙을 기반으로 표시 됩니다.**<br /><br />사용자 정의 형식의 테이블 열 VARCHAR(8000)로 변환 됩니다.<br /><br />사용자의 인수 정의 저장된 프로시저에 형식 또는 함수 VARCHAR(8000)로 변환 됩니다.<br /><br />PL/SQL 블록의 사용자 정의 형식의 변수 VARCHAR(8000)로 변환 됩니다.<br /><br />개체 테이블은 표준 테이블으로 변환 됩니다.<br /><br />개체 뷰는 표준 보기로 변환 됩니다.|  
  
## <a name="converting-oracle-database-objects"></a>Oracle 데이터베이스 개체를 변환합니다.  
Oracle 데이터베이스 개체를 변환 하려면 먼저, 변환할 개체를 선택 및 SSMA는 변환을 수행 해야 합니다. 변환 중에 출력 메시지를 볼 수는 **보기** 메뉴 선택 **출력**합니다.  
  
**SQL Server 구문으로 Oracle 개체를 변환 하려면**  
  
1.  Oracle 메타 데이터 탐색기에서 Oracle 서버를 확장 한 다음 확장 **스키마**합니다.  
  
2.  변환할 개체를 선택 합니다.  
  
    -   모든 스키마를 변환 하려면 확인란을 옆에 선택 **스키마**합니다.  
  
    -   를 변환 하거나 데이터베이스를 생략 하려면 스키마 이름 옆에 있는 확인란을 선택 합니다.  
  
    -   를 변환 하거나 개체의 범주를 생략 하려면 스키마를 확장 한 다음 선택 하거나 범주 옆의 확인란의 선택을 취소 합니다.  
  
    -   를 변환 하거나 개별 개체를 생략 하려면 범주 폴더를 확장 한 다음 선택 하거나 개체 옆에 있는 확인란의 선택을 취소 합니다.  
  
3.  선택한 모든 개체를 변환 하려면 마우스 오른쪽 단추로 클릭 **스키마** 선택 **변환 스키마**합니다.  
  
    개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 한 다음 선택 하 여 개별 개체 또는 개체 범주의 변환할 수도 **변환 스키마**합니다.  
  
## <a name="viewing-conversion-problems"></a>변환 문제 보기  
일부 Oracle 개체를 변환할 수 있습니다. 변환 요약 보고서를 확인 하 여 변환 성공률을 확인할 수 있습니다.  
  
**요약 보고서를 보려면**  
  
1.  Oracle 메타 데이터 탐색기에서 선택 **스키마**합니다.  
  
2.  오른쪽 창에서 선택 된 **보고서** 탭 합니다.  
  
    이 보고서는 평가 되거나 변환 된 모든 데이터베이스 개체에 대 한 요약 평가 보고서를 표시 합니다. 개별 개체에 대 한 요약 보고서를 볼 수 있습니다.  
  
    -   개별 스키마에 대 한 보고서를 보려면 Oracle 메타 데이터 탐색기에서 스키마를 선택 합니다.  
  
    -   개별 개체에 대 한 보고서를 보려면 Oracle 메타 데이터 탐색기에서 개체를 선택 합니다. 빨간색 오류 아이콘이 변환 문제가 발생 하는 개체.  
  
개체의 변환에 실패 한 경우 변환 실패 시 발생 하는 구문을 볼 수 있습니다.  
  
**개별 변환 문제를 보려면**  
  
1.  Oracle 메타 데이터 탐색기에서 확장 **스키마**합니다.  
  
2.  빨간색 오류 아이콘을 보여 주는 스키마를 확장 합니다.  
  
3.  스키마에서 빨간색 오류 아이콘을가지고 있는 폴더를 확장 합니다.  
  
4.  빨간색 오류 아이콘을 가진 개체를 선택 합니다.  
  
5.  오른쪽 창에서 클릭 하 고 **보고서** 탭 합니다.  
  
6.  맨 위에 있는 **보고서** 탭은 드롭 다운 목록입니다. 목록에 표시 하는 경우 **통계**, 선택 영역을 변경 **소스**합니다.  
  
    SSMA는 소스 코드 및 코드 바로 위의 여러 개의 단추가 표시 됩니다.  
  
7.  클릭는 **다음 문제점** 단추입니다. 오른쪽을 가리키는 화살표가 있는 빨간색 오류 아이콘입니다.  
  
    SSMA는 현재 개체에서 찾은 첫 번째 문제가 있는 소스 코드를 강조 표시 합니다.  
  
변환 될 수 있는 각 항목에 대 한 해당 개체를 사용 하 여 수행할를 결정 해야 합니다.  
  
-   프로시저에 대 한 소스 코드를 수정할 수는 **SQL** 탭 합니다.  
  
-   제거 하거나 문제가 있는 코드를 수정 하려면 Oracle 데이터베이스에서 개체를 수정할 수 있습니다. SSMA에 업데이트 된 코드를 로드 하려면 메타 데이터를 업데이트 해야 합니다. 자세한 내용은 참조 [Oracle 데이터베이스 &#40; OracleToSQL &#41;에 연결](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)합니다.  
  
-   마이그레이션에서 개체를 제외할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 메타 데이터 탐색기 및 Oracle 메타 데이터 탐색기가 개체를 로드 하기 전에 항목 옆에 있는 확인란의 선택을 취소 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 및 Oracle에서 데이터 마이그레이션.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계에서는 [SQL Server로 변환된 된 개체를 로드](http://msdn.microsoft.com/en-us/a8ae33b2-1883-4785-922b-ea0e31c0b37a)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server &#40; OracleToSQL &#41; Oracle 데이터베이스 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
