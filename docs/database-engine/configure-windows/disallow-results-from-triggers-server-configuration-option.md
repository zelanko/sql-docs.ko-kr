---
title: disallow results from triggers 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], result sets
- result sets [SQL Server], triggers
- disallow results from triggers option
ms.assetid: 47149073-307d-47a5-b7d2-66a737d3231d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 28bf3b201d54798f26c9e887e86a9d0bed78ee15
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68011864"
---
# <a name="disallow-results-from-triggers-server-configuration-option"></a>disallow results from triggers 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **disallow results from triggers** 옵션을 사용하여 트리거에서 결과 집합을 반환하는지 여부를 제어할 수 있습니다. 결과 집합을 반환하는 트리거는 트리거가 작동하지 않는 애플리케이션에 예기치 않은 동작을 유발할 수도 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 이 값을 1로 설정하는 것이 좋습니다.  
  
 1로 설정하면 **disallow results from triggers** 옵션이 ON으로 설정됩니다. 이 옵션의 기본 설정은 0(OFF)입니다. 이 옵션을 1(ON)로 설정하면 트리거가 결과 집합을 반환하지 못하며 사용자에게 다음 오류 메시지가 표시됩니다.  
  
 "메시지 524, 수준 16, 상태 1, 프로시저 \<프로시저 이름>, 줄 \<줄#>  
  
 "트리거가 결과 집합을 반환했으며 서버 옵션 'disallow_results_from_triggers'가 True입니다."  
  
 **disallow results from triggers** 옵션은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 수준에서 적용되며 인스턴스에 있는 기존의 모든 트리거에 대한 동작을 결정합니다.  
  
 **disallow results from triggers** 옵션은 고급 옵션입니다. **sp_configure** 시스템 저장 프로시저를 사용하여 설정을 변경하는 경우 **show advanced options** 를 1로 설정할 때만 disallow results from triggers를 변경할 수 있습니다. 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
