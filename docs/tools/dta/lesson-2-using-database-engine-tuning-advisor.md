---
title: '2단원: 데이터베이스 엔진 튜닝 관리자 사용 | Microsoft'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 3317d4f8-ed9e-4f2e-b5f1-a6bf3a9d6c8d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b2f526510f69a91e3228431953f73717790246f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034745"
---
# <a name="lesson-2-using-database-engine-tuning-advisor"></a>2단원: 데이터베이스 엔진 튜닝 관리자 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
데이터베이스 엔진 튜닝 관리자를 사용하면 데이터베이스를 튜닝하고 튜닝 세션을 관리하며 튜닝 권장 구성을 확인할 수 있습니다. 물리적 디자인 구조에 대해 잘 아는 사용자라면 이 도구를 사용하여 탐구적인 데이터베이스 튜닝 분석을 수행할 수 있습니다. 데이터베이스 튜닝에 대해 잘 모르는 사용자도 이 도구를 사용하여 자신이 튜닝하는 작업에 가장 적합한 물리적 디자인 구조 구성을 찾을 수 있습니다. 이 단원에서는 데이터베이스 엔진 튜닝 관리자 그래픽 사용자 인터페이스를 처음 접하는 데이터베이스 관리자와 물리적 디자인 구조에 대한 광범위한 지식이 없는 시스템 관리자에게 기본 연습을 제공합니다.  

## <a name="prerequisites"></a>사전 요구 사항 

이 자습서를 완료하려면 SQL Server Management Studio, SQL Server를 실행하는 서버에 대한 액세스 및 AdventureWorks 데이터베이스가 필요합니다.

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)을 설치합니다.
- [AdventureWorks2017 샘플 데이터베이스](https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017)를 다운로드합니다.


SSMS에서 데이터베이스를 복원하기 위한 지침은 [데이터베이스 복원](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms?view=sql-server-2017)을 참조하세요.

  >[!NOTE]
  > 이 자습서는 SQL Server Management Studio 및 기본적인 데이터베이스 관리 작업을 사용 하는 데 익숙한 사용자를 위한 것입니다. 
  
## <a name="tuning-a-workload"></a>작업 튜닝
데이터베이스 엔진 튜닝 관리자를 사용하여 튜닝하려고 선택한 데이터베이스와 테이블의 쿼리 성능에 가장 적합한 물리적 데이터베이스 디자인을 찾을 수 있습니다.  

1.  Sample [select](../../t-sql/queries/select-examples-transact-sql.md) 문을 복사 하 여의 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]쿼리 편집기에 문을 붙여넣습니다. 쉽게 찾을 수 있는 디렉터리에 **MyScript.sql**이라는 이름으로 파일을 저장합니다. AdventureWorks2017 데이터베이스에 대해 작동 하는 예제는 아래에 제공 되어 있습니다.  

 ```sql
 Use [Adventureworks2017]; -- may need to modify database name to match database
 GO
 SELECT DISTINCT pp.LastName, pp.FirstName 
 FROM Person.Person pp JOIN HumanResources.Employee e
 ON e.BusinessEntityID = pp.BusinessEntityID WHERE pp.BusinessEntityID IN 
 (SELECT SalesPersonID 
 FROM Sales.SalesOrderHeader
 WHERE SalesOrderID IN 
 (SELECT SalesOrderID 
 FROM Sales.SalesOrderDetail
 WHERE ProductID IN 
 (SELECT ProductID 
 FROM Production.Product p 
 WHERE ProductNumber = 'BK-M68B-42')));
 GO
 ```

  ![SQL 쿼리 저장](media/dta-tutorials/dta-save-query.png)
  
