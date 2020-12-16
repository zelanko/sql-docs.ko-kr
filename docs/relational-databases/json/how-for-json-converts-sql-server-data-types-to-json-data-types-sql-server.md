---
description: FOR JSON을 통해 SQL Server 데이터 형식을 JSON 데이터 형식으로 변환하는 방법(SQL Server)
title: FOR JSON을 통해 SQL Server 데이터 형식을 JSON 데이터 형식으로 변환하는 방법
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ff06a77af1592bf9bf2386742a53033ade76aecd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478124"
---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>FOR JSON을 통해 SQL Server 데이터 형식을 JSON 데이터 형식으로 변환하는 방법(SQL Server)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sqlserver2016-asdb.md)]

  **FOR JSON** 절은 다음 규칙을 사용하여 JSON 출력에서 SQL Server 데이터 형식을 JSON 형식으로 변환합니다.  
  
|Category|SQL Server 데이터 형식|JSON 데이터 형식|  
|--------------|--------------|---------------|  
|문자 및 문자열 유형|char, nchar, varchar, nvarchar|문자열|  
|숫자 유형|int, bigint, float, decimal, numeric|number|  
|비트 유형|bit|부울(true 또는 false)|  
|날짜 및 시간 유형|date, datetime, datetime2, time, datetimeoffset|문자열|  
|이진 유형|varbinary, binary, image, timestamp, rowversion|Base64로 인코딩된 문자열|  
|CLR 유형|geometry, geography, 기타 CLR 형식|지원 안 됨 이러한 유형은 오류를 반환합니다.<br /><br /> SELECT 문에서 CAST 또는 CONVERT를 사용하거나 CLR 속성 또는 메서드를 사용하여, JSON 형식으로 변환할 수 있는 SQL Server 데이터 형식으로 원본 데이터를 변환합니다. 예를 들어 모든 geometry 형식의 경우 **STAsText()** 를 사용하고 CLR 형식의 경우 **ToString()** 를 사용합니다. 그러면 JSON 출력 값의 형식이 SELECT 문에서 적용하는 변환의 반환 형식에서 파생됩니다.|  
|기타 형식|uniqueidentifier, money|문자열|  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
### <a name="microsoft-videos"></a>Microsoft 비디오

SQL Server 및 Azure SQL Database에서 기본 제공 JSON 지원에 대한 시각적 소개는 다음 비디오를 참조하세요.

-   [SQL Server 2016 및 JSON 지원](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 및 Azure SQL Database에서 JSON 사용](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL과 관계형 간에 브리지인 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>참고 항목  
 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
