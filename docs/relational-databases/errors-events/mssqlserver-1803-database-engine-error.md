---
title: "MSSQLSERVER_1803 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f14c8fb9f7ec553478ad378764265a13b783a0c5
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver1803"></a>MSSQLSERVER_1803
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|1803|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|NO_SPACE|  
|메시지 텍스트|CREATE DATABASE가 실패했습니다. model 데이터베이스의 복사본을 수용하려면 주 파일이 최소한 %dMB여야 합니다.|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 모델 데이터베이스의 복사본을 만들어 데이터베이스를 만듭니다. 그런 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 복사본의 이름을 바꾸고 새 데이터베이스를 요청된 크기로 확대합니다. 이 경우 사용자가 model 데이터베이스보다 작은 데이터베이스를 만들려고 시도했습니다. 그러나 model 데이터베이스 복사본이 주 데이터 파일에 맞지 않거나 파일이 model 데이터베이스보다 작기 때문에 이 작업이 실패했습니다.  
  
## <a name="user-action"></a>사용자 동작  
더 큰 데이터베이스 파일 크기를 사용하여 데이터베이스를 만듭니다. 그런 다음 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 DBCC SHRINKDATABASE 문을 사용하여 원하는 경우 데이터베이스를 축소합니다.  
  

