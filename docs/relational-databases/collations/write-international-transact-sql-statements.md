---
title: 국가별 Transact-SQL 문 작성 | Microsoft 문서
ms.custom: ''
ms.date: 04/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- writing international statements
- Transact-SQL international considerations
- international considerations [SQL Server], Transact-SQL
- Database Engine international considerations [SQL Server], Transact-SQL
- statements [SQL Server], international
- database international considerations [SQL Server], Transact-SQL
- dates [SQL Server], international considerations
ms.assetid: f0b10fee-27f7-45fe-aece-ccc3f63bdcdb
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4eb6cf7d397bc8fdc8ab37d17e830ad2b373882e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140824"
---
# <a name="write-international-transact-sql-statements"></a>국가별 Transact-SQL 문 작성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  다음 지침에 따라 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용하는 데이터베이스 및 데이터베이스 애플리케이션을 특정 언어에서 다른 언어로 이식하거나 여러 언어를 지원하도록 할 수 있습니다.  

-   [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터 다음 중 하나를 사용합니다.
    -   [UTF-8](../../relational-databases/collations/collation-and-unicode-support.md#utf8) 사용 데이터 정렬을 사용하는 **char**, **varchar** 및 **varchar(max)** 데이터 형식.
    -   [보조 문자](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters) 사용 데이터 정렬을 사용하는 **char**, **varchar** 및 **varchar(max)** 데이터 형식.      

    이렇게 하면 코드 페이지 변환 문제가 발생하지 않습니다. 다른 고려 사항은 [UTF-8과 UTF-16 간의 스토리지 차이점](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences)을 참조하세요.  

-   [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]까지 **char**, **varchar** 및 **varchar(max)** 데이터 형식을 사용하는 경우 모두 **nchar**, **nvarchar** 및 **nvarchar(max)** 로 대체합니다. 이렇게 하면 코드 페이지 변환 문제가 발생하지 않습니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요. 
    > [!IMPORTANT]
    > **텍스트** 데이터 형식은 더 이상 사용되지 않으며 새로운 개발 작업에 사용하면 안됩니다. **텍스트** 데이터를 **varchar(max)** 로 변환하도록 계획합니다.
  
-   월과 요일을 비교하고 작업을 수행할 때는 문자열 이름 대신 숫자 형식의 날짜 부분을 사용합니다. 언어 설정이 다르면 월과 요일에 대해 각기 다른 이름이 반환됩니다. 예를 들어 언어가 미국으로 설정된 경우 `DATENAME(MONTH,GETDATE())`는 `May`를 반환합니다. 영어는 언어가 독일어로 설정된 경우 `Mai`를 반환하고 언어가 프랑스어로 설정된 경우 `mai`를 반환합니다. 대신 이름이 아닌 해당 월의 숫자를 사용하는 [DATEPART](../../t-sql/functions/datepart-transact-sql.md)와 같은 함수를 사용합니다. 날짜 이름이 숫자 표시보다 의미를 쉽게 알 수 있으므로 사용자에게 표시되는 결과 집합을 만들 때에는 DATEPART 이름을 사용합니다. 그러나 특정 언어로 표시된 이름에 따라 달라지는 논리는 코딩하지 마세요.  
  
-   INSERT 또는 UPDATE 문을 위한 입력이나 비교를 위해 날짜를 지정할 때 모든 언어 설정에서 동일하게 해석되는 상수를 사용하십시오.  
  
    -   ADO, OLE DB 및 ODBC 애플리케이션은 다음과 같은 ODBC용 타임스탬프, 날짜 및 시간 이스케이프 절을 사용해야 합니다.  
  
         **{ ts'** _yyyy_ **-** _mm_ **-** _dd_ _hh_ **:** _mm_ **:** _ss_ [ **.** _fff_] **'}** 예: **{ ts'1998-09-24 10:02:20'}**  
  
         **{ d'** _yyyy_ **-** _mm_ **-** _dd_ **'}** 예: **{ d'1998-09-24'}**
  
         **{ t'** _hh_ **:** _mm_ **:** _ss_ **'}** 예: **{ t'10:02:20'}**  
  
    -   다른 API나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트, 저장 프로시저, 트리거를 사용하는 애플리케이션에서는 분리되지 않은 숫자 문자열을 사용해야 합니다. 예를 들어 19980924와 같은 *yyyymmdd* 를 사용합니다.  
  
    -   다른 API나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트, 저장 프로시저 및 트리거를 사용하는 애플리케이션에서는 **time**, **date**, **smalldate**, **datetime**, **datetime2** 및 **datetimeoffset** 데이터 형식과 문자열 데이터 형식 간의 모든 변환에 명시적 스타일 매개 변수가 있는 [CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) 문을 사용해야 합니다. 예를 들어 다음 문은 모든 언어 또는 날짜 형식 연결 설정에서 똑같이 해석됩니다.  
  
        ```sql  
        SELECT *  
        FROM AdventureWorks2012.Sales.SalesOrderHeader  
        WHERE OrderDate = CONVERT(DATETIME, '20060719', 101)  
        ```  
  
## <a name="see-also"></a>관련 항목:
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)     
[DATEPART &#40;Transact-SQL&#41;](../../t-sql/functions/datepart-transact-sql.md)        
[데이터 정렬 및 유니코드 지원](../../relational-databases/collations/collation-and-unicode-support.md)      
