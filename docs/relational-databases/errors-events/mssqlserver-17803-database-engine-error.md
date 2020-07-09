---
title: MSSQLSERVER_17803 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17803 (Database Engine error)
ms.assetid: 28591a19-258d-4891-b78a-4686789bb2d7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ac4c4c08c13a700e795ddad0901c0c43829d623f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780749"
---
# <a name="mssqlserver_17803"></a>MSSQLSERVER_17803
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|17803|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SRV_NOMEMORY|  
|메시지 텍스트|연결 설정 중 메모리 할당에 실패했습니다. 필요하지 않은 메모리 로드를 줄이거나 시스템 메모리를 늘리십시오. 연결이 닫혔습니다.%.*ls|  
  
## <a name="explanation"></a>설명  
서버에 메모리가 부족합니다.  
  
## <a name="user-action"></a>사용자 동작  
서버에 메모리가 부족한 원인을 확인합니다. 일반적인 메모리 문제 해결 단계가 유용할 수 있습니다.  
  
