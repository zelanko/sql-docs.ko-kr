---
title: srv_setutype(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_setutype
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_setutype
ms.assetid: 6160f15d-1b68-411e-ab6d-491ec288f264
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2439b19c4550d07b8d50a0bed6d72b603b1601a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62745792"
---
# <a name="srvsetutype-extended-stored-procedure-api"></a>srv_setutype(확장 저장 프로시저 API)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 행의 열에 대해 사용자 정의 데이터 형식을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_setutype (  
SRV_PROC *  
srvproc  
,  
int   
column  
,   
DBINT  
user_type   
);  
  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 애플리케이션과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
 *column*  
 설정할 열을 나타냅니다. 열 번호는 1부터 시작됩니다.  
  
 *user_type*  
 사용자 정의 데이터 형식 코드를 지정합니다.  
  
## <a name="returns"></a>반환 값  
 SUCCEED 또는 FAIL 열이 없는 경우 FAIL을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 열에는 두 가지 데이터 형식(실제 데이터 형식 및 사용자 정의 데이터 형식)이 있습니다. 사용자 정의 데이터 형식은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 열의 실제 사용자 정의 데이터 형식(있는 경우) 및 열 설명 정보(예: Null 허용 여부 및 업데이트 가능성)를 저장하는 데 사용됩니다.  
  
 **srv_describe** 를 사용하여 *column* 이 정의된 후, 마지막 행이 전송되기 전에 언제든지 **srv_setutype** 함수를 호출할 수 있습니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [srv_describe(확장 저장 프로시저 API)](srv-describe-extended-stored-procedure-api.md)  
  
  
