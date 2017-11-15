---
title: "MSSQLSERVER_21898 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 21898 (Database Engine error)
ms.assetid: 02405b21-3d4e-4c2d-b4b3-d7b1ec05edb4
caps.latest.revision: "6"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 0390684964b318e6c2add660a54f5b3e30c61c37
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver21898"></a>MSSQLSERVER_21898
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21898|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQLErrorNum21898|  
|메시지 텍스트|게시자 '%s'이(가) 배포 데이터베이스 '%s'을(를) 사용하며, 게시 데이터베이스 '%s'을(를) 호스팅하는 데 필요한 '%s'이(가) 아닙니다. 배포자 '%s'에서 **sp_changedistpublisher**를 실행하여 게시자가 사용하는 배포 데이터베이스를 '%s'(으)로 변경하세요.|  
  
## <a name="explanation"></a>설명  
**sp_validate_redirected_publisher**는 로컬 배포자에서 msdb.dbo.MSdistpublishers를 쿼리하여 새 게시자가 사용하는 배포 데이터베이스가 원래 게시자에 사용된 배포 데이터베이스와 동일한지 확인합니다. 이 오류는 이 두 데이터베이스가 서로 달라 게시자가 게시자 데이터베이스에 대한 적합한 호스트가 될 수 없는 경우에 반환됩니다.  
  
## <a name="user-action"></a>사용자 동작  
**sp_changedistpublisher** 저장 프로시저를 실행하여 새 게시자의 배포 데이터베이스를 원래 게시자에 사용된 배포 데이터베이스로 변경합니다.  
  
> [!NOTE]  
> 배포자에서 게시자에 대해 **sp_adddistpublisher**를 실행할 때 잘못된 배포 데이터베이스를 입력한 경우 **sp_changedistpublisher**를 실행하면 문제가 해결됩니다. 그러나 원격 게시자에 식별된 배포 데이터베이스를 사용하는 다른 게시 데이터베이스의 기존 게시가 있는 경우에는 이와 같은 변경이 적절하지 않습니다. 명명된 배포 데이터베이스를 사용하는 복제를 체계적으로 제거한 다음 원래 게시자의 배포 데이터베이스를 사용하여 데이터베이스를 다시 설정해야만 새 게시자가 적합한 호스트로 작동할 수 있습니다.  
  
