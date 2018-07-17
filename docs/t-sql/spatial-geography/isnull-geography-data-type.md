---
title: IsNull(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IsNull (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 855b5f4f94c48dc0010075372439b4266b8c5b26
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36243575"
---
# <a name="isnull-geography-data-type"></a>IsNull(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geography** 인스턴스의 null 여부를 지정하는 속성입니다. 해당 인스턴스가 Null이면 'TRUE'를 반환하고 Null이 아니면 0을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.IsNull  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식: **bit**  
  
 CLR 형식: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 `IsNull`을 사용하여 **geography** 인스턴스가 Null인지 여부를 테스트할 수 있습니다. 이 속성은 인스턴스가 Null이 아니면 0을 반환하고 인스턴스가 Null이면 Null을 반환하므로 결과가 다소 혼동스러울 수 있습니다.  
  
 이 메서드는 주로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인프라에서 사용됩니다. **geography** 인스턴스가 Null인지 여부를 테스트하는 데는 T-SQL 조건자 IS NULL을 사용하는 것이 좋습니다. T-SQL 조건자 IS NULL에 대한 자세한 내용은 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
