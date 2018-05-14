---
title: Alter 명령 (TMSL) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6dc7ba58ce3e5db228046324c17c91719db35d0b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="alter-command-tmsl"></a>변경 명령을 TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  테이블 형식 모드에서 Analysis Services 인스턴스에서 자식 없습니다 되지만 기존 개체를 변경합니다.  개체가 없으면 명령에서 오류가 발생 합니다.  
  
 사용 하 여 **Alter** 의 모든 열에도 지정 하지 않고 테이블에 속성을 설정 하는 등의 대상으로 지정 된 업데이트에 대 한 명령입니다. 이 명령은 비슷합니다 **CreateOrReplace**, 있지만 전체 개체 정의 제공 하지 않고 있습니다.  
  
 에 대 한 읽기 / 쓰기 속성 하나를 지정 하는 경우 읽기 / 쓰기 속성을 포함 된 개체를 모든를 사용 하 여 새로운 또는 기존 값을 지정 하려면 해야 합니다. 속성 목록을 보려면 AMO PowerShell을 사용할 수 있습니다. 
  
## <a name="request"></a>요청  
 **Alter** 특성이 없습니다. 입력 개체를 변경할 수, 수정 된 개체 정의 다음에 포함 됩니다.  
  
 다음 예제에서는 파티션 개체에서 속성을 변경 하는 것에 대 한 구문을 보여 줍니다. 개체 경로 파티션을 설정 개체가 부모 개체의 이름-값 쌍을 통해 변경할 수 있습니다. 두 번째 입력에는 새 속성 값을 지정 하는 파티션 개체입니다.  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "\<database-name>",   
      "table": "\<table-name>",   
      "partition": "\<partition-name>"   
    },   
    "partition": {   
      "name": "\<new-partition-name>",   
       . . .  << other properties   
    }   
  }   
}   
```  
  
 요청의 구조 개체에 따라 다릅니다. **Alter** 다음 개체를 사용 하 여 사용할 수 있습니다.  
  
 [데이터베이스 개체 &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md) 데이터베이스 이름 바꾸기.  
  
```  
"alter": {   
    "object": {   
      "database": "\<database-name>"  
    },   
    "database": {   
      "name": "\<new-database-name>",   
    }   
  }   
```  
  
 [데이터 원본 개체 &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md) 자식 개체가 데이터베이스의 연결 이름 바꾸기.  
  
```  
{   
   "alter":{   
      "object":{   
         "database":"AdventureWorksTabular1200",  
         "dataSource":"SqlServer localhost AdventureworksDW2016"  
      },  
      "dataSource":{   
         "name":"A new connection name"  
      }  
   }  
}  
```  
  
 [Tables 개체 &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) 참조 **예 1** 아래 합니다.  
  
 [파티션 개체 &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md) 참조 **예 2** 아래 합니다.  
  
 [역할 개체 &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) 역할 개체의 속성을 변경 합니다.  
  
```  
{   
   "alter":{   
      "object":{   
         "database":"AdventureWorksTabular1200",  
         "role":"DataReader"  
      },  
      "role":{   
         "name":"New Name"  
      }  
   }  
}  
```  
  
## <a name="response"></a>응답  
 명령이 성공 하는 경우 빈 결과 반환 합니다. 그렇지 않은 경우 XMLA 예외가 반환 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Management Studio의 XMLA 창에서 실행 하거나에 대 한 입력으로 사용할 수 있는 스크립트를 보여 줍니다. [Invoke-ascmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) AMO PowerShell에서 합니다.  
  
 **예제 1** -이 스크립트는 테이블에 name 속성을 변경 합니다.  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "AdventureWorksDW2016",   
      "table": "DimDate"  
    },   
    "table": {   
      "name": "DimDate2"  
    }   
  }   
}  
```  
  
 명명 된 인스턴스는 로컬 가정 (인스턴스 이름이 "tabular") 및 alter 스크립트를 사용 하면이 명령은 JSON 파일에서 DimDate 테이블 이름을 DimDate2로 변경:  
  
 `invoke-ascmd -inputfile '\\my-computer\my-shared-folder\altertablename.json' -server 'localhost\Tabular'`  
  
 **예제 2** -이 스크립트의 예를 들어 끝 연도 현재 연도의 이전 연도 되 면 파티션의 이름을 바꿉니다. 모든 속성을 지정 해야 합니다. 두면 **소스** 지정 하지 않으면 수 제거 하면 기존 파티션 정의 모두 합니다.  
  
 을 만들면 교체, 또는 자체 데이터 원본 개체를 변경 (예: 아래 파티션 스크립트) 스크립트에서 참조 되는 모든 데이터 원본에서 기존 이어야 합니다 하지 않는 한 **DataSource** 개체 모델에서. 데이터 원본을 변경 해야 할 경우 이렇게 하려면 별도 단계로 합니다.  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "InternetSales",   
      "table": "DimDate",  
      "partition": "CurrentYear"  
    },   
    "partition": {   
      "name": "Year2009",  
       "source": {  
             "query":  "SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] WHERE [dbo].[DimDate].CalendarYear = 2009",  
              "dataSource": "SqlServer localhost AdventureworksDW2016"  
        }  
    }   
  }   
}  
```  
  
## <a name="usage-endpoints"></a>사용 현황 (끝점)  
 Command 요소에이의 문에 사용 되는 [메서드 실행 &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) 다음과 같은 방법으로 노출 하는 XMLA 끝점을 통해 호출 합니다.  
  
-   SQL Server Management Studio (SSMS)의 XMLA 창으로  
  
-   에 대 한 입력 파일로 **호출 ascmd** PowerShell cmdlet  
  
-   SSIS 태스크 나 SQL Server 에이전트 작업에 대 한 입력으로  
  
 SSMS에서이 명령에 대 한 기본으로 제공 되는 스크립트를 생성할 수 없습니다. 대신, 예를 들어 하거나 직접 작성 수 있습니다.  
  
 [ \[MS-SSAS-T\]: QL Server Analysis Services 테이블 (SQL Server 기술 프로토콜)](http://go.microsoft.com/fwlink/p/?LinkId=784855) JSON 테이블 형식 메타 데이터 명령 및 개체의 구조를 설명 하는 섹션 3.1.5.2.2 문서를 포함 합니다. 현재 문서에서는 명령과 기능은 아직 구현 되지 않은 TMSL 스크립트에서 다룹니다. 항목을 참조 ([테이블 형식 모델 스크립팅 언어 &#40;TMSL&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md))에 대 한 지원 되는 기능에 대 한 설명입니다.  

## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
