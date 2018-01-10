---
title: "FOR JSON을 통해 SQL Server 데이터 형식을 JSON 데이터 형식으로 변환하는 방법(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 07/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b5c5f0145e3a5f2809acc4d68decc206d5799b35
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>FOR JSON을 통해 SQL Server 데이터 형식을 JSON 데이터 형식으로 변환하는 방법(SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  **FOR JSON** 절은 다음 규칙을 사용하여 JSON 출력에서 SQL Server 데이터 형식을 JSON 형식으로 변환합니다.  
  
|범주|SQL Server 데이터 형식|JSON 데이터 형식|  
|--------------|--------------|---------------|  
|문자 및 문자열 유형|char, nchar, varchar, nvarchar|string|  
|숫자 유형|int, bigint, float, decimal, numeric|number|  
|비트 유형|bit|부울(true 또는 false)|  
|날짜 및 시간 유형|date, datetime, datetime2, time, datetimeoffset|string|  
|이진 유형|varbinary, binary, image, timestamp, rowversion|Base64로 인코딩된 문자열|  
|CLR 유형|geometry, geography, 기타 CLR 형식|지원되지 않습니다. 이러한 유형은 오류를 반환합니다.<br /><br /> SELECT 문에서 CAST 또는 CONVERT를 사용하거나, CLR 속성 또는 메서드를 사용하여 원본 데이터를 JSON 형식으로 변환할 수 있는 SQL Server 데이터 형식으로 변환합니다. 예를 들어 모든 geometry 형식의 경우 **STAsText()**를 사용하고 CLR 형식의 경우 **ToString()**를 사용합니다. 그러면 JSON 출력 값의 형식이 SELECT 문에서 적용하는 변환의 반환 형식에서 파생됩니다.|  
|다른 유형|uniqueidentifier, money|string|  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>SQL Server의 기본 제공 JSON 지원에 대한 자세한 정보  
많은 특정 솔루션, 사용 사례 및 권장 사항은 Microsoft 프로그램 관리자인 Jovan Popovic이 제공하는 SQL Server 및 Azure SQL Database의 [기본 제공 JSON 지원에 대한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.
  
## <a name="see-also"></a>참고 항목  
 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
