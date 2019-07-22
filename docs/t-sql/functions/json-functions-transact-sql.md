---
title: JSON 함수(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: t-sql
ms.topic: language-reference
helpviewer_keywords:
- JSON functions
ms.assetid: ec97d451-06af-44a3-8304-305d410cfc8e
author: jovanpop-msft
ms.author: jovanpop
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 5b83e6f6eefce1cf56b71e7d433dca19cb4575d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109425"
---
# <a name="json-functions-transact-sql"></a>JSON 함수(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

JSON 텍스트에 대한 유효성 검사 또는 변경을 수행하거나 간단한 값이나 복잡한 값을 추출하려면 이 섹션의 페이지에 설명된 함수를 사용합니다.  
  
|함수|설명|  
|--------------|-----------------|  
|[ISJSON](../../t-sql/functions/isjson-transact-sql.md)|문자열에 유효한 JSON이 포함되어 있는지 테스트합니다.|  
|[JSON_VALUE](../../t-sql/functions/json-value-transact-sql.md)|JSON 문자열에서 스칼라 값을 추출합니다.|  
|[JSON_QUERY](../../t-sql/functions/json-query-transact-sql.md)|JSON 문자열에서 개체 또는 배열을 추출합니다.|  
|[JSON_MODIFY](../../t-sql/functions/json-modify-transact-sql.md)|JSON 문자열의 속성 값을 업데이트하고 업데이트된 JSON 문자열을 반환합니다.|

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 JSON에 대한 기본 제공 지원에 관한 자세한 내용은 [JSON 데이터&#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)를 참조하세요.  

## <a name="see-also"></a>참고 항목

 - [기본 제공 함수를 사용하여 JSON 데이터 유효성 검사, 쿼리, 변경&#40;SQL Server&#41;](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)
 - [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)
 - [JSON 데이터&#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
