---
title: CopyRecord 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords:
- CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d11a8d5d775499246bd8af709764dec3f2ad61e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698512"
---
# <a name="copyrecord-method-ado"></a>CopyRecord 메서드(ADO)
복사 나타내는 엔터티를 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 다른 위치로 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 (선택 사항) A **문자열** URL을 지정 하면 복사할 (예: 파일 또는 디렉터리)를 포함 하는 값입니다. 하는 경우 *소스* 생략 되거나 빈 문자열로, 파일 또는 현재 디렉터리를 지정 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 복사 됩니다.  
  
 *대상*  
 (선택 사항) A **문자열** 위치를 지정 하는 URL이 포함 된 값 위치 *원본* 복사 됩니다.  
  
 *UserName*  
 (선택 사항) A **문자열** 필요한 경우에 대 한 액세스 권한을 부여 하는 사용자 ID를 포함 하는 값 *대상*합니다.  
  
 *암호*  
 (선택 사항) A **문자열** 필요한 경우를 확인 하는 암호가 포함 된 값 *UserName*합니다.  
  
 *옵션*  
 (선택 사항) A [메서드의 동작](../../../ado/reference/ado-api/copyrecordoptionsenum.md) 값의 기본 값을 가진 **adCopyUnspecified**합니다. 이 메서드의 동작을 지정 합니다.  
  
 *Async*  
 (선택 사항) A **부울** 값을 때 **True**,이 작업이 비동기 되도록 지정 합니다.  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 일반적으로 값을 반환 하는 값인 *대상*합니다. 그러나 공급자에 따라 다릅니다는 정확한 값을 반환 합니다.  
  
## <a name="remarks"></a>Remarks  
 값 *원본* 하 고 *대상* 아니어야 고, 그렇지 않으면 동일 하면 런타임 오류가 발생 합니다. 하나 이상의 서버, 경로 또는 리소스 이름이 달라 야 합니다.  
  
 모든 자식 항목 (예를 들어, 하위 디렉터리) *소스* 않는다면를 재귀적으로 복사 **adCopyNonRecursive** 지정 됩니다. 재귀 작업에서 *대상* 의 하위 디렉터리가 아니어야 *원본*고, 그렇지 않으면 작업이 완료 되지 것입니다.  
  
 이 메서드가 실패 하는 경우 *대상* 하지 않으면 (예를 들어, 파일 또는 디렉터리), 기존 엔터티를 식별 **adCopyOverWrite** 지정 됩니다.  
  
> [!IMPORTANT]
>  사용 된 **adCopyOverWrite** 옵션을 신중 하 게 합니다. 예를 들어 디렉터리에 파일을 복사 하는 경우이 옵션을 지정 하는 *삭제* 디렉터리 파일을 바꿉니다.  
  
> [!NOTE]
>  Http 체계를 사용 하 여 Url은 자동으로 호출 합니다 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. 자세한 내용은 [절대 및 상대 Url](../../../ado/guide/data/absolute-and-relative-urls.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)
