---
title: srv_sendrow(확장 저장 프로시저 API) | Microsoft Docs
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
- srv_sendrow
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_sendrow
ms.assetid: a08f608a-10e6-4bff-9b48-0d02e8026cdb
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 39635048aead2326468259f7b10d023b85bcc1b7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182793"
---
# <a name="srvsendrow-extended-stored-procedure-api"></a>srv_sendrow(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 데이터 행을 클라이언트로 전송합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_sendrow ( SRV_PROC *  
srvproc   
);  
  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 언어 요청을 수신한 핸들)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 응용 프로그램과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 클라이언트로 보내는 각 행에 대해 한 번씩 **srv_sendrow** 함수를 호출합니다. **srv_sendmsg**, **srv_status**또는 **srv_senddone**을 사용하여 각각 메시지, 상태 값 또는 완료 상태를 보내기 전에 모든 행을 클라이언트로 보내야 합니다.  
  
 **srv_describe** 를 사용하여 정의되지 않은 열이 포함된 행을 보내면 확장 저장 프로시저 API 응용 프로그램에서 정보 오류 메시지를 발생시키고 클라이언트에 FAIL을 반환합니다. 이 경우 행이 전송되지 않습니다.  
  
> [!NOTE]  
>  확장 저장 프로시저 API를 통해서는 계산 행을 클라이언트로 보낼 수 없습니다. 또한 `ntext`, `text` 또는 `image` 데이터가 있는 행을 클라이언트로 보내는 경우 텍스트 포인터와 텍스트 타임스탬프는 제외됩니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [srv_describe(확장 저장 프로시저 API)](srv-describe-extended-stored-procedure-api.md)  
  
  