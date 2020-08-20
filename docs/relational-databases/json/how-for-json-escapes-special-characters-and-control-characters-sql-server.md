---
description: FOR JSON이 특수 문자 및 제어 문자를 이스케이프 처리하는 방법(SQL Server)
title: FOR JSON이 특수 문자 및 제어 문자를 이스케이프 처리하는 방법
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON, special characters
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c96ae7e539a4a5783d238d71ff94d9e04f179251
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499257"
---
# <a name="how-for-json-escapes-special-characters-and-control-characters-sql-server"></a>FOR JSON이 특수 문자 및 제어 문자를 이스케이프 처리하는 방법(SQL Server)

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  이 항목에서는 SQL Server **SELECT**의 **FOR JSON** 절이 특수 문자를 이스케이프 처리하고 JSON 출력에서 제어 문자를 표시하는 방법에 대해 설명합니다.  

> [!IMPORTANT]
> 이 페이지에서는 Microsoft SQL Server에서 기본 제공되는 JSON 지원에 대해 설명합니다. JSON에서 이스케이프 및 인코딩에 대한 일반적인 정보는 JSON RFC - [https://www.ietf.org/rfc/rfc4627.txt](https://www.ietf.org/rfc/rfc4627.txt)의 섹션 2.5를 참조하세요.

## <a name="escaping-of-special-characters"></a>특수 문자를 이스케이프 처리  
원본 데이터에 특수 문자가 포함된 경우 **FOR JSON** 절은 다음 표에 나와 있는 것처럼 `\`를 사용하여 JSON 출력의 특수 문자를 이스케이프 처리합니다. 속성 이름과 해당 값에서 모두 특수 문자가 이와 같이 이스케이프 처리됩니다.  
  
|**특수 문자**|**이스케이프 처리된 출력**|  
|---------------------------|--------------------------|  
|따옴표(")|\\"|  
|백슬래시(\\)|\\\\|  
|슬래시(/)|\\/|  
|백스페이스|\b|  
|폼 피드|\f|  
|줄 바꿈|\n|  
|캐리지 리턴|\r|  
|가로 탭|\t|  
  
## <a name="control-characters"></a>제어 문자  
원본 데이터에 제어 문자가 포함된 경우 **FOR JSON** 절은 다음 표에 나와 있는 것처럼 JSON 출력의 제어 문자를 `\u<code>` 형식으로 인코딩합니다.  
  
|**제어 문자**|**인코딩된 출력**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|...|...|  
|CHAR(31)|\u001f|  
  
## <a name="example"></a>예제  
 다음은 특수 문자와 제어 문자를 모두 포함하는 원본 데이터에 대한 **FOR JSON** 출력의 예입니다.  
  
 쿼리:  
  
```sql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 결과:  
  
```json  
{
    "KEY\\\t\/\"": "VALUE\\\t\/\r\n\"",
    "0": "\u0000",
    "1": "\u0001",
    "31": "\u001f"
}
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
### <a name="microsoft-videos"></a>Microsoft 비디오

SQL Server 및 Azure SQL Database에서 기본 제공 JSON 지원에 대한 시각적 소개는 다음 비디오를 참조하세요.

-   [SQL Server 2016 및 JSON 지원](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 및 Azure SQL Database에서 JSON 사용](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL과 관계형 간에 브리지인 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>참고 항목  
 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
[FOR 절](../../t-sql/queries/select-for-clause-transact-sql.md)
