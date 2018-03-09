---
title: "만들기 및 배포 (Analysis Services AMO-TOM) 빈 데이터베이스 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: dcb916e9-97c5-47e0-922a-404891423b2a
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9f2529d4f7cb3e4912b3d0b6d0ee0879c46d83ec
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="create-and-deploy-an-empty-database-analysis-services-amo-tom"></a>만들기 및 배포 (Analysis Services AMO-TOM) 빈 데이터베이스
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]일반적인 프로그래밍 시나리오에 AMO TOM 데이터베이스 및 모델 즉석에서 생성 하는 것입니다. 이 문서에서는 데이터베이스를 만드는 과정을 안내 합니다. 

테이블 형식 솔루션에 대 한 데이터베이스와 데이터베이스 마다 하나의 모델로 모델 간의 한 일 대응이 됩니다. 하나 또는 다른 일반적으로 지정 하 고 엔진에서 누락 된 개체를 유추 합니다. 

만들기 및 새 데이터베이스를 배포 하는 세 부분으로 구성 태스크: 

* 인스턴스화하는 **데이터베이스** 개체 및 이름을 포함 한 속성을 설정 합니다. 

* 추가 **데이터베이스** 개체는 **Server.Databases** 컬렉션입니다. 

* 호출의 **업데이트** 에서 메서드는 **데이터베이스** 개체를 저장할는 **서버**합니다. 

## <a name="code-example-create-empty-database"></a>코드 예제에서는: 빈 데이터베이스 만들기 

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
                    server.Databases.GetNewName("New Empty Database"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var blankDatabase = new Database() 
                { 
                    Name = newDatabaseName, 
                    ID = newDatabaseName, 
                    CompatibilityLevel = 1200, 
                    StorageEngineUsed = StorageEngineUsed.TabularMetadata, 
                }; 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(blankDatabase); 
                blankDatabase.Update(UpdateOptions.ExpandFull); 

                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(blankDatabase.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```

## <a name="next-steps"></a>다음 단계 

데이터베이스를 만든 후에 모델 개체를 추가할 수 있습니다. 

- [테이블 형식 모델에 데이터 소스 추가](../../analysis-services/tabular-model-programming-compatibility-level-1200/add-a-data-source-to-tabular-model-analysis-services-amo-tom.md)
- [테이블 형식 모델에 테이블, 파티션 및 열 만들기](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-tables-partitions-and-columns-in-a-tabular-model.md)
 
