---
title: "문자 집합 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::Charset
helpviewer_keywords:
- Charset property [ADO]
ms.assetid: e42507cb-9b46-4ce4-8191-2948eaf14ca2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8c3f9568a04572718bb6b1a968a3bacae4520898
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="charset-property-ado"></a>문자 집합 속성 (ADO)
문자 집합을 나타냅니다는 텍스트의 내용을 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 의 내부 버퍼에 저장 하기 위해 변환 되어야 합니다는 **스트림** 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **문자열** 는 문자를 지정 하는 값 집합의 내용을 **스트림** 변환 됩니다. 기본값은 **유니코드**합니다. 허용 되는 값은 인터넷 문자 집합 이름 (예를 들어 "iso-8859-1", "windows-1252")으로 인터페이스를 통해 전달 되는 일반 문자열입니다. 목록이 알려 지는 시스템에서 문자 집합 이름에 대 한 Windows 레지스트리에 HKEY_CLASSES_ROOT\MIME\Database\Charset의 하위 키를 참조 하십시오.  
  
## <a name="remarks"></a>주의  
 텍스트에서 **스트림** 개체, 문자 집합에 지정 된 내용에 텍스트 데이터가 저장 되는 **Charset** 속성입니다. 기본값은 유니코드입니다. **Charset** 속성은로 이동 하는 데이터 변환을 위해 사용 됩니다.는 **스트림** 의 향후 또는 **스트림**합니다. 예를 들어 경우는 **스트림** 포함 iso-8859-1 데이터와 데이터가 BSTR을에 복사 되는 **스트림** 개체 데이터를 유니코드로 변환 됩니다. 그 반대의 경우도 마찬가지입니다.  
  
 열린에 대 한 **스트림**, 현재 [위치](../../../ado/reference/ado-api/position-property-ado.md) 의 시작 부분에 있어야는 **스트림** (0)를 설정 하려면 **Charset**합니다.  
  
 **Charset** 텍스트에만 사용 됩니다 **스트림** 개체 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 은 **adTypeText**). 이 속성은 무시 **형식** 은 **adTypeBinary**합니다.  
  
 코드 샘플을 보려면 [4 단계: 정보 텍스트 상자 채우기](../../../ado/guide/data/step-4-populate-the-details-text-box.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)

