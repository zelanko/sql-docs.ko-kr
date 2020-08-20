---
description: StartService 메서드(SqlService 클래스)
title: StartService 메서드 (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- StartService Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- StartService method
ms.assetid: 83dfb6bd-dbd5-45d8-aad2-a11926317f91
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5add2aebb0a2a148b803fadbab454d2d72c2bf3b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485081"
---
# <a name="startservice-method-sqlservice-class"></a>StartService 메서드(SqlService 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  서비스를 시작된 상태로 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.StartService()  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서비스를 나타내는 [SqlService 클래스](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 다음 시작 상태 중 하나를 지정하는 uint32 값입니다.  
  
 0  
 성공했습니다. 요청이 수락되었습니다.  
  
 1  
 지원되지 않습니다. 요청이 지원되지 않습니다.  
  
 2  
 액세스가 거부되었습니다.)가 나타납니다. 사용자에게 적절한 액세스 권한이 없습니다.  
  
 3  
 종속 서비스가 실행 중입니다. 실행 중인 다른 서비스가 이 서비스에 종속되어 있어서 이 서비스를 중지할 수 없습니다.  
  
 4  
 서비스 제어가 잘못되었습니다. 요청한 제어 코드가 잘못되었거나 서비스에 사용할 수 없습니다.  
  
 5  
 서비스에서 제어를 받아들일 수 없습니다. 서비스 상태(Win32_BaseService:State)가 0, 1 또는 2이므로 요청한 제어 코드를 서비스로 보낼 수 없습니다.  
  
 6  
 서비스가 활성화되지 않았습니다. 서비스가 시작되지 않았습니다.  
  
 7  
 서비스 요청 시간이 초과되었습니다. 서비스가 시작 요청에 시기 적절하게 응답하지 않았습니다.  
  
 8  
 알 수 없는 오류가 발생했습니다. 서비스를 시작할 때 알 수 없는 오류가 발생했습니다.  
  
 9  
 경로를 찾을 수 없습니다. 서비스 실행 파일의 디렉터리 경로를 찾을 수 없습니다.  
  
 10  
 서비스가 이미 실행 중입니다. 서비스가 이미 실행되고 있습니다.  
  
 11  
 서비스 데이터베이스가 잠겨 있습니다. 새 서비스를 추가할 데이터베이스가 잠겨 있습니다.  
  
 12  
 서비스 종속성이 삭제되었습니다. 이 서비스의 종속성이 시스템에서 제거되었습니다.  
  
 13  
 서비스 종속성이 실패했습니다. 종속 서비스에서 필요한 서비스를 찾지 못했습니다.  
  
 14  
 서비스를 사용할 수 없습니다. 서비스가 시스템에서 비활성화되었습니다.  
  
 15  
 서비스 로그온이 실패했습니다. 서비스에 시스템에서 실행하기 위한 올바른 인증이 없습니다.  
  
 16  
 서비스가 삭제되도록 표시되었습니다. 시스템에서 이 서비스를 제거하는 중입니다.  
  
 17  
 서비스에 스레드가 없습니다. 서비스에 대한 실행 스레드가 없습니다.  
  
 18  
 순환 종속성입니다. 서비스 시작 시 순환 종속성이 있습니다.  
  
 19  
 이름이 중복됩니다. 같은 이름으로 실행 중인 서비스가 있습니다.  
  
 20  
 이름이 잘못되었습니다. 서비스 이름에 잘못된 문자가 있습니다.  
  
 21  
 매개 변수가 잘못되었습니다. 잘못된 매개 변수가 서비스로 전달되었습니다.  
  
 22  
 서비스 계정이 잘못되었습니다. 이 서비스를 실행할 계정이 잘못되었거나 서비스 실행 권한이 없습니다.  
  
 23  
 서비스가 있습니다. 서비스가 시스템에서 사용할 수 있는 서비스 데이터베이스에 있습니다.  
  
 24  
 서비스가 이미 일시 중지되었습니다. 서비스가 현재 시스템에서 일시 중지되었습니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서비스 시작 및 중지](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
