---
title: ChangePassword 메서드 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords:
- ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 981f2e5b801cd35b0aedb04e5f1aa11b741e4535
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708008"
---
# <a name="changepassword-method-adox"></a>ChangePassword 메서드(ADOX)
암호를 변경 된 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 계정.  
  
## <a name="syntax"></a>구문  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>매개 변수  
 *OldPassword*  
 A **문자열** 사용자의 기존 암호를 지정 하는 값입니다. 사용자 암호가 현재 없는 경우 빈 문자열을 사용 하 여 ("")에 대 한 *OldPassword*합니다.  
  
 *NewPassword*  
 A **문자열** 새 암호를 지정 하는 값입니다.  
  
## <a name="remarks"></a>Remarks  
 보안상의 이유로 새 암호 외에도 이전 암호를 지정 해야 합니다.  
  
 공급자 트러스트를 받을 대상 속성의 관리를 지원 하지 않는 경우 오류가 발생 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>관련 항목  
 [Groups 및 Users Append, ChangePassword 메서드 예제(VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
