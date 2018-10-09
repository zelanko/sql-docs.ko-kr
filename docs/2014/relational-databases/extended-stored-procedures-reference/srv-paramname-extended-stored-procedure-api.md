---
title: srv_paramname(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- srv_paramname
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramname
ms.assetid: 1a53d707-7b06-49cc-a0df-ac727cfe953f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 65844bb9d810242381eabada835ceea5053ca414
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48114983"
---
# <a name="srvparamname-extended-stored-procedure-api"></a>srv_paramname(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 원격 저장 프로시저 호출 매개 변수의 이름을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DBCHAR * srv_paramname (  
SRV_PROC * srvproc,intn, int *len );  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 원격 저장 프로시저 호출을 수신한 핸들)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 응용 프로그램과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
 *n*  
 매개 변수의 번호를 나타냅니다. 첫 번째 매개 변수는 1입니다.  
  
 *len*  
 매개 변수 이름의 길이(바이트)를 포함하는 `int` 변수에 대한 포인터를 제공합니다. *len*이 NULL이면 원격 저장 프로시저 매개 변수 이름의 길이가 반환되지 않습니다.  
  
## <a name="returns"></a>반환 값  
 매개 변수 이름을 포함하는 null로 끝나는 문자열에 대한 포인터입니다. 매개 변수 이름의 길이는 *len*에 저장됩니다. *n*번째 매개 변수가 없거나 원격 저장 프로시저가 없으면 NULL을 반환하고 *len*이 -1로 설정되며 정보 오류 메시지가 전송됩니다. 매개 변수 이름이 NULL이면 *len*이 0으로 설정되고 null로 끝나는 빈 문자열이 반환됩니다.  
  
## <a name="remarks"></a>Remarks  
 이 함수는 원격 저장 프로시저 호출 매개 변수의 이름을 가져옵니다. 매개 변수를 사용하여 원격 저장 프로시저를 호출하는 경우 매개 변수를 이름 또는 위치(이름 없음)로 전달할 수 있습니다. 일부 매개 변수는 이름으로 전달하고 일부 매개 변수는 위치로 전달하여 원격 저장 프로시저를 호출하면 오류가 발생합니다. 이 경우에도 SRV_RPC 핸들러는 호출되지만 매개 변수가 없는 것과 같이 처리되며 **srv_rpcparams**는 0을 반환합니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [srv_rpcparams(확장 저장 프로시저 API)](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
