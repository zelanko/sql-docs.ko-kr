---
title: MarshalOptions 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 69b9b44fc20fe832bffdd4c03536117a626916ac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697298"
---
# <a name="marshaloptions-property-ado"></a>MarshalOptions 속성(ADO)
레코드를 지정 합니다 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 서버에 다시 마샬링되어야 하는 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 [MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md) 값입니다. 기본값은 **adMarshalAll**합니다.  
  
## <a name="remarks"></a>Remarks  
 클라이언트 쪽을 사용 하는 경우 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 클라이언트에서 수정 된 레코드는 중간 계층 또는 인터페이스 메서드를 보내고 패키징 프로세스 마샬링 이라는 기법을 통해 웹 서버에 다시 기록 됩니다 스레드 또는 프로세스 경계를 넘어 매개 변수입니다. 설정 된 **MarshalOptions** 속성 수정 된 원격 데이터 다시 중간 계층 또는 웹 서버에 업데이트에 대 한 마샬링될 때 성능을 개선할 수 있습니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 이 속성을 사용 하는 클라이언트 쪽 에서만 **레코드 집합**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [MarshalOptions 속성 예제 (VB)](../../../ado/reference/ado-api/marshaloptions-property-example-vb.md)   
 [MarshalOptions 속성 예제(VC++)](../../../ado/reference/ado-api/marshaloptions-property-example-vc.md)   
