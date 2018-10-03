---
title: Charset 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Charset
helpviewer_keywords:
- Charset property [ADO]
ms.assetid: e42507cb-9b46-4ce4-8191-2948eaf14ca2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20fff124f33bfeccaec665c74687753e2c0af20b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47752341"
---
# <a name="charset-property-ado"></a>Charset 속성(ADO)
문자는 집합을 나타냅니다 텍스트 내용의 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 저장소의 내부 버퍼에 대 한 변환 되어야 합니다 **Stream** 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환를 **문자열** 넣을 문자를 지정 하는 값이 설정의 내용을 합니다 **Stream** 변환 됩니다. 기본값은 **유니코드**합니다. 허용 되는 값은 인터넷 문자 집합 이름 (예: "iso-8859-1", "Windows-1252" 및 등)으로 인터페이스를 통해 전달 하는 일반적인 문자열입니다. 시스템에서 알려진 문자 집합 이름의 목록을 Windows 레지스트리에서 HKEY_CLASSES_ROOT\MIME\Database\Charset의 하위 키를 참조 하세요.  
  
## <a name="remarks"></a>Remarks  
 텍스트에서 **Stream** 개체를 텍스트 데이터는 지정 된 문자 집합에 저장 됩니다 합니다 **Charset** 속성입니다. 기본값은 유니코드입니다. **Charset** 속성은 데이터를 변환 하는 데 사용 됩니다.는 **Stream** 의 앞 또는 **Stream**합니다. 예를 들어 경우는 **Stream** ISO-8859-1 데이터와 데이터를 BSTR 복사 되도록 합니다 **Stream** 개체는 데이터를 유니코드로 변환 합니다. 그 반대의 경우도 마찬가지입니다.  
  
 개방적이 고에 대 한 **Stream**, 현재 [위치](../../../ado/reference/ado-api/position-property-ado.md) 의 시작 부분에 있어야 합니다 **Stream** (0)를 설정할 수 **Charset**.  
  
 **Charset** 텍스트에만 사용 됩니다 **Stream** 개체 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 됩니다 **adTypeText**). 하는 경우이 속성은 무시 됩니다 **형식** 됩니다 **adTypeBinary**합니다.  
  
 코드 샘플을 보려면 [4 단계: 정보 텍스트 상자를 채우는](../../../ado/guide/data/step-4-populate-the-details-text-box.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
