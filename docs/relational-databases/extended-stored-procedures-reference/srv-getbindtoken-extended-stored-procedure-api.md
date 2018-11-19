---
title: srv_getbindtoken(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_getbindtoken
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_getbindtoken
ms.assetid: c947d011-08ac-4fb8-b925-3da6e0999277
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 04d0993fc8e0a84d001dfd7e899dedf6ecc8dde2
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51655632"
---
# <a name="srvgetbindtoken-extended-stored-procedure-api"></a>srv_getbindtoken(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 현재 클라이언트 세션의 트랜잭션에서 확장 저장 프로시저를 호출하는 바인드 토큰을 가져옵니다.  
  
 바인드 토큰을 가져오면 확장 저장 프로시저는 **sp_bindsession**을 사용하여 같은 서버에 대해 새로 만드는 모든 세션을 기존 트랜잭션에 바인딩할 수 있습니다. 이렇게 하면 새 세션은 확장 저장 프로시저를 호출한 클라이언트 세션과 동일한 트랜잭션 잠금 공간을 공유할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_getbindtoken (  
SRV_PROC*  
srvproc  
,  
char*  
bindtoken  
);  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 응용 프로그램과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 모든 정보가 들어 있습니다.  
  
 *bindtoken*  
 바인드 토큰이 복사될 버퍼에 대한 포인터입니다. 바인드 토큰은 null로 끝나는 문자열로 표현됩니다. 지정하는 버퍼의 길이는 255바이트 이상이어야 합니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
  
### <a name="to-bind-an-extended-stored-procedure-session-to-the-client-session-that-called-it-so-they-share-the-same-transaction-lock-space"></a>동일한 트랜잭션 잠금 공간을 공유하도록 확장 저장 프로시저를 호출한 클라이언트 세션에 확장 저장 프로시저 세션을 바인딩하려면  
  
1.  확장 저장 프로시저에서 **svr_getbindtoken**을 호출하여 세션의 현재 트랜잭션에 대한 바인드 토큰을 가져옵니다. 토큰은 지정된 *bindtoken* 매개 변수로 반환됩니다.  
  
2.  확장 저장 프로시저에서 동일한 서버에 대해 새로운 세션을 엽니다. 이 세션에서 확장 저장 프로시저는 **sp_bindsession**에 바인드 토큰을 사용하여 새 세션을 동일한 트랜잭션에 바인딩합니다. 확장 저장 프로시저에서는 세션을 여러 개 만든 다음 모든 세션을 같은 트랜잭션에 바인딩할 수 있습니다.  
  
3.  외부 저장 프로시저가 반환되거나, 빈 문자열을 사용하여 **sp_bindsession**을 호출하면 바인딩된 세션이 바인딩 해제됩니다.  
  
    > [!NOTE]  
    >  한 번에 하나의 바인딩된 세션만 공유 연결에 액세스할 수 있습니다. 특정 세션이 서버에서 문을 실행하고 있거나, 서버로부터 보류 중인 결과가 있으면 바인딩된 동일한 연결을 공유하는 다른 세션에서는 현재 세션이 현재 문의 실행을 완료할 때까지 서버에 액세스할 수 없습니다. 서버가 작업 중일 때 특정 세션이 연결에 액세스하려고 시도하면 연결이 사용 중이므로 나중에 다시 시도하라는 오류가 해당 세션에 반환됩니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [sp_bindsession&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [sp_getbindtoken&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)  
  
  
