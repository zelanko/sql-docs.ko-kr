---
title: "FOR JSON을 통해 SQL Server 데이터 형식을 JSON 데이터 형식으로 변환하는 방법(SQL Server) | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 527cb99c5caf0bb805e17f3b77b7d5e017e28ace
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>FOR JSON을 통해 SQL Server 데이터 형식을 JSON 데이터 형식으로 변환하는 방법(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **FOR JSON** 절은 다음 규칙을 사용하여 JSON 출력에서 SQL Server 데이터 형식을 JSON 형식으로 변환합니다.  
  
|범주|SQL Server 데이터 형식|JSON 데이터 형식|  
|--------------|--------------|---------------|  
|문자 및 문자열 유형|char, nchar, varchar, nvarchar|string|  
|숫자 유형|int, bigint, float, decimal, numeric|number|  
|비트 유형|bit|부울(true 또는 false)|  
|날짜 및 시간 유형|date, datetime, datetime2, time, datetimeoffset|string|  
|이진 유형|varbinary, binary, image, timestamp, rowversion|Base64로 인코딩된 문자열|  
|CLR 유형|geometry, geography, 다른 CLR 형식|지원되지 않습니다. 이러한 유형은 오류를 반환합니다.<br /><br /> SELECT 문에서 CAST를 사용 하 여 변환 또는 CLR 속성 또는 메서드를 사용 하 여 JSON 형식으로 성공적으로 변환 될 수 있는 SQL Server 데이터 형식으로 원본 데이터를 변환할 또는 합니다. 사용 예를 들어 **stastext ()** geometry 유형 또는 사용에 대 한 **tostring ()** 모든 CLR 형식에 대 한 합니다. JSON 출력 값의 형식은 SELECT 문에 적용 하는 변환의 반환 형식에서 파생 됩니다.|  
|다른 유형|uniqueidentifier, money|string|  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>기본 제공 SQL Server에서 JSON 지원에 대 한 자세한 정보  
특정 솔루션에 많이 사용 사례 및 권장 사항, 참조는 [기본 제공 JSON 지원에 대 한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) SQL Server와 Microsoft 프로그램 관리자 인 Jovan popovic의 Azure SQL 데이터베이스에 있습니다.
  
## <a name="see-also"></a>관련 항목:  
 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  

