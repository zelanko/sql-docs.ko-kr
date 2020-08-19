---
description: SetServiceAccount 메서드(SqlService 클래스)
title: SetServiceAccount 메서드 (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetServiceAccount Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceAccount method
ms.assetid: d5782892-e9d8-4d48-92af-b3afe9610f84
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 898d6a1eae5cf82915bc4647690b3ce991aa3352
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460045"
---
# <a name="setserviceaccount-method-sqlservice-class"></a>SetServiceAccount 메서드(SqlService 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  서비스 인스턴스가 실행되는 사용자 이름과 암호를 변경합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetServiceAccount(ServiceStartName , ServiceStartPassword)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서비스를 나타내는 [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *ServiceStartName*  
 서비스가 실행되는 계정 이름을 지정하는 문자열 값입니다. 서비스 유형에 따라 다를 수 있지만 계정 이름 형식은 DomainName\Username일 수 있습니다. 서비스 프로세스는 실행 시 다음 두 형식 중 하나를 사용하여 로그온됩니다.  
  
-   계정이 기본 제공 도메인에 속하는 경우에는 \Username을 지정할 수 있습니다.  
  
-   NULL을 지정 하면 서비스는 **LocalSystem** 계정으로 로그온 됩니다.  
  
 커널 또는 시스템 수준 드라이버의 경우 *StartName* 에는 i/o 시스템에서 장치 드라이버를 로드 하는 데 사용 하는 \FileSystem\Rdr 또는 \Driver\Xns 드라이버 개체 이름이 포함 됩니다. NULL을 지정하면 I/O 시스템에서 서비스 이름을 기반으로 만든 기본 개체 이름(예: DWDOM\Admin)으로 드라이버가 실행됩니다.  
  
 *ServiceStartPassword*  
 *StartName* 매개 변수의 계정 이름에 대 한 암호를 지정 하는 문자열 값입니다. 암호를 변경하지 않으려면 NULL을 지정하고, 서비스에 암호가 없으면 빈 문자열을 지정합니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 **uint32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
