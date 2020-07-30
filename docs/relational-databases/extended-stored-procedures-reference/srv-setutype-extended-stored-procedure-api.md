---
title: srv_setutype(확장 저장 프로시저 API) | Microsoft Docs
description: Srv_setutype에 대해 알아봅니다. srv_setutype은 행의 열에 대해 사용자 정의 데이터 형식을 설정 합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_setutype
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setutype
ms.assetid: 6160f15d-1b68-411e-ab6d-491ec288f264
author: rothja
ms.author: jroth
ms.openlocfilehash: 9ecdbaef663059146f3ca6bd4a88305e12d4f495
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248196"
---
# <a name="srv_setutype-extended-stored-procedure-api"></a>srv_setutype(확장 저장 프로시저 API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
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
  
## <a name="returns"></a>반환  
 SUCCEED 또는 FAIL 열이 없는 경우 FAIL을 반환합니다.  
  
## <a name="remarks"></a>설명  
 열에는 두 가지 데이터 형식(실제 데이터 형식 및 사용자 정의 데이터 형식)이 있습니다. 사용자 정의 데이터 형식은에서 열의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실제 사용자 정의 데이터 형식 (있는 경우) 및 열 설명 정보 (예: null 허용 여부 및 업데이트 가능성)를 저장 하는 데 사용 됩니다.  
  
 **srv_describe** 를 사용하여 *column* 이 정의된 후, 마지막 행이 전송되기 전에 언제든지 **srv_setutype** 함수를 호출할 수 있습니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://www.microsoft.com/msrc?rtc=1)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [srv_describe &#40;확장 저장 프로시저 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
