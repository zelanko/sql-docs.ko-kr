---
title: '8단원: 데이터 필터 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 19ccbdba-e3da-40a4-b652-32c628cf32e5
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d5004ad7cb8283be11d7e89f96ee46bd29ccccd6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189923"
---
# <a name="lesson-8-create-a-data-filter"></a>8단원: 데이터 필터 만들기
  부모 보고서에 드릴스루 동작을 추가한 후에는 자식 보고서에 대해 정의한 데이터 테이블에 대한 데이터 필터를 만듭니다.  
  
 드릴스루 보고서에 대한 테이블 기반 필터 **또는** 쿼리 필터를 만들 수 있습니다. 이 단원에서는 두 옵션에 대한 지침을 제공합니다.  
  
## <a name="table-based-filter"></a>테이블 기반 필터  
 테이블 기반 필터를 구현하려면 다음 태스크를 완료해야 합니다.  
  
-   자식 보고서의 테이블릭스에 필터 식을 추가합니다.  
  
-   `PurchaseOrderDetail` 테이블에서 필터링되지 않은 데이터를 선택하는 함수를 만듭니다.  
  
-   자식 보고서에 `PurchaseOrderDetail` DataTable을 바인딩하는 이벤트 처리기를 추가합니다.  
  
#### <a name="to-add-a-filter-expression-to-the-tablix-in-the-child-report"></a>자식 보고서의 테이블릭스에 필터 식을 추가하려면  
  
1.  자식 보고서를 엽니다.  
  
2.  테이블 릭 스에서 열 머리글을 선택, 열 머리글 위에 표시 된 회색 셀을 마우스 오른쪽 단추로 클릭 하 고, 클릭 **테이블 릭 스 속성**합니다.  
  
3.  클릭 합니다 **필터** 페이지를 선택한 다음 클릭 **추가**합니다.  
  
4.  에 **식을** 제출 클릭 `ProductID` 드롭 다운 목록에서. 이는 필터를 적용할 열입니다.  
  
5.  등호를 클릭 합니다. (**=**) 연산자를 **연산자** 드롭 다운 목록.  
  
6.  옆의 식 단추를 클릭 합니다 **값** 필드를 클릭 **매개 변수** 에 **범주** 영역에서 마우스 두 번 클릭 `productid` 에  **값** 영역입니다. 이제 **다음에 대한 식 설정: 값** 필드에 **=Parameters!productid.Value**와 비슷한 식이 포함됩니다.  
  
7.  클릭 **확인** 하 고 **확인** 다시 합니다 **테이블 릭 스 속성** 대화 상자.  
  
8.  .rdlc 파일을 저장합니다.  
  
#### <a name="to-create-a-function-that-selects-unfiltered-data-from-the-purchaseordedetail-table"></a>PurchaseOrdeDetail 테이블에서 필터링되지 않은 데이터를 선택하는 함수를 만들려면  
  
1.  솔루션 탐색기에서 Default.aspx를 확장하고 Default.aspx.cs를 두 번 클릭합니다.  
  
2.  정수 형식의 `productid` 매개 변수를 허용하고 `datatable` 개체를 반환하고 다음을 수행하는 새 함수를 만듭니다.  
  
    1.  데이터 집합의 인스턴스를 만듭니다 `DataSet2`의 2 단계에서에서 만든 [4 단원: 자식 보고서에 대 한 데이터 연결 및 데이터 테이블 정의](lesson-4-define-a-data-connection-and-data-table-for-child-report.md)합니다.  
  
    2.  SqlServer 데이터베이스에 대한 연결을 만들어 **4단원: 자식 보고서에 대한 데이터 연결 및 데이터 테이블 정의**에서 정의된 쿼리를 실행합니다.  
  
    3.  쿼리는 필터링되지 않은 데이터를 반환합니다.  
  
    4.  쿼리를 실행하여 필터링되지 않은 데이터로 DataSet 인스턴스를 채웁니다.  
  
    5.  `PurchaseOrderDetail` DataTable을 반환합니다.  
  
         함수는 아래와 비슷하며 이는 단순히 참조용입니다. 원하는 패턴을 따라 자식 보고서에 필요한 데이터를 인출할 수 있습니다.  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table, fetch the  
            /// unfiltered data and bind it with the Child report  
            /// </summary>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail()  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlDataAdapter adap = new SqlDataAdapter("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail ", sqlconn);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
#### <a name="to-add-an-event-handler-that-binds-the-purchaseorderdetail-datatable-to-the-child-report"></a>자식 보고서에 PurchaseOrderDetail DataTable을 바인딩하는 이벤트 처리기를 추가하려면  
  
1.  Default.aspx를 엽니다.  
  
2.  ReportViewer 컨트롤을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성입니다.**  
  
3.  에 **속성** 페이지를 클릭 합니다 **이벤트** 아이콘입니다.  
  
4.  두 번 클릭 합니다 **드릴스루** 이벤트입니다.  
  
     그러면 코드에 아래 블록과 비슷한 이벤트 처리기 섹션이 추가됩니다.  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  이벤트 처리기를 완성합니다. 이벤트 처리기에는 다음 기능이 포함되어 있어야 합니다.  
  
    1.  *DrillthroughEventArgs* 매개 변수에서 자식 보고서 개체 참조를 인출합니다.  
  
    2.  함수를 호출 합니다. `GetPurchaseOrderDetail`  
  
    3.  `PurchaseOrderDetail` DataTable을 보고서의 해당 데이터 원본과 바인딩합니다.  
  
         완성된 이벤트 처리기 코드는 다음과 비슷합니다.  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                     //Get the instance of the Target report, in our case the JumpReport.rdlc.  
                    LocalReport report = (LocalReport)e.Report;  
  
                     //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail()));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  파일을 저장합니다.  
  
