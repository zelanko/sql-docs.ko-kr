---
title: "8단원: 데이터 필터 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 19ccbdba-e3da-40a4-b652-32c628cf32e5
caps.latest.revision: "9"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 906e435e8259a1d32c84f322795001f8ea38c8a7
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="lesson-8-create-a-data-filter"></a>8단원: 데이터 필터 만들기
부모 보고서에 드릴스루 동작을 추가한 후에는 자식 보고서에 대해 정의한 데이터 테이블에 대한 데이터 필터를 만듭니다.  
  
드릴스루 보고서에 대한 테이블 기반 필터 **또는** 쿼리 필터를 만들 수 있습니다. 이 단원에서는 두 옵션에 대한 지침을 제공합니다.  
  
## <a name="table-based-filter"></a>테이블 기반 필터  
테이블 기반 필터를 구현하려면 다음 태스크를 완료해야 합니다.  
  
-   자식 보고서의 테이블릭스에 필터 식을 추가합니다.  
  
-   **PurchaseOrderDetail** 테이블에서 필터링되지 않은 데이터를 선택하는 함수를 만듭니다.  
  
-   자식 보고서에 **PurchaseOrderDetail DataTable** 을 바인딩하는 이벤트 처리기를 추가합니다.  
  
### <a name="to-add-a-filter-expression-to-the-tablix-in-the-child-report"></a>자식 보고서의 테이블릭스에 필터 식을 추가하려면  
  
1.  자식 보고서를 엽니다.  
  
2.  테이블릭스에서 열 제목을 선택하고 열 제목 위에 표시된 회색 셀을 마우스 오른쪽 단추로 클릭한 다음 **테이블릭스 속성**을 선택합니다.  
  
3.  **필터** 페이지를 선택한 다음 **추가**를 선택합니다.  
  
4.  **식** 필드의 드롭다운 목록에서 **ProductID** 를 선택합니다. 이는 필터를 적용할 열입니다.  
  
5.  **=**연산자 **드롭다운 목록에서 같음 연산자(** )를 선택합니다.  
  
6.  **값** 필드 옆의 식 단추를 선택하고 **범주** 영역에서 **매개 변수** 를 선택한 다음 **값** 영역에서 **productid** 를 두 번 클릭합니다. 이제 **다음에 대한 식 설정: 값** 필드에 **=Parameters!productid.Value**와 비슷한 식이 포함됩니다.  
  
7.  **확인** 을 선택하고 **테이블릭스 속성** 대화 상자에서 **확인** 을 다시 선택합니다.  
  
8.  .rdlc 파일을 저장합니다.  
  
### <a name="to-create-a-function-that-selects-unfiltered-data-from-the-purchaseordedetail-table"></a>PurchaseOrdeDetail 테이블에서 필터링되지 않은 데이터를 선택하는 함수를 만들려면  
  
1.  솔루션 탐색기에서 Default.aspx를 확장하고 Default.aspx.cs를 두 번 클릭합니다.  
  
2.  정수 형식의 **productid**매개 변수를 허용하며 **datatable** 개체를 반환하고 다음을 수행하는 새 함수를 만듭니다.  
  
    1.  **4단원: 자식 보고서에 대한 데이터 연결 및 데이터 테이블 정의**의 2단계에서 만든 데이터 집합 [DataSet2](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)인스턴스를 만듭니다.  
  
    2.  SqlServer 데이터베이스에 대한 연결을 만들어 **4단원: 자식 보고서에 대한 데이터 연결 및 데이터 테이블 정의**에서 정의된 쿼리를 실행합니다.  
  
    3.  쿼리는 필터링되지 않은 데이터를 반환합니다.  
  
    4.  쿼리를 실행하여 필터링되지 않은 데이터로 DataSet 인스턴스를 채웁니다.  
  
    5.  **PurchaseOrderDetail** DataTable을 반환합니다.  
  
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
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks2014;Integrated Security=SSPI"))  
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
  
### <a name="to-add-an-event-handler-that-binds-the-purchaseorderdetail-datatable-to-the-child-report"></a>자식 보고서에 PurchaseOrderDetail DataTable을 바인딩하는 이벤트 처리기를 추가하려면  
  
1.  디자이너 보기에서 Default.aspx를 엽니다.  
  
2.  ReportViewer 컨트롤을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
3.  **속성** 페이지에서 **이벤트** 아이콘을 선택합니다.  
  
