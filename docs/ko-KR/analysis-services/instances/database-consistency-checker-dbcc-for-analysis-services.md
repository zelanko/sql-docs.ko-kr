---
title: Analysis Services에 대 한 일관성 검사 (DBCC) 데이터베이스 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4a25919df6cb26609e008b6910ae6fb67bafba84
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="database-consistency-checker-dbcc-for-analysis-services"></a>Analysis Services에 대 한 데이터베이스 일관성 검사 (DBCC)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  DBCC는 Analysis Services 인스턴스에서 다차원 및 테이블 형식의 데이터베이스에 대한 주문형 데이터베이스 유효성 검사를 제공합니다. SSMS(SQL Server Management Studio)의 MDX 또는 XMLA 쿼리 창에서 DBCC를 실행하고 SSMS의 SQL Server Profiler 또는 xEvent 세션에서 DBCC 출력을 추적할 수 있습니다.  
이 명령은 개체 정의를 가져왔다가 빈 결과 집합을 반환하거나 개체가 손상된 경우 자세한 오류 정보를 반환합니다.   이 문서에서는 명령을 실행하고, 결과를 해석하고 발생한 문제를 해결하는 방법에 대해 알아봅니다.  
  
 테이블 형식 데이터베이스의 경우 DBCC에 의해 수행되는 일관성 검사는 데이터베이스를 다시 로드하거나, 동기화하거나, 복원할 때마다 자동으로 발생하는 기본 제공 유효성 검사와 동일합니다.  반면에 다차원 데이터베이스에 대한 일관성 검사는 DBCC를 주문형으로 실행할 경우에만 수행됩니다.  
  
 다양한 검사 범위에 맞게 적용되는 테이블 형식 데이터베이스에서 유효성 검사 범위는 모드를 기준으로 달라집니다.  
 DBCC 작업의 특징도 서버 모드별로 달라집니다. 다차원 데이터베이스의 검사 작업에는 디스크에서 데이터를 읽고, 실제 인덱스와의 비교를 위한 임시 인덱스를 생성하는 작업이 포함되며 이러한 작업 모두 완료하는 데 시간이 상당히 소요됩니다.  
  
 DBCC 명령 구문에서는 검사 중인 데이터베이스 형식과 관련된 개체 메타데이터가 사용됩니다.  
  
-   다차원 SQL Server 2016 이전 버전의 테이블 형식 1100 또는 1103 호환성 수준 데이터베이스는 **cubeID**, **measuregroupID**및 **partitionID**와 같은 다차원 모델링 구문에서 설명됩니다.  
  
-   메타 데이터 설명자로 구성 됩니다 새 테이블 형식 모델 데이터베이스의 호환성 수준 1200 이상에서 같은 **TableName** 및 **PartitionName**합니다.  
  
 데이터베이스가 SQL Server 2016 인스턴스에서 실행되는 한 Analysis Services에 대한 DBCC는 호환성 수준과 Analysis Services 데이터베이스 형식에 상관없이 모든 경우에 실행됩니다. 단지 각 데이터베이스 형식에 올바른 명령 구문을 사용하고 있어야 합니다.  
  
> [!NOTE]  
>  [DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)에 대해 잘 알고 있는 경우 Analysis Services에서 DBCC가 훨씬 범위가 좁다는 것을 즉시 확인할 수 있습니다. Analysis Services에서 DBCC는 데이터베이스 또는 개별 개체 전체에서 데이터 손상 시 단독으로 보고하는 단일 명령입니다. 정보를 수집하는 것과 같이 다른 작업을 고려하고 있는 경우에는 AMO PowerShell 또는 XMLA 스크립트를 대신 사용해 보세요. 자세한 내용은 [Monitor an Analysis Services Instance](../../analysis-services/instances/monitor-an-analysis-services-instance.md) 링크를 참조하세요.  
  
## <a name="permission-requirements"></a>사용 권한 요구 사항  
 명령을 실행하려면 Analysis Services 데이터베이스 또는 서버 관리자(서버 역할의 멤버)여야 합니다. 자세한 내용은 [데이터베이스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) 및 [Analysis Services 인스턴스에 서버 관리 권한 부여](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)를 참조하세요.  
  
