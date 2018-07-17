---
title: Write(데이터베이스 엔진) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d5976050ef20e2f6d63aa6e6d121a7b05229d724
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429754"
---
# <a name="write-database-engine"></a>Write(데이터베이스 엔진)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Write는 전달된 **BinaryWriter**에 **SqlHierarchyId**의 이진 표현을 씁니다. [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 Write를 호출할 수 없습니다. 대신 CAST 또는 CONVERT를 사용합니다.
  
## <a name="syntax"></a>구문  
  
```sql
void Write( BinaryWriter w )   
```  
  
## <a name="arguments"></a>인수  
*w*  
이 **hierarchyid** 노드의 이진 표현을 쓸 **BinaryWriter** 개체입니다.
  
## <a name="return-types"></a>반환 형식  
**CLR 반환 형식: void**
  
## <a name="remarks"></a>Remarks  
Write는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 **hierarchyid** 열에서 데이터를 로드할 때와 같이 필요한 경우 내부적으로 사용됩니다. 또한 Write는 **hierarchyid**와 **varbinary** 간의 변환 시 내부적으로 호출됩니다.
  
## <a name="examples"></a>예  
  
```sql
MemoryStream stream = new MemoryStream();  
BinaryWriter bw = new BinaryWriter(stream);  
hid.Write(bw);  
byte[] encoding = stream.ToArray();  
  
```  
  
## <a name="see-also"></a>관련 항목:
[Read&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/read-database-engine.md)  
[ToString&#40;데이터베이스 엔진&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST 및 CONVERT&#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[hierarchyid 데이터 형식 메서드 참조](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
