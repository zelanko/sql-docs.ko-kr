---
title: "srv_willconvert(확장 저장 프로시저 API) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e4a39602f8e7e75dabacbac405758aee6879b0b2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="srvwillconvert-extended-stored-procedure-api"></a>srv_willconvert(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 대신 CLR 통합을 사용하십시오.  
  
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
  
## <a name="returns"></a>반환 값  
 데이터 형식 변환이 지원되면 True, 데이터 형식 변환이 지원되지 않으면 False입니다.  
  
## <a name="remarks"></a>Remarks  
 각 데이터 형식에 대한 설명은 [데이터 형식(확장 저장 프로시저 API)](../../relational-databases/extended-stored-procedures-reference/data-types-extended-stored-procedure-api.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [srv_convert(확장 저장 프로시저 API)](../../relational-databases/extended-stored-procedures-reference/srv-convert-extended-stored-procedure-api.md)  
  
  
