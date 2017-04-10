---
title: "OLE 자동화 결과 집합 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-ole"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "데이터 형식 [SQL Server], OLE 자동화"
  - "2차원 배열"
  - "1차원 배열"
  - "결과 집합 [SQL Server], OLE 자동화"
  - "OLE 자동화 [SQL Server], 결과 집합"
  - "배열 [SQL Server]"
ms.assetid: b2f99e33-2303-427c-94b9-9d55f8e2a6ab
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# OLE 자동화 결과 집합
  OLE 자동화 속성 또는 메서드에서 1차원 또는 2차원 배열로 데이터를 반환하면 해당 배열은 클라이언트에 결과 집합으로 반환됩니다.  
  
-   1차원 배열은 배열 내 요소 수만큼의 열이 포함된 단일 행 결과 집합으로 클라이언트에게 반환됩니다. 예를 들어 array(10)는 10개의 열이 포함된 단일 행으로 반환됩니다.  
  
-   2차원 배열은 배열의 첫 번째 차원에 있는 요소 수만큼의 열과 두 번째 차원에 있는 요소 수만큼의 행이 포함된 결과 집합으로 클라이언트에게 반환됩니다. 예를 들어 array(2,3)는 2개의 열과 3개의 행으로 반환됩니다.  
  
 속성 반환 값이나 메서드 반환 값이 배열인 경우 sp_OAGetProperty나 sp_OAMethod가 결과 집합을 클라이언트에 반환합니다. (메서드 출력 매개 변수는 배열이 될 수 없습니다) 이러한 프로시저는 배열의 모든 데이터 값을 검색하여 결과 집합의 각 열에 알맞은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식과 데이터 길이를 결정합니다. 특정 열에 대해서는 이러한 프로시저에서 해당 열의 모든 데이터 값을 나타내기 위해 필요한 데이터 형식과 길이를 사용합니다.  
  
 하나의 열에 있는 모든 데이터 값이 같은 데이터 형식을 공유하는 경우에는 해당 데이터 형식이 전체 열에 대해 사용됩니다. 한 열의 여러 데이터 값이 다른 데이터 형식을 사용하는 경우에는 다음 표를 기준으로 전체 열의 데이터 형식이 선택됩니다. 다음 표를 사용하려면 왼쪽 행 축에 나열된 데이터 형식 중 하나를 찾은 다음 두 번째 데이터 형식으로 위쪽 열 축에 나열된 데이터 형식을 찾습니다. 행과 열이 교차하는 위치에 결과 집합 열의 데이터 형식이 설명되어 있습니다.  
  
||||||||  
|-|-|-|-|-|-|-|  
||**int**|**float**|**money**|**datetime**|**varchar**|**nvarchar**|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## 관련 내용  
 [OLE 자동화 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
 [Ole Automation Procedures 서버 구성 옵션](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  
  
  