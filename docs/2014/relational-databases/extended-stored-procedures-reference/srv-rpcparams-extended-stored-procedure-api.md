---
title: srv_rpcparams(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- srv_rpcparams
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcparams
ms.assetid: 96a5e6f6-d320-4623-b96e-0a856e3abebb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b99010c8d4ece2811c8b98b588489b874501544e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069883"
---
# <a name="srvrpcparams-extended-stored-procedure-api"></a>srv_rpcparams(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 현재 원격 저장 프로시저의 매개 변수 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_rpcparams ( SRV_PROC *  
srvproc   
);  
  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 원격 저장 프로시저를 수신한 핸들)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 애플리케이션과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
## <a name="returns"></a>반환 값  
 원격 저장 프로시저의 매개 변수 수. 현재 원격 저장 프로시저가 없거나 원격 저장 프로시저에 매개 변수가 없으면 -1이 반환되고 알림 오류가 발생합니다.  
  
## <a name="remarks"></a>Remarks  
 이 함수는 현재 원격 저장 프로시저의 매개 변수의 수를 반환하며 일반적으로 원격 저장 프로시저에서 호출됩니다.  
  
 매개 변수를 사용하여 원격 저장 프로시저를 호출하는 경우 매개 변수를 이름 또는 위치(이름 없음)로 전달할 수 있습니다. 일부 매개 변수는 이름으로 전달하고 일부 매개 변수는 위치로 전달하여 원격 저장 프로시저를 호출하면 오류가 발생합니다. 이 오류가 발생하면 원격 저장 프로시저 처리기가 호출되지만 이 처리기에 매개 변수가 전달되지 않고 **srv_rpcparams**가 0을 변환합니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
