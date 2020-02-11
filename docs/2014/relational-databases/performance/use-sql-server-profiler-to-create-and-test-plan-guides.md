---
title: SQL Server Profiler를 사용하여 계획 지침 작성 및 테스트 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- checking plan guides
- plan guides [SQL Server], testing
- plan guides [SQL Server], SQL Server Profiler
- matching queries to plan guides [SQL Server]
- testing plan guides
- SQL Server Profiler, plan guides
- plan guides [SQL Server], creating
- capturing query text [SQL Server]
- verifying plan guides
- Profiler [SQL Server Profiler], plan guides
- query-to-plan guide matching [SQL Server]
ms.assetid: 7018dbf0-1a1a-411a-88af-327bedf9cfbd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fcdbfe9f9289ab9cc529d4d37eb27d877dfff3ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150484"
---
# <a name="use-sql-server-profiler-to-create-and-test-plan-guides"></a>SQL Server Profiler를 사용하여 계획 지침 작성 및 테스트
  계획 지침을 만들 때는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 *sp_create_plan_guide* 저장 프로시저의 **statement_text** 인수에서 사용할 정확한 쿼리 텍스트를 캡처할 수 있습니다. 이렇게 하면 컴파일 시 계획 지침이 쿼리와 일치하도록 보장할 수 있습니다. 계획 지침을 만든 다음 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 실제로 계획 지침이 쿼리와 일치하는지 여부를 테스트할 수도 있습니다. 일반적으로 쿼리가 계획 지침과 일치하는지 확인하기 위해 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하여 계획 지침을 테스트해야 합니다.  
  
## <a name="capturing-query-text-by-using-sql-server-profiler"></a>SQL Server Profiler를 사용하여 쿼리 텍스트 캡처  
 쿼리를 실행하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]에 전송된 대로 정확히 텍스트를 캡처하려는 경우 쿼리 텍스트와 정확히 일치하는 SQL 또는 TEMPLATE 유형의 계획 지침을 만들 수 있습니다. 이렇게 하면 쿼리 최적화 프로그램에서 이 계획 지침이 사용되도록 보장할 수 있습니다.  
  
 애플리케이션에 의해 독립 실행형 일괄 처리로 전송되는 다음 쿼리를 고려하십시오.  
  
```  
SELECT COUNT(*) AS c  
FROM Sales.SalesOrderHeader AS h  
INNER JOIN Sales.SalesOrderDetail AS d  
  ON h.SalesOrderID = d.SalesOrderID  
WHERE h.OrderDate BETWEEN '20000101' and '20050101';  
```  
  
 병합 조인 연산을 사용하여 이 쿼리를 실행하려고 하지만 SHOWPLAN에 이 쿼리가 병합 조인을 사용하지 않는 것으로 표시된다고 가정해 보십시오. 애플리케이션에서는 쿼리를 직접 변경할 수 없기 때문에 그 대신 컴파일 시 쿼리에 MERGE JOIN 쿼리 힌트를 첨부하도록 지정하는 계획 지침을 만듭니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 수신하는 것과 정확히 같은 쿼리 텍스트를 캡처하려면 다음 단계를 수행하십시오.  
  
1.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 추적을 시작하고 **SQL:BatchStarting** 이벤트 유형을 선택합니다.  
  
2.  애플리케이션이 쿼리를 실행하도록 합니다.  
  
3.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 추적을 일시 중지합니다.  
  
4.  이 쿼리에 해당하는 **SQL:BatchStarting** 이벤트를 클릭합니다.  
  
5.  마우스 오른쪽 단추로 클릭하고 **이벤트 데이터 추출**을 선택합니다.  
  
    > [!IMPORTANT]  
    >  프로파일러 추적 창의 아래쪽 창에서 일괄 처리 텍스트를 선택하여 복사하려고 하지 마십시오. 이렇게 하면 만든 계획 지침이 원본 일괄 처리와 일치하지 않을 수 있습니다.  
  
6.  이벤트 데이터를 파일에 저장합니다. 이 데이터는 일괄 처리 텍스트입니다.  
  
7.  일괄 처리 텍스트 파일을 메모장에서 열고 텍스트를 복사 및 붙여 넣기 버퍼로 복사합니다.  
  
8.  계획 지침을 만들고 복사한 텍스트를 **@stmt**인수에 대해 지정된 따옴표( **@stmt** ) 안에 붙여넣습니다. **@stmt** 인수의 앞에 다른 작은따옴표를 사용 하 여 임의의 작은따옴표를 이스케이프 해야 합니다. 작은따옴표를 삽입할 때는 다른 문자를 추가 또는 제거하지 않도록 주의해야 합니다. 예를 들어 날짜 리터럴 **'** 20000101 **'** 은 **''** 20000101 **''** 로 구분해야 합니다.  
  
 계획 지침은 다음과 같습니다.  
  
```  
EXEC sp_create_plan_guide   
    @name = N'MyGuide1',  
    @stmt = N'<paste the text copied from the batch text file here>',  
    @type = N'SQL',  
    @module_or_batch = NULL,  
    @params = NULL,  
    @hints = N'OPTION (MERGE JOIN)';  
```  
  
## <a name="testing-plan-guides-by-using-sql-server-profiler"></a>SQL Server Profiler를 사용하여 계획 지침 테스트  
 계획 지침이 쿼리와 일치하는지 확인하려면 다음 단계를 수행하십시오.  
  
1.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 추적을 시작하고 **성능** 노드 아래에 있는 **Showplan XML** 이벤트 유형을 선택합니다.  
  
2.  애플리케이션이 쿼리를 실행하도록 합니다.  
  
3.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 추적을 일시 중지합니다.  
  
4.  해당 쿼리에 대한 **Showplan XML** 이벤트를 찾습니다.  
  
    > [!NOTE]  
    >  **Showplan XML for Query Compile** 이벤트를 사용할 수 없습니다. 해당 이벤트에**PlanGuideDB** 가 없습니다.  
  
5.  계획 지침이 OBJECT 또는 SQL 유형인 경우 쿼리와 일치할 것으로 예상되는 계획 지침의 **PlanGuideDB** 및 **PlanGuideName** 특성이 **Showplan XML** 이벤트에 포함되어 있는지 확인합니다. 또는 TEMPLATE 계획 지침의 경우 예상되는 계획 지침의 **TemplatePlanGuideDB** 및 **TemplatePlanGuideName** 특성이 **Showplan XML** 이벤트에 포함되어 있는지 확인합니다. 그러면 계획 지침이 작동하는지 확인할 수 있습니다. 이러한 특성은 계획의 **\<StmtSimple>** 요소에 포함됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [sp_create_plan_guide&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)  
  
  
