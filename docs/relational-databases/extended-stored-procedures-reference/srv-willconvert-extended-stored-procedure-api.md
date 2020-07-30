---
title: srv_willconvert(확장 저장 프로시저 API) | Microsoft Docs
description: 특정 데이터 형식 변환을 ODS 라이브러리 내에서 사용할 수 있는지 여부를 srv_willconvert 확인 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_willconvert
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_willconvert
ms.assetid: 6f4db5fd-215a-461c-95e4-17697852733e
author: rothja
ms.author: jroth
ms.openlocfilehash: ef515b200221a6bb439a65a02e546017046dd0e4
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248230"
---
# <a name="srv_willconvert-extended-stored-procedure-api"></a>srv_willconvert(확장 저장 프로시저 API)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하세요.  
  
 ODS 라이브러리 내에서 특정 데이터 형식 변환이 가능한지 확인합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
BOOL srv_willconvert (  
int  
srctype  
,  
int  
desttype   
);  
```  
  
## <a name="arguments"></a>인수  
 *srctype*  
 변환할 데이터의 데이터 형식을 나타냅니다. 이 매개 변수는 임의의 확장 저장 프로시저 API 데이터 형식일 수 있습니다.  
  
 *desttype*  
 원본 데이터를 변환할 데이터 형식을 나타냅니다. 이 매개 변수는 임의의 확장 저장 프로시저 API 데이터 형식일 수 있습니다.  
  
## <a name="returns"></a>반환  
 데이터 형식 변환이 지원되면 True, 데이터 형식 변환이 지원되지 않으면 False입니다.  
  
## <a name="remarks"></a>설명  
 각 데이터 형식에 대한 설명은 [데이터 형식(확장 저장 프로시저 API)](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://www.microsoft.com/msrc?rtc=1)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [srv_convert(확장 저장 프로시저 API)](../../relational-databases/extended-stored-procedures-reference/srv-convert-extended-stored-procedure-api.md)  
  
  
