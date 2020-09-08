---
description: SetValue 메서드(ServerSettingsGeneralFlag 클래스)
title: SetValue 메서드 (ServerSettingsGeneralFlag)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetValue Method (ServerSettingsGeneralFlag Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetValue method
ms.assetid: a889feac-c0e0-4635-b506-843863d86967
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 87d6daffaee3454dbb53decaf15aafe9750e1800
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89517395"
---
# <a name="setvalue-method-serversettingsgeneralflag-class"></a>SetValue 메서드(ServerSettingsGeneralFlag 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  참조된 플래그의 모든 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetValue(Value)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서버 설정에 대한 일반 플래그를 나타내는 [ServerSettingsGeneralFlag 클래스](../../../relational-databases/wmi-provider-configuration-classes/serversettingsgeneralflag-class/serversettingsgeneralflag-class.md) 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*값*|플래그의 값을 지정하는 부울 값입니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
