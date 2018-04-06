---
title: WinForms ReportViewer 컨트롤 사용 | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: ''
ms.component: application-integration
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ReportViewer controls
ms.assetid: 29fb9f7d-ba65-49fd-9cbc-4c380869de96
caps.latest.revision: 28
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Active
ms.openlocfilehash: 70933dbcd48c06d74879845679d817b9890a926b
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="using-the-winforms-reportviewer-control"></a>WinForms ReportViewer 컨트롤 사용
  보고서 서버에 배포된 보고서 또는 로컬 파일 시스템에 있는 보고서를 보려면 WinForms ReportViewer 컨트롤을 사용하여 Windows 응용 프로그램에서 렌더링할 수 있습니다.  
  
## <a name="to-add-the-reportviewer-control-to-a-windows-application"></a>ReportViewer 컨트롤을 Windows 응용 프로그램에 추가하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]을 사용하여 새 Windows 응용 프로그램을 만듭니다.  
  
     \- 또는 -  
  
     기존 Windows 응용 프로그램 프로젝트를 열고 새 폼을 추가합니다.  
  
2.  **도구 상자**에서 ReportViewer 컨트롤을 찾습니다. **도구 상자**가 보이지 않을 경우 **보기** 메뉴에서 **도구 상자**를 선택하여 액세스할 수 있습니다.  
  
     ![ReportViewer 컨트롤 선택](../../reporting-services/application-integration/media/windowsapp-toolboxreportviewer.png "ReportViewer 컨트롤 선택")  
  
3.  ReportViewer 컨트롤을 Windows Form의 디자인 화면으로 끌어 놓습니다.  
  
     이름이 reportViewer1인 ReportViewer 컨트롤이 폼에 추가됩니다.  
  
 컨트롤이 폼에 추가되면 **ReportViewer 태스크** 스마트 태그가 나타나 보고서를 선택하도록 알립니다.  
  
 보려는 보고서가 보고서 서버에 배포된 경우 **보고서 선택** 드롭다운 목록에서 **\<서버 보고서>** 옵션을 선택합니다. **\<서버 보고서>** 옵션이 선택되면 **보고서 서버 URL** 및 **보고서 경로**의 두 가지 속성이 추가로 나타납니다. **보고서 서버 URL**은 보고서 서버에 대한 주소이고 **보고서 경로**는 렌더링할 보고서의 전체 경로입니다.  
  
 ![서버 보고서 선택](../../reporting-services/application-integration/media/windowsapp-serverreportsettings.png "서버 보고서 선택")  
  
 로컬 모드로 보고서를 보려는 경우 **새 보고서 디자인** 옵션을 선택하여 보고서 디자이너를 시작하거나 기존 프로젝트에 속한 보고서를 선택합니다.  
  
 ![로컬 보고서 선택](../../reporting-services/application-integration/media/windowsapp-localreportsettings.png "로컬 보고서 선택")  
  
## <a name="viewing-reports-in-remote-processing-mode"></a>원격 처리 모드로 보고서 보기  
 다음 예는 WinForms ReportViewer 컨트롤을 사용하여 보고서 서버에 배포된 보고서를 렌더링하는 방법을 보여 줍니다. 이 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 보고서 프로젝트에 포함된 Sales Order Detail 보고서를 사용합니다.  
 
