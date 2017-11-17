---
title: "읽기 (데이터베이스 엔진) | Microsoft Docs"
ms.custom: 
ms.date: 7/22/2017
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
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 21f27c627a36f747d9e3ecbb52d14d1ac6bc5d28
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="read-database-engine"></a>Read(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

읽기의 이진 표현을 읽고 **SqlHierarchyId** 전달 기능에서 **BinaryReader** 설정 하 고는 **SqlHierarchyId** 개체를 해당 값입니다. 읽기를 사용 하 여 호출할 수 없습니다 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다. 대신 CAST 또는 CONVERT를 사용합니다.
  
## <a name="syntax"></a>구문  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>인수  
*r*  
 **BinaryReader** 의 이진 표현에 해당 하는 이진 스트림을 생성 하는 개체는 **hierarchyid** 노드.  
  
## <a name="return-types"></a>반환 형식
 **CLR 반환 형식: void**  
  
## <a name="remarks"></a>주의  
 읽기는 입력 유효성을 검사 하지 않습니다. 잘못 된 이진 입력이 지정 되 면 읽기 예외가 발생 될 수 있습니다. 성공 하 고 잘못 된 생성 될 수 있습니다 또는 **SqlHierarchyId** 개체 메서드 예기치 않은 결과 제공 하거나 예외를 발생 시킬 수 있습니다.  
  
 읽기 에서만 호출 될 수는 새로 만든 **SqlHierarchyId** 개체입니다.  
  
 읽기 내부적으로 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 되었을 때와 같이 필요한 데이터를 쓸 때 **hierarchyid** 열입니다. 읽기 간의 변환 시 내부적으로 호출 또한 **varbinary** 및 **hierarchyid**합니다.  
  
## <a name="examples"></a>예  
  
```sql
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>관련 항목:  
[쓰기 &#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/write-database-engine.md)  
[Tostring&#40; 데이터베이스 엔진 &#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

