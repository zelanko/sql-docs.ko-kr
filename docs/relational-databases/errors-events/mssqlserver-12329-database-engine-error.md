---
title: MSSQLSERVER_12329 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 12329 (Database Engine error)
ms.assetid: 43f90287-36d5-46c2-ac91-a37202dcf6d3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 404f414a1f4bfe75c3476e0954e810c4b36ddaa3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002904"
---
# <a name="mssqlserver12329"></a>MSSQLSERVER_12329
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|12329|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|HK_UNSUPPORTED_NON_LATIN_CODEPAGE|  
|메시지 텍스트|1252가 아닌 코드 페이지가 있는 데이터 정렬을 사용하는 데이터 형식 char(n) 및 varchar(n)는 *construct*에서 지원되지 않습니다.|  
  
## <a name="explanation"></a>설명  
1252가 아닌 코드 페이지가 있는 데이터 정렬을 사용하는 데이터 형식 char(n) 및 varchar(n)를 사용하지 마십시오.  
  
## <a name="user-action"></a>사용자 동작  
이 오류를 발생시킬 수 있는 예기치 않은 한 가지 상황은 다음과 같습니다.  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = 'us_english')  
```  
  
대신 다음을 사용하십시오.  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
```  
  
