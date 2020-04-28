---
title: 서버로 결과 집합 보내기(확장 저장 프로시저 API)
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
ms.custom: seo-dt-2019
ms.openlocfilehash: 4a54ad922e7033737ccd256c1b3a0a34f543a6dd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74095940"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>서버로 결과 집합 보내기(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]결과 집합을 보낼 때 확장 저장 프로시저는 다음과 같이 적절 한 API를 호출 해야 합니다.  
  
-   **Srv_sendmsg** 함수는 **srv_sendrow**를 사용 하 여 모든 행 (있는 경우)이 전송 되기 전이나 후에 순서에 관계 없이 호출 될 수 있습니다. **Srv_senddone**를 사용 하 여 완료 상태를 보내기 전에 모든 메시지를 클라이언트로 보내야 합니다.  
  
-   클라이언트로 보내는 각 행에 대해 한 번씩 **srv_sendrow** 함수를 호출합니다. 메시지, 상태 값 또는 완료 상태가 **srv_sendmsg**, **srv_pfield**의 **srv_status** 인수 또는 **srv_senddone**를 전송 하기 전에 모든 행을 클라이언트로 보내야 합니다.  
  
-   **Srv_describe** 를 사용 하 여 정의 된 모든 열이 없는 행을 보내면 응용 프로그램에서 정보 오류 메시지를 발생 시키고 클라이언트에 FAIL을 반환 합니다. 이 경우 행이 전송되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [확장 저장 프로시저 만들기](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)  
  
  