4.  **드릴스루** 이벤트를 두 번 클릭합니다.  
  
    그러면 코드에 아래 블록과 비슷한 이벤트 처리기 섹션이 추가됩니다.  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  이벤트 처리기를 완성합니다. 이벤트 처리기에는 다음 기능이 포함되어 있어야 합니다.  
  
    1.  *DrillthroughEventArgs* 매개 변수에서 자식 보고서 개체 참조를 인출합니다.  
  
    2.  **GetPurchaseOrderDetail**함수를 호출합니다.  
  
    3.  **PurchaseOrderDetail** DataTable을 보고서의 해당 데이터 원본과 바인딩합니다.  
  
        완성된 이벤트 처리기 코드는 다음과 비슷합니다.  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                     //Get the instance of the Target report.  
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
  
-   **PurchaseOrderDetail** 테이블에서 필터링된 데이터를 선택하는 함수를 만듭니다.  
  
-   매개 변수 값을 검색하고 자식 보고서에 **PurchaseOrdeDetail DataTable** 을 바인딩하는 이벤트 처리기를 추가합니다.  
  
### <a name="to-create-a-function-that-selects-filtered-data-from-the-purchaseorderdetail-table"></a>PurchaseOrderDetail 테이블에서 필터링된 데이터를 선택하는 함수를 만들려면  
  
1.  솔루션 탐색기에서 Default.aspx를 확장하고 Default.aspx.cs를 두 번 클릭합니다.  
  
2.  정수 형식의 **productid**매개 변수를 허용하며 **datatable** 개체를 반환하고 다음을 수행하는 새 함수를 만듭니다.  
  
    1.  **4단원: 자식 보고서에 대한 데이터 연결 및 데이터 테이블 정의**의 2단계에서 만든 데이터 집합 [DataSet2](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)인스턴스를 만듭니다.  
  
    2.  SqlServer 데이터베이스에 대한 연결을 만들어 **4단원: 자식 보고서에 대한 데이터 연결 및 데이터 테이블 정의**에서 정의된 쿼리를 실행합니다.  
  
    3.  쿼리에는 반환된 데이터가 부모 보고서에서 선택한 **ProductID**를 기반으로 필터링되어 있는지 확인하는 **productid** 매개 변수가 포함됩니다.  
  
    4.  쿼리를 실행하여 필터링된 데이터로 DataSet 인스턴스를 채웁니다.  
  
    5.  **PurchaseOrderDetail** DataTable을 반환합니다.  
  
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
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks2014;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlCommand cmd = new SqlCommand("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail where ProductID = @ProductID", sqlconn);  
                  
                        // Sets the productid parameter.  
                        cmd.Parameters.Add((new SqlParameter("@ProductID", SqlDbType.Int)).Value = productid);  
  
                        SqlDataAdapter adap = new SqlDataAdapter(cmd);  
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
  
### <a name="to-add-an-event-handler-that-retrieves-parameter-values-and-binds-the-purchaseordedetail-datatable-to-the-child-report"></a>매개 변수 값을 검색하고 자식 보고서에 PurchaseOrdeDetail DataTable을 바인딩하는 이벤트 처리기를 추가하려면  
  
1.  디자이너 보기에서 Default.aspx를 엽니다.  
  
2.  ReportViewer 컨트롤을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
3.  **속성** 창에서 **이벤트** 아이콘을 선택합니다.  
  
4.  **드릴스루** 이벤트를 두 번 클릭합니다.  
  
    그러면 코드에 다음과 비슷한 이벤트 처리기 섹션이 추가됩니다.  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  이벤트 처리기를 완성합니다. 이벤트 처리기에는 다음 기능이 포함되어 있어야 합니다.  
  
    1.  *DrillthroughEventArgs* 매개 변수에서 자식 보고서 개체 참조를 인출합니다.  
  
    2.  인출한 자식 보고서 개체에서 자식 보고서 매개 변수 목록을 가져옵니다.  
  
    3.  매개 변수 컬렉션을 반복 처리하고 부모 보고서에서 전달되는 **ProductID**매개 변수 값을 검색합니다.  
  
    4.  **GetPurchaseOrderDetail**함수를 호출하고 **ProductID**매개 변수 값을 전달합니다.  
  
    5.  **PurchaseOrderDetail** DataTable을 보고서의 해당 데이터 원본과 바인딩합니다.  
  
        완성된 이벤트 처리기 코드는 다음과 비슷합니다.  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                    //Variable to store the parameter value passed from the MainReport.  
                    int productid = 0;  
  
                    //Get the instance of the Target report.  
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
자식 보고서에 대해 정의한 데이터 테이블에 대한 데이터 필터를 성공적으로 만들었습니다. 이제 웹 사이트 응용 프로그램을 빌드하고 실행합니다. [9단원: 응용 프로그램 빌드 및 실행](../reporting-services/lesson-9-build-and-run-the-application.md)을 참조하세요.  
  
  
  

