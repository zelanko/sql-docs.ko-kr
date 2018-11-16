---
title: SetDefaults 메서드 (ServerSettings 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: 76e4cfab-4b15-4da4-bb2f-8aac6f927f79
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 5e7a9dfd6d68f25b98469a79850444fc4726d785
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51668082"
---
# <a name="setdefaults-method-serversettings-class"></a>SetDefaults 메서드(ServerSettings 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  인스턴스에 대 한 모든 기본값을 설정 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기존 데이터 덮어쓰기 옵션을 사용 하 여 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>부분  
 *object*  
 A [ServerSettings 클래스](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md) 나타내는 개체를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트 인스턴스.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*OverwriteAll*|인스턴스의 기존 값을 덮어쓸지 여부를 지정 하는 부울 값 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: **true** 기존 데이터를 덮어쓰고 또는 **false** 경우 기존 데이터를 덮어쓰지 않습니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 u**int32** 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
