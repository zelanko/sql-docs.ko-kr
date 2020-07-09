---
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
ms.openlocfilehash: 8050e55674f801608053938f14f1c5456ee9217d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731193"
---
# <a name="hasm-geography-data-type"></a>HasM(geography 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

공간 개체에 M 값이 하나 이상 포함된 경우 1(true)을 반환하고, 그렇지 않으면 0(false)을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
  
.HasM  
```  
  
## <a name="return-types"></a>반환 형식  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
CLR 반환 형식: **Boolean**  
  
## <a name="remarks"></a>설명  
  
## <a name="examples"></a>예  
  
```sql  
DECLARE @p GEOGRAPHY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)  
  
  
