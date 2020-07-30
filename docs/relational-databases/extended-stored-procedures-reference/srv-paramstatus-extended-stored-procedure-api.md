---
title: srv_paramstatus(확장 저장 프로시저 API) | Microsoft Docs
description: Srv_paramstatus에서 특정 원격 저장 프로시저 호출 매개 변수의 상태를 반환 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramstatus
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramstatus
ms.assetid: 86cecd45-0b09-42e9-8152-32a12a1c2b7a
author: rothja
ms.author: jroth
ms.openlocfilehash: e55986b0d781b311b050eb5695ca350f7331e25c
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248387"
---
# <a name="srv_paramstatus-extended-stored-procedure-api"></a>srv_paramstatus(확장 저장 프로시저 API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 특정 원격 저장 프로시저 호출 매개 변수의 상태를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int srv_paramstatus (  
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
 매개 변수의 번호를 나타냅니다. 첫 번째 매개 변수의 번호는 1입니다.  
  
## <a name="returns"></a>반환  
 매개 변수의 상태 플래그가 들어 있는 **int** 입니다. 현재는 플래그가 하나만 있습니다. 비트 0을 1로 설정하면 매개 변수가 반환 매개 변수입니다. *n*번째 매개 변수가 없거나 원격 저장 프로시저가 없으면 -1이 반환됩니다.  
  
## <a name="remarks"></a>설명  
 이 루틴은 원격 저장 프로시저 호출 매개 변수의 상태 플래그를 반환합니다.  
  
 매개 변수에는 원격 저장 프로시저를 사용하여 클라이언트와 애플리케이션 간에 전달되는 데이터가 포함되어 있습니다. 클라이언트는 특정 매개 변수를 반환 매개 변수로 지정할 수 있습니다. 이러한 반환 매개 변수에는 애플리케이션이 다시 클라이언트에 전달하는 값이 포함될 수 있습니다.  
  
 현재 유일한 상태 플래그는 매개 변수가 반환 매개 변수인지 여부를 나타내는 상태 플래그입니다.  
  
 매개 변수를 사용하여 원격 저장 프로시저를 호출하는 경우 매개 변수를 이름 또는 위치(이름 없음)로 전달할 수 있습니다. 일부 매개 변수는 이름으로 전달하고 일부 매개 변수는 위치로 전달하여 원격 저장 프로시저를 호출하면 오류가 발생합니다. 오류가 발생 하면 SRV_RPC 처리기가 계속 호출 되지만 매개 변수가 없는 것 처럼 표시 되 고 **srv_rpcparams** 0을 반환 합니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [srv_rpcparams(확장 저장 프로시저 API)](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
