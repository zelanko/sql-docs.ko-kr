---
title: srv_pfield(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- srv_pfield
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_pfield
ms.assetid: a61e4c1f-e65b-48ea-a7d1-3e1544af389d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 02b7b2a76944575d9935d538e341641d33db43df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47728931"
---
# <a name="srvpfield-extended-stored-procedure-api"></a>srv_pfield(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 데이터베이스 연결에 대한 정보를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DBCHAR * srv_pfield (  
SRV_PROC *  
srvproc  
,  
int   
field  
,  
int *  
len  
);  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 데이터베이스 연결을 식별하는 포인터입니다.  
  
 *field*  
 반환할 연결 데이터를 지정합니다.  
  
|값|반환 값|  
|-----------|-------------|  
|SRV_APPLNAME|연결을 설정할 때 클라이언트가 제공한 응용 프로그램 이름입니다.|  
|SRV_BCPFLAG|플래그로, 클라이언트가 대량 복사 작업을 준비 중이면 TRUE이고, 그렇지 않으면 FALSE입니다.|  
|SRV_CLIB|클라이언트에서 서버로의 통신을 가능하게 하는 라이브러리의 이름입니다.|  
|SRV_CPID|클라이언트 원본 컴퓨터의 클라이언트 프로세스 ID입니다.|  
|SRV_HOST|연결을 설정할 때 클라이언트가 제공한 클라이언트 컴퓨터 이름입니다.|  
|SRV_LIBVERS|클라이언트 라이브러리의 버전입니다.|  
|SRV_LSECURE|플래그입니다. 연결에서 통합 보안을 사용하여 로그인한 경우 TRUE입니다.|  
|SRV_NETWORK_MODULE|연결에서 사용하는 네트워크 라이브러리 DLL의 이름입니다.|  
|SRV_NETWORK_VERSION|연결에서 사용하는 네트워크 라이브러리 DLL의 버전입니다.|  
|SRV_NETWORK_CONNECTION|현재 *srvproc* 연결에 사용된 네트워크 라이브러리 DLL에 전달된 연결 문자열입니다.|  
|SRV_PIPEHANDLE|연결된 클라이언트의 파이프 핸들이 포함된 문자열입니다. 클라이언트가 명명된 파이프를 사용하지 않는 네트워크에 연결된 경우에는 NULL입니다. 이 핸들을 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows에서 유효한 파이프 핸들로 사용하려면 이 문자열을 정수로 변환하십시오.|  
|SRV_RMTSERVER|클라이언트 프로세스가 로그인해 온 서버입니다. 클라이언트에서 로그인한 경우에는 이 값이 빈 문자열입니다.|  
|SRV_ROWSENT|현재 결과 집합에 대해 *srvproc*를 통해 이미 전송된 행 수입니다.|  
|SRV_SPID|*srvproc*의 서버 스레드 ID입니다. 확장 저장 프로시저의 경우 이 값은 **sys.sysprocesses**의 **kpid** 열과 같으며 시간이 지나면 변경될 수 있습니다.|  
|SRV_SPROC_CODEPAGE|서버에서 멀티바이트 데이터를 해석하는 데 사용하는 코드 페이지입니다.|  
|SRV_STATUS|*srvproc*의 현재 상태로, 실행 중이거나 닫힌 상태입니다.|  
|SRV_TYPE|*srvproc*의 연결 형식입니다. 서버가 반환되면 *srvproc*가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 연결된 것입니다. 클라이언트가 반환되면 *srvproc*가 DB-Library 또는 ODBC 클라이언트에서 연결된 것입니다.|  
|SRV_USER|연결 사용자의 이름입니다.|  
|||  
  
 *len*  
 반환된 *field* 값의 길이가 포함된 **int** 변수에 대한 포인터입니다. *len*이 NULL이면 문자열 길이가 반환되지 않습니다.  
  
## <a name="returns"></a>반환 값  
 SRV_PROC 구조에 지정된 필드에 대한 현재 값이 포함된 Null로 끝나는 문자열에 대한 포인터입니다. 필드가 비어 있으면 빈 문자열에 대한 올바른 포인터가 반환되고 *len*에 0이 포함됩니다. 필드가 알 수 없는 필드이면 NULL이 반환되고 *len*에 -1 값이 포함됩니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [보안 개발자 센터(Security Developer Center)](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하세요.  
  
  
