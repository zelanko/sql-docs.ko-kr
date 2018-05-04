---
title: srv_rpcdb(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- srv_rpcdb
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcdb
ms.assetid: d52bfd22-7a7c-4ab0-af65-df96ff359e6f
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2e613fc49853e913fa0ed3f6f5696aacb2c583a5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="srvrpcdb-extended-stored-procedure-api"></a>srv_rpcdb(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 현재 원격 저장 프로시저에 대한 데이터베이스 이름 구성 요소를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DBCHAR * srv_rpcdb (  
SRV_PROC * srvproc,int *len );  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 응용 프로그램과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
 *len*  
 데이터베이스 이름의 길이를 받는 **int** 변수에 대한 포인터입니다. *len*이 NULL이면 데이터베이스 이름의 길이가 반환되지 않습니다.  
  
## <a name="returns"></a>반환 값  
 현재 원격 저장 프로시저의 데이터베이스 이름 부분에서 null로 끝나는 문자열에 대한 DBCHAR 포인터입니다. 현재 원격 저장 프로시저가 없으면 NULL이 반환되고 *len* 매개 변수가 -1로 설정됩니다.  
  
## <a name="remarks"></a>Remarks  
 이 함수는 원격 저장 프로시저 개체 이름에서 데이터베이스 구성 요소만 반환합니다. 소유자, 원격 저장 프로시저 이름, 원격 저장 프로시저 번호에 대한 선택적 지정자는 포함되지 않습니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
