---
description: GetRoot(데이터베이스 엔진)
title: GetRoot(데이터베이스 엔진) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetRoot
- GetRoot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetRoot [Database Engine]
ms.assetid: 240b70f1-eeda-44ab-b4bb-9e4af80fa7c0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 645c39d8108ba52212788a65ae2d6116ee629e34
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92037136"
---
# <a name="getroot-database-engine"></a>GetRoot(데이터베이스 엔진)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

계층 트리의 루트를 반환합니다. GetRoot ()는 정적 메서드입니다.
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Transact-SQL syntax  
hierarchyid::GetRoot ( )   
```  
  
```syntaxsql
-- CLR syntax  
static SqlHierarchyId GetRoot ( )   
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식  
**SQL Server 반환 형식: hierarchyid**
  
**CLR 반환 형식: SqlHierarchyId**
  
## <a name="remarks"></a>설명  
계층 트리의 루트 노드를 확인하는 데 사용됩니다.
  
## <a name="examples"></a>예제  
  
### <a name="a-transact-sql-example"></a>A. Transact-SQL 예  
다음 예에서는 계층 트리의 루트를 반환합니다.
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode = hierarchyid::GetRoot()  
```  
  
### <a name="b-clr-example"></a>B. CLR 예  
다음 코드 조각은 GetRoot() 메서드를 호출합니다.
  
```sql
SqlHierarchyId.GetRoot()  
```  
  
## <a name="see-also"></a>참고 항목
[hierarchyid 데이터 형식 메서드 참조](./hierarchyid-data-type-method-reference.md)  
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
