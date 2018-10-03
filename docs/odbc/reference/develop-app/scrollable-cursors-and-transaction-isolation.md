---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5510eb58315f70195eb40390edec1766c350fb6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662351"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>스크롤 가능 커서 및 트랜잭션 격리
다음 표에서 변경 내용의 표시 유형을 제어 하는 요소를 나열 합니다.  
  
|수행한 변경 내용:|표시 여부에 따라 달라 집니다.|  
|----------------------|----------------------------|  
|커서|커서 유형을 커서 구현|  
|동일한 트랜잭션에서 다른 문|커서 유형|  
|다른 트랜잭션의 문|커서 유형을 트랜잭션 격리 수준|  
  
 이러한 요소는 다음 그림에 표시 됩니다.  
  
 ![변경 내용 표시를 제어 하는 요인](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 다음 표에서 자체적으로, 해당 트랜잭션의 다른 작업 및 다른 트랜잭션에 의해 변경 내용을 검색 하는 각 커서 유형의 기능을 보여 줍니다. 두 번째 변경 내용 표시 커서 유형 및 커서가 있는 트랜잭션의 격리 수준에 따라 달라 집니다.  
  
|커서 type\action|자체|소유<br /><br /> 트랜잭션 수|수도<br /><br /> 트랜잭션 수<br /><br /> (RU[a])|수도<br /><br /> 트랜잭션 수<br /><br /> (RC[a])|수도<br /><br /> 트랜잭션 수<br /><br /> (RR[a])|수도<br /><br /> 트랜잭션 수<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|정적|||||||  
|Insert|Maybe [b]|아니요|아니요|아니요|아니요|아니요|  
|Update|Maybe [b]|아니요|아니요|아니요|아니요|아니요|  
|DELETE|Maybe [b]|아니요|아니요|아니요|아니요|아니요|  
|키 집합|||||||  
|Insert|Maybe [b]|아니요|아니요|아니요|아니요|아니요|  
|Update|사용자 계정 컨트롤|예|예|예|아니오|아니요|  
|DELETE|Maybe [b]|사용자 계정 컨트롤|예|예|아니오|아니요|  
|Dynamic|||||||  
|Insert|사용자 계정 컨트롤|예|예|예|예|아니요|  
|Update|사용자 계정 컨트롤|예|예|예|아니오|아니요|  
|DELETE|사용자 계정 컨트롤|예|예|예|아니오|아니요|  
  
 [a] 괄호 문자는 커서를 포함 하는 트랜잭션의 격리 수준을 나타냅니다 (에 변경 된) 다른 트랜잭션 격리 수준을 관련이 없습니다.  
  
 커밋되지 않은 RU: 읽기  
  
 Read committed에 RC의 경우:  
  
 RR: 반복 가능한 읽기  
  
 S: 직렬화 가능  
  
 [b] 커서 구현 방법에 따라 달라 집니다. SQL_STATIC_SENSITIVITY 옵션을 통해 보고 됩니다 커서가 이러한 변경 내용을 검색할 수 있는지 여부 **SQLGetInfo**합니다.
