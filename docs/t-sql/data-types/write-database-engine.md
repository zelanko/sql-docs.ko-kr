---
title: "Write (데이터베이스 엔진) | Microsoft Docs"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Write_TSQL
- Write
dev_langs:
- TSQL
helpviewer_keywords:
- Write [Database Engine]
ms.assetid: 7c554334-d2d9-4eae-a4ae-097aa4020e1a
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 60707b57671c2ad607bd85b0fedececccd478038
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="write-database-engine"></a>Write(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

쓰기의 이진 표현을 쓸 **SqlHierarchyId** 전달 기능에 **BinaryWriter**합니다. 쓰기를 사용 하 여 호출할 수 없습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다. 대신 CAST 또는 CONVERT를 사용합니다.
  
## <a name="syntax"></a>구문  
  
```sql
void Write( BinaryWriter w )   
```  
  
## <a name="arguments"></a>인수  
*w*  
A **BinaryWriter** 있는 개체를이의 이진 표현 **hierarchyid** 노드가 작성 됩니다.
  
## <a name="return-types"></a>반환 형식  
**CLR 반환 형식: void**
  
## <a name="remarks"></a>주의  
쓰기 내부적으로 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 되었을 때와 같이 필요한 데이터를 로드 하는 경우는 **hierarchyid** 열입니다. 쓰기 간의 변환 시 내부적으로 호출 또한 **hierarchyid** 및 **varbinary**합니다.
  
## <a name="examples"></a>예  
  
```sql
MemoryStream stream = new MemoryStream();  
BinaryWriter bw = new BinaryWriter(stream);  
hid.Write(bw);  
byte[] encoding = stream.ToArray();  
  
```  
  
## <a name="see-also"></a>참고 항목
[읽기 &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/read-database-engine.md)  
[Tostring&#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

