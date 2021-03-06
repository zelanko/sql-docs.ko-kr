---
title: srv_alloc(확장 저장 프로시저 API) | Microsoft Docs
description: 확장 저장 프로시저 API의 srv_alloc 및 메모리를 동적으로 할당 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_alloc
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_alloc
ms.assetid: 91505c59-a273-452f-b71d-5e8205c21863
author: rothja
ms.author: jroth
ms.openlocfilehash: b2caa2f1a3959a723854c94a474a20e966f54fb5
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332392"
---
# <a name="srv_alloc-extended-stored-procedure-api"></a>srv_alloc(확장 저장 프로시저 API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 메모리를 동적으로 할당합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
void * srv_alloc ( DBINT  
size  
);  
```  
  
## <a name="arguments"></a>인수  
 *size*  
 할당할 바이트 수를 지정합니다.  
  
## <a name="returns"></a>반환  
 새로 할당된 공간을 가리키는 포인터. *size*바이트를 할당할 수 없는 경우 null 포인터가 반환됩니다.  
  
## <a name="remarks"></a>설명  
 **srv_alloc** 함수는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows API **GlobalAlloc** 함수와 같습니다. 일반적인 Windows API C 런타임 메모리 관리 함수는 확장 저장 프로시저 API 애플리케이션에서 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
