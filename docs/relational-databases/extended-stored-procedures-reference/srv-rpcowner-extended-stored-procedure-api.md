---
title: srv_rpcowner(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- srv_rpcowner
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcowner
ms.assetid: e81a60e6-14ea-47bc-a11c-3d7635344447
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 64ee7f8ad02c141a35cb3bc1cd2f5a599a229f4c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696291"
---
# <a name="srvrpcowner-extended-stored-procedure-api"></a>srv_rpcowner(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 현재 원격 저장 프로시저에 대한 소유자 구성 요소를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DBCHAR * srv_rpcowner (  
SRV_PROC *  
srvproc  
,  
int *  
len   
);  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 원격 저장 프로시저를 수신한 핸들)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 응용 프로그램과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
 *len*  
 소유자 이름의 길이를 받는 정수 변수에 대한 포인터입니다. *len* 매개 변수는 NULL일 수 있으며, 이 경우 소유자 구성 요소의 길이가 반환되지 않습니다.  
  
## <a name="returns"></a>반환 값  
 현재 원격 저장 프로시저의 Null로 끝나는 소유자 구성 요소에 대한 DBCHAR 포인터입니다. 현재 원격 저장 프로시저가 없으면 NULL이 반환되고 *len*이 -1로 설정됩니다.  
  
## <a name="remarks"></a>Remarks  
 이 함수는 원격 저장 프로시저의 소유자 구성 요소만 반환합니다. 이름, 원격 저장 프로시저 이름 및 원격 저장 프로시저 번호에 대한 선택적 지정자는 포함되지 않습니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
