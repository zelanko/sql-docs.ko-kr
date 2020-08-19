---
description: IsNull(geography 데이터 형식)
title: IsNull(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsNull (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: cd161c4d14241a6596e2a54ae79cd919fb776c59
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422377"
---
# <a name="isnull-geography-data-type"></a>IsNull(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** 인스턴스의 null 여부를 지정하는 속성입니다. 해당 인스턴스가 Null이면 'TRUE'를 반환하고 Null이 아니면 0을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.IsNull  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식: **bit**  
  
 CLR 형식: **SqlBoolean**  
  
## <a name="remarks"></a>설명  
 `IsNull`을 사용하여 **geography** 인스턴스가 Null인지 여부를 테스트할 수 있습니다. 이 속성은 인스턴스가 Null이 아니면 0을 반환하고 인스턴스가 Null이면 Null을 반환하므로 결과가 다소 혼동스러울 수 있습니다.  
  
 이 메서드는 주로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인프라에서 사용됩니다. **geography** 인스턴스가 Null인지 여부를 테스트하는 데는 T-SQL 조건자 IS NULL을 사용하는 것이 좋습니다. T-SQL 조건자 IS NULL에 대한 자세한 내용은 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
