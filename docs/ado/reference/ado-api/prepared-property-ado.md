---
title: 준비 된 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
author: rothja
ms.author: jroth
ms.openlocfilehash: 58cce35e57116618137f4ee776901dba2a44eff4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761961"
---
# <a name="prepared-property-ado"></a>준비된 속성(ADO)
실행 전에 [명령의](../../../ado/reference/ado-api/command-object-ado.md) 컴파일된 버전을 저장할지 여부를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **True**로 설정 된 경우 명령을 준비 해야 함을 나타내는 **부울** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **준비** 된 속성을 사용 하 여 공급자가 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체의 첫 번째 실행 전에 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성에 지정 된 준비 된 (또는 컴파일된) 버전의 쿼리를 저장 하도록 합니다. 이렇게 하면 명령의 첫 번째 실행 속도가 느려질 수 있지만 공급자가 명령을 컴파일하면 이후 실행에 대해 컴파일된 버전의 명령이 사용 됩니다 .이로 인해 성능이 향상 됩니다.  
  
 속성이 **False**이면 공급자는 컴파일된 버전을 만들지 않고 **명령** 개체를 직접 실행 합니다.  
  
 공급자가 명령 준비를 지원 하지 않는 경우이 속성이 **True**로 설정 되 면 오류를 반환할 수 있습니다. 공급자가 오류를 반환 하지 않는 경우 단순히 명령을 준비 하는 요청을 무시 하 고 **준비** 된 속성을 **False**로 설정 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [준비 된 속성 예제 (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Prepared 속성 예제(VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
