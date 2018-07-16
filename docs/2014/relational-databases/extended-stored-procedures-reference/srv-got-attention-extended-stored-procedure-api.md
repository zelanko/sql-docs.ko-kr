---
title: srv_got_attention(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- srv_got_attention
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_got_attention
ms.assetid: 805e68e1-d17f-41bd-8b9f-a27283bb6fbe
caps.latest.revision: 17
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d7d6f026b9c851c7fb8636442cfda27a870be861
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201403"
---
# <a name="srvgotattention-extended-stored-procedure-api"></a>srv_got_attention(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 현재 연결 또는 태스크를 중단해야 하는지 확인하고 연결이 끊기거나 일괄 처리가 중단되면 TRUE를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL srv_got_attention  
(SRV_PROC *  
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
  
  