## <a name="query-filter"></a>쿼리 필터  
 쿼리 필터를 구현하려면 다음 태스크를 완료해야 합니다.  
  
-   `PurchaseOrderDetail` 테이블에서 필터링된 데이터를 선택하는 함수를 만듭니다.  
  
-   매개 변수 값을 검색하고 자식 보고서에 `PurchaseOrdeDetail` DataTable을 바인딩하는 이벤트 처리기를 추가합니다.  
  
#### <a name="to-create-a-function-that-selects-filtered-data-from-the-purchaseorderdetail-table"></a>PurchaseOrderDetail 테이블에서 필터링된 데이터를 선택하는 함수를 만들려면  
  
1.  솔루션 탐색기에서 Default.aspx를 확장하고 Default.aspx.cs를 두 번 클릭합니다.  
  
2.  정수 형식의 `productid` 매개 변수를 허용하고 `datatable` 개체를 반환하고 다음을 수행하는 새 함수를 만듭니다.  
  
    1.  데이터 집합의 인스턴스를 만듭니다 `DataSet2`의 2 단계에서에서 만든 [4 단원: 자식 보고서에 대 한 데이터 연결 및 데이터 테이블 정의](lesson-4-define-a-data-connection-and-data-table-for-child-report.md)합니다.  
  
    2.  SqlServer 데이터베이스에 대한 연결을 만들어 **4단원: 자식 보고서에 대한 데이터 연결 및 데이터 테이블 정의**에서 정의된 쿼리를 실행합니다.  
  
    3.  쿼리에는 반환된 데이터가 부모 보고서에서 선택한 `productid`를 기반으로 필터링되어 있는지 확인하는 `ProductID` 매개 변수가 포함됩니다.  
  
    4.  쿼리를 실행하여 필터링된 데이터로 DataSet 인스턴스를 채웁니다.  
  
    5.  `PurchaseOrderDetail` DataTable을 반환합니다.  
  
         함수는 아래와 비슷하며 이는 단순히 참조용입니다. 원하는 패턴을 따라 자식 보고서에 필요한 데이터를 인출할 수 있습니다.  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table and filter the  
            /// data for a specific ProductID selected in the Parent report.  
            /// </summary>  
            /// <param name="productid">Parameter passed from the Parent report to filter data.</param>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail(int productid)  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlDataAdapter adap = new SqlDataAdapter("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail where ProductID = " + productid, sqlconn);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
#### <a name="to-add-an-event-handler-that-retrieves-parameter-values-and-binds-the-purchaseordedetail-datatable-to-the-child-report"></a>매개 변수 값을 검색하고 자식 보고서에 PurchaseOrdeDetail DataTable을 바인딩하는 이벤트 처리기를 추가하려면  
  
1.  Default.aspx를 엽니다.  
  
2.  ReportViewer 컨트롤을 마우스 오른쪽 단추로 누른 **속성**합니다.  
  
3.  에 **속성** 창 클릭 합니다 **이벤트** 아이콘입니다.  
  
4.  두 번 클릭 합니다 **드릴스루** 이벤트입니다.  
  
     그러면 코드에 다음과 비슷한 이벤트 처리기 섹션이 추가됩니다.  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  이벤트 처리기를 완성합니다. 이벤트 처리기에는 다음 기능이 포함되어 있어야 합니다.  
  
    1.  *DrillthroughEventArgs* 매개 변수에서 자식 보고서 개체 참조를 인출합니다.  
  
    2.  인출한 자식 보고서 개체에서 자식 보고서 매개 변수 목록을 가져옵니다.  
  
    3.  매개 변수 컬렉션을 반복 처리하고 부모 보고서에서 전달되는 `ProductID` 매개 변수 값을 검색합니다.  
  
    4.  `GetPurchaseOrderDetail` 함수를 호출하고 `ProductID` 매개 변수 값을 전달합니다.  
  
    5.  `PurchaseOrderDetail` DataTable을 보고서의 해당 데이터 원본과 바인딩합니다.  
  
         완성된 이벤트 처리기 코드는 다음과 비슷합니다.  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                    //Variable to store the parameter value passed from the MainReport.  
                    int productid = 0;  
  
                    //Get the instance of the Target report, in our case the JumpReport.rdlc.  
                    LocalReport report = (LocalReport)e.Report;  
  
                    //Get all the parameters passed from the main report to the target report.  
                    //OriginalParametersToDrillthrough actually returns a Generic list of   
                    //type ReportParameter.  
                    IList<ReportParameter> list = report.OriginalParametersToDrillthrough;  
  
                    //Parse through each parameters to fetch the values passed along with them.  
                    foreach (ReportParameter param in list)  
                    {  
                        //Since we know the report has only one parameter and it is not a multivalued,   
                        //we can directly fetch the first value from the Values array.  
                        productid = Convert.ToInt32(param.Values[0].ToString());  
                    }  
  
                    //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail(productid)));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  파일을 저장합니다.  
  
## <a name="next-task"></a>다음 태스크  
 자식 보고서에 대해 정의한 데이터 테이블에 대한 데이터 필터를 성공적으로 만들었습니다. 이제 웹 사이트 애플리케이션을 빌드하고 실행합니다.  
  
  
