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
ms.openlocfilehash: 0212f3b4cb663bd56adaa1bdbc3ab6675c3ce888
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67932278"
---
# <a name="marshaloptions-property-ado"></a>MarshalOptions 속성(ADO)
서버에 다시 마샬링할 레코드 [집합](../../../ado/reference/ado-api/recordset-object-ado.md) 의 레코드를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 [MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md) 값을 설정 하거나 반환 합니다. 기본값은 **adMarshalAll**입니다.  
  
## <a name="remarks"></a>설명  
 클라이언트 쪽 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)을 사용 하는 경우 클라이언트에서 수정 된 레코드는 마샬링 기법 (스레드 또는 프로세스 경계를 넘어 인터페이스 메서드 매개 변수를 패키징 및 전송 하는 프로세스)을 통해 중간 계층 이나 웹 서버에 다시 기록 됩니다. **MarshalOptions** 속성을 설정 하면 수정 된 원격 데이터를 중간 계층 또는 웹 서버로 다시 업데이트 하기 위해 마샬링할 때 성능이 향상 될 수 있습니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 이 속성은 클라이언트 쪽 **레코드 집합**에만 사용 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [MarshalOptions 속성 예제 (VB)](../../../ado/reference/ado-api/marshaloptions-property-example-vb.md)   
 [MarshalOptions 속성 예제(VC++)](../../../ado/reference/ado-api/marshaloptions-property-example-vc.md)   
