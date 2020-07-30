---
title: srv_rpcoptions(확장 저장 프로시저 API) | Microsoft Docs
description: 확장 저장 프로시저 API에서 srv_rpcoptions 현재 원격 저장 프로시저에 대 한 런타임 옵션을 반환 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcoptions
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcoptions
ms.assetid: dbcce5d1-d5a1-4379-9597-04e43af5923d
author: rothja
ms.author: jroth
ms.openlocfilehash: 3d4bd331b54b4bb555fcc6cdbe59155a553332eb
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332472"
---
# <a name="srv_rpcoptions-extended-stored-procedure-api"></a>srv_rpcoptions(확장 저장 프로시저 API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 현재 원격 저장 프로시저에 대한 런타임 옵션을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DBUSMALLINT srv_rpcoptions ( SRV_PROC *  
srvproc   
);  
```  
  
## <a name="arguments"></a>인수  
 *srvproc*  
 특정 클라이언트 연결에 대한 핸들(이 경우 원격 저장 프로시저를 수신한 핸들)인 SRV_PROC 구조에 대한 포인터입니다. 이 구조에는 확장 저장 프로시저 API 라이브러리가 애플리케이션과 클라이언트 간 통신 및 데이터를 관리하는 데 사용하는 정보가 들어 있습니다.  
  
## <a name="returns"></a>반환  
 현재 원격 저장 프로시저에 대한 논리 OR로 결합된 런타임 플래그가 들어 있는 비트맵. 현재 원격 저장 프로시저가 없으면 0이 반환되고 메시지가 생성됩니다.  
  
## <a name="remarks"></a>설명  
 다음 표에서는 각 런타임 플래그에 대해 설명합니다.  
  
|런타임 플래그|설명|  
|--------------------|-----------------|  
|SRV_NOMETADATA|클라이언트가 메타데이터 정보를 사용하지 않고 결과를 요청했습니다. 이 플래그는 클라이언트가 인스턴스와 통신 하는 경우에만 사용 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 확장 저장 프로시저 API 애플리케이션은 메타데이터 정보를 생략할 수 없습니다.|  
|SRV_RECOMPILE|클라이언트가 원격 저장 프로시저를 실행하기 전에 재컴파일하도록 요청했습니다. 이 플래그는 확장 저장 프로시저 API 애플리케이션에 적용되지 않을 수 있습니다.|  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