## <a name="command-syntax"></a>명령 구문 
 1200에서 테이블 형식 데이터베이스와 더 높은 호환성 수준을 개체 정의 대 한 테이블 형식 메타 데이터를 사용합니다. 다음 예제에서는 SQL Server 2016 기능 수준에서 만든 테이블 형식 데이터베이스에 대한 전체 DBCC 구문을 보여 줍니다.  
  
 두 구문 간 주요 차이점 최신 XMLA 네임 스페이스에 더 포함 \<개체 > 요소와 아니요 \<모델 > 요소 (데이터베이스당 모델이 한 개만) 있습니다.  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2014/engine">  
     <DatabaseID>MyTabular1200DB_7811b5d8-c407-4203-8793-12e16c3d1b9b</DatabaseID>  
     <TableName>FactSales</TableName>  
     <PartitionName>FactSales 4</PartitionName>  
</DBCC>  
```  
  
 테이블 또는 파티션 이름 같은 하위 수준의 개체를 생략하여 전체 스키마를 확인할 수 있습니다.  
  
 각 개체의 속성 페이지를 통해 Management Studio에서 개체 이름 및 DatabaseID를 가져올 수 있습니다.  
  
## <a name="command-syntax-for-multidimensional-and-tabular-110x-databases"></a>다차원 및 테이블 형식 110x 데이터베이스에 대한 명령 구문  
 DBCC에서는 다차원뿐 아니라 테이블 형식 1100 및 1103 데이터베이스에서 동일한 구문을 사용합니다. 전체 데이터베이스를 포함하여 특정 데이터베이스 개체에 대해 DBCC를 실행할 수 있습니다. 개체 정의에 대한 자세한 내용은 [Object 요소&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)를 참조하세요.  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2006</PartitionID>  
     </Object>  
</DBCC>  
  
```  
  
 개체 체인에서 상위에 있는 개체에 대해 DBCC를 실행하려면 필요없는 하위 수준 개체 ID 요소를 모두 삭제합니다.  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
     </Object>  
</DBCC>  
  
```  
  
 테이블 형식 110x 데이터베이스의 경우 개체 정의 구문은 Process 명령 구문 다음에 모델링됩니다(특히 테이블이 차원과 측정값 그룹으로 매핑되는 방식에 대한 명령).  
  
-   **CubeID** 는 **Model**인 모델 ID로 매핑합니다.  
  
-   **MeasureGroupID** 는 테이블 ID로 매핑합니다.  
  
-   **PartitionID** 는 파티션 ID로 매핑합니다.  
  
## <a name="usage"></a>사용법  
 SQL Server Management Studio에서는 MDX 또는 XMLA 쿼리 창을 사용하여 DBCC를 호출할 수 있습니다. 또한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Profiler 또는 Analysis Services xEvents를 사용하여 DBCC 출력을 확인할 수 있습니다. SSAS DBCC 메시지는 Windows 응용 프로그램 이벤트 로그나 msmdsrv.log 파일에 보고되지 않습니다.  
  
 DBCC는 세그먼트에 고아 멤버가 있을 경우에 발생하는 논리 데이터 손상과 물리 데이터 손상을 검사합니다. DBCC를 실행하려면 먼저 데이터베이스를 처리해야 합니다. 원격이거나, 비어 있거나, 처리되지 않은 파티션은 건너뜁니다.  
  
 명령은 읽기 트랜잭션에서 실행되며, 강제 제한 시간 제한에 따라 종료될 수 있습니다. 파티션 검사는 병렬로 실행됩니다.  
  
 마지막으로 서비스를 다시 시작하고 난 후 발생한 손상 오류를 선택하려면 서비스를 다시 시작해야 할 수도 있습니다. 서버에 다시 연결하는 것만으로는 변경 사항을 선택하는 데 충분하지 않습니다.  
  
### <a name="run-dbcc-commands-in-management-studio"></a>Management Studio에서 DBCC 명령 실행  
 임시 쿼리에 대해 SQL Server Management Studio에서 MDX 또는 XMLA 쿼리 창을 엽니다. 이렇게 하려면 데이터베이스 | **새 쿼리** | **XMLA**를 마우스 오른쪽 단추로 클릭하여 명령을 실행하고 출력을 읽습니다.  
  
 ![Management Studio에서 DBCC XML 명령](../../analysis-services/instances/media/ssas-dbcc-ssms.gif "Management Studio에서 DBCC XML 명령")  
  
 문제가 검색되지 않으면 스크린샷과 같이 결과 탭에 빈 결과 집합이 표시됩니다.  
  
 메시지 탭에서는 세부 정보를 제공하지만 크기가 작은 데이터베이스의 경우 항상 신뢰할 수는 없습니다. 경우에 따라 상태 메시지가 잘리기도 하는데 이런 경우 상태 검사 메시지 없이 명령이 완료되었다고 나타납니다. 일반적인 메시지 보고서는 아래 표시된 보고서와 유사하게 나타날 수 있습니다.  
  
 **큐브 유효성 검사에 대해 DBCC에서 보고한 메시지**  
  
```  
Executing the query ...  
READS, 0  
READ_KB, 0  
WRITES, 0  
WRITE_KB, 0  
CPU_TIME_MS, 0  
ROWS_SCANNED, 0  
ROWS_RETURNED, 0  
  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
