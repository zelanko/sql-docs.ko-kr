---
description: 스크롤 가능 커서 및 트랜잭션 격리
title: 스크롤 가능 커서 및 트랜잭션 격리 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 790b2d0c4d80c821645c3a4360d1295cc55a8a4e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476505"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>스크롤 가능 커서 및 트랜잭션 격리
다음 표에서는 변경 내용에 대 한 표시 여부를 제어 하는 요소를 보여 줍니다.  
  
|다음에서 변경한 내용:|표시 여부는 다음에 따라 달라 집니다.|  
|----------------------|----------------------------|  
|커서|커서 유형, 커서 구현|  
|동일한 트랜잭션의 다른 문|커서 유형|  
|다른 트랜잭션의 문|커서 유형, 트랜잭션 격리 수준|  
  
 이러한 요소는 다음 그림에 나와 있습니다.  
  
 ![변경 내용 표시를 제어하는 요소](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 다음 표에서는 각 커서 유형의 변경 내용을 검색 하는 기능, 자체 트랜잭션의 다른 작업 및 기타 트랜잭션에 대해 간략하게 설명 합니다. 후자 변경을 표시 하는 방법은 커서 유형 및 커서를 포함 하는 트랜잭션의 격리 수준에 따라 달라 집니다.  
  
|커서 type\action|자체|자체<br /><br /> 트랜잭션|기타<br /><br /> 트랜잭션<br /><br /> ([A])|기타<br /><br /> 트랜잭션<br /><br /> (RC [a])|기타<br /><br /> 트랜잭션<br /><br /> (RR [a])|기타<br /><br /> 트랜잭션<br /><br /> (S [a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|정적|||||||  
|Insert|아마도 [b]|예|예|예|예|예|  
|업데이트|아마도 [b]|예|예|예|예|예|  
|DELETE|아마도 [b]|예|예|예|예|예|  
|키 집합|||||||  
|Insert|아마도 [b]|예|예|예|예|예|  
|업데이트|예|예|예|예|예|예|  
|DELETE|아마도 [b]|예|예|예|예|예|  
|동적|||||||  
|Insert|예|예|예|예|예|예|  
|업데이트|예|예|예|예|예|예|  
|삭제|예|예|예|예|예|예|  
  
 [a] 괄호 안의 문자는 커서를 포함 하는 트랜잭션의 격리 수준을 의미 합니다. 변경 내용이 적용 된 다른 트랜잭션의 격리 수준은 관련이 없습니다.  
  
 R u: 커밋되지 않은 읽기  
  
 RC: 커밋된 읽기  
  
 RR: 반복 가능한 읽기  
  
 S: Serializable  
  
 [b]는 커서 구현 방법에 따라 달라 집니다. 커서가 이러한 변경 내용을 검색할 수 있는지 여부는 **SQLGetInfo**의 SQL_STATIC_SENSITIVITY 옵션을 통해 보고 됩니다.
