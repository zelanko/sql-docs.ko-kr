---
title: STIsEmpty(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsEmpty_TSQL
- STIsEmpty (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsEmpty (geometry Data Type)
ms.assetid: dcbd6ae1-5d63-485f-9d58-28bfd504524e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 44b62d04c52ddb707bfd094d3b29fbfe84cf5bb4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762395"
---
# <a name="stisempty-geometry-data-type"></a>STIsEmpty(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** 인스턴스가 비어 있으면 1을 반환합니다. **geometry** 인스턴스가 비어 있지 않으면 0을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STIsEmpty ( )  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="examples"></a>예  
 다음 예에서는 비어 있는 `geometry` 인스턴스를 만들고 `STIsEmpty()`를 사용하여 인스턴스가 비어 있는지 테스트합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON EMPTY', 0);  
SELECT @g.STIsEmpty();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

