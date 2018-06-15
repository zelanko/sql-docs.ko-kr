---
title: Read(데이터베이스 엔진) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 60575f2c5c5f1de4a7fa5b2531fb8431f13b4441
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33052250"
---
# <a name="read-database-engine"></a>Read(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Read는 전달된 **BinaryReader**에서 **SqlHierarchyId**의 이진 표현을 읽고 **SqlHierarchyId** 개체를 해당 값으로 설정합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 Read를 호출할 수 없습니다. 대신 CAST 또는 CONVERT를 사용합니다.
  
## <a name="syntax"></a>구문  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>인수  
*r*  
 **hierarchyid** 노드의 이진 표현에 해당하는 이진 스트림을 생성하는 **BinaryReader** 개체입니다.  
  
## <a name="return-types"></a>반환 형식
 **CLR 반환 형식: void**  
  
## <a name="remarks"></a>Remarks  
 Read는 입력 유효성을 검사하지 않습니다. 잘못된 이진 입력이 지정되면 Read는 예외를 발생시킵니다. 성공하더라도 메서드가 예상치 못한 결과를 반환하거나 예외를 발생시킬 수 있는 잘못된 **SqlHierarchyId** 개체가 생성될 수 있습니다.  
  
 Read는 새로 생성된 **SqlHierarchyId** 개체에서만 호출할 수 있습니다.  
  
 Read는 **hierarchyid** 열에 데이터를 쓸 때와 같이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 필요한 경우에 내부적으로 사용됩니다. 또한 Read는 **varbinary**와 **hierarchyid** 간의 변환 시 내부적으로 호출됩니다.  
  
## <a name="examples"></a>예  
  
```sql
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>참고 항목  
[Write&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
