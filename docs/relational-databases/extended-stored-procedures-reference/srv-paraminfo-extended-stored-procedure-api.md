---
title: srv_paraminfo(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- srv_paraminfo
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paraminfo
ms.assetid: ee2afd4e-0d91-462b-9403-98d481546330
caps.latest.revision: 31
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: abdc661f43a3dfbc63e4b0a6e141e121e74241e7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32933578"
---
# <a name="srvparaminfo-extended-stored-procedure-api"></a>srv_paraminfo(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 매개 변수에 대한 정보를 반환합니다. 이 함수는 [srv_paramtype](../../relational-databases/extended-stored-procedures-reference/srv-paramtype-extended-stored-procedure-api.md), [srv_paramlen](../../relational-databases/extended-stored-procedures-reference/srv-paramlen-extended-stored-procedure-api.md), [srv_parammaxlen](../../relational-databases/extended-stored-procedures-reference/srv-parammaxlen-extended-stored-procedure-api.md) 및 [srv_paramdata](../../relational-databases/extended-stored-procedures-reference/srv-paramdata-extended-stored-procedure-api.md) 함수를 대체합니다. **srv_paraminfo**는 [데이터 형식](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md)의 데이터 형식과 길이가 0인 데이터를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_paraminfo (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbType  
,  
ULONG *  
pcbMaxLen  
,  
ULONG *  
pcbActualLen  
,  
BYTE *  
pbData  
,  
BOOL *  
pfNull  
);  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 클라이언트 연결의 핸들입니다.  
  
 *n*  
 설정할 매개 변수의 서수입니다. 첫 번째 매개 변수는 1입니다.  
  
 *pbType*  
 매개 변수의 데이터 형식입니다.  
  
 *pcbMaxLen*  
 매개 변수의 최대 길이에 대한 포인터입니다.  
  
 *pcbActualLen*  
 매개 변수의 실제 길이에 대한 포인터입니다. **pfNull*이 FALSE로 설정되어 있으면 0 값(\**pcbActualLen* == 0)은 길이가 0인 데이터를 나타냅니다.  
  
 *pbData*  
 매개 변수 데이터의 버퍼에 대한 포인터입니다. *pbData*가 NULL이 아닌 경우 확장 저장 프로시저 API는 \**pcbActualLen* 바이트의 데이터를 \**pbData*에 기록합니다. *pbData*가 NULL인 경우 데이터가 \**pbData*에 기록되지 않지만 함수는 \**pbType*, \**pcbMaxLen*, \**pcbActualLen* 및 **pfNull*을 반환합니다. 이 버퍼에 대한 메모리는 응용 프로그램으로 관리해야 합니다.  
  
 *pfNull*  
 NULL 플래그에 대한 포인터입니다.매개 변수 값이 NULL인 경우  **pfNull*이 TRUE로 설정됩니다.  
  
## <a name="returns"></a>반환 값  
 매개 변수 정보를 성공적으로 가져오면 SUCCEED가 반환되고 그렇지 않으면 FAIL이 반환됩니다. 현재 원격 저장 프로시저가 없고 *n*번째 원격 저장 프로시저 매개 변수가 없으면 FAIL이 반환됩니다.  
  
## <a name="remarks"></a>Remarks  
 **보안 정보** 확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 컴파일한 DLL을 설치하기 전에 해당 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [확장 저장 프로시저 프로그래머 참조](../../relational-databases/extended-stored-procedures-reference/database-engine-extended-stored-procedures-reference.md)  
  
  
