---
title: srv_paramlen(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paramlen
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramlen
ms.assetid: d1fe92ff-cad6-4396-8216-125e5642e81e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2c858d0fa8579aff288efd7026ab4b65035bad8d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63127191"
---
# <a name="srv_paramlen-extended-stored-procedure-api"></a>srv_paramlen(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]대신 CLR 통합을 사용 하세요.  
  
 원격 저장 프로시저 호출 매개 변수의 데이터 길이를 반환합니다. 이 함수는 **srv_paraminfo** 함수로 대체되었습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_paramlen (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 원격 저장 프로시저 호출을 수신한 핸들)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 애플리케이션과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
 *n*  
 매개 변수의 번호를 나타냅니다. 첫 번째 매개 변수는 1입니다.  
  
## <a name="returns"></a>반환  
 매개 변수 데이터의 실제 길이(바이트)입니다. 
  *n*번째 매개 변수가 없거나 원격 저장 프로시저가 없으면 -1이 반환되고, 
  *n*번째 매개 변수가 NULL이면 0이 반환됩니다.  
  
 매개 변수가 다음 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 시스템 데이터 형식 중 하나 이면이 함수는 다음 값을 반환 합니다.  
  
|새 데이터 형식|입력 데이터 길이|  
|--------------------|-----------------------|  
|`BITN`|**NULL:** 1<br /><br /> **0:** 1<br /><br /> **>= 255:** 해당 없음<br /><br /> **<255:** 해당 없음|  
|`BIGVARCHAR`|**NULL:** 0<br /><br /> **0:** 1<br /><br /> **>= 255:** 255<br /><br /> **<255:** 실제 *len*|  
|`BIGCHAR`|**NULL:** 0<br /><br /> **0:** 255<br /><br /> **>= 255:** 255<br /><br /> **<255:** 255|  
|`BIGBINARY`|**NULL:** 0<br /><br /> **0:** 255<br /><br /> **>= 255:** 255<br /><br /> **<255:** 255|  
|`BIGVARBINARY`|**NULL:** 0<br /><br /> **0:** 1<br /><br /> **>= 255:** 255<br /><br /> **<255:** 실제 *len*|  
|`NCHAR`|**NULL:** 0<br /><br /> **0:** 255<br /><br /> **>= 255:** 255<br /><br /> **<255:** 255|  
|`NVARCHAR`|**NULL:** 0<br /><br /> **0:** 1<br /><br /> **>= 255:** 255<br /><br /> **<255:** 실제 *len*|  
|`NTEXT`|**NULL:** -1<br /><br /> **0:** -1<br /><br /> **>= 255:** -1<br /><br /> **<255:** -1|  
  
 \*실제 *len* = 멀티 바이트 문자열 (cch)의 길이  
  
## <a name="remarks"></a>설명  
 각 원격 저장 프로시저 매개 변수에는 실제 데이터 길이와 최대 데이터 길이가 있습니다. Null 값을 사용할 수 없는 고정 길이의 표준 데이터 형식의 경우 실제 길이와 최대 길이가 같습니다. 가변 길이의 데이터 형식의 경우 데이터 길이가 다를 수 있습니다. 예를 들어 `varchar(30)`로 선언한 매개 변수의 데이터 길이는 최대 10바이트입니다. 이 매개 변수의 실제 길이는 10이고 최대 길이는 30입니다. 
  **srv_paramlen** 함수는 원격 저장 프로시저의 실제 데이터 길이(바이트)를 가져옵니다. 매개 변수의 최대 데이터 길이를 가져오려면 **srv_parammaxlen**을 사용합니다.  
  
 매개 변수를 사용하여 원격 저장 프로시저를 호출하는 경우 매개 변수를 이름 또는 위치(이름 없음)로 전달할 수 있습니다. 일부 매개 변수는 이름으로 전달하고 일부 매개 변수는 위치로 전달하여 원격 저장 프로시저를 호출하면 오류가 발생합니다. 이 경우에도 SRV_RPC 핸들러는 호출되지만 매개 변수가 없는 것과 같이 처리되며 **srv_rpcparams**는 0을 반환합니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [srv_paraminfo &#40;확장 저장 프로시저 API&#41;](srv-paraminfo-extended-stored-procedure-api.md)   
 [srv_rpcparams &#40;확장 저장 프로시저 API&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
