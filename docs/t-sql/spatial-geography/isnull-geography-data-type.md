---
title: "IsNull (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IsNull (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9b9f65a3860b1b0d54231d3243fdfdf1902ae8ca
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="isnull-geography-data-type"></a>IsNull(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  하는 경우를 지정 하는 속성은 **geography** 인스턴스가 null입니다. 해당 인스턴스가 Null이면 'TRUE'를 반환하고 Null이 아니면 0을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.IsNull  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]형식: **비트**  
  
 CLR 형식: **SqlBoolean**  
  
## <a name="remarks"></a>주의  
 `IsNull`테스트에 사용할 수 있는지 여부를 **geography** 인스턴스가 null입니다. 이 속성은 인스턴스가 Null이 아니면 0을 반환하고 인스턴스가 Null이면 Null을 반환하므로 결과가 다소 혼동스러울 수 있습니다.  
  
 이 메서드는 주로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인프라; T-SQL 조건자 IS NULL 테스트를 사용 하는 것이 좋습니다. 있는지 여부를 **geography** 인스턴스가 null입니다. T-SQL에 대 한 자세한 내용은 조건자 IS NULL, 참조 [IS NULL &#40; Transact SQL &#41; ](../../t-sql/queries/is-null-transact-sql.md).  
  
## <a name="examples"></a>예  
  
## <a name="see-also"></a>관련 항목:  
 [Geography 인스턴스의 확장된 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  

