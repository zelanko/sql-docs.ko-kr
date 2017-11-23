---
title: "범위란 메서드 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords: CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9459d144016deaaec593a8edd92bf5b518a8962b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="copyrecord-method-ado"></a>범위란 메서드 (ADO)
복사로 표시 되는 엔터티에 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 다른 위치에 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 (선택 사항) A **문자열** URL이 포함 된 엔터티 지정을 복사할 (예를 들어 파일 또는 디렉터리) 값입니다. 경우 *소스* 를 생략 하거나 빈 문자열, 파일 또는 현재 디렉터리 지정 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 복사 됩니다.  
  
 *대상*  
 (선택 사항) A **문자열** 값 위치를 지정 하는 URL이 포함 된 여기서 *소스* 복사 됩니다.  
  
 *UserName*  
 (선택 사항) A **문자열** 필요한 경우에 대 한 액세스 권한을 부여 하는 사용자 ID를 포함 하는 값 *대상*합니다.  
  
 *암호*  
 (선택 사항) A **문자열** 필요한 경우를 확인 하는 암호를 포함 하는 값 *UserName*합니다.  
  
 *옵션*  
 (선택 사항) A [메서드의 동작](../../../ado/reference/ado-api/copyrecordoptionsenum.md) 의 기본값을 가진 값 **adCopyUnspecified**합니다. 이 메서드의 동작을 지정합니다.  
  
 *비동기*  
 (선택 사항) A **부울** 값 때 **True**,이 작업이 비동기 이어야 함을 지정 합니다.  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 일반적으로 값을 반환 하는 값 *대상*합니다. 그러나 반환 된 정확한 값은 공급자에 따라 다릅니다.  
  
## <a name="remarks"></a>주의  
 값 *소스* 및 *대상* 않아야 고, 그렇지 않으면 동일 하면 런타임 오류가 발생 합니다. 서버, 경로 또는 리소스 이름 중 하나 이상 달라 야 합니다.  
  
 모든 자식 항목 (예를 들어 하위 디렉터리) *소스* 복사한 재귀적으로 아니라면 **adCopyNonRecursive** 지정 됩니다. 재귀 작업에서 *대상* 의 하위 아니어야 *소스*, 그렇지 않으면 작업을 완료 하지 못합니다.  
  
 이 메서드는 실패 하는 경우 *대상* 하지 않으면 (예를 들어 파일 또는 디렉터리)을 기존 엔터티를 식별 **adCopyOverWrite** 지정 됩니다.  
  
> [!IMPORTANT]
>  사용 하 여는 **adCopyOverWrite** 주의 해 서 옵션입니다. 예를 들어 디렉터리에 파일을 복사할 때이 옵션을 지정 하는 *삭제* 디렉터리 및 파일로 바꿉니다.  
  
> [!NOTE]
>  Url은 http 체계를 사용 하 여 자동으로 호출 됩니다는 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 참조 [절대 경로 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)
