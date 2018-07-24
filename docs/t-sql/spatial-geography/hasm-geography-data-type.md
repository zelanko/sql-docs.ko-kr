---
title: HasM(geography 데이터 형식) | Miciosoft Docs
ms.custom: ''
ms.date: 05/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- HasM_TSQL
- HasM
dev_langs:
- TSQL
helpviewer_keywords:
- HasM geography
ms.assetid: e752e97f-1619-437d-b962-48c188b4e94c
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d4731467cbc32316d48a7c78298f39bd5bc0abbb
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37986334"
---
# <a name="hasm-geography-data-type"></a>HasM(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  공간 개체에 M 값이 하나 이상 포함된 경우 1(true)을 반환하고, 그렇지 않으면 0(false)을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.HasM  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **Boolean**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>예  
  
```sql  
DECLARE @p GEOGRAPHY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)  
  
  
