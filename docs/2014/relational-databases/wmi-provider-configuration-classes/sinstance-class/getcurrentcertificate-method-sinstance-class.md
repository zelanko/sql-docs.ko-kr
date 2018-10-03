---
title: GetCurrentCertificate 메서드 (SInstance 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- GetCurrentCertificate Method (SInstance Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- GetCurrentCertificate method
ms.assetid: 9d2b72df-cb21-414a-abef-917f13d4de62
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5a5a5bb76cc99d859a459745f3c1315c35acc815
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48221702"
---
# <a name="getcurrentcertificate-method-sinstance-class"></a>GetCurrentCertificate 메서드(SInstance 클래스)
  현재 보안 인증서를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.GetCurrentCertificate(  
SHA  
)  
  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [인스턴스의 서버 설정을 나타내는](sinstance-class.md) SInstance 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*SHA*|메서드가 완료된 후 현재 보안 인증서를 지정하는 문자열 개체 값(출력 매개 변수)입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 `uint32` 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
