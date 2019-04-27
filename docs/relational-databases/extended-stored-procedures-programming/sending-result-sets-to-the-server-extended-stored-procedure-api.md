---
title: 결과 집합 (확장 저장된 프로시저 API) 서버로 보내는 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ab77fa15bb4d3d1e68b8335a1c9026b1831a8619
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62742119"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>서버로 결과 집합 보내기(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 결과 집합을 보내면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 확장된 저장된 프로시저는 다음과 같이 적절 한 API를 호출 해야 합니다.  
  
-   합니다 **srv_sendmsg** 전이나 후 모든 행 (있는 경우)을 사용 하 여 보낸 순서에 관계 없이 함수를 호출할 수 있습니다 **srv_sendrow**합니다. 완료 상태를 사용 하 여 전송 되기 전에 클라이언트에 모든 메시지를 전송 해야 **srv_senddone**합니다.  
  
-   클라이언트로 보내는 각 행에 대해 한 번씩 **srv_sendrow** 함수를 호출합니다. 메시지, 상태 값 되기 전에 클라이언트에 모든 행을 보내야 또는 완료 상태와 함께 보낼 **srv_sendmsg**의 **srv_status** 인수의 **srv_pfield**, 또는 **srv_senddone**합니다.  
  
-   정의 된 모든 열에 있던 행을 보내면 **srv_describe** 응용 프로그램이 정보 오류 메시지를 발생 시키고 클라이언트에 FAIL을 반환 하도록 합니다. 이 경우 행이 전송되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [확장 저장 프로시저 만들기](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)  
  
  
