---
title: "테이블 형식 모델 (Analysis Services AMO-TOM)에 데이터 원본을 추가 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e54a8a1b-b964-4b6e-9057-44d50af676c0
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b8f6397f70727173345a41e92704a4277de32ddd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="add-a-data-source-to-tabular-model-analysis-services-amo-tom"></a>테이블 형식 모델 (Analysis Services AMO-TOM)에 데이터 소스 추가

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

**DataSource** Microsoft.AnalysisServices.Tabular 네임 스페이스의 클래스 값은 데이터 새로 고침 작업 중 유형을 지정 하는 테이블 형식 모델의 데이터 원본에 대 한 추상화 및 가져온된 데이터의 위치입니다. 

파생 된 클래스의 개체를 인스턴스화하고 테이블 형식 모델에 데이터 소스를 추가할 수 있습니다 **DataSource**, 다음에 추가 하는 **DataSources** 모델 개체의 컬렉션입니다. 호출 서버에 변경 내용을 커밋 **Model.SaveChanges()** 또는 **Database.Update(UpdateOptions.ExpandFull)**합니다. 

SQL Server 2016 Analysis Services 데이터 공급자가 데이터 형식으로 테이블 및 열을 표시 하는 관계형 데이터베이스에서 데이터 가져오기를 지원 합니다. 이와 같이 테이블 형식 개체 모델 (데이터 원본에서 파생) ProviderDataSource 클래스를 사용 하 여이 기능을 노출 합니다. 

## <a name="code-example-add-a-data-source"></a>코드 예제에서는: 데이터 소스 추가 

이 예제를 인스턴스화하는 방법을 보여 줍니다는 **ProviderDataSource** 데이터 모델에 추가 합니다. 

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
                    server.Databases.GetNewName("Database with a Data Source Definition"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var dbWithDataSource = new Database() 
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
                dbWithDataSource.Model = new Model() 
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
                dbWithDataSource.Model.DataSources.Add(new ProviderDataSource() 
                { 
                    Name = "SQL Server Data Source Example", 
                    Description = "A data source definition that uses explicit Windows credentials for authentication against SQL Server.", 
                    ConnectionString = "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureWorks2014;Integrated Security=SSPI;Persist Security Info=false", 
                    ImpersonationMode = Microsoft.AnalysisServices.Tabular.ImpersonationMode.ImpersonateAccount, 
                    Account = @".\Administrator", 
                    Password = "P@ssw0rd", 
                }); 
 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(dbWithDataSource); 
                dbWithDataSource.Update(UpdateOptions.ExpandFull); 
 
                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(dbWithDataSource.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
                Console.WriteLine("The data model includes the following data source definitions:"); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                foreach (DataSource ds in dbWithDataSource.Model.DataSources) 
                { 
                    Console.WriteLine("\tData source name:\t\t{0}", ds.Name); 
                    Console.WriteLine("\tData source description:\t{0}", ds.Description); 
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

## <a name="next-step"></a>다음 단계 

모델 내에서 데이터 원본에서 원본 열을 모델에서 대상 열에 매핑되는 데이터 바인딩을 설정 해야 합니다. 파티션 최소 테이블당 1 데이터를 저장 하는 정의 해야 합니다. 다음 링크를 클릭 하는 방법을 보여 줍니다: [테이블, 파티션 및 열 만들기](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-tables-partitions-and-columns-in-a-tabular-model.md) 
