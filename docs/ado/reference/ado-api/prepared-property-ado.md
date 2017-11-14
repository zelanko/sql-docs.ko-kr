---
title: "속성 (ADO)를 준비 | Microsoft Docs"
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
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f47836c824401e5ca49edd5eac33c2f6f6393993
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="prepared-property-ado"></a>준비 된 속성 (ADO)
컴파일된 버전을 저장할지 여부를 나타냅니다는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 실행 하기 전에.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **부울** 값으로 설정 **True**, 명령을 준비할 나타냅니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **Prepared** 속성에 지정 된 쿼리 준비 된 (또는 컴파일된) 버전을 저장 하는 공급자에 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 하기 전에 속성을 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체의 첫 번째 실행 합니다. 명령의 첫 번째 실행 속도가 느려질 수 있습니다이 있지만 공급자 명령의 컴파일된 버전 성능이 향상 됩니다. 후속 실행에 대 한 사용 하는 명령을 컴파일한, 합니다.  
  
 속성이 **False**, 공급자는 실행의 **명령** 컴파일된 버전을 만들지 않고 직접 개체입니다.  
  
 이 속성 설정 된 경우 오류를 반환 합니다 공급자 명령 준비를 지원 하지 않는 경우 **True**합니다. 명령 및 집합을 준비 하려면 요청 무시 하기만 공급자 오류를 반환 하지는 **Prepared** 속성을 **False**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [준비 속성 예제 (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Prepared 속성 예제(VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   

