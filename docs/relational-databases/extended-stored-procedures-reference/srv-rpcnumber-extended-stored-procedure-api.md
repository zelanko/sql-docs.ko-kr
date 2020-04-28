---
title: srv_rpcnumber(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcnumber
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcnumber
ms.assetid: 3094085e-fe9e-423d-bf87-7852352c2d26
author: rothja
ms.author: jroth
ms.openlocfilehash: c39074a8d1caf59d47990524a6030242ac33f95c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68005472"
---
# <a name="srv_rpcnumber-extended-stored-procedure-api"></a>srv_rpcnumber(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 현재 원격 저장 프로시저 호출에 대한 번호 구성 요소를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_rpcnumber ( SRV_PROC *  
srvproc   
)  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 원격 저장 프로시저를 수신한 핸들)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 애플리케이션과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
## <a name="returns"></a>반환  
 현재 원격 저장 프로시저에 대한 번호 구성 요소입니다. 클라이언트에서 원격 저장 프로시저를 실행할 때 번호 구성 요소를 사용하지 않거나 현재 원격 저장 프로시저가 없는 경우 -1이 반환됩니다.  
  
## <a name="remarks"></a>설명  
 이 함수는 원격 저장 프로시저의 번호 구성 요소만 반환합니다. 소유자, 원격 저장 프로시저 이름 및 데이터베이스 이름에 대한 선택적 지정자는 포함되지 않습니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
