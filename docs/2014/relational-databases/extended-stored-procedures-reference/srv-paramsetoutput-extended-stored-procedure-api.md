---
title: srv_paramsetoutput(확장 저장 프로시저 API) | Microsoft Docs
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
- srv_paramsetoutput
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramsetoutput
ms.assetid: f2810e19-e513-458b-8925-5756b6ee1313
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3d1ea832995c65a0b0b07fc4f666523fbdf07b31
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37190423"
---
# <a name="srvparamsetoutput-extended-stored-procedure-api"></a>srv_paramsetoutput(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 반환 매개 변수의 값을 설정합니다. 이 함수는 **srv_paramset** 함수를 대체합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_paramsetoutput (  
SRV_PROC *  
srvproc  
,  
int  
n  
,  
BYTE *  
pbData  
,  
ULONG   
cbLen  
,  
BOOL  
fNull   
);  
  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 클라이언트 연결의 핸들입니다.  
  
 *n*  
 설정할 매개 변수의 서수입니다. 첫 번째 매개 변수는 1입니다.  
  
 *pbData*  
 클라이언트에 프로시저 반환 매개 변수로 전달될 데이터 값에 대한 포인터입니다.  
  
 *cbLen*  
 반환할 데이터의 실제 길이입니다. 매개 변수의 데이터 형식이 상수 길이 값이고 Null 값을 허용하지 않는 경우(예: *srvbit* 또는 *srvint1*) *cbLen*은 무시됩니다. *fNull*이 FALSE인 경우 값이 0이면 길이가 0인 데이터를 나타냅니다.  
  
 *fNull*  
 반환 매개 변수의 값이 NULL인지 여부를 나타내는 플래그입니다. 매개 변수가 NULL로 설정되어야 하는 경우 이 플래그를 TRUE로 설정합니다. 기본값은 FALSE입니다. *fNull*이 TRUE로 설정되어 있는 경우 *cbLen*을 0으로 설정하지 않으면 함수가 실패합니다.  
  
## <a name="returns"></a>반환 값  
 매개 변수 정보가 성공적으로 설정되면 SUCCEED가 반환되고 그렇지 않으면 FAIL이 반환됩니다. FAIL은 다음과 같은 경우에 반환됩니다.  
  
-   매개 변수가 반환 매개 변수가 아닌 경우  
  
-   *cbLen* 인수가 잘못된 경우  
  
## <a name="remarks"></a>Remarks  
 **보안 정보** 확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 컴파일한 DLL을 설치하기 전에 해당 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
