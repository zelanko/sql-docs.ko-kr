---
title: "MSSQLSERVER_511 | Microsoft 문서"
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
- 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6f1ef308a5c84a9c0bdee065c67fcc3328798136
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver511"></a>MSSQLSERVER_511
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|511|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|ROW_TOOBIG|  
|메시지 텍스트|최대 허용 크기(%d)보다 큰 행(%d)을 만들 수 없습니다.|  
  
## <a name="explanation"></a>설명  
시도한 작업이 최대 행 크기를 초과했습니다. 일반적으로 최대 행 크기는 8,060바이트입니다. 데이터에 사용할 수 있는 행 크기를 줄일 수 있는 오버헤드가 일부 저장소 형식에 포함되어 있습니다. 예를 들어 스파스 열을 사용할 경우 최대 행 크기는 8,018바이트입니다. 행을 추가하거나 제거하는 일부 작업과 열의 데이터 형식을 변경하는 일부 작업을 수행하려면 데이터 페이지에서 행을 다시 작성한 다음 원래 행을 제거해야 합니다. 이 작업에서 유효한 행 크기 한계는 최대 한계의 절반입니다. 이는 원래 행과 수정된 행 모두 단기간 데이터 페이지에 포함되어 있어야 하기 때문입니다.  
  
## <a name="user-action"></a>사용자 동작  
가능하면 행 크기를 줄입니다.  
  
행을 현재 위치에서 업데이트한 결과로 문제가 발생한 경우 여러 단계를 수행하여 테이블을 변경해야 합니다. 새 테이블을 만들고 데이터를 새 테이블로 전송합니다. 그런 다음 원래 테이블을 삭제하고 새 테이블의 이름을 바꾸거나 원래 테이블을 자르고 원래 테이블의 행을 수정한 후 해당 테이블로 데이터를 다시 이동합니다.  
  

