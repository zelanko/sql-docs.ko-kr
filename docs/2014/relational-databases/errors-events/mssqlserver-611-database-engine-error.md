---
title: MSSQLSERVER_611 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 634c86066508aae367f90ff6e00b452a81939967
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867327"
---
# <a name="mssqlserver611"></a>MSSQLSERVER_611
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|611|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|VAR_SIZE_TOO_BIG|  
|메시지 텍스트|오버헤드를 포함한 전체 변수 열 크기가 한도보다 큰 %d바이트이기 때문에 행을 삽입하거나 업데이트할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 최대 변수 열 크기가 스키마에서 허용하는 것보다 큽니다. VarDecimal 스토리지 형식을 사용할 때 변수 열 크기가 한도를 초과하거나, 변수 열 크기가 압축된 데이터 레코드에 대해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 허용하는 한도를 초과하면 오류 611이 반환됩니다.  
  
## <a name="user-action"></a>사용자 동작  
 레코드의 크기를 줄입니다.  
  
  
