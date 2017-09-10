---
title: "테이블 형식 모델에 테이블, 파티션 및 열 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: cf0e4791-ad3b-41a8-81ce-509d4cf223f8
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 42d7a07de0c82921f08fd091f72aef125ebe053e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-tables-partitions-and-columns-in-a-tabular-model"></a>테이블 형식 모델에 테이블, 파티션 및 열 만들기

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

테이블 형식 모델 테이블의 행과 열 구성 됩니다. 행은 증분 데이터 새로 고침을 지원 하기 위해 파티션으로 구성 됩니다. 테이블 형식 솔루션에는 여러 유형의 데이터에서 온 것인지에 따라 테이블을 지원할 수 있습니다.  

* 일반 테이블과 데이터는 데이터 공급자를 통해 관계형 데이터 원본에서 발생 하는 위치입니다. 

* 여기서 데이터 내보내집니다"테이블에 프로그래밍 방식으로 푸시된 테이블입니다. 

* 계산 된 테이블의 데이터에 모델 내의 다른 개체를 참조 하는 DAX 식에서 데이터 원본 위치입니다.  

아래 코드 예제에서 일반 테이블을 정의 합니다. 

## <a name="required-elements"></a>필수 요소 

테이블에 파티션이 하나 이상 있어야 합니다. 일반 테이블에 정의 된 열을 하나 이상 있어야 합니다. 

모든 파티션에 데이터의 출처를 지정 하는 원본 소스를 설정할 수 있습니다 하지만 null로 합니다. 일반적으로 원본은 관련 데이터베이스 쿼리 언어에는 데이터 조각을 정의 하는 쿼리 식입니다. 

## <a name="code-example-create-a-table-column-parition"></a>코드 예제: 테이블, 열, 파티션 만들기

테이블 (Microsoft.AnalysisServices.Tabular 네임 스페이스)에서 테이블 클래스에 의해 표현 됩니다. 

아래 예제에는 일반 테이블에는 관계형 데이터 원본 및 몇 가지 일반 열에 연결 하는 하나의 파티션만 정의 합니다. 또한 서버에 변경 내용을 전송 하 고 모델에 데이터를 제공 하는 데이터 새로 고침 합니다. 이 테이블 형식 솔루션으로 SQL Server 관계형 데이터베이스에서 데이터를 로드 하려는 경우 가장 일반적인 시나리오를 나타냅니다. 


```
using System; 
using Microsoft.AnalysisServices; 
using Microsoft.AnalysisServices.Tabular; 
 
namespace TOMSamples 
{ 
    class Program 
    { 
        static void Main(string[] args) 
        { 
            // 
            // Connect to the local default instance of Analysis Services 
            // 
            string ConnectionString = "DataSource=localhost"; 
 
            // 
            // The using syntax ensures the correct use of the 
            // Microsoft.AnalysisServices.Tabular.Server object. 
            // 
            using (Server server = new Server()) 
            { 
                server.Connect(ConnectionString); 
 
                // 
                // Generate a new database name and use GetNewName 
                // to ensure the database name is unique. 
                // 
                string newDatabaseName = 
                    server.Databases.GetNewName("Database with a Table Definition"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var dbWithTable = new Database() 
                { 
                    Name = newDatabaseName, 
                    ID = newDatabaseName, 
                    CompatibilityLevel = 1200, 
                    StorageEngineUsed = StorageEngineUsed.TabularMetadata, 
                }; 
 
                // 
                // Add a Microsoft.AnalysisServices.Tabular.Model object to the 
                // database, which acts as a root for all other Tabular metadata objects. 
                // 
                dbWithTable.Model = new Model() 
                { 
                    Name = "Tabular Data Model", 
                    Description = "A Tabular data model at the 1200 compatibility level." 
                }; 
 
                // 
                // Add a Microsoft.AnalysisServices.Tabular.ProviderDataSource object 
                // to the data Model object created in the previous step. The connection 
                // string of the data source object in this example  
                // points to an instance of the AdventureWorks2014 SQL Server database. 
                // 
                string dataSourceName = "SQL Server Data Source Example"; 
                dbWithTable.Model.DataSources.Add(new ProviderDataSource() 
                { 
                    Name = dataSourceName, 
                    Description = "A data source definition that uses explicit Windows credentials for authentication against SQL Server.", 
                    ConnectionString = "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureWorks2014;Integrated Security=SSPI;Persist Security Info=false", 
                    ImpersonationMode = Microsoft.AnalysisServices.Tabular.ImpersonationMode.ImpersonateAccount, 
                    Account = @".\Administrator", 
                    Password = "P@ssw0rd", 
                }); 
 
                //  
                // Add a table called Individual Customers to the data model 
                // with a partition that points to a [Sales].[vIndividualCustomer] view 
                // in the underlying data source. 
                // 
                dbWithTable.Model.Tables.Add(new Table() 
                { 
                    Name = dbWithTable.Model.Tables.GetNewName("Individual Customers"), 
                    Description = "Individual customers (names and email addresses) that purchase Adventure Works Cycles products online.", 
                    Partitions = { 
                        // 
                        // Create a single partition with a QueryPartitionSource for a query 
                        // that imports all customer rows from the underlying data source. 
                        // 
                        new Partition() { 
                            Name = "All Customers", 
                            Source = new QueryPartitionSource() { 
                                DataSource = dbWithTable.Model.DataSources[dataSourceName], 
                                Query = @"SELECT   [FirstName] 
                                                    ,[MiddleName] 
                                                    ,[LastName] 
                                                    ,[PhoneNumber]  
                                                    ,[EmailAddress] 
                                                    ,[City] 
                                        FROM [Sales].[vIndividualCustomer]", 
                            } 
                        } 
                    }, 
                    Columns = 
                    { 
                        // 
                       // DataColumn objects refer to regular table columns.  
                        // Each DataColumn object corresponds to a column in the underlying data source query. 
                        // 
                        new DataColumn() { 
                            Name = "FirstName", 
                            DataType = DataType.String, 
                            SourceColumn = "FirstName", 
                        }, 
                        new DataColumn() { 
                            Name = "MiddleName", 
                            DataType = DataType.String, 
                            SourceColumn = "MiddleName", 
                        }, 
                        new DataColumn() { 
                            Name = "LastName", 
                            DataType = DataType.String, 
                            SourceColumn = "LastName", 
                        }, 
                        new DataColumn() { 
                            Name = "PhoneNumber", 
                            DataType = DataType.String, 
                            SourceColumn = "PhoneNumber", 
                        }, 
                        new DataColumn() { 
                            Name = "EmailAddress", 
                            DataType = DataType.String, 
                            SourceColumn = "EmailAddress", 
                        }, 
                        new DataColumn() { 
                            Name = "City", 
                            DataType = DataType.String, 
                            SourceColumn = "City", 
                        }, 
                    } 
                }); 
 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(dbWithTable); 
 
                //  
                // Request a full refresh to import the data from the data source and 
                // and perform any necessary recalculations. 
                // The refresh operation will be performed with the next 
                // invocation of Model.SaveChanges() or Database.Update(UpdateOptions.ExpandFull). 
                dbWithTable.Model.RequestRefresh(Microsoft.AnalysisServices.Tabular.RefreshType.Full); 
                dbWithTable.Update(UpdateOptions.ExpandFull); 
 
 
                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(dbWithTable.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
 
                Console.WriteLine("The data model includes the following table definitions:"); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                foreach (Table tbl in dbWithTable.Model.Tables) 
                { 
                    Console.WriteLine("\tTable name:\t\t{0}", tbl.Name); 
                    Console.WriteLine("\ttbl description:\t{0}", tbl.Description); 
                } 
                Console.ResetColor(); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```

