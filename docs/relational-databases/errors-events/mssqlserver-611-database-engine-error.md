---
title: MSSQLSERVER_611 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e118451f77e736da34edad35d7e1c64ec95bad37
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34324994"
---
# <a name="mssqlserver611"></a>MSSQLSERVER_611
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|611|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|VAR_SIZE_TOO_BIG|  
|메시지 텍스트|오버헤드를 포함한 전체 변수 열 크기가 한도보다 큰 %d바이트이기 때문에 행을 삽입하거나 업데이트할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
최대 변수 열 크기가 스키마에서 허용하는 것보다 큽니다. VarDecimal 저장소 형식을 사용할 때 변수 열 크기가 한도를 초과하거나, 변수 열 크기가 압축된 데이터 레코드에 대해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 허용하는 한도를 초과하면 오류 611이 반환됩니다.  
  
## <a name="user-action"></a>사용자 동작  
레코드의 크기를 줄입니다.  
  
