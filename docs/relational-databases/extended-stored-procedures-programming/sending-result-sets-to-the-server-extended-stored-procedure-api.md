---
title: 결과 집합 (확장 저장된 프로시저 API) 서버에 보내기 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c5285cbe8160de3fc7b53d1d8660a3dd24fa2920
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>서버로 결과 집합 보내기(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 결과 집합을 보낼 때 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 확장된 저장된 프로시저는 다음과 같이 적절 한 API를 호출 해야 합니다.  
  
-   **srv_sendmsg** 이전 또는 이후 모든 행 (있는 경우)으로 전송 된 순서에 관계 없이 함수를 호출할 수 있습니다 **srv_sendrow**합니다. 완료 상태를 보내기 전에 클라이언트에 모든 메시지를 전송 합니다 **srv_senddone**합니다.  
  
-   클라이언트로 보내는 각 행에 대해 한 번씩 **srv_sendrow** 함수를 호출합니다. 메시지, 상태 값 하기 전에 클라이언트에 모든 행을 보내야 합니다 또는 완료 상태 **srv_sendmsg**, **srv_status** 의 인수 **srv_pfield**, 또는 **srv_senddone**합니다.  
  
-   정의 된 모든 열에 있던 행을 보내는 **srv_describe** 응용 프로그램이 정보 오류 메시지를 발생 시키고 클라이언트에 FAIL을 반환 합니다. 이 경우 행이 전송되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [확장 저장 프로시저 만들기](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)  
  
  
