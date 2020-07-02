---
title: GetCurrentCertificate 메서드 (SecurityCertificate)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- GetCurrentCertificate Method (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GetCurrentCertificate method
ms.assetid: 987a2671-1801-45c4-93e6-29f883c58720
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7934cc4888cc12c49c20fc9f69939c728efd15c4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731420"
---
# <a name="getcurrentcertificate-method-securitycertificate-class"></a>GetCurrentCertificate 메서드(SecurityCertificate 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/applies-to-version/sqlserver.md)]
  현재 보안 인증서를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.GetCurrentCertificate(SHA , SQLInstance)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 보안 인증서를 나타내는 [SecurityCertificate 클래스](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*S*|메서드가 완료된 후 현재 보안 인증서 SHA 지문을 지정하는 문자열 값(출력 매개 변수)입니다.|  
|*SQLInstance*|인증서가 필요한 인스턴스를 지정하는 문자열 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
