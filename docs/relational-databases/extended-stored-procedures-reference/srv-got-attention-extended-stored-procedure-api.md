---
title: "srv_got_attention(확장 저장 프로시저 API) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- srv_got_attention
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_got_attention
ms.assetid: 805e68e1-d17f-41bd-8b9f-a27283bb6fbe
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 541d9ebe6bb7752a9025f65f1570df28f253bb88
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="srvgotattention-extended-stored-procedure-api"></a>srv_got_attention(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 현재 연결 또는 태스크를 중단해야 하는지 확인하고 연결이 끊기거나 일괄 처리가 중단되면 TRUE를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL srv_got_attention (SRV_PROC *   
srvproc  
);  
```  
  
#### <a name="parameters"></a>매개 변수  
 *srvproc*  
 데이터베이스 연결을 식별하는 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
 연결이 끊기거나 일괄 처리가 중단되면 TRUE입니다. 연결 또는 일괄 처리가 활성 상태이면 FALSE입니다.  
  
## <a name="remarks"></a>Remarks  
 장기 실행 확장 저장 프로시저는 연결이 끊기거나 일괄 처리가 중단될 경우 프로시저가 자동으로 종료될 수 있도록 주기적으로 **srv_got_attention**을 호출하여 서버 상태를 확인해야 합니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
