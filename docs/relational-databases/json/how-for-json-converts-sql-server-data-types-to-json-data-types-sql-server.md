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
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c256bc9ecc0e518bb54d206a04f36d2b736500d8
ms.lasthandoff: 04/11/2017

---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>FOR JSON을 통해 SQL Server 데이터 형식을 JSON 데이터 형식으로 변환하는 방법(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  **FOR JSON** 절은 다음 규칙을 사용하여 JSON 출력에서 SQL Server 데이터 형식을 JSON 형식으로 변환합니다.  
  
|범주|SQL Server 데이터 형식|JSON 데이터 형식|  
|--------------|--------------|---------------|  
|문자 및 문자열 유형|(n)(var)(char)|string|  
|숫자 유형|int, bigint, float, decimal, numeric|number|  
|비트 유형|bit|부울(true 또는 false)|  
|날짜 및 시간 유형|date, datetime, datetime2, time, datetimeoffset|string|  
|이진 유형|varbinary, binary, image, timestamp, rowversion|Base64로 인코딩된 문자열|  
|CLR 유형|CLR, geometry, geography|지원되지 않습니다. 이러한 유형은 오류를 반환합니다.<br /><br /> SELECT 문에서 CAST 또는 CONVERT를 사용하거나, CLR 속성 또는 메서드를 사용하여 데이터를 JSON 형식으로 변환할 수 있는 데이터 형식으로 변환합니다. 예를 들어 모든 CLR 형식의 경우 **ToString()** 을 사용하고 geometry 형식의 경우 **STAsText()** 를 사용합니다. JSON 출력 값의 형식은 SELECT 문에 사용하는 변환의 반환 형식에서 파생됩니다.|  
|다른 유형|uniqueidentifier, money|string|  
  
## <a name="see-also"></a>참고 항목  
 [FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  

