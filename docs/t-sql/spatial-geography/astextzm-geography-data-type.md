---
title: AsTextZM(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsTextZM (geography Data Type)
- AsTextZM_TSQL
- AsTextZM
- AsTextZM_(geography_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM method
ms.assetid: e9dc27f6-e945-4457-8498-7644db34008e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f8a147ff48d0436c51519532af3485e0bde11ed2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47713021"
---
# <a name="astextzm-geography-data-type"></a>AsTextZM(geography 데이터 형식)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  인스턴스에서 얻어진 **Z**(높이) 값 및 **M**(측정값) 값을 사용하여 보강된 **geography** 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **nvarchar(max)**  
  
 CLR 반환 형식: **SqlChars**  
  
## <a name="remarks"></a>Remarks  
  
## <a name="examples"></a>예  
 다음 예에서는 **Z**(높이) 값 및 **M**(측정값) 값을 포함하는 `Point` 인스턴스를 만듭니다. `STAsText()`는 WKT 값인 (-122.34900 47.65100)을 선택하며 `AsTextZM()`도 동일한 WKT 값을 선택하여 **Z** 및 **M**의 값을 반환하여 (-122.34900 47.65100 10.3 12)를 반환합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [M&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/m-geography-data-type.md)   
 [Z&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
