---
title: srv_senddone(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_senddone
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_senddone
ms.assetid: 1fc4f1d5-56d4-43f6-b5e4-0c0cc295cba3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2bce064ee38082861e9b6c5d4f2c6e28bf41dded
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745524"
---
# <a name="srvsenddone-extended-stored-procedure-api"></a>srv_senddone(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 결과 완료 메시지를 클라이언트에게 보냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_senddone (  
SRV_PROC *  
srvproc  
,  
DBUSMALLINT   
status  
,  
DBUSMALLINT  
info  
,  
DBINT  
count   
);  
  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 언어 요청을 수신한 핸들)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 애플리케이션과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
 *상태*  
 다양한 *status* 플래그에 대한 2바이트 필드입니다. *status* 플래그 값에 AND 및 OR 논리 연산자를 사용하여 여러 플래그를 설정할 수 있습니다. 다음 표에서는 가능한 *status* 플래그를 보여 줍니다.  
  
|상태 플래그|Description|  
|-----------------|-----------------|  
|SRV_DONE_COUNT|*count* 매개 변수에 올바른 개수가 포함되어 있습니다.|  
|SRV_DONE_ERROR|현재 클라이언트 명령에 오류가 수신되었습니다.|  
  
 *info*  
 예약된 2바이트 필드입니다. 이 값을 0으로 설정합니다.  
  
 *count*  
 현재 결과 집합의 개수를 나타내는 데 사용되는 4바이트 필드입니다. *status* 필드에 SRV_DONE_COUNT 플래그를 설정하면 *count* 에 올바른 개수가 포함됩니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 클라이언트 요청으로 인해 서버에서 많은 명령을 실행하고 많은 결과 집합을 반환할 수 있습니다. 각 결과 집합에 대해 **srv_senddone** 에서 결과 완료 메시지를 클라이언트에 반환해야 합니다.  
  
 *count* 필드는 명령의 영향을 받는 행 수를 나타냅니다. *count* 필드에 개수가 포함되어 있는 경우 *status* 필드에 SRV_DONE_COUNT 플래그를 설정해야 합니다. 이 설정을 사용하면 클라이언트에서 *count* 값 0과 사용되지 않은 *count* 필드를 구분할 수 있습니다.  
  
 SRV_CONNECT 처리기에서 **srv_senddone** 을 호출하지 마십시오.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
