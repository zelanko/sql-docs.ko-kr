---
title: "마샬링 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 01ea12405f6b00ba834b624403891d4ddf66d066
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="marshaloptions-property-ado"></a>마샬링 속성 (ADO)
레코드를 지정 된 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 서버에 다시 마샬링해야 하는 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 [MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md) 값입니다. 기본값은 **adMarshalAll**합니다.  
  
## <a name="remarks"></a>주의  
 클라이언트 쪽을 사용 하는 경우 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 클라이언트에서 수정 된 레코드는 중간 계층 또는 마샬링을 패키지 하 고 인터페이스 메서드를 보내는 프로세스 라는 기술을 통해 웹 서버에 다시 기록 스레드 또는 프로세스 경계를 넘어 매개 변수입니다. 설정의 **마샬링** 속성 중간 계층 또는 웹 서버에 다시 쓰여집니다 수정 된 원격 데이터를 마샬링하는 경우 성능을 개선할 수 있습니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에만이 속성은 사용 **레코드 집합**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [마샬링 예제 (VB)](../../../ado/reference/ado-api/marshaloptions-property-example-vb.md)   
 [MarshalOptions 속성 예제(VC++)](../../../ado/reference/ado-api/marshaloptions-property-example-vc.md)   

