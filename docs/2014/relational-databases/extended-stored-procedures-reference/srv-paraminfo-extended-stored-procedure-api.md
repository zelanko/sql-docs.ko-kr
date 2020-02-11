---
title: srv_paraminfo(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_paraminfo
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paraminfo
ms.assetid: ee2afd4e-0d91-462b-9403-98d481546330
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f3c89eb2e6f810902e28e01c7e5ffbcdcc0375c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63127182"
---
# <a name="srv_paraminfo-extended-stored-procedure-api"></a>srv_paraminfo(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]대신 CLR 통합을 사용 하세요.  
  
 매개 변수에 대한 정보를 반환합니다. 이 함수는 [srv_paramtype](srv-paramtype-extended-stored-procedure-api.md), [srv_paramlen](srv-paramlen-extended-stored-procedure-api.md), [srv_parammaxlen](srv-parammaxlen-extended-stored-procedure-api.md) 및 [srv_paramdata](srv-paramdata-extended-stored-procedure-api.md) 함수를 대체합니다. **srv_paraminfo** 는 데이터 [형식과](data-types-extended-stored-procedure-api.md) 길이가 0 인 데이터의 데이터 형식을 지원 합니다.  
  
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
  
 *Ptype*  
 매개 변수의 데이터 형식입니다.  
  
 *pcbMaxLen*  
 매개 변수의 최대 길이에 대한 포인터입니다.  
  
 *pcbActualLen*  
 매개 변수의 실제 길이에 대한 포인터입니다. *\*pfNull*이 FALSE로 설정되어 있으면 0 값(**pcbActualLen* == 0)은 길이가 0인 데이터를 나타냅니다.  
  
 *pbData*  
 매개 변수 데이터의 버퍼에 대한 포인터입니다. 
  *pbData*가 NULL이 아닌 경우 확장 저장 프로시저 API는 \**pcbActualLen* 바이트의 데이터를 \**pbData*에 기록합니다. 
  *pbData*가 NULL인 경우 데이터가 \**pbData*에 기록되지 않지만 함수는 \**pbType*, \**pcbMaxLen*, \**pcbActualLen* 및 **pfNull*을 반환합니다. 이 버퍼에 대한 메모리는 애플리케이션으로 관리해야 합니다.  
  
 *pfNull*  
 NULL 플래그에 대한 포인터입니다. *매개 변수 값이 NULL 이면 *pfNull* 가 TRUE로 설정 됩니다.  
  
## <a name="returns"></a>반환  
 매개 변수 정보를 성공적으로 가져오면 SUCCEED가 반환되고 그렇지 않으면 FAIL이 반환됩니다. 현재 원격 저장 프로시저가 없고 *n*번째 원격 저장 프로시저 매개 변수가 없으면 FAIL이 반환됩니다.  
  
## <a name="remarks"></a>설명  
 **보안 정보** 확장 저장 프로시저의 원본 코드를 철저히 검토 하 고 프로덕션 서버에 설치 하기 전에 컴파일된 Dll을 테스트 해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [확장 저장 프로시저 프로그래머 참조](database-engine-extended-stored-procedures-reference.md)  
  
  
