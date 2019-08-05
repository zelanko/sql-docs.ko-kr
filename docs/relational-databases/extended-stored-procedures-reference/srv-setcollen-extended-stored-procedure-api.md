---
title: srv_setcollen(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_setcollen
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setcollen
ms.assetid: 3c60f1c3-4562-463a-a259-12df172788bd
author: rothja
ms.author: jroth
ms.openlocfilehash: 15bd83b902ad64213fcde3ef15a185d69fde8cd4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119636"
---
# <a name="srvsetcollen-extended-stored-procedure-api"></a>srv_setcollen(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 가변 길이 열이나 NULL 값을 허용하는 열의 현재 데이터 길이(바이트)를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_setcollen (  
SRV_PROC *  
srvproc  
,  
int   
column  
,  
int  
len   
);  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 애플리케이션과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
 *column*  
 데이터 길이가 지정되는 열의 번호를 나타냅니다. 열 번호는 1부터 시작됩니다.  
  
 *len*  
 열 데이터의 길이(바이트)를 나타냅니다. 길이가 0이면 열 데이터 값이 Null입니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL  
  
## <a name="remarks"></a>Remarks  
 먼저 **srv_describe**를 사용하여 행의 각 열을 정의해야 합니다. 열 데이터 길이는 **srv_describe** 또는 **srv_setcollen**에 대한 마지막 호출에서 설정됩니다. 행의 가변 길이 데이터(Null로 끝나는 데이터)가 변경되는 경우 **srv_sendrow**를 호출하기 전에 **srv_setcollen**을 사용하여 새 길이로 설정해야 합니다. Null 값을 허용하는 열의 경우 *desttype*이 Null을 허용하는 데이터 형식(예: SRVINTN)으로 설정되어 **srv_describe**가 호출되었으며, *len*을 0으로 설정하여 **srv_setcollen**이 호출되어 Null 데이터가 지정됩니다. 길이가 0인 데이터는 확장 저장 프로시저 API를 사용하여 지정할 수 없습니다.  
  
 열의 데이터 형식이 가변 길이인 경우에는 *len*이 확인되지 않습니다. 고정 길이 열에 대해 호출하면 이 함수는 FAIL을 반환합니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [srv_describe &#40;확장 저장 프로시저 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
