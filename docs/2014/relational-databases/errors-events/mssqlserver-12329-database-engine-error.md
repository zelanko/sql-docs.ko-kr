---
title: MSSQLSERVER_12329 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 12329 (Database Engine error)
ms.assetid: 43f90287-36d5-46c2-ac91-a37202dcf6d3
caps.latest.revision: 5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8fd526df2e17aea8935918b388d0965d49173cc3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407921"
---
# <a name="mssqlserver12329"></a>MSSQLSERVER_12329
    
## <a name="details"></a>설명  
  
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
  
  