2.  데이터베이스 엔진 튜닝 관리자를 시작합니다. SSMS (SQL Server Management Studio)의 **도구** 메뉴에서 **데이터베이스 튜닝 관리자** 를 선택 합니다.  자세한 내용은 [Launch Database Engine Tuning Advisor](lesson-1-basic-navigation-in-database-engine-tuning-advisor.md#launch-database-tuning-advisor)(데이터베이스 엔진 튜닝 관리자 시작)를 참조하세요. **서버에 연결** 대화 상자에서 SQL Server에 연결 합니다.  
  
3.  데이터베이스 엔진 튜닝 관리자 GUI 오른쪽 창의 **일반** 탭에서 **세션 이름**에 **MySession**을 입력합니다. 
  
4.  **작업**에 대해 **파일** 을 선택 하 고 쌍안경 아이콘을 선택 하 여 **작업 파일을 찾습니다**. 1 단계에서 저장 한 **MyScript** 파일을 찾습니다.  

   ![이전에 저장 된 스크립트 찾기](media/dta-tutorials/dta-script.png)
  
5.  **작업 분석용 데이터베이스** 목록에서 AdventureWorks2017을 선택하고 **튜닝할 데이터베이스 및 테이블 선택** 그리드에서 AdventureWorks2017을 선택하고 **튜닝 로그 저장**을 선택합니다. **작업 분석용 데이터베이스** 는 작업 튜닝 시 데이터베이스 엔진 튜닝 관리자가 연결하는 첫 번째 데이터베이스를 지정합니다. 튜닝이 시작된 후 데이터베이스 엔진 튜닝 관리자는 작업에 포함된 `USE DATABASE` 문으로 지정한 데이터베이스에 연결합니다.  

  ![Db에 대 한 DTA 옵션](media/dta-tutorials/dta-select-db.png)
  
6.  **튜닝 옵션** 탭을 클릭합니다. 이 연습에서는 튜닝 옵션을 전혀 설정하지 않지만 잠시 기본 튜닝 옵션을 검토합니다. 이 탭 페이지에 대한 도움말을 보려면 F1 키를 누릅니다. 추가 튜닝 옵션을 보려면 **고급 옵션** 을 클릭합니다. **고급 튜닝 옵션** 대화 상자에서 표시된 튜닝 옵션에 대한 정보를 보려면 **도움말** 을 클릭합니다. 기본 옵션을 선택한 상태에서 **고급 튜닝 옵션** 대화 상자를 닫으려면 **취소** 를 클릭합니다.  

  ![DTA 튜닝 옵션](media/dta-tutorials/dta-tuning-options.png)
  
7.  도구 모음에서 **분석 시작** 단추를 클릭합니다. 데이터베이스 엔진 튜닝 관리자에서 작업을 분석하는 동안 **진행률** 탭에서 상태를 모니터링할 수 있습니다. 튜닝이 완료되면 **권장 구성** 탭이 표시됩니다.  
  
    튜닝 중지 날짜 및 시간에 대해 오류가 발생하면 주 **튜닝 옵션** 탭에서 **중지 시간** 을 확인합니다. **중지 시간** 날짜 및 시간이 현재 날짜 및 시간 이후인지 확인한 다음 필요한 경우 변경합니다.  

  ![DTA 분석 시작](media/dta-tutorials/dta-start-analysis.png)

  
8.  분석을 완료한 후 [!INCLUDE[tsql](../../includes/tsql-md.md)] 동작 **메뉴에서** 권장 구성 저장 **을 클릭하여** 스크립트로 권장 구성을 저장합니다. **다른 이름으로 저장** 대화 상자에서 권장 구성 스크립트를 저장할 디렉터리로 이동하고 파일 이름 **MyRecommendations**를 입력합니다.  

  ![DTA 권장 사항 저장](media/dta-tutorials/dta-save-recommendations.png)

## <a name="view-tuning-recommendations"></a>튜닝 권장 구성 보기
  
1.  **권장 구성** 탭에서 탭 페이지 맨 아래의 스크롤 막대를 사용하여 모든 **인덱스 권장 구성** 열을 볼 수 있습니다. 각 행은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자에서 권장하는 데이터베이스 개체(인덱스 또는 인덱싱된 뷰)가 삭제되는지 만들어지는지 나타냅니다. 맨 오른쪽 열로 스크롤하여 **정의**를 클릭합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자에 해당 행에서 데이터베이스 개체를 만들거나 삭제하는 **스크립트를 볼 수 있는** SQL 스크립트 미리 보기 [!INCLUDE[tsql](../../includes/tsql-md.md)] 창이 표시됩니다. **닫기** 를 클릭하여 미리 보기 창을 닫습니다.  
  
    링크를 포함하는 **정의** 를 찾기 힘든 경우 탭 페이지 맨 아래에 있는 **기존 개체 표시** 확인란의 선택을 취소합니다. 그러면 표시되는 행 수가 줄어듭니다. 이 확인란의 선택을 취소하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자에서 권장 구성을 생성한 개체만 표시합니다. 현재 **데이터베이스에 있는 모든 데이터베이스 개체를 보려면** 기존 개체 표시 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 확인란을 선택합니다. 탭 페이지 오른쪽의 스크롤 막대를 사용하여 모든 개체를 볼 수 있습니다.

  ![DTA 인덱스 권장 사항](media/dta-tutorials/dta-recommendation.png)  
  
2.  **인덱스 권장 구성** 창의 표를 마우스 오른쪽 단추로 클릭합니다. 바로 가기 메뉴에서 권장 구성을 선택하거나 권장 구성의 선택을 취소할 수 있습니다. 표 텍스트의 글꼴을 변경할 수도 있습니다.  
 
   ![인덱스 권장 사항에 대 한 선택 메뉴](media/dta-tutorials/dta-index-recommendation-options.png)
  
3.  **동작** 메뉴에서 **권장 구성 저장** 을 클릭하여 모든 권장 구성을 하나의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트에 저장합니다. 스크립트 이름을 **MySessionRecommendations.sql**로 지정합니다.  
  
    [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 의 쿼리 편집기에서 MySessionRecommendations.sql 스크립트를 열어 봅니다. 쿼리 편집기에서 스크립트를 실행하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스에 권장 구성을 적용할 수 있지만 이렇게 하지 마십시오. 쿼리 편집기에서 스크립트를 실행하지 않고 닫습니다.  
  
    또는 **튜닝 관리자의** 동작 **메뉴에서** 권장 구성 적용 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 클릭하여 권장 구성을 적용할 수도 있지만 이 연습에서는 이러한 권장 구성을 지금 적용하지 마세요.  
  
4.  **권장 구성** 탭에 권장 구성이 2개 이상 있는 경우 **인덱스 권장 구성** 표에서 데이터베이스 개체를 나열하는 행의 일부를 지웁니다.  
  
5.  **동작** 메뉴에서 **권장 구성 평가**를 클릭합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자에서 MySession의 원래 권장 구성의 하위 집합을 평가할 수 있는 새 튜닝 세션이 만들어집니다.  
  
6.  새 **세션 이름** 으로 **EvaluateMySession**을 입력하고 도구 모음에서 **분석 시작** 단추를 클릭합니다. 이 새 튜닝 세션에 대해 2단계와 3단계를 반복하여 해당 권장 구성을 볼 수 있습니다.  
  
### <a name="summary"></a>요약  
튜닝 권장 구성의 하위 집합 평가는 세션 실행 후 튜닝 옵션을 변경해야 할 경우에 필요할 수 있습니다. 예를 들어 세션에 대한 튜닝 옵션을 지정할 때 인덱싱된 뷰를 고려하도록 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자에 요청했지만 권장 구성이 생성된 후 인덱싱된 뷰를 사용하지 않도록 결정하는 경우를 가정해 봅니다. 이 경우 **동작** 메뉴의 **권장 구성 평가** 옵션을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자에서 인덱싱된 뷰를 고려하지 않고 세션을 다시 평가하도록 할 수 있습니다. **권장 구성 평가** 옵션을 사용하면 이전에 생성된 권장 구성이 현재 물리적 디자인에 가상으로 적용되어 두 번째 튜닝 세션의 물리적 디자인에 전달됩니다.  
  
추가 튜닝 결과 정보는 이 단원의 다음 태스크에 설명된 **보고서** 탭에서 볼 수 있습니다.  

## <a name="view-tuning-reports"></a>튜닝 보고서 보기
튜닝 결과를 구현하는 데 사용할 수 있는 스크립트를 보면 도움이 되지만 데이터베이스 엔진 튜닝 관리자에서 제공하는 여러 가지 보고서를 보아도 유용합니다. 이러한 보고서는 튜닝하고 있는 데이터베이스의 기존 물리적 디자인 구조와 권장 구조에 대한 정보를 제공합니다. 튜닝 보고서는 다음 연습에서 설명하는 대로 **보고서** 탭을 클릭하여 볼 수 있습니다.


1. 데이터베이스 튜닝 관리자에서 **보고서** 탭을 선택 합니다. 
2. **튜닝 요약** 창에서 이 튜닝 세션에 대한 정보를 볼 수 있습니다. 스크롤 막대를 사용하여 모든 창 내용을 볼 수 있습니다. **예상 향상률** 과 **권장 구성이 사용하는 공간**을 확인합니다. 튜닝 옵션을 설정할 때 권장 구성이 사용하는 공간을 제한할 수 있습니다. **튜닝 옵션** 탭에서 **고급 옵션**을 선택합니다. **권장 구성에 필요한 최대 공간 정의**를 선택하고 권장 구성이 사용할 수 있는 최대 공간(MB)을 지정합니다. 도움말 브라우저의 **뒤로** 단추를 사용하여 이 자습서로 돌아올 수 있습니다. 

    ![DTA 튜닝 요약](media/dta-tutorials/dta-tuning-summary.png)
  
3.  **튜닝 보고서** 창의 **보고서 선택** 목록에서 **문 비용 보고서** 를 클릭합니다. 보고서를 표시할 공간이 더 필요한 경우 **세션 모니터** 창 테두리를 왼쪽으로 끕니다. 데이터베이스의 테이블에 대해 실행되는 각 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에는 성능 비용이 연결되어 있습니다. 테이블에서 자주 액세스되는 열에 효율적인 인덱스를 만들어 이 성능 비용을 줄일 수 있습니다. 이 보고서에는 작업에서 문을 실행한 경우의 원래 비용과 튜닝 권장 구성이 구현된 경우의 비용 간에 예상되는 향상률이 표시됩니다. 보고서에 포함된 정보의 양은 작업의 길이와 복잡성을 기반으로 합니다.  

    ![DTA 보고서-문 비용](media/dta-tutorials/dta-statement-cost.png)
  
4.  표 영역에서 **문 비용 보고서** 창을 마우스 오른쪽 단추로 클릭하고 **파일로 내보내기**를 클릭합니다. **MyReport**라는 이름으로 보고서를 저장합니다. 파일 이름에 .xml 확장명이 자동으로 추가됩니다. 즐겨 사용하는 XML 편집기나 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 MyReport.xml을 열어 보고서 내용을 볼 수 있습니다.  
  
5.  데이터베이스 엔진 튜닝 관리자의 **보고서** 탭으로 돌아가서 **문 비용 보고서** 를 마우스 오른쪽 단추로 다시 클릭합니다. 사용 가능한 다른 옵션을 검토합니다. 보고 있는 보고서의 글꼴을 변경할 수 있습니다. 여기에서 글꼴을 변경하면 다른 탭 페이지에서도 변경됩니다.  
  
6.  **보고서 선택** 목록에서 다른 보고서를 클릭하여 보고서에 익숙해집니다.  
  
### <a name="summary"></a>요약  
이제 MySession 튜닝 세션에 대한 데이터베이스 엔진 튜닝 관리자 GUI의 **보고서** 탭을 탐색했습니다. 이와 같은 단계를 사용하여 EvaluateMySession 튜닝 세션에 대해 생성된 보고서를 탐색할 수 있습니다. **세션 모니터** 창에서 **EvaluateMySession** 을 두 번 클릭하여 시작합니다.  


 ## <a name="next-lesson"></a>다음 단원  
[3단원: DTA 명령 프롬프트 유틸리티 사용](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
   
  
  
