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
ms.openlocfilehash: aaabb32234cefe2e3c3727ce5a18dd2d98549a77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933412"
---
# <a name="copyrecord-method-ado"></a>CopyRecord 메서드(ADO)
[레코드가](../../../ado/reference/ado-api/record-object-ado.md) 나타내는 엔터티를 다른 위치로 복사 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *원본*  
 (선택 사항) 복사할 엔터티 (예: 파일 또는 디렉터리)를 지정 하는 URL을 포함 하는 **문자열** 값입니다. *Source* 를 생략 하거나 빈 문자열을 지정 하면 현재 [레코드가](../../../ado/reference/ado-api/record-object-ado.md) 나타내는 파일이 나 디렉터리가 복사 됩니다.  
  
 *대상*  
 (선택 사항) *원본이* 복사 될 위치를 지정 하는 URL을 포함 하는 **문자열** 값입니다.  
  
 *이름*  
 (선택 사항) 필요한 경우 *대상*에 대 한 액세스 권한을 부여 하는 사용자 ID를 포함 하는 **문자열** 값입니다.  
  
 *암호*  
 (선택 사항) 필요한 경우 *사용자 이름을*확인 하는 암호를 포함 하는 **문자열** 값입니다.  
  
 *옵션*  
 (선택 사항) 기본값은 **adCopyUnspecified**인 [CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md) 값입니다. 이 메서드의 동작을 지정 합니다.  
  
 *동기화*  
 (선택 사항) **부울** 값입니다. **True**인 경우이 작업을 비동기로 지정 합니다.  
  
## <a name="return-value"></a>Return Value  
 일반적으로 *Destination*값을 반환 하는 **문자열** 값입니다. 그러나 반환 되는 정확한 값은 공급자에 따라 다릅니다.  
  
## <a name="remarks"></a>설명  
 *원본* 및 *대상* 의 값은 달라 야 합니다. 그렇지 않으면 런타임 오류가 발생 합니다. 서버, 경로 또는 리소스 이름 중 하나 이상이 달라 야 합니다.  
  
 **Adcopynonrecursive** 가 지정 되지 않은 경우 *원본* 의 모든 자식 (예: 하위 디렉터리)은 재귀적으로 복사 됩니다. 재귀 작업에서 *대상은* *원본의*하위 디렉터리가 아니어야 합니다. 그렇지 않으면 작업이 완료 되지 않습니다.  
  
 **AdCopyOverWrite** 가 지정 되지 않은 경우 *대상* 에서 기존 엔터티 (예: 파일 또는 디렉터리)를 식별 하는 경우이 메서드는 실패 합니다.  
  
> [!IMPORTANT]
>  **AdCopyOverWrite** 옵션을 신중 하 게 사용 합니다. 예를 들어 디렉터리에 파일을 복사할 때이 옵션을 지정 하면 디렉터리가 *삭제* 되 고 파일로 바뀝니다.  
  
> [!NOTE]
>  Http 체계를 사용 하는 Url은 자동으로 [Microsoft OLE DB 공급자에 게 Internet 게시용](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)으로 호출 됩니다. 자세한 내용은 [절대 및 상대 url](../../../ado/guide/data/absolute-and-relative-urls.md)을 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)
