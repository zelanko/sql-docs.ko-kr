---
title: "4 단원: 자식 보고서에 대 한 데이터 연결 및 데이터 테이블 정의 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: a6aa2c56-227c-43c5-a28e-c7104131ac5e
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 214067875871c249aa56d0ed191f787a08b3ed7b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>4단원: 자식 보고서에 대한 데이터 연결 및 데이터 테이블 정의
부모 보고서를 디자인 한 후에는 자식 보고서에 대한 데이터 연결 및 데이터 테이블을 만듭니다. 이 자습서에서 데이터 연결은 AdventureWorks2014 데이터베이스에 대한 연결입니다.  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>DataSet을 추가하여 자식 보고서에 대한 데이터 연결 및 DataTable을 정의하려면  
  
1.  **웹 사이트** 메뉴에서 **새 항목 추가**를 선택합니다.  
  
2.  **새 항목 추가** 대화 상자에서 **DataSet** 을 선택한 다음 **추가**를 선택합니다. 메시지가 표시되면 **예** 를 선택하여 **App_Code**폴더에 항목을 추가해야 합니다.  
  
    그러면 프로젝트에 새 XSD 파일 **DataSet2.xsd** 가 추가되고 데이터 집합 디자이너가 열립니다.  
  
3.  도구 상자 창에서 **TableAdapter** 컨트롤을 디자인 화면으로 끌어옵니다. 그러면 **TableAdapter** 구성 마법사가 시작됩니다.  
  
4.  **데이터 연결 선택** 페이지에서, 2단원에서 만든 연결을 선택할 수 있습니다. 2단원에서 연결을 만든 경우 **다음** 을 선택하고 8단계로 이동합니다. 만들지 않은 경우 **새 연결**을 선택합니다.  
  
5.  **연결 추가** 대화 상자에서 다음 단계를 수행합니다.  
  
    1.  **서버 이름** 상자에 **AdventureWorks2014** 데이터베이스가 있는 서버를 입력합니다.  
  
        기본 SQL Server Express 인스턴스는 **(local)\sqlexpress**입니다.  
  
    2.  **서버에 로그온** 섹션에서 데이터에 액세스할 수 있는 옵션을 선택합니다. **Windows 인증 사용** 이 기본값입니다.  
  
    3.  **데이터베이스 이름 선택 또는 입력** 드롭다운 목록에서 **AdventureWorks2014**를 선택합니다.  
  
    4.  **확인**선택하고 **다음**을 선택합니다.  
  
6.  5단계 (b)에서 **SQL Server 인증 사용** 을 선택한 경우 문자열에 중요한 데이터를 포함할지 응용 프로그램 코드에 정보를 설정할지 여부에 대한 옵션을 선택합니다.  
  
7.  **응용 프로그램 구성 파일에 연결 문자열 저장** 페이지에서 연결 문자열의 이름을 입력하거나 기본값 **AdventureWorks2014ConnectionString**을 적용합니다. **다음**을 선택합니다.  
  
8.  **명령 유형을 선택하세요.** 페이지에서 **SQL 문 사용**을 선택하고 **다음**을 선택합니다.  
  
9. **SQL 문 입력** 페이지에서 다음 Transact-SQL 쿼리를 입력하여 **AdventureWorks2014** 데이터베이스에서 데이터를 검색하고 **다음**을 선택합니다.  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
    **쿼리 작성기**를 선택하여 쿼리를 만든 다음 **쿼리 실행** 단추를 선택하여 쿼리를 확인할 수도 있습니다. 쿼리에서 예상된 데이터가 반환되지 않는 경우 이전 버전의 AdventureWorks를 사용하고 있을 수 있습니다. **AdventureWorks2014** 샘플 데이터베이스를 가져오는 방법에 대한 자세한 내용은 [Microsoft SQL Server 데이터베이스 제품 샘플](http://msftdbprodsamples.codeplex.com/)을 참조하세요.  
  
10. **생성할 메서드 선택** 페이지에서 **업데이트를 데이터베이스로 직접 보내는 메서드 만들기(GenerateDBDirectMethods)**의 선택을 취소한 다음 **마침**을 선택합니다.  
  
    > [!WARNING]  
    > **업데이트를 데이터베이스로 직접 보내는 메서드 만들기(GenerateDBDirectMethods)**의 선택을 취소해야 합니다.  
  
    이제 ADO.NET [DataTable](http://msdn.microsoft.com/library/system.data.datatable.aspx) 을 보고서의 데이터 원본으로 구성하는 작업을 완료했습니다. Visual Studio의 데이터 집합 디자이너 페이지에서 추가한 **DataTable** 이 표시되며 쿼리에 지정한 열이 나열됩니다. DataSet2에는 PurhcaseOrderDetail 테이블에서 쿼리를 기반으로 하는 데이터가 포함됩니다.  
  
11. 파일을 저장합니다.  
  
12. 데이터를 미리 보려면 **데이터** 메뉴에서 **데이터 미리 보기** 를 선택한 다음 **미리 보기**를 선택합니다.  
  
## <a name="next-task"></a>다음 태스크  
자식 보고서에 대한 데이터 연결 및 데이터 테이블을 성공적으로 만들었습니다. 이제 보고서 마법사를 사용하여 자식 보고서를 디자인합니다. [5단원: 보고서 마법사를 사용하여 자식 보고서 디자인](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)을 참조하세요.  
  