## <a name="partitions-in-a-table"></a>테이블의 파티션 

파티션 표현 됩니다는 **파티션** 클래스 (Microsoft.AnalysisServices.Tabular 네임 스페이스). **파티션** 클래스가 노출 한 **소스** 속성 p**artitionSource** 입력 데이터를 수집 하는 방법에 대 한 다양 한 방식을 통해 추상화를 제공 하는 파티션입니다. A **파티션** 인스턴스에 있을 수 있습니다는 **소스** 속성 데이터의 일부로 서버에 데이터 청크를 전송 하 여 파티션을 밀어넣습니다 있는지를 나타내는 null로,으로 강제 Analysis Services에 의해 노출 되는 데이터 API . SQL Server 2016에서 **PartitionSource** 클래스를 파티션으로 데이터를 바인딩하는 방법을 나타내는 두 가지 파생된 클래스에: **QueryPartitionSource** 및 **CalculatedPartitionSource**. 

## <a name="columns-in-a-table"></a>테이블의 열 

열은 기본에서 파생 된 여러 클래스에서 나타납니다 **열** 클래스 (Microsoft.AnalysisServices.Tabular 네임 스페이스): 

* **DataColumn** (예: 기본 테이블의 일반 열)
* **CalculatedColumn** (열에 대 한 DAX 식에서 지원)
* **CalculatedTableColumn** (일반의 열에 대해 계산 된 테이블)
* **RowNumberColumn** (특수 한 유형의 모든 테이블에 대 한 SSAS에서 만든 열)입니다. 

## <a name="row-numbers-in-a-table"></a>테이블의 행 번호 

모든 **테이블** 서버에서 개체에는 **RowNumberColumn** 목적을 인덱싱하는 데 사용 합니다. 명시적으로 추가 하거나 만들 수 없습니다. 열 저장 하거나 개체를 업데이트할 때 자동으로 만들어집니다. 

* **db 합니다. SaveChanges** 

* **db 합니다. Update(ExpandFull)** 

두 방법 중 하나를 호출할 때 서버는 행 번호 열 자동으로 만들으로 표시 됩니다 **RowNumberColumn** 테이블의 열 컬렉션입니다. 

## <a name="calculated-tables"></a>계산 테이블 

아웃오브 라인 바인딩 또는 모델의 기존 데이터 구조에서 데이터를 repurposes 하는 DAX 식에서 계산 된 테이블 원본으로 제공 합니다. 계산된 테이블을 프로그래밍 방식으로 만들려면 다음을 수행 합니다. 

* 일반 만들기 **테이블**합니다. 

* 형식의 Source로 하 여 파티션을 추가 **CalculatedPartitionSource**, 소스는 DAX 식입니다. 파티션의 원본 계산 된 테이블에서 일반 테이블 구별 됩니다. 

서버의 유추 된 목록을 반환 합니다. 서버에 변경 내용을 저장 하면 **CalculatedTableColumns** (계산 된 테이블은 계산 된 테이블 열으로 구성), 테이블의 열 컬렉션을 통해 볼 수 있습니다. 

## <a name="next-steps"></a>다음 단계

TOM의 예외 처리에 사용 되는 클래스를 검토: [TOM에서 오류 처리](../../analysis-services/tabular-model-programming-compatibility-level-1200/handling-errors-in-the-tom-api-analysis-services-amo-tom.md)
  
