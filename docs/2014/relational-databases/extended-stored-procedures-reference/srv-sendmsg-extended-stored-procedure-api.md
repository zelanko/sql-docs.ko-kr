---
title: srv_sendmsg(확장 저장 프로시저 API) | Microsoft Docs
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
- srv_sendmsg
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_sendmsg
ms.assetid: efcb50b9-f8ff-4121-bf67-05830171b928
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 34575c3377c806b2671a2bdf92405864d0d5bf1b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181122"
---
# <a name="srvsendmsg-extended-stored-procedure-api"></a>srv_sendmsg(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 클라이언트에 메시지를 보냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_sendmsg (  
SRV_PROC *  
srvproc  
,  
int  
msgtype  
,  
DBINT  
msgnum  
,  
DBTINYINT  
class  
,   
DBTINYINT  
state  
,  
DBCHAR *  
rpcname  
,  
int   
rpcnamelen  
,  
DBUSMALLINT  
linenum  
,  
DBCHAR *  
message  
,  
int  
msglen   
);  
  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 언어 요청을 수신한 핸들)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 응용 프로그램과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
 *msgtype*  
 서버에서 정보 메시지 또는 오류 메시지를 보내는지에 따라 SRV_MSG_INFO 또는 SRV_MSG_ERROR가 됩니다.  
  
 *msgnum*  
 4바이트 메시지 번호입니다.  
  
 *class*  
 오류 심각도를 지정합니다. 심각도가 10보다 작거나 같으면 정보 메시지로 간주됩니다.  
  
 *state*  
 현재 메시지의 오류 상태 번호를 제공합니다. 이 오류 상태 번호는 오류의 컨텍스트에 대한 정보를 제공합니다. 유효한 상태 번호는 0에서 255까지입니다.  
  
 *rpcname*  
 현재 지원되지 않습니다.  
  
 *rpcnamelen*  
 현재 지원되지 않습니다.  
  
 *linenum*  
 언어 명령 일괄 처리에서 메시지가 적용되는 줄 번호입니다. 줄 번호는 1부터 시작하며 메시지에 *linenum*이 적용되지 않으면 0으로 설정됩니다.  
  
 *message*  
 클라이언트로 보낼 문자열에 대한 포인터입니다.  
  
 *msglen*  
 *message*의 길이(바이트)를 지정합니다. *message*가 Null로 끝나는 경우 *msglen*을 SRV_NULLTERM으로 설정합니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 클라이언트에 오류 메시지 또는 정보 메시지를 보내는 함수입니다. 보낼 각 메시지에 대해 한 번씩 호출됩니다.  
  
 **srv_sendrow**를 사용하여 모든 행(있는 경우)을 보내기 전후에 **srv_sendmsg**를 사용하여 순서에 상관없이 클라이언트에 메시지를 보낼 수 있습니다. **srv_senddone**을 사용하여 완료 상태를 보내기 전에는 모든 메시지(있는 경우)를 클라이언트로 보내야 합니다.  
  
 메시지를 유니코드로 보내려면 **srv_sendmsg** 대신 **srv_wsendmsg**를 사용합니다.  
  
 자세한 내용은 [유니코드 데이터 및 서버 코드 페이지](../extended-stored-procedures-programming/unicode-data-and-server-code-pages.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
  