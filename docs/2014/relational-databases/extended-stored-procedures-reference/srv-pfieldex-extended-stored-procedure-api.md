---
title: srv_pfieldex(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_pfieldex
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_pfieldex
ms.assetid: d4e9a34b-b3a3-434f-8556-768bd20d145a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8bacfd4f955f60b17b439c8066a3b1cba2c52392
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63126949"
---
# <a name="srv_pfieldex-extended-stored-procedure-api"></a>srv_pfieldex(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]대신 CLR 통합을 사용 하세요.  
  
 요청한 SRV_PROC 필드가 포함된 데이터에 대한 포인터를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
void *srv_pfieldex(SRV_PROC *   
srvproc  
, int   
field  
, int *   
len  
);  
  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 애플리케이션과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
 *필드가*  
 반환할 *srvproc* 필드를 지정합니다.  
  
|필드|Description|반환 형식|  
|-----------|-----------------|------------------|  
|SRV_MSGLCID|현재 세션 메시지 LCID입니다.|ULONG*|  
|SRV_INSTANCENAME|인스턴스 이름(명명된 경우)을 반환하거나, 그렇지 않으면 NULL을 반환합니다.|WCHAR*|  
  
 *길이가*  
 반환된 **field** 값의 길이(바이트)가 포함된 *int* 변수에 대한 포인터입니다. 
  *len*이 NULL이면 길이가 반환되지 않습니다. NULL이 반환되면 **len*이 0으로 설정됩니다.  
  
## <a name="returns"></a>반환  
 
  *field*에 따라 형식이 결정되는 데이터에 대한 포인터입니다. 
  *len*이 NULL이거나 *srvproc*가 NULL이면 NULL이 반환됩니다. 
  *field*를 알 수 없으면 NULL이 반환됩니다. NULL이 반환되면 **len*이 0으로 설정됩니다.  
  
> [!IMPORTANT]  
>  서버에서 반환되는 버퍼는 읽기 전용이어야 합니다. 그렇지 않으면 서버 상태가 손상될 수 있습니다.  
  
## <a name="remarks"></a>설명  
 **보안 정보** 확장 저장 프로시저의 원본 코드를 철저히 검토 하 고 프로덕션 서버에 설치 하기 전에 컴파일된 Dll을 테스트 해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
