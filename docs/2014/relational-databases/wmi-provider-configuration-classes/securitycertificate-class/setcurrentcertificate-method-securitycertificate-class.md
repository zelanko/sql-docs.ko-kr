---
title: SetCurrentCertificate 메서드 (SecurityCertificate 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SetCurrentCertificate Method (SecurityCertificate Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetCurrentCertificate method
ms.assetid: 04b1a76a-932d-4824-8506-e346afe7554e
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6dbc39c89311681026b190eb3032ce6a1ecc5981
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092810"
---
# <a name="setcurrentcertificate-method-securitycertificate-class"></a>SetCurrentCertificate 메서드(SecurityCertificate 클래스)
  현재 보안 인증서를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.SetCurrentCertificate(  
SHA , SQLInstance  
)  
  
```  
  
## <a name="parts"></a>부분  
 *object*  
 Securitycertificate [SecurityCertificate 클래스]-class.md) 보안 인증서를 나타내는 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*S H A*|필요한 보안 인증서의 SHA(Secure Hash Algorithm) 지문을 지정하는 문자열 값입니다.|  
|*SQLInstance*|인증서가 필요한 인스턴스를 지정하는 문자열 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 uint32 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  