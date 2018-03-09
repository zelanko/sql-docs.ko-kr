---
title: "srv_rpcparams(확장 저장 프로시저 API) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
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
- srv_rpcparams
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcparams
ms.assetid: 96a5e6f6-d320-4623-b96e-0a856e3abebb
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cffcb229c0701ace61ac26a2a47c67d13a4591fd
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="srvrpcparams-extended-stored-procedure-api"></a>srv_rpcparams(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 현재 원격 저장 프로시저의 매개 변수 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_rpcparams ( SRV_PROC *  
srvproc   
);  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 원격 저장 프로시저를 수신한 핸들)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 응용 프로그램과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
## <a name="returns"></a>반환 값  
 원격 저장 프로시저의 매개 변수 수. 현재 원격 저장 프로시저가 없거나 원격 저장 프로시저에 매개 변수가 없으면 -1이 반환되고 알림 오류가 발생합니다.  
  
## <a name="remarks"></a>Remarks  
 이 함수는 현재 원격 저장 프로시저의 매개 변수의 수를 반환하며 일반적으로 원격 저장 프로시저에서 호출됩니다.  
  
 매개 변수를 사용하여 원격 저장 프로시저를 호출하는 경우 매개 변수를 이름 또는 위치(이름 없음)로 전달할 수 있습니다. 일부 매개 변수는 이름으로 전달하고 일부 매개 변수는 위치로 전달하여 원격 저장 프로시저를 호출하면 오류가 발생합니다. 이 오류가 발생하면 원격 저장 프로시저 처리기가 호출되지만 이 처리기에 매개 변수가 전달되지 않고 **srv_rpcparams**가 0을 변환합니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
