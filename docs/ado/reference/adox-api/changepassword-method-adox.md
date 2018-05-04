---
title: ChangePassword 메서드 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords:
- ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 111f549f419404b8174d90e3d1298a7c3789913d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="changepassword-method-adox"></a>ChangePassword 메서드 (ADOX)
암호를 변경 하면는 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 계정.  
  
## <a name="syntax"></a>구문  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>매개 변수  
 *OldPassword*  
 A **문자열** 기존 사용자의 암호를 지정 하는 값입니다. 없으면 사용자 현재 암호를 사용 하 여 빈 문자열 ("")에 대 한 *OldPassword*합니다.  
  
 *새 암호*  
 A **문자열** 새 암호를 지정 하는 값입니다.  
  
## <a name="remarks"></a>주의  
 보안상의 이유로 새 암호 외에도 이전 암호를 지정 해야 합니다.  
  
 공급자 트러스트를 받을 대상 속성의 관리를 지원 하지 않는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Groups 및 Users Append, ChangePassword 메서드 예제(VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
