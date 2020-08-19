---
description: HasM(geography 데이터 형식)
title: HasM(geography 데이터 형식) | Miciosoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HasM_TSQL
- HasM
dev_langs:
- TSQL
helpviewer_keywords:
- HasM geography
ms.assetid: e752e97f-1619-437d-b962-48c188b4e94c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 33c1bdd90dae6fc6d7f40872355056b539d8016b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445268"
---
# <a name="hasm-geography-data-type"></a>HasM(geography 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

공간 개체에 M 값이 하나 이상 포함된 경우 1(true)을 반환하고, 그렇지 않으면 0(false)을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
  
.HasM  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
CLR 반환 형식: **Boolean**  
  
## <a name="remarks"></a>설명  
  
## <a name="examples"></a>예제  
  
```sql  
DECLARE @p GEOGRAPHY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)  
  
  
