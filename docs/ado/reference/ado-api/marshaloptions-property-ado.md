---
description: MarshalOptions 속성(ADO)
title: MarshalOptions 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e7e574836f09df6f3bb8fdb078661c85cbf6355
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990674"
---
# <a name="marshaloptions-property-ado"></a>MarshalOptions 속성(ADO)
서버에 다시 마샬링할 레코드 [집합](./recordset-object-ado.md) 의 레코드를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 [MarshalOptionsEnum](./marshaloptionsenum.md) 값을 설정 하거나 반환 합니다. 기본값은 **adMarshalAll**입니다.  
  
## <a name="remarks"></a>설명  
 클라이언트 쪽 [레코드 집합](./recordset-object-ado.md)을 사용 하는 경우 클라이언트에서 수정 된 레코드는 마샬링 기법 (스레드 또는 프로세스 경계를 넘어 인터페이스 메서드 매개 변수를 패키징 및 전송 하는 프로세스)을 통해 중간 계층 이나 웹 서버에 다시 기록 됩니다. **MarshalOptions** 속성을 설정 하면 수정 된 원격 데이터를 중간 계층 또는 웹 서버로 다시 업데이트 하기 위해 마샬링할 때 성능이 향상 될 수 있습니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 이 속성은 클라이언트 쪽 **레코드 집합**에만 사용 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [MarshalOptions 속성 예제 (VB)](./marshaloptions-property-example-vb.md)   
 [MarshalOptions 속성 예제(VC++)](./marshaloptions-property-example-vc.md)