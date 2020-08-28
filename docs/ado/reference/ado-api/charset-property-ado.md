---
description: Charset 속성(ADO)
title: Charset 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 52daa13826bbe372b141501a0c99ac281d3118dc
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975504"
---
# <a name="charset-property-ado"></a>Charset 속성(ADO)
**스트림** 개체의 내부 버퍼에서 저장소에 대해 텍스트 [스트림의](./stream-object-ado.md) 내용을 변환 해야 하는 문자 집합을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **스트림의** 내용이 변환 될 문자 집합을 지정 하는 **문자열** 값을 설정 하거나 반환 합니다. 기본값은 **Unicode**입니다. 허용 되는 값은 인터페이스를 통해 인터넷 문자 집합 이름으로 전달 되는 일반 문자열입니다 (예: "iso-8859-1", "Windows-1252" 등). 시스템에서 알려진 문자 집합 이름 목록은 Windows 레지스트리에서 HKEY_CLASSES_ROOT \MIME\Database\Charset의 하위 키를 참조 하세요.  
  
## <a name="remarks"></a>설명  
 텍스트 **스트림** 개체에서 텍스트 데이터는 **Charset** 속성으로 지정 된 문자 집합에 저장 됩니다. 기본값은 Unicode입니다. **Charset** 속성은 **스트림으로** 이동 하거나 **스트림에서**오는 데이터를 변환 하는 데 사용 됩니다. 예를 들어 **스트림에** ISO-8859-1 데이터가 포함 되어 있고 데이터가 BSTR로 복사 된 경우 **stream** 개체는 데이터를 유니코드로 변환 합니다. 그 반대의 경우도 마찬가지입니다.  
  
 열려 있는 **스트림의**경우 현재 [위치](./position-property-ado.md) 는 **문자**집합을 설정할 수 있도록 **스트림** (0)의 시작 부분에 있어야 합니다.  
  
 **Charset** 은 텍스트 **스트림** 개체 ( **adTypeText**[형식](./type-property-ado-stream.md) )와 함께 사용 됩니다. **형식이** **adtypebinary**인 경우이 속성은 무시 됩니다.  
  
 코드 샘플은 [Step 4: 채우기 The Details 텍스트 상자](../../guide/data/step-4-populate-the-details-text-box.md)를 참조 하세요.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](./stream-object-ado.md)