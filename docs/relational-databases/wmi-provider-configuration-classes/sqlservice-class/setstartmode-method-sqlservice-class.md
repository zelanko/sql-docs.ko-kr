---
title: SetStartMode 메서드 (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetStartMode Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStartMode method
ms.assetid: f6f198b4-f9a4-468c-8977-76462ef06e61
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: edd3b4a5fa4d787292f1978da80c5f7803242010
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73660906"
---
# <a name="setstartmode-method-sqlservice-class"></a>SetStartMode 메서드(SqlService 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  서비스 인스턴스의 시작 모드를 수정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetStartMode(StartMode)  
```  
  
## <a name="parts"></a>부분  
 *개체가*  
 서비스를 나타내는 [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *StartMode*  
 서비스 인스턴스의 시작 모드를 지정하는 **uint32** 값입니다.  
  
 유효한 값은 다음과 같습니다.  
  
 값 = 0. 부팅 - 운영 체제 로더에 의해 디바이스 드라이버가 시작됩니다. 이 값은 드라이버 서비스에 대해서만 유효합니다.  
  
 값 = 1입니다. 시스템 - **IoInitSystem** 메서드에 의해 디바이스 드라이버가 시작됩니다. 이 값은 드라이버 서비스에 대해서만 유효합니다.  
  
 값 = 2입니다. 자동 - 시스템 시작 중 서비스 제어 관리자에 의해 자동으로 서비스가 시작됩니다.  
  
 값 = 3입니다. 수동 - 프로세스에서 **StartService** 메서드를 호출할 때 컴퓨터 관리자에 의해 서비스가 시작됩니다.  
  
 값 = 4입니다. 사용 안 함 - 서비스를 더 이상 시작할 수 없습니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 
  **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