**C#**
```csharp  
public partial class Form1 : Form  
{  
    private void Form1_Load(object sender, EventArgs e)  
    {  
        // Set the processing mode for the ReportViewer to Remote  
        reportViewer1.ProcessingMode = ProcessingMode.Remote;  
  
        ServerReport serverReport = reportViewer1.ServerReport;  
  
        // Get a reference to the default credentials  
        System.Net.ICredentials credentials =  
            System.Net.CredentialCache.DefaultCredentials;  
  
        // Get a reference to the report server credentials  
        ReportServerCredentials rsCredentials =  
            serverReport.ReportServerCredentials;  
  
        // Set the credentials for the server report  
        rsCredentials.NetworkCredentials = credentials;  
  
        // Set the report server URL and report path  
        serverReport.ReportServerUrl =   
            new Uri("http:// <Server Name>/reportserver");  
        serverReport.ReportPath =   
            "/AdventureWorks Sample Reports/Sales Order Detail";  
  
        // Create the sales order number report parameter  
        ReportParameter salesOrderNumber = new ReportParameter();  
        salesOrderNumber.Name = "SalesOrderNumber";  
        salesOrderNumber.Values.Add("SO43661");  
  
        // Set the report parameters for the report  
        reportViewer1.ServerReport.SetParameters(  
            new ReportParameter[] { salesOrderNumber });  
  
        // Refresh the report  
        reportViewer1.RefreshReport();  
    }  
}  
```  
**VB.NET**
```vb  
Imports Microsoft.Reporting.WinForms  
  
Public Class Form1  
  
    Private Sub Form1_Load(ByVal sender As System.Object, _  
                           ByVal e As System.EventArgs) _  
                           Handles MyBase.Load  
  
        'Set the processing mode for the ReportViewer to Remote  
        reportViewer1.ProcessingMode = ProcessingMode.Remote  
  
        Dim serverReport As ServerReport  
        serverReport = reportViewer1.ServerReport  
  
        'Get a reference to the default credentials  
        Dim credentials As System.Net.ICredentials  
        credentials = System.Net.CredentialCache.DefaultCredentials  
  
        'Get a reference to the report server credentials  
        Dim rsCredentials As ReportServerCredentials  
        rsCredentials = serverReport.ReportServerCredentials  
  
        'Set the credentials for the server report  
        rsCredentials.NetworkCredentials = credentials  
  
        'Set the report server URL and report path  
        serverReport.ReportServerUrl = _  
           New Uri("http://<Server Name>/reportserver")  
        serverReport.ReportPath = _  
           "/AdventureWorks Sample Reports/Sales Order Detail"  
  
        'Create the sales order number report parameter  
        Dim salesOrderNumber As New ReportParameter()  
        salesOrderNumber.Name = "SalesOrderNumber"  
        salesOrderNumber.Values.Add("SO43661")  
  
        'Set the report parameters for the report  
        Dim parameters() As ReportParameter = {salesOrderNumber}  
        serverReport.SetParameters(parameters)  
  
        'Refresh the report  
        reportViewer1.RefreshReport()  
    End Sub  
  
End Class  
```  
  
## <a name="viewing-reports-in-local-processing-mode"></a>로컬 처리 모드로 보고서 보기  
 다음 예는 Windows 응용 프로그램의 일부이고 보고서 서버에 배포되지 않은 보고서를 렌더링하는 방법을 보여 줍니다.  
  
### <a name="to-add-the-sales-order-detail-report-to-a-windows-application"></a>Sales Order Detail 보고서를 Windows 응용 프로그램에 추가하려면  
  
1.  보고서를 추가할 Windows 프로젝트를 엽니다.  
  
2.  **프로젝트** 메뉴에서 **기존 항목 추가**를 선택합니다.  
  
3.  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 보고서 샘플 프로젝트를 설치한 위치를 찾습니다.  
  
     보고서 샘플을 다운로드하려면 [AdventureWorks 2012 보고서 샘플](http://go.microsoft.com/fwlink/?LinkId=404153)(영문)로 이동합니다.  
  
4.  Sales Order Detail.rdl 파일을 선택하고 **추가** 단추를 클릭합니다.  
  
     이제 Sales Order Detail.rdl 파일이 프로젝트의 일부여야 합니다.  
  
     ![판매 주문 세부 정보 보고서](../../reporting-services/application-integration/media/windowsapp-salesorderdetailreport.png "판매 주문 세부 정보 보고서")  
  
5.  솔루션 탐색기에서 Sales Order Detail.rdl 파일을 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택합니다. 보고서 이름을 **Sales Order Detail.rdlc**로 바꾸고 ENTER 키를 누릅니다.  
  
     솔루션 탐색기가 보이지 않으면 **보기** 메뉴에서 **솔루션 탐색기**를 선택하여 열 수 있습니다.  
  
    > [!NOTE]  
    >  파일 확장명을 rdl에서 rdlc로 바꾸면 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvslong](../../includes/vsprvslong-md.md)]의 보고서 디자이너를 사용하여 보고서를 편집할 수 있습니다.  
  
