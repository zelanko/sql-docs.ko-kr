---
title: srv_pfieldex(확장 저장 프로시저 API) | Microsoft Docs
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
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 77ce8845cce63eb942c57c45d60dc56ce500f73b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091725"
---
# <a name="srvpfieldex-extended-stored-procedure-api"></a>srv_pfieldex(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
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
 특정 클라이언트 연결에 대한 핸들인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 응용 프로그램과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
 *field*  
 반환할 *srvproc* 필드를 지정합니다.  
  
|필드|Description|반환 형식|  
|-----------|-----------------|------------------|  
|SRV_MSGLCID|현재 세션 메시지 LCID입니다.|ULONG*|  
|SRV_INSTANCENAME|인스턴스 이름(명명된 경우)을 반환하거나, 그렇지 않으면 NULL을 반환합니다.|WCHAR*|  
  
 *len*  
 반환된 *field* 값의 길이(바이트)가 포함된 **int** 변수에 대한 포인터입니다. *len*이 NULL이면 길이가 반환되지 않습니다. NULL이 반환되면 **len*이 0으로 설정됩니다.  
  
## <a name="returns"></a>반환 값  
 *field*에 따라 형식이 결정되는 데이터에 대한 포인터입니다. *len*이 NULL이거나 *srvproc*가 NULL이면 NULL이 반환됩니다. *field*를 알 수 없으면 NULL이 반환됩니다. NULL이 반환되면 **len*이 0으로 설정됩니다.  
  
> [!IMPORTANT]  
>  서버에서 반환되는 버퍼는 읽기 전용이어야 합니다. 그렇지 않으면 서버 상태가 손상될 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 **보안 정보** 확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 컴파일한 DLL을 설치하기 전에 해당 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
  