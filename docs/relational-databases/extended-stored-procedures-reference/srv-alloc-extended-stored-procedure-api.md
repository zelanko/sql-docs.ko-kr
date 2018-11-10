---
title: srv_alloc(확장 저장 프로시저 API) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 0b7f2627c61b96bb0efa5c19886c554268c2cd2f
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030950"
---
# <a name="srvalloc-extended-stored-procedure-api"></a>srv_alloc(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
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
  
## <a name="returns"></a>반환 값  
 새로 할당된 공간을 가리키는 포인터. *size*바이트를 할당할 수 없는 경우 null 포인터가 반환됩니다.  
  
## <a name="remarks"></a>Remarks  
 **srv_alloc** 함수는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows API **GlobalAlloc** 함수와 같습니다. 일반적인 Windows API C 런타임 메모리 관리 함수는 확장 저장 프로시저 API 응용 프로그램에서 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
