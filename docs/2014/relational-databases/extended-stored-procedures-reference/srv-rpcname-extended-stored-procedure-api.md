---
title: srv_rpcname(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcname
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcname
ms.assetid: 0a1424e4-3319-4836-b8d8-5e0344cc683f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f309349b2867412d552372e83ed1947b34242336
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046652"
---
# <a name="srvrpcname-extended-stored-procedure-api"></a>srv_rpcname(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 현재 원격 저장 프로시저에 대한 프로시저 이름 구성 요소를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DBCHAR * srv_rpcname (  
SRV_PROC *  
srvproc  
,  
int *  
len   
);  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 원격 저장 프로시저를 수신한 핸들)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 애플리케이션과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
 *len*  
 데이터베이스 이름의 길이를 받는 정수 변수에 대한 포인터입니다. *len* 이 NULL이면 원격 저장 프로시저 이름의 길이가 반환되지 않습니다.  
  
## <a name="returns"></a>반환 값  
 현재 원격 저장 프로시저의 원격 저장 프로시저 이름 구성 요소의 null로 끝나는 문자열에 대한 DBCHAR 포인터입니다. 현재 원격 저장 프로시저가 없으면 NULL이 반환되고 *len* 이 -1로 설정됩니다.  
  
## <a name="remarks"></a>Remarks  
 이 함수는 원격 저장 프로시저의 이름만 반환합니다. 소유자, 데이터베이스 이름 및 원격 저장 프로시저 번호에 대한 선택적 지정자는 포함되지 않습니다.  
  
 원격 저장 프로시저가 없는 경우에도 **srv_rpcname** 을 호출할 수 있으므로(정보 오류가 발생하지 않음) 이 함수를 사용하여 원격 저장 프로시저가 있는지 여부를 확인할 수 있습니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