6.  보고서 이름을 변경했으면 파일을 선택하고 속성 창을 찾습니다. **출력 디렉터리로 복사** 속성을 **변경된 내용만 복사**로 변경합니다.  
  
     ![출력에 복사 설정 구성](../../reporting-services/application-integration/media/windowsapp-copytooutputsetting.png "출력에 복사 설정 구성")  
  
     **속성** 창이 보이지 않으면 **보기** 메뉴에서 **속성 창**을 선택하여 열 수 있습니다.  
  
 다음 코드 예에서는 판매 주문 데이터에 대한 데이터 집합을 만든 다음 Sales Order Detail 보고서를 로컬 모드에서 렌더링합니다.  

**C#**
```csharp  
public partial class Form1 : Form  
{  
    private void Form1_Load(object sender, EventArgs e)  
    {  
        // Set the processing mode for the ReportViewer to Local  
        reportViewer1.ProcessingMode = ProcessingMode.Local;  
  
        LocalReport localReport = reportViewer1.LocalReport;  
  
        localReport.ReportPath = "Sales Order Detail.rdlc";  
  
        DataSet dataset = new DataSet("Sales Order Detail");  
  
        string salesOrderNumber = "SO43661";  
  
        // Get the sales order data  
        GetSalesOrderData(salesOrderNumber, ref dataset);  
  
        // Create a report data source for the sales order data  
        ReportDataSource dsSalesOrder = new ReportDataSource();  
        dsSalesOrder.Name = "SalesOrder";  
        dsSalesOrder.Value = dataset.Tables["SalesOrder"];  
  
        localReport.DataSources.Add(dsSalesOrder);  
  
        // Get the sales order detail data  
        GetSalesOrderDetailData(salesOrderNumber, ref dataset);  
  
        // Create a report data source for the sales order detail   
        // data  
        ReportDataSource dsSalesOrderDetail =  
            new ReportDataSource();  
        dsSalesOrderDetail.Name = "SalesOrderDetail";  
        dsSalesOrderDetail.Value =  
            dataset.Tables["SalesOrderDetail"];  
  
        localReport.DataSources.Add(dsSalesOrderDetail);  
  
        // Create a report parameter for the sales order number   
        ReportParameter rpSalesOrderNumber = new ReportParameter();  
        rpSalesOrderNumber.Name = "SalesOrderNumber";  
        rpSalesOrderNumber.Values.Add("SO43661");  
  
        // Set the report parameters for the report  
        localReport.SetParameters(  
            new ReportParameter[] { rpSalesOrderNumber });  
  
        // Refresh the report  
        reportViewer1.RefreshReport();  
    }  
  
    private void GetSalesOrderData(string salesOrderNumber,  
                                   ref DataSet dsSalesOrder)  
    {  
        string sqlSalesOrder =  
            "SELECT SOH.SalesOrderNumber, S.Name AS Store, " +  
            "       SOH.OrderDate, C.FirstName AS SalesFirstName, " +  
            "       C.LastName AS SalesLastName, E.Title AS " +  
            "       SalesTitle, SOH.PurchaseOrderNumber, " +  
            "       SM.Name AS ShipMethod, BA.AddressLine1 " +  
            "       AS BillAddress1, BA.AddressLine2 AS " +  
            "       BillAddress2, BA.City AS BillCity, " +  
            "       BA.PostalCode AS BillPostalCode, BSP.Name " +  
            "       AS BillStateProvince, BCR.Name AS " +  
            "       BillCountryRegion, SA.AddressLine1 AS " +  
            "       ShipAddress1, SA.AddressLine2 AS " +  
            "       ShipAddress2, SA.City AS ShipCity, " +  
            "       SA.PostalCode AS ShipPostalCode, SSP.Name " +  
            "       AS ShipStateProvince, SCR.Name AS " +  
            "       ShipCountryRegion, CC.Phone AS CustPhone, " +  
            "       CC.FirstName AS CustFirstName, CC.LastName " +  
            "       AS CustLastName " +  
            "FROM   Person.Address SA INNER JOIN " +  
            "       Person.StateProvince SSP ON " +  
            "       SA.StateProvinceID = SSP.StateProvinceID " +  
            "       INNER JOIN Person.CountryRegion SCR ON " +  
            "       SSP.CountryRegionCode = SCR.CountryRegionCode " +  
            "       RIGHT OUTER JOIN Sales.SalesOrderHeader SOH " +  
            "       LEFT OUTER JOIN  Person.Contact CC ON " +  
            "       SOH.ContactID = CC.ContactID LEFT OUTER JOIN" +  
            "       Person.Address BA INNER JOIN " +  
            "       Person.StateProvince BSP ON " +  
            "       BA.StateProvinceID = BSP.StateProvinceID " +  
            "       INNER JOIN Person.CountryRegion BCR ON " +  
            "       BSP.CountryRegionCode = " +  
            "       BCR.CountryRegionCode ON SOH.BillToAddressID " +  
            "       = BA.AddressID ON  SA.AddressID = " +  
            "       SOH.ShipToAddressID LEFT OUTER JOIN " +  
            "       Person.Contact C RIGHT OUTER JOIN " +  
            "       HumanResources.Employee E ON C.ContactID = " +  
            "       E.ContactID ON SOH.SalesPersonID = " +  
            "       E.EmployeeID LEFT OUTER JOIN " +  
            "       Purchasing.ShipMethod SM ON SOH.ShipMethodID " +  
            "       = SM.ShipMethodID LEFT OUTER JOIN Sales.Store" +  
            "        S ON SOH.CustomerID = S.CustomerID " +  
            "WHERE  (SOH.SalesOrderNumber = @SalesOrderNumber)";  
  
        SqlConnection connection = new  
            SqlConnection("Data Source=(local); " +  
                          "Initial Catalog=AdventureWorks; " +  
                          "Integrated Security=SSPI");  
  
        SqlCommand command =  
            new SqlCommand(sqlSalesOrder, connection);  
  
        command.Parameters.Add(  
            new SqlParameter("SalesOrderNumber",  
            salesOrderNumber));  
  
        SqlDataAdapter salesOrderAdapter = new  
            SqlDataAdapter(command);  
  
        salesOrderAdapter.Fill(dsSalesOrder, "SalesOrder");  
    }  
  
    private void GetSalesOrderDetailData(string salesOrderNumber,  
                           ref DataSet dsSalesOrder)  
    {  
        string sqlSalesOrderDetail =  
            "SELECT  SOD.SalesOrderDetailID, SOD.OrderQty, " +  
            "        SOD.UnitPrice, CASE WHEN " +  
            "        SOD.UnitPriceDiscount IS NULL THEN 0 " +  
            "        ELSE SOD.UnitPriceDiscount END AS " +  
            "        UnitPriceDiscount, SOD.LineTotal, " +  
            "        SOD.CarrierTrackingNumber, " +  
            "        SOD.SalesOrderID, P.Name, P.ProductNumber " +  
            "FROM    Sales.SalesOrderDetail SOD INNER JOIN " +  
            "        Production.Product P ON SOD.ProductID = " +  
            "        P.ProductID INNER JOIN " +  
            "        Sales.SalesOrderHeader SOH ON " +  
            "        SOD.SalesOrderID = SOH.SalesOrderID " +  
            "WHERE   (SOH.SalesOrderNumber = @SalesOrderNumber) " +  
            "ORDER BY SOD.SalesOrderDetailID";  
  
        using (SqlConnection connection = new  
            SqlConnection("Data Source=(local); " +  
                          "Initial Catalog=AdventureWorks; " +  
                          "Integrated Security=SSPI"))  
        {  
  
            SqlCommand command =  
                new SqlCommand(sqlSalesOrderDetail, connection);  
  
            command.Parameters.Add(  
                new SqlParameter("SalesOrderNumber",  
                salesOrderNumber));  
  
            SqlDataAdapter salesOrderDetailAdapter = new  
                SqlDataAdapter(command);  
  
            salesOrderDetailAdapter.Fill(dsSalesOrder,  
                "SalesOrderDetail");  
        }  
    }  
}  
```  
**VB.NET**
```vb  
Imports System.Data.SqlClient  
Imports Microsoft.Reporting.WinForms  
  
Public Class Form1  
  
    Private Sub Form1_Load(ByVal sender As System.Object, _  
                        ByVal e As System.EventArgs) _  
                        Handles MyBase.Load  
  
        'Set the processing mode for the ReportViewer to Local  
        reportViewer1.ProcessingMode = ProcessingMode.Local  
  
        Dim localReport As LocalReport  
        localReport = reportViewer1.LocalReport  
  
        localReport.ReportEmbeddedResource = _  
            "ReportViewerIntro.Sales Order Detail.rdlc"  
  
        Dim dataset As New DataSet("Sales Order Detail")  
  
        Dim salesOrderNumber As String = "SO43661"  
  
        'Get the sales order data  
        GetSalesOrderData(salesOrderNumber, dataset)  
  
        'Create a report data source for the sales order data  
        Dim dsSalesOrder As New ReportDataSource()  
        dsSalesOrder.Name = "SalesOrder"  
        dsSalesOrder.Value = dataset.Tables("SalesOrder")  
  
        localReport.DataSources.Add(dsSalesOrder)  
  
        'Get the sales order detail data  
        GetSalesOrderDetailData(salesOrderNumber, dataset)  
  
        'Create a report data source for the sales   
        'order detail data  
        Dim dsSalesOrderDetail As New ReportDataSource()  
        dsSalesOrderDetail.Name = "SalesOrderDetail"  
        dsSalesOrderDetail.Value = _  
            dataset.Tables("SalesOrderDetail")  
  
        localReport.DataSources.Add(dsSalesOrderDetail)  
  
        'Create a report parameter for the sales order number   
        Dim rpSalesOrderNumber As New ReportParameter()  
        rpSalesOrderNumber.Name = "SalesOrderNumber"  
        rpSalesOrderNumber.Values.Add("SO43661")  
  
        'Set the report parameters for the report  
        Dim parameters() As ReportParameter = {rpSalesOrderNumber}  
        localReport.SetParameters(parameters)  
  
        'Refresh the report  
        reportViewer1.RefreshReport()  
  
    End Sub  
  
    Private Sub GetSalesOrderData(ByVal salesOrderNumber As String, _  
                               ByRef dsSalesOrder As DataSet)  
  
        Dim sqlSalesOrder As String = _  
            "SELECT SOH.SalesOrderNumber, S.Name AS Store, " & _  
            "       SOH.OrderDate, C.FirstName AS SalesFirstName, " & _  
            "       C.LastName AS SalesLastName, E.Title AS " & _  
            "       SalesTitle, SOH.PurchaseOrderNumber, " & _  
            "       SM.Name AS ShipMethod, BA.AddressLine1 " & _  
            "       AS BillAddress1, BA.AddressLine2 AS " & _  
            "       BillAddress2, BA.City AS BillCity, " & _  
            "       BA.PostalCode AS BillPostalCode, BSP.Name " & _  
            "       AS BillStateProvince, BCR.Name AS " & _  
            "       BillCountryRegion, SA.AddressLine1 AS " & _  
            "       ShipAddress1, SA.AddressLine2 AS " & _  
            "       ShipAddress2, SA.City AS ShipCity, " & _  
            "       SA.PostalCode AS ShipPostalCode, SSP.Name " & _  
            "       AS ShipStateProvince, SCR.Name AS " & _  
            "       ShipCountryRegion, CC.Phone AS CustPhone, " & _  
            "       CC.FirstName AS CustFirstName, CC.LastName " & _  
            "       AS CustLastName " & _  
            "FROM   Person.Address SA INNER JOIN " & _  
            "       Person.StateProvince SSP ON " & _  
            "       SA.StateProvinceID = SSP.StateProvinceID " & _  
            "       INNER JOIN Person.CountryRegion SCR ON " & _  
            "       SSP.CountryRegionCode = SCR.CountryRegionCode " & _  
            "       RIGHT OUTER JOIN Sales.SalesOrderHeader SOH " & _  
            "       LEFT OUTER JOIN  Person.Contact CC ON " & _  
            "       SOH.ContactID = CC.ContactID LEFT OUTER JOIN" & _  
            "       Person.Address BA INNER JOIN " & _  
            "       Person.StateProvince BSP ON " & _  
            "       BA.StateProvinceID = BSP.StateProvinceID " & _  
            "       INNER JOIN Person.CountryRegion BCR ON " & _  
            "       BSP.CountryRegionCode = " & _  
            "       BCR.CountryRegionCode ON SOH.BillToAddressID " & _  
            "       = BA.AddressID ON  SA.AddressID = " & _  
            "       SOH.ShipToAddressID LEFT OUTER JOIN " & _  
            "       Person.Contact C RIGHT OUTER JOIN " & _  
            "       HumanResources.Employee E ON C.ContactID = " & _  
            "       E.ContactID ON SOH.SalesPersonID = " & _  
            "       E.EmployeeID LEFT OUTER JOIN " & _  
            "       Purchasing.ShipMethod SM ON SOH.ShipMethodID " & _  
            "       = SM.ShipMethodID LEFT OUTER JOIN Sales.Store" & _  
            "        S ON SOH.CustomerID = S.CustomerID " & _  
            "WHERE  (SOH.SalesOrderNumber = @SalesOrderNumber)"  
  
        Using connection As New SqlConnection( _  
                      "Data Source=(local); " & _  
                      "Initial Catalog=AdventureWorks; " & _  
                      "Integrated Security=SSPI")  
  
            Dim command As New SqlCommand(sqlSalesOrder, connection)  
  
            Dim parameter As New SqlParameter("SalesOrderNumber", _  
                salesOrderNumber)  
            command.Parameters.Add(parameter)  
  
            Dim salesOrderAdapter As New SqlDataAdapter(command)  
  
            salesOrderAdapter.Fill(dsSalesOrder, "SalesOrder")  
  
        End Using  
  
    End Sub  
  
    Private Sub GetSalesOrderDetailData( _  
                           ByVal salesOrderNumber As String, _  
                           ByRef dsSalesOrder As DataSet)  
  
        Dim sqlSalesOrderDetail As String = _  
            "SELECT  SOD.SalesOrderDetailID, SOD.OrderQty, " & _  
            "        SOD.UnitPrice, CASE WHEN " & _  
            "        SOD.UnitPriceDiscount IS NULL THEN 0 " & _  
            "        ELSE SOD.UnitPriceDiscount END AS " & _  
            "        UnitPriceDiscount, SOD.LineTotal, " & _  
            "        SOD.CarrierTrackingNumber, " & _  
            "        SOD.SalesOrderID, P.Name, P.ProductNumber " & _  
            "FROM    Sales.SalesOrderDetail SOD INNER JOIN " & _  
            "        Production.Product P ON SOD.ProductID = " & _  
            "        P.ProductID INNER JOIN " & _  
            "        Sales.SalesOrderHeader SOH ON " & _  
            "        SOD.SalesOrderID = SOH.SalesOrderID " & _  
            "WHERE   (SOH.SalesOrderNumber = @SalesOrderNumber) " & _  
            "ORDER BY SOD.SalesOrderDetailID"  
  
        Using connection As New SqlConnection( _  
                      "Data Source=(local); " & _  
                      "Initial Catalog=AdventureWorks; " & _  
                      "Integrated Security=SSPI")  
  
            Dim command As New SqlCommand(sqlSalesOrderDetail, _  
                                          connection)  
  
            Dim parameter As New SqlParameter("SalesOrderNumber", _  
                salesOrderNumber)  
            command.Parameters.Add(parameter)  
  
            Dim salesOrderDetailAdapter As New SqlDataAdapter(command)  
  
            salesOrderDetailAdapter.Fill(dsSalesOrder, _  
                "SalesOrderDetail")  
  
        End Using  
  
    End Sub  
  
End Class  
```  
  
## <a name="see-also"></a>참고 항목  
 [ReportViewer 컨트롤을 사용하여 Reporting Services 통합](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
  
  
