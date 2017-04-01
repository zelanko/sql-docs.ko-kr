---
title: "R 데이터 형식 사용 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5df99e1c-a89a-42c1-9d68-ffe8d9577c94
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# R 데이터 형식 사용
  반면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 여러 수십 개의 데이터 형식을 지원 R에 스칼라 데이터 형식의 제한 된 수 (숫자, 복잡 한, 논리, 문자, 정수, 날짜/시간 및 원시). 따라서 R 스크립트에서  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 데이터를 사용할 경우 몇 가지 경우가 발생할 수 있습니다.  
  
-   데이터가 호환되는 데이터 형식으로 암시적으로 변환됩니다.  
  
-   데이터를 암시적으로 변환할 수 없고 오류가 반환됩니다.  
  
 일반적으로 특정 데이터 형식 또는 데이터 구조가 R에서 어떻게 사용되는지 잘 모를 경우  `str()` 함수를 사용하여 R개체의 내부 구조와 형식을 가져옵니다. 함수 결과는 R 콘솔에 인쇄되며 **의** 메시지 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]탭에서 쿼리 결과로도 확인할 수 있습니다.  
  
 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] r, 데이터 형식이 지원 되지 않습니다 하지만 R 스크립트에서 데이터의 열을 사용 해야 하 고, 사용 하는 것이 좋습니다는 [CAST 및 CONVERT & #40; TRANSACT-SQL & #41;](../../t-sql/functions/cast-and-convert-transact-sql.md) 데이터 형식 변환 있는지 확인 하는 함수 R 스크립트에서 데이터를 사용 하기 전에 의도 한 대로 수행 됩니다.  
  
 에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식 참조 [데이터 형식 및 #40; TRANSACT-SQL & #41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
## R 및 SQL Server 간 데이터 형식 변환  
 다음 표는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 데이터를 R 스크립트에 사용한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 반환할 때 데이터 형식 및 값의 변화를 보여줍니다.  
  
|||||  
|-|-|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식|R 클래스| **RESULT SET**에서의 형식|주석|  
|**smalldatetime**|`POSIXct`|**날짜/시간**|GMT로 표시됨|  
|**smallmoney**|`numeric`|**부동**||  
|**날짜/시간**|`POSIXct`|**날짜/시간**|GMT로 표시됨|  
|**money**|`numeric`|**부동**||  
|**uniqueidentifier**|`character`|**varchar(max)**||  
|**numeric(p,s)**|`numeric`|**부동**||  
|**decimal(p,s)**|`numeric`|**부동**||  
|**date**|`POSIXct`|**날짜/시간**|GMT로 표시됨|  
|**tinyint**|`integer`|**int**||  
|**bit**|`logical`|**bit**||  
|**smallint**|`integer`|**int**||  
|**int**|`integer`|**int**||  
|**부동**|`numeric`|**부동**||  
|**real**|`numeric`|**부동**||  
|**bigint**|`numeric`|**부동**||  
|**binary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|입력 매개 변수 및 출력으로만 허용됨|  
|**char(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||  
|**varbinary (n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|입력 매개 변수 및 출력으로만 허용됨|  
|**varchar(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||  
|**varbinary(max)**|`raw`|**varbinary(max)**|입력 매개 변수 및 출력으로만 허용됨|  
  
## 데이터 형식 변환 예  
 다음 쿼리는 일련의 값을 가져옵니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 및 저장된 프로시저를 사용 하 여  [sp_execute_external_script & #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) R 런타임을 사용 하는 값을 출력 합니다.  
  
```  
CREATE TABLE MyTable (    
 c1 int,    
 c2 varchar(10),    
 c3 uniqueidentifier    
);    
go    
INSERT MyTable VALUES(1, 'Hello', newid());    
INSERT MyTable VALUES(-11, 'world', newid());    
SELECT * FROM MyTable;    
  
EXECUTE sp_execute_external_script    
 @language = N'R'    
 , @script = N'    
inputDataSet["cR"] <- c(4, 2)    
str(inputDataSet)    
outputDataSet <- inputDataSet'    
 , @input_data_1 = N'SELECT c1, c2, c3 FROM MyTable'    
 , @input_data_1_name = N'inputDataSet'    
 , @output_data_1_name = N'outputDataSet'    
 WITH RESULT SETS((C1 int, C2 varchar(max), C3 varchar(max), C4 float));  
```  
  
 **결과**  
  
||||||  
|-|-|-|-|-|  
||C1|C2|C3|C4|  
|1|1|Hello|6e225611-4b58-4995-a0a5-554d19012ef1|4|  
|1|-11|world|6732ea46-2d5d-430b-8ao1-86e7f3351c3e|2|  
  
 R에서 `str` 함수를 사용할 경우 출력 데이터의 스키마를 가져옵니다. 이 함수는 다음 정보를 반환합니다.  
  
```  
'data.frame':2 obs. of  4 variables:   
 $ c1: int  1 -11   
 $ c2: Factor w/ 2 levels "Hello","world": 1 2   
 $ c3: Factor w/ 2 levels "6732EA46-2D5D-430B-8A01-86E7F3351C3E",..: 2 1   
 $ cR: num  4 2  
```  
  
 여기에서 이 쿼리의 일환으로 다음의 데이터 형식 변환이 암시적으로 실행된 것을 볼 수 있습니다.  
  
-   **열 C1**: 열으로 표시 됩니다 **int** 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `integer` r에서는 및 **int** 출력 결과 집합에 있습니다.  
  
     형식 변환은 실행되지 않았습니다.  
  
-   **열 C2**: 열으로 표시 됩니다 **varchar (10)** 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `factor` r에서는 및 **varchar (max)** 출력에서 합니다.  
  
     Note 어떻게 출력 변경 합니다. 모든 문자열 r (인수 또는 일반 문자열)로 표시 됩니다 **varchar (max)**, 문자열의 길이 관계 없이.  
  
-   **열 C3**:  열으로 표시 됩니다 **uniqueidentifier** 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `character` r에서는 및 **varchar (max)** 출력에서 합니다.  
  
     여기서 실행된 데이터 형식 변환을 주목하십시오. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원 된 **uniqueidentifier** 하지만 R 하지 않습니다; 따라서 식별자 문자열로 표시 됩니다.  
  
-   **열 C4**: 이 열에는 R 스크립트에서 생성된 값이 포함되며 원본 데이터에 표시되지 않습니다.  
 
 ## 참고 항목
 [SQL Server R Services 기능 및 태스크](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)
  
  