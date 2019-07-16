---
title: 확장 저장 프로시저 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- warnings [SQL Server]
- extended stored procedures [SQL Server], debugging
- extended stored procedures [SQL Server], creating
- messages [SQL Server], extended stored procedures
ms.assetid: 9f7c0cdb-6d88-44c0-b049-29953ae75717
author: rothja
ms.author: jroth
ms.openlocfilehash: 3c22077de3bf41bc09864ac2c7f24dbdd4ecc3e7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032045"
---
# <a name="creating-extended-stored-procedures"></a>확장 저장 프로시저 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
 확장 저장 프로시저는 프로토타입이 다음과 같은 함수입니다.  
  
 SRVRETCODE *xp_extendedProcName* **(** SRVPROC **\*);**  
  
 접두사 xp_는 필요에 따라 사용할 수 있습니다. 확장 저장 프로시저의 이름은 서버에 설치된 코드 페이지/정렬 순서에 관계없이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 참조할 때는 대/소문자를 구분합니다. DLL을 빌드하는 경우 다음 작업을 수행합니다.  
  
-   진입점이 필요하면 DllMain 함수를 작성합니다.  
  
     이 함수는 옵션입니다. 원본 코드에서 이 함수를 제공하지 않으면 컴파일러가 자체 버전에 연결하며 이 경우 아무 작업도 수행되지 않고 TRUE가 반환됩니다. DllMain 함수를 제공하면 스레드나 프로세스가 DLL에 연결되거나 DLL에서 분리될 때 운영 체제에서 이 함수를 호출합니다.  
  
-   DLL 외부에서 호출된 모든 함수(모든 확장 저장 프로시저 Efunction)는 내보내야 합니다.  
  
     .Def 파일의 EXPORTS 섹션에서 해당 이름을 나열 하 여 함수를 내보낼 수 있습니다 또는 Microsoft 컴파일러 확장인 __declspec (dllexport) 사용 하 여 소스 코드에서 함수 이름을 접두사로 붙일 수 있습니다 (유의 \__declspec()에 밑줄 두 개를 사용 하 여 시작)입니다.  
  
 확장 저장 프로시저 DLL을 만드는 데 필요한 파일은 다음과 같습니다.  
  
|파일|설명|  
|----------|-----------------|  
|Srv.h|확장 저장 프로시저 API 헤더 파일|  
|Opends60.lib|Opends60.dll용 가져오기 라이브러리|  
  
 확장 저장 프로시저 DLL을 만들려면 동적 연결 라이브러리 형식의 프로젝트를 만듭니다. DLL을 만드는 방법은 개발 환경 설명서를 참조하십시오.  
  
 모든 확장 저장 프로시저 DLL에서 다음 함수를 구현하고 내보내는 것이 좋습니다.  
  
```  
__declspec(dllexport) ULONG __GetXpVersion()  
{  
   return ODS_VERSION;  
}  
```  
  
> [!NOTE]  
>  __declspec(dllexport)은 Microsoft 전용 컴파일러 확장입니다. 컴파일러에서 이 지시어를 지원하지 않으면 DEF 파일의 EXPORTS 섹션 아래에서 이 함수를 내보내야 합니다.  
  
 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 추적을 사용 하 여 시작 플래그-T260 또는 시스템 관리자 권한이 있는 사용자는 DBCC TRACEON (260)를 실행 하는 경우 및 확장 저장 프로시저가 DLL __getxpversion (), 경고 메시지를 지원 하지 않습니다 (오류 8131: 확장된 저장된 프로시저 DLL '%'을 내보내지 않습니다 \__GetXpVersion().) 오류 로그에 출력 됩니다. (유의 \__GetXpVersion()에 밑줄 두 개를 사용 하 여 시작 합니다.)  
  
 확장 저장 프로시저 DLL이 __GetXpVersion()을 내보내지만 함수에서 반환하는 버전이 서버에 필요한 버전보다 낮을 경우 함수에서 반환한 버전과 서버에 필요한 버전을 알리는 경고 메시지가 오류 로그에 출력됩니다. 잘못 된 값을 반환 하는이 메시지를 받게 되 면 \__GetXpVersion(), 또는 이전 버전 srv.h를 사용 하 여 컴파일하는 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Win32 함수인 SetErrorMode는 확장 저장 프로시저 내에서 호출하지 않아야 합니다.  
  
 장기 실행 확장 저장 프로시저의 경우 연결이 끊기거나 일괄 처리가 중단될 경우 프로시저가 자동으로 종료될 수 있도록 주기적으로 srv_got_attention을 호출하는 것이 좋습니다.  
  
 확장 저장 프로시저 DLL을 디버깅하려면 DLL을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Binn 디렉터리에 복사합니다. 디버깅 세션에 대 한 실행 파일을 지정 하려면의 경로 및 파일 이름을 입력 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 파일 (예: C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\MSSQL\Binn\Sqlservr.exe)입니다. Sqlservr 인수에 대 한 자세한 내용은 [응용 프로그램 sqlservr](../../tools/sqlservr-application.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [srv_got_attention &#40;확장 저장 프로시저 API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-got-attention-extended-stored-procedure-api.md)  
  
  
