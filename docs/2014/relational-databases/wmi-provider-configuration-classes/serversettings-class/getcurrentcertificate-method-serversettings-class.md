---
title: GetCurrentCertificate 메서드 (ServerSettings 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- GetCurrentCertificate Method (ServerSettings Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- GetCurrentCertificate method
ms.assetid: 450e33c6-91d4-420f-ab7c-1905111f5658
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4b68c9be215354ed96646baa4a997b675d8c9b74
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995872"
---
# <a name="getcurrentcertificate-method-serversettings-class"></a>GetCurrentCertificate 메서드(ServerSettings 클래스)
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
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 서버 설정을 나타내는 `ServerSettings` 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*S*|메서드가 완료된 후 현재 보안 인증서를 지정하는 문자열 개체 값(출력 매개 변수)입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 `uint32` 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
