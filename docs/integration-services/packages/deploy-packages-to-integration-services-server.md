---
title: "Integration Services 서버에 패키지 배포 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c26ce7f4-7b34-4c9a-8649-ba767d30c827
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Integration Services 서버에 패키지 배포
  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 에 도입된 증분 패키지 배포 기능을 사용하면 전체 프로젝트를 배포하지 않고 기존 프로젝트나 새 프로젝트에 하나 이상의 패키지를 배포할 수 있습니다.  
  
##  <a name="DeployWizard"></a> Integration Services 배포 마법사를 사용하여 패키지 배포  
  
1.  명령 프롬프트의 **%ProgramFiles%\Microsoft SQL Server\130\DTS\Binn**에서 **isdeploymentwizard.exe**를 실행합니다. 64비트 컴퓨터의 **%ProgramFiles(x86)%\Microsoft SQL Server\130\DTS\Binn**에는 도구의 32비트 버전도 있습니다.  
  
2.  **원본 선택** 페이지에서 **패키지 배포 모델**로 전환합니다. 그런 다음 원본 패키지가 포함된 폴더를 선택하고 패키지를 구성합니다.  
  
3.  마법사를 완료합니다. [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel)에서 설명하는 나머지 단계를 수행합니다.  
  
##  <a name="SSMS"></a> SQL Server Management Studio를 사용하여 패키지 배포  
  
1.  SQL Server Management Studio의 개체 탐색기에서 **Integration Services 카탈로그** > **SSISDB** 노드를 확장합니다.  
  
2.  **프로젝트** 폴더를 마우스 오른쪽 단추로 클릭하고 **프로젝트 배포**를 클릭합니다.  
  
3.  **소개** 페이지가 표시되면 **다음** 을 클릭하여 계속합니다.  
  
4.  **원본 선택** 페이지에서 **패키지 배포 모델**로 전환합니다. 그런 다음 원본 패키지가 포함된 폴더를 선택하고 패키지를 구성합니다.  
  
5.  마법사를 완료합니다. [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel)에서 설명하는 나머지 단계를 수행합니다.  
  
##  <a name="SSDT"></a> SQL Server Data Tools(Visual Studio)를 사용하여 패키지 배포  
  
1.  Visual Studio에서 Integration Services 프로젝트를 연 상태로 배포할 패키지를 하나 이상 선택합니다.  
  
2.  마우스 오른쪽 단추를 클릭하고 **패키지 배포**를 선택합니다. 선택한 패키지가 원본 패키지로 구성된 상태로 배포 마법사가 열립니다.  
  
3.  마법사를 완료합니다. [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel)에서 설명하는 나머지 단계를 수행합니다.  
  
##  <a name="StoredProcedure"></a> deploy_packages 저장 프로시저를 사용하여 패키지 배포  
 **[catalog].[deploy_packages]** 저장 프로시저를 사용하여 SSIS 카탈로그에 SSIS 패키지를 하나 이상 배포할 수 있습니다. 다음 코드 예제에서는 이 저장 프로시저를 사용하여 SSIS 서버에 패키지를 배포하는 방법을 보여 줍니다. 자세한 내용은 [catalog.deploy_packages](../../integration-services/system-stored-procedures/catalog-deploy-packages.md)를 참조하세요.  
  
```  
  
private static void Main(string[] args)  
{  
    // Connection string to SSISDB  
    var connectionString = "Data Source=.;Initial Catalog=SSISDB;Integrated Security=True;MultipleActiveResultSets=false";  
  
    using (var sqlConnection = new SqlConnection(connectionString))  
    {  
        sqlConnection.Open();  
  
        var sqlCommand = new SqlCommand  
        {  
            Connection = sqlConnection,  
            CommandType = CommandType.StoredProcedure,  
            CommandText = "[catalog].[deploy_packages]"  
        };  
  
        var packageData = Encoding.UTF8.GetBytes(File.ReadAllText(@"C:\Test\Package.dtsx"));  
  
        // DataTable: name is the package name without extension and package_data is byte array of package.  
        var packageTable = new DataTable();  
        packageTable.Columns.Add("name", typeof(string));  
        packageTable.Columns.Add("package_data", typeof(byte[]));  
        packageTable.Rows.Add("Package", packageData);  
  
        // Set the destination project and folder which is named Folder and Project.  
        sqlCommand.Parameters.Add(new SqlParameter("@folder_name", SqlDbType.NVarChar, ParameterDirection.Input, "Folder", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@project_name", SqlDbType.NVarChar, ParameterDirection.Input, "Project", -1));  
        sqlCommand.Parameters.Add(new SqlParameter("@packages_table", SqlDbType.Structured, ParameterDirection.Input, packageTable, -1));  
  
        var result = sqlCommand.Parameters.Add("RetVal", SqlDbType.Int);  
        result.Direction = ParameterDirection.ReturnValue;  
  
        sqlCommand.ExecuteNonQuery();  
    }  
}  
  
```  
  
##  <a name="MOMApi"></a> 관리 개체 모델 API를 사용하여 패키지 배포  
 다음 코드 예제에서는 관리 개체 모델 API를 사용하여 서버에 패키지를 배포하는 방법을 보여 줍니다.  
  
```  
  
static void Main()  
 {  
     // Before deploying packages, make sure the destination project exists in SSISDB.  
     var connectionString = "Data Source=.;Integrated Security=True;MultipleActiveResultSets=false";  
     var catalogName = "SSISDB";  
     var folderName = "Folder";  
     var projectName = "Project";  
  
     // Get the folder instance.  
     var sqlConnection = new SqlConnection(connectionString);  
     var store = new Microsoft.SqlServer.Management.IntegrationServices.IntegrationServices(sqlConnection);  
     var folder = store.Catalogs[catalogName].Folders[folderName];  
  
     // Key is package name without extension and value is package binaries.  
     var packageDict = new Dictionary<string, string>();  
  
     var packageData = File.ReadAllText(@"C:\Folder\Package.dtsx");  
     packageDict.Add("Package", packageData);  
  
     // Deploy package to the destination project.  
     folder.DeployPackages(projectName, packageDict);  
 }  
  
```  
  
  