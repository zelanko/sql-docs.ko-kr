---
title: "IsNull (geography 데이터 형식) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c07ddb41209c507845da7e790035ab54ed1044f1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="isnull-geography-data-type"></a>IsNull(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

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
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