<Object>  
<DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
<CubeID>Adventure Works</CubeID>  
</Object>  
</DBCC>  
Started checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2012' partition.  
Finished checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2013' partition.  
Finished checking segment indexes for the 'Internet_Sales_2012' partition.  
Started checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2011' partition.  
Finished checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2012' partition.  
Started checking segment indexes for the 'Internet_Orders_2013' partition.  
Finished checking segment indexes for the 'Internet_Orders_2012' partition.  
...   
Run complete  
  
```  
  
 **이전 버전의 Analysis Services에 대해 DBCC 실행 시 출력**  
  
 DBCC는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스에서 실행되는 데이터베이스에만 지원됩니다. 이전 시스템에서 명령을 실행하면 이 오류가 반환됩니다.  
  
```  
Executing the query ...  
The DBCC element at line 7, column 87 (namespace http://schemas.microsoft.com/analysisservices/2003/engine) cannot appear under Envelope/Body/Execute/Command.  
Execution complete  
  
```  
  
### <a name="trace-dbcc-output-in-sql-server-profiler-2016"></a>SQL Server Profiler 2016에서 DBCC 출력 추적  
 Progress Reports 이벤트(Progress Report Begin, Progress Report Current, Progress Report End, Progress Report Error)를 포함하는 Profiler 추적에서 DBCC 출력을 확인할 수 있습니다.  
  
1.  추적을 시작합니다. Analysis Services에서 SQL Server Profiler를 사용하는 방법에 대한 자세한 내용은 [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md) 을 참조하세요.  
  
2.  **Command Begin** , **Command End** 그리고 **Progress Report** 이벤트 일부 또는 전체를 선택합니다.  
  
3.  Management Studio의 XMLA 또는 MDX 쿼리 창에서 이전 섹션에서 제공된 구문을 사용하여 DBCC 명령을 실행합니다.  
  
4.  SQL Server Profiler에서 DBCC 활동은 DBCC의 이벤트 하위 클래스가 있는 **Command** 이벤트를 통해 나타납니다.  
  
     ![ssas-dbcc-profiler-eventsubclass](../../analysis-services/instances/media/ssas-dbcc-profiler-eventsubclass.PNG "ssas-dbcc-profiler-eventsubclass")  
  
     이벤트 코드 32는 DBCC 실행을 나타냅니다.  
  
     이벤트 코드 64는 개별 개체에 대한 DBCC 진행률 보고서를 나타냅니다.  
  
     이벤트 코드 63은 다차원 개체에 대한 세그먼트 검사를 나타냅니다.  
  
     두 이벤트의 하위 클래스는 DBCC에서 반환되는 메시지에서 **TextData** 값을 확인하세요.  
  
     로 시작 된 상태 메시지 "의 일관성을 검사할 \<개체 >", "확인을 시작 했습니다 \<개체 >", 또는 "확인을 완료 했습니다 \<개체 >"입니다.  
  
    > [!NOTE]  
    >  CTP 3.0에서 개체는 내부 이름으로 식별됩니다. H$ 범주-로 Categories 계층은 명시 하는 예를 들어\<objectID > 합니다. 향후 CTP에서 내부 이름은 사용자에게 친숙한 이름으로 바꿔야 합니다.  
  
     오류 메시지는 아래 표에 나열되어 있습니다.  
  
### <a name="trace-dbcc-output-in-an-xevent-session-in-ssms"></a>SSMS의 xEvent 세션에서 DBCC 출력 추적  
 확장된 이벤트 세션에서는 프로파일러 이벤트 또는 xEvent를 모두 사용할 수 있습니다. **Command** 및 **Progress Report** 이벤트를 추가하는 지침에 대한 자세한 내용은 이전 섹션을 참조하세요.  
  
1.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **관리** >**확장 이벤트** >  **세션** > **새 세션**을 선택하여 세션을 시작합니다. 자세한 내용은  [Monitor Analysis Services with SQL Server Extended Events](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) 을 참조하세요.  
  
2.  Profiler 이벤트 범주에서는 **Progress Report** 이벤트를, PureXevent 범주에서는 **RequestProgress** 이벤트를 일부 또는 전체 선택합니다.  
  
3.  Management Studio의 XMLA 또는 MDX 쿼리 창에서 이전 섹션에서 제공된 구문을 사용하여 DBCC 명령을 실행합니다.  
  
4.  SSMS에서 세션 폴더를 새로 고칩니다. 세션 이름을 마우스 오른쪽 단추로 클릭하고 **라이브 데이터 감시**를 선택합니다.  
  
5.  DBCC에서 반환되는 메시지에서 TextData 값을 검토합니다.  TextData는 이벤트 필드 속성으로 이벤트에서 반환되는 상태 및 오류 메시지를 보여 줍니다.  
  
     로 시작 된 상태 메시지 "의 일관성을 검사할 \<개체 >", "확인을 시작 했습니다 \<개체 >", 또는 "확인을 완료 했습니다 \<개체 >"입니다.  
  
     오류 메시지는 아래 표에 나열되어 있습니다.  
  
## <a name="reference-consistency-checks-and-errors-for-multidimensional-databases"></a>참조: 다차원 데이터베이스에 대한 일관성 검사 및 오류  
 다차원 데이터베이스의 경우 파티션 인덱스만 유효성 검사 대상이 됩니다.  실행 중 DBCC는 파티션별로 임시 인덱스를 빌드하고 디스크의 지속형 인덱스와 비교합니다.  임시 인덱스를 빌드하려면 디스크에 있는 파티션 데이터에서 모든 데이터를 읽고, 비교를 위해 메모리에서 임시 인덱스를 유지해야 합니다. 추가 작업이 지정된 서버는 DBCC를 실행하는 동안 상당한 디스크 IO 및 메모리 사용을 경험할 수 있습니다.  
  
 다차원 인덱스 손상 검색 시 포함되는 검사 항목은 다음과 같습니다. 이 표에 표시되는 오류는 개체 수준에서 실패에 대한 xEvent 또는 Profiler 추적에서 나타납니다.  
  
||||  
|-|-|-|  
|**개체**|**DBCC 검사 항목 설명**|**실패 시 오류**|  
|파티션 인덱스|세그먼트 통계 및 인덱스를 확인합니다.<br /><br /> 디스크에 저장된 파티션 통계와 임시 파티션 인덱스의 각 멤버 ID를 비교합니다.  임시 인덱스에서 데이터 ID 값이 디스크의 파티션 인덱스 통계에 저장된 범위를 벗어난 멤버가 있는 경우 인덱스의 통계는 손상된 것으로 간주됩니다.|파티션 세그먼트 통계가 손상되었습니다.|  
|파티션 인덱스|메타데이터의 유효성을 검사합니다.<br /><br /> 임시 인덱스에 있는 각 멤버가 디스크의 세그먼트에 대한 인덱스 헤더 파일에 있는지 확인합니다.|파티션 세그먼트가 손상되었습니다.|  
|파티션 인덱스|세그먼트를 검색하여 물리적 손상을 찾습니다.<br /><br /> 임시 인덱스에 있는 각 멤버에 대해 디스크의 인덱스 파일을 읽고 인덱스 레코드 크기가 일치하는지, 동일한 데이터 페이지에 현재 멤버의 레코드가 있는 것으로 플래그가 지정되었는지 확인합니다.|파티션 세그먼트가 손상되었습니다.|  
  
## <a name="reference-consistency-checks-and-errors-for-tabular-databases"></a>참조: 테이블 형식 데이터베이스에 대한 일관성 검사 및 오류  
 다음 표는 검사에서 손상으로 나타날 경우 발생하는 오류와 함께 테이블 형식 개체에 수행하는 모든 일관성 검사 목록을 보여 줍니다. 이 표에 표시되는 오류는 개체 수준에서 실패에 대한 xEvent 또는 Profiler 추적에서 나타납니다.  
  
||||  
|-|-|-|  
|**개체**|**DBCC 검사 항목 설명**|**실패 시 오류**|  
|데이터베이스|데이터베이스의 테이블 수를 검사합니다.  0보다 작은 값은 손상을 나타냅니다.|저장소 계층이 손상되었습니다. '%{parent/}' 데이터베이스의 테이블 컬렉션이 손상되었습니다.|  
|데이터베이스|참조 무결성을 추적하는 데 사용하는 내부 구조를 검사하고 크기가 올바르지 않으면 오류를 throw합니다.|데이터베이스 파일이 일관성 검사를 통과하지 못했습니다.|  
|테이블|테이블이 차원 또는 팩트 테이블인지 확인하는 데 사용하는 내부 값을 검사합니다.  알려진 범위를 벗어나는 값은 손상을 나타냅니다.|테이블 통계를 검사하는 동안 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|테이블|세그먼트 맵에서 테이블에 대한 파티션 수가 테이블에 정의된 파티션 수와 일치하는지 검사합니다.|저장소 계층이 손상되었습니다. '%{parent/}' 테이블의 파티션 컬렉션이 손상되었습니다.|  
|테이블|테이블 형식 데이터베이스를 만들었거나 PowerPivot for Excel 2010에서 가져왔는데 파티션 수가 1보다 큰 경우에는 파티션 지원 기능이 이후 버전에서 추가되었으므로 오류가 발생하고, 손상되었음을 나타냅니다.|세그먼트 맵 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|Partition|세그먼트에서 각 데이터 세그먼트에 대한 레코드 수와 데이터 세그먼트 수가 세그먼트의 인덱스에 저장된 값과 일치하는지 각 파티션에 대해 확인합니다.|세그먼트 맵 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|Partition|총 레코드, 세그먼트 또는 세그먼트당 레코드 수가 올바르지 않거나(0 미만), 세그먼트 수가 총 레코드 수를 기준으로 계산된 필수 세그먼트 수와 일치하지 않을 경우 오류를 발생시킵니다.|세그먼트 맵 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|관계|관계에 대한 데이터를 저장하는 데 사용되는 구조에 레코드가 없거나 관계에 사용되는 테이블 이름이 비어 있으면 오류를 발생시킵니다.|관계 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|관계|기본 테이블, 기본 열, 외래 테이블 및 외부 열 이름이 설정되어 있고 관계와 관련된 열과 테이블에 액세스할 수 있는지 확인합니다.<br /><br /> 관련된 열 형식이 유효한지, 기본 키-외래 키 값의 인덱스 결과로 올바른 조회 구조가 생성되는지 확인합니다.|관계 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|계층|계층에 대한 정렬 순서가 인식되는 값이 아닌 경우 오류를 발생시킵니다.|'%{hier/}' 계층 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|계층|계층에서 수행되는 검사는 사용되는 계층 매핑 구성표의 내부 형식에 따라 달라집니다.<br /><br /> 모든 계층에서 올바른 처리 상태인지, 계층 저장소가 있는지, 해당되는 경우 데이터-ID-계층-위치 변환에 사용되는 데이터 구조가 있는지 검사됩니다.<br /><br /> 이러한 검사를 모두 통과하면 계층 구조는 계층의 각 위치에서 올바른 멤버를 가리키는지 확인하는 단계로 이동합니다.<br />테스트 중 하나라도 실패할 경우 오류가 발생합니다.|'%{hier/}' 계층 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|사용자 정의 계층|계층 수준 이름이 설정되어 있는지 검사합니다.<br /><br /> 계층을 처리할 때 내부 계층 데이터 저장소의 형식이 올바른지 검사합니다.  내부 계층 저장소에 잘못된 데이터 값이 포함되지 않았는지 확인합니다.<br /><br /> 계층이 처리되지 않은 상태로 표시되면 이 상태가 이전 데이터 구조에 적용되는지 확인하고, 모든 계층 수준이 빈 상태로 표시되는지 확인합니다.|'%{hier/}' 계층 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|열|열에 사용되는 인코딩이 알려진 값으로 설정되어 있지 않으면 오류가 오류를 발생시킵니다.|열 통계 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|열|메모리 내 엔진에서 열을 압축했는지 여부를 검사합니다.|열 통계 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|열|알려진 값에 대해 열의 압축 유형을 검사합니다.|열 통계 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|열|"토큰화" 열이 알려진 값으로 설정되어 있지 않으면 오류를 발생시킵니다.|열 통계 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|열|열 데이터 사전에 저장된 ID 범위가 데이터 사전의 값 수와 일치 하지 않거나 허용된 범위를 벗어난 경우 오류를 발생시킵니다.|데이터 사전 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|열|열에 대한 데이터 세그먼트의 수가 속해 있는 테이블에 대한 데이터 세그먼트의 수와 일치하는지 검사합니다.|저장소 계층이 손상되었습니다. '%{parent/}' 열의 세그먼트 컬렉션이 손상되었습니다.|  
|열|데이터 열에 대한 파티션 수가 데이터 세그먼트 맵에서 열에 대한 파티션 수와 일치하는지 검사합니다.|세그먼트 맵 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|열|열 세그먼트의 레코드 수가 해당 열 세그먼트에 대해 인덱스에 저장된 레코드 수와 일치하는지 검사합니다.|저장소 계층이 손상되었습니다. '%{parent/}' 열의 세그먼트 컬렉션이 손상되었습니다.|  
|열|열에 세그먼트 통계가 없으면 오류를 발생시킵니다.|세그먼트 통계 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|열|열에 압축 정보 또는 세그먼트 저장소가 없으면 오류를 발생시킵니다.|데이터베이스 파일이 일관성 검사를 통과하지 못했습니다.|  
|열|열에 대한 세그먼트 통계가 최소 데이터 ID, 최대 데이터 ID, 고유 값 수, 행 수, NULL 값의 존재 여부에 대한 실제 열 값과 일치하지 않을 경우 오류로 보고합니다.|세그먼트 통계 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|ColumnSegment|최소 데이터 ID 또는 최대 데이터 ID가 NULL에 대한 시스템 예약값보다 작은 경우, 열 세그먼트 정보가 손상된 것으로 표시합니다.|세그먼트 통계 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|ColumnSegment|이 세그먼트에 대한 행이 없는 경우에는 열에 대한 최소 및 최대 데이터 값이 NULL에 대한 시스템 예약값으로 설정되어 있어야 합니다.  값이 null이면 오류를 발생시킵니다.|세그먼트 통계 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|ColumnSegment|열에 행이 있고, null이 아닌 값이 하나 이상 있는 경우 열에 대한 최소 및 최대 데이터 ID가 NULL에 대한 시스템 예약값보다 큰지 검사합니다.|세그먼트 통계 검사 중에 DBCC(데이터베이스 일관성 검사)가 실패했습니다.|  
|내부|저장소 토큰화 힌트가 설정되어 있고 저장소가 처리된 경우 내부 테이블에 대해 유효한 포인터가 있는지 확인합니다.  저장소가 처리되지 않은 경우에는 모든 포인터가 null인지 확인합니다.<br />그렇지 않으면 일반 DBCC 오류를 반환합니다.|데이터베이스 파일이 일관성 검사를 통과하지 못했습니다.|  
|DBCC 데이터베이스|데이터베이스 스키마에 테이블이 없거나 하나 이상의 테이블에 액세스할 수 없는 경우 오류를 발생시킵니다.|저장소 계층이 손상되었습니다. '%{parent/}' 데이터베이스의 테이블 컬렉션이 손상되었습니다.|  
|DBCC 데이터베이스|테이블이 임시로 표시되거나 알 수 없는 형식일 경우 오류를 발생시킵니다.|잘못된 테이블 형식이 발견되었습니다.|  
|DBCC 데이터베이스|테이블에 대한 관계 수에 음수 값이 있거나 모든 테이블에서 관계가 정의되었지만 해당 관계 구조를 찾을 수 없는 경우 오류를 발생시킵니다.|저장소 계층이 손상되었습니다. '%{parent/}' 테이블의 관계 컬렉션이 손상되었습니다.|  
|DBCC 데이터베이스|데이터베이스의 호환성 수준이 1050(SQL Server 2008 R2/PowerPivot v1.0)이고 관계 수가 모델의 테이블 수를 초과하는 경우 데이터베이스가 손상되었다고 표시합니다.|데이터베이스 파일이 일관성 검사를 통과하지 못했습니다.|  
|DBCC 테이블|유효성 검사 중인 테이블의 경우 열 수가 0보다 작은지 검사하고 true인 경우 오류를 발생시킵니다.  테이블에서 열에 대한 열 저장소가 NULL인 경우에도 오류가 발생합니다.|저장소 계층이 손상되었습니다. '%{parent/}' 테이블의 열 컬렉션이 손상되었습니다.|  
|DBCC 파티션|유효성 검사 중인 파티션이 속해 있는 테이블을 검사하고 테이블의 열 수가 0보다 작은 경우 테이블에서 열 컬렉션이 손상되었음을 표시합니다. 테이블에서 열에 대한 열 저장소가 NULL인 경우에도 오류가 발생합니다.|저장소 계층이 손상되었습니다. '%{parent/}' 테이블의 열 컬렉션이 손상되었습니다.|  
|DBCC 파티션|선택한 파티션에 대한 각 열을 반복하고 파티션의 각 세그먼트에 열 세그먼트 구조에 대한 올바른 링크가 있는지 검사합니다.  세그먼트에 NULL인 링크가 있는 경우 파티션은 손상된 것으로 간주됩니다.|저장소 계층이 손상되었습니다. '%{parent/}' 열의 세그먼트 컬렉션이 손상되었습니다.|  
|열|열 형식이 올바르지 않으면 오류가 반환됩니다.|잘못된 세그먼트 형식이 발견되었습니다.|  
|열|열의 세그먼트 수에 대해 음수가 있거나 세그먼트에 대한 열 세그먼트 구조 포인터에 NULL인 링크가 있을 경우 오류가 반환됩니다.|저장소 계층이 손상되었습니다. '%{parent/}' 열의 세그먼트 컬렉션이 손상되었습니다.|  
|DBCC 명령|DBCC 명령은 DBCC 작업을 통해 진행되므로 여러 개의 상태 메시지를 보고합니다.  시작하기 전에 개체의 데이터베이스, 테이블 또는 열 이름을 포함하는 상태 메시지를 보고하고, 각 개체 검사를 완료한 후에 다시 보고합니다.|일관성 검사는 \<개체 이름 > \<objecttype > 합니다. 단계: 사전 검사<br /><br /> 일관성 검사는 \<개체 이름 > \<objecttype > 합니다. 단계: 사후 검사|  
  
## <a name="common-resolutions-for-error-conditions"></a>오류 상태에 대한 일반적인 해결 방법  
 다음 오류는 SQL Server Management Studio 또는 msmdsrv.log 파일에 표시됩니다. 검사를 하나 이상 통과하지 못할 경우 이 오류가 나타납니다. 오류에 따라 개체를 다시 처리하고 솔루션을 삭제하고 다시 배포하거나, 데이터베이스를 복원하는 해결 방법이 권장됩니다.  
  
|오류|문제점|해결 방법|  
|-----------|-----------|----------------|  
|**메타데이터 관리자에서 오류가 발생했습니다.**<br /><br /> 개체 참조 '\<objectID >' 올바르지 않습니다. 메타데이터 클래스 계층 구조와 일치하지 않습니다.|형식이 잘못된 명령|명령 구문을 확인합니다. 부모 개체 중 하나 이상을 지정하지 않고 하위 수준 개체를 포함시킨 경우가 많습니다.|  
|**메타데이터 관리자에서 오류가 발생했습니다.**<br /><br /> 중 하나는 \<개체 >의 ID와 '\<objectID >'에 존재 하지 않는 \<parentobject >의 ID와 '\<parentobjectID >', 사용자 개체에 액세스할 수 있는 사용 권한이 없습니다.|인덱스 손상(다차원)|개체와 모든 종속 개체를 다시 처리합니다.|  
|**파티션의 일관성 검사 중에 오류가 발생했습니다.**<br /><br /> 일관성을 확인 하는 동안 오류가 발생 했습니다.는 \<파티션-이름 >의 파티션에 \<측정값 그룹 이름 > 측정값 그룹에 대 한는 \<큐브-이름 >에서 큐브는 \<데이터베이스 이름 > 데이터베이스. 파티션 또는 인덱스를 다시 처리하여 손상을 해결하세요.|인덱스 손상(다차원)|개체와 모든 종속 개체를 다시 처리합니다.|  
|**파티션 세그먼트 통계가 손상되었습니다.**|인덱스 손상(다차원)|개체와 모든 종속 개체를 다시 처리합니다.|  
|**파티션 세그먼트가 손상되었습니다.**|메타데이터 손상(다차원 또는 테이블 형식)|프로젝트를 삭제하고 다시 배포하거나 백업에서 복원하여 다시 처리합니다.<br /><br /> 자세한 내용은 [How to handle corruption in Analysis Services databases (blog)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Analysis Services 데이터베이스에서 손상을 처리하는 방법(블로그))를 참조하세요.|  
|**테이블 메타데이터 손상**<br /><br /> 테이블 \<테이블-이름 > 메타 데이터 파일이 손상 되었습니다. 주 테이블을 DataFileList 노드 아래에서 찾을 수 없습니다.|메타데이터 손상(테이블 형식만)|프로젝트를 삭제하고 다시 배포하거나 백업에서 복원하여 다시 처리합니다.<br /><br /> 자세한 내용은 [How to handle corruption in Analysis Services databases (blog)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Analysis Services 데이터베이스에서 손상을 처리하는 방법(블로그))를 참조하세요.|  
|**저장소 계층 손상**<br /><br /> 저장소 계층 손상:의 컬렉션 \<형식-이름 >에 \<부모-이름 > \<부모-형식 > 손상 되었습니다.|메타데이터 손상(테이블 형식만)|프로젝트를 삭제하고 다시 배포하거나 백업에서 복원하여 다시 처리합니다.<br /><br /> 자세한 내용은 [How to handle corruption in Analysis Services databases (blog)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Analysis Services 데이터베이스에서 손상을 처리하는 방법(블로그))를 참조하세요.|  
|**시스템 테이블이 없습니다.**<br /><br /> 시스템 테이블 \<테이블-이름 >가 없습니다.|개체 손상(테이블 형식만)|개체와 모든 종속 개체를 다시 처리합니다.|  
|**테이블 통계가 손상되었습니다.**<br /><br /> 시스템 테이블의 통계 \<테이블-이름 >가 없습니다.|메타데이터 손상(테이블 형식만)|프로젝트를 삭제하고 다시 배포하거나 백업에서 복원하여 다시 처리합니다.<br /><br /> 자세한 내용은 [How to handle corruption in Analysis Services databases (blog)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Analysis Services 데이터베이스에서 손상을 처리하는 방법(블로그))를 참조하세요.|  
  
## <a name="disable-automatic-consistency-checks-on-database-load-operations-through--the-msmdsrvini-configuration-file"></a>msmdsrv.ini 구성 파일을 통한 데이터베이스 로드 작업에서 자동 일관성 검사를 사용하지 않도록 설정  
 권장하지는 않지만 데이터베이스 로드 이벤트에서 자동으로 발생하는 기본 제공 데이터베이스 일관성 검사를 사용하지 않도록 설정할 수 있습니다(테이블 형식 데이터베이스만 해당). 이렇게 하려면 msmdsrv.ini 파일에서 구성 설정을 수정해야 합니다.  
  
```  
<ConfigurationSettings>  
     <Vertipaq />  
          <DisableConsistencyChecks />  
```  
  
 이 설정은 구성 파일에 나타나지 않으며 수동으로 추가해야 합니다.  
  
 유효한 값은 다음과 같습니다.  
  
-   **-2** (기본값) DBCC를 사용하도록 설정합니다. 서버에서 오류를 논리적으로 해결할 수 있을 확신이 높을 경우 자동으로 수정이 적용됩니다. 그렇지 않으면 오류가 기록됩니다.  
  
-   **-1** DBCC를 부분적으로 사용하도록 설정합니다. 트랜잭션이 완료될 때 데이터베이스 상태를 검사하는 사전 커밋 유효성 검사와 RESTORE 작업에 대해 설정됩니다.  
  
-   **0** DBCC를 부분적으로 사용하도록 설정합니다. 데이터베이스 일관성 검사가 RESTORE, IMAGELOAD, LOCALCUBELOAD, ATTACH 작업 중  
         수행됩니다.  
  
-   **1** DBCC를 사용하지 않도록 설정합니다. 데이터 무결성 검사는 사용하지 않도록 설정되지만 deserialization 검사는 계속 발생됩니다.  
  
> [!NOTE]  
>  명령을 주문형으로 실행하는 경우 이 설정은 DBCC에 영향을 미치지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스, 테이블 또는 파티션 처리&#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)   
 [다차원 모델 처리&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Analysis Services 인스턴스 모니터](../../analysis-services/instances/monitor-an-analysis-services-instance.md)   
 [Analysis services에서 테이블 형식 모델에 대한 호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services에서 서버 속성](../../analysis-services/server-properties/server-properties-in-analysis-services.md)  
  
  
