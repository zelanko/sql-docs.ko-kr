---
title: 반환된 XML 모양 지정에서 AUTO 모드 추론 | Microsoft 문서
description: FOR XML 절과 함께 AUTO 모드 추론을 사용하여 인접한 행의 열 값을 비교하고 쿼리에서 반환되는 XML의 모양을 결정하는 방법을 알아봅니다.
ms.custom: fresh2019may
ms.date: 04/03/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, heuristics in shaping returned XML
ms.assetid: 6c5cb6c1-2921-4ba1-8100-0bf8074f9103
author: RothJa
ms.author: jroth
ms.openlocfilehash: b4683364ed4f2a27d5b9f25f3e368dfd40ef56aa
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474544"
---
# <a name="auto-mode-heuristics-in-shaping-returned-xml"></a>반환된 XML 모양 지정에서 AUTO 모드 추론

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

AUTO 모드는 쿼리를 기반으로 반환된 XML의 모양을 결정합니다. 요소 중첩 방법을 결정할 때 AUTO 모드 추론은 인접한 행의 열 값을 비교합니다. **ntext**, **text**, **image** 및 **xml** 을 제외한 모든 유형의 열이 비교됩니다. **(n)varchar(max)** 및 **varbinary(max)** 유형의 열이 비교됩니다.  
  
 다음 예에서는 결과 XML의 모양을 결정하는 AUTO 모드 추론에 대해 설명합니다.  
  
```sql
SELECT T1.Id, T2.Id, T1.Name  
FROM   T1, T2  
WHERE ...  
ORDER BY T1.Id
FOR XML AUTO;
```  
  
 테이블 T1의 키가 지정되지 않은 경우 새로운 <`T1`> 요소가 시작되는 위치를 확인하기 위해 **ntext**, **text**, **image** 및 **xml** 을 제외한 T1의 모든 열 값이 비교됩니다. 그런 다음 **Name** 열이 **nvarchar(40)** 이고 SELECT 문이 이 행 집합을 반환한다고 가정합니다.  
  
```  
T1.Id  T1.Name  T2.Id  
-----------------------  
1       Andrew    2  
1       Andrew    3  
1       Nancy     4  
```  
  
 AUTO 모드 추론은 테이블 T1, Id 및 Name 열의 모든 값을 비교합니다. 처음 두 행은 Id 및 Name 열에 대한 값이 같기 때문에 두 개의 \<T2> 자식 요소가 포함된 하나의 \<T1> 요소가 결과에 추가됩니다.  
  
 다음은 반환되는 XML입니다.  
  
```xml
<T1 Id="1" Name="Andrew">  
    <T2 Id="2" />  
    <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
      <T2 Id="4" />  
</T>  
```  
  
 이제 Name 열이 **text** 유형이라고 가정해 보십시오. AUTO 모드 추론은 이 유형의 값을 비교하지 않습니다. 그 대신 값이 같지 않다고 가정합니다. 그 결과 다음과 같이 XML이 생성됩니다.  
  
```xml
<T1 Id="1" Name="Andrew" >  
  <T2 Id="2" />  
</T1>  
<T1 Id="1" Name="Andrew" >  
  <T2 Id="3" />  
</T1>  
<T1 Id="1" Name="Nancy" >  
  <T2 Id="4" />  
</T1>  
```  
  
## <a name="see-also"></a>참고 항목  
 [FOR XML에서 AUTO 모드 사용](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
  
  
