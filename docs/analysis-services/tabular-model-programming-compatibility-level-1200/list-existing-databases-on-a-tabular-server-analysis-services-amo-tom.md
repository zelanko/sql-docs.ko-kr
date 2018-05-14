---
title: 테이블 형식 서버 (Analysis Services AMO-TOM)에 있는 기존 데이터베이스 목록 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0e698e1e2335a2002c895afd097a886859747319
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="list-existing-databases-on-a-tabular-server-analysis-services-amo-tom"></a>테이블 형식 서버 (Analysis Services AMO-TOM)에 있는 기존 데이터베이스 목록
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
있는 경우는 **서버** 되는 개체를 Analysis Services 인스턴스에 연결을 반복할 수 있습니다 **Server.Databases** Anlaysis 서비스 인스턴스에 의해 호스트 되는 모든 데이터베이스를 나열 하는 컬렉션입니다. 

**Server.Databases** 컬렉션을 포함 하나 **데이터베이스** 서버 모드 (다차원 또는 테이블 형식) 또는 데이터베이스 유형 (다차원에 관계 없이 서버에서 호스팅되는 모든 데이터베이스에 대 한 개체 테이블 형식 사전 1200 또는 테이블 형식 1200 이상)입니다. 

통해 데이터베이스의 유형을 확인할 수 있습니다 **Database.StorageEngineUsed** 속성입니다.  

테이블 형식 1200 이상 데이터베이스에는 null이 아닌 반환 됩니다 **Database.Model** 모든 테이블 형식 메타 데이터 개체에 액세스할 수 있는 속성: 테이블, 열, 관계 및 등입니다.  

다차원 또는 테이블 형식 1103 및는 Database.Model 아래 속성 null이 됩니다. 이 경우-테이블 형식 메타 데이터 (예: Database.Cubes 및 Database.Dimensions) 다차원 속성에서 사용할 수 있지만 이러한 속성에만 표시 됩니다 (AMO)에서 Microsoft.AnalysisServices.Database 클래스가 아니라 (예: TOM) Microsoft.AnalysisServices.Tabular.Database 합니다. 데이터베이스 클래스를 사용 하는 방법에 대 한 자세한 내용은 참조 [설치, 배포 및 TOM 클라이언트 라이브러리를 참조](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md)합니다.

Database.StorageEngineUsed TabularMetadata로 설정 되어에 액세스 하거나 모델 트리를 조작 테이블 형식 네임 스페이스의 다른 클래스를 사용할 수 없습니다. 

다음 표에서 서버 또는 Microsoft.AnalysisServices.Tabular 클래스를 사용 하 여 서버 또는 데이터베이스에서 데이터베이스에 연결할 때 예상 되는 동작을 요약 합니다. 

mode | Database.model | Database.StorageEngineUsed
-----|----------------|---------------------------
테이블 형식 1200 1400 | 모델의 이름을 반환합니다.| StorageEngineUsed.TabularMetadata 
테이블 형식 1103 1050, 1100 | Null을 반환 합니다. | StorageEngineUsed.InMemory 
다차원 | Null을 반환 합니다. | StorageEngineUsed.Traditional 

## <a name="code-example-list-existing-databases"></a>코드 예제에서는: 기존 데이터베이스를 나열

아래 코드에는 서버에서 호스팅되는 서버와 목록은 데이터베이스에 연결 하는 방법을 보여 줍니다. 

```
using System; using Microsoft.AnalysisServices; 
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
                // List common properties for the databases on the server. 
                // 
                foreach (Database db in server.Databases) 
                { 
                    Console.WriteLine("Properties for database {0}:", db.Name); 
                    Console.ForegroundColor = ConsoleColor.Yellow; 
                    Console.WriteLine("Database ID:\t\t\t{0}", db.ID); 
                    Console.WriteLine("Database compatibility level:\t{0}", db.CompatibilityLevel); 
                    Console.WriteLine("Database collation:\t\t{0}", db.Collation); 
                    Console.WriteLine("Database created timestamp:\t{0}", db.CreatedTimestamp); 
                    Console.WriteLine("Database language ID:\t\t{0}", db.Language); 
                    Console.WriteLine("Database model type:\t\t{0}", db.ModelType); 
                    Console.WriteLine("Database state:\t\t\t{0}", db.State); 
                    Console.ResetColor(); 
                    Console.WriteLine(); 
                } 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```


## <a name="get-an-item-from-a-database"></a>데이터베이스에서 항목 가져오기 

다음 코드 조각에는 데이터베이스 열 또는 테이블 형식 가져오는 방법을 보여 줍니다. 


```
var db = srv.Databases.GetByName("abc"); 

Column c1 = db.Model.Tables["foo"].Columns["bar"]; 
if (c1.ObjectType == ObjectType.Column) // always true 

MetadataObject obj; 

switch(obj.ObjectType) 
{ 
 case ObjectType.Table: 
  var t1 = (Table)obj; 
  break; 
} 
```

## <a name="next-steps"></a>다음 단계

이해 하는 방법 [만들기 빈 데이터베이스를 배포 하 고](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md) TOM API를 사용 하 여 합니다.

