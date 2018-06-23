---
title: SetDefaults 메서드 (ClientSettings 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SetDefaults Method (ClientSettings Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDefaults method
ms.assetid: 056508f3-a5c8-467c-a196-dc1ef1f5178f
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 58cfbe5b2a53bfdce97037602058466ccd1af187
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181301"
---
# <a name="setdefaults-method-clientsettings-class"></a>SetDefaults 메서드(ClientSettings 클래스)
  인스턴스에 대 한 모든 기본값을 설정는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기존 데이터 덮어쓰기 옵션을 사용 하 여 클라이언트입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.SetDefaults(  
OverwriteAll  
)  
  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 인스턴스를 나타내는 `ClientSettings` 개체입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*OverwriteAll*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 인스턴스의 기존 값을 덮어쓸지 여부를 지정하는 부울 값입니다. `true`인 경우 기존 데이터를 덮어쓰고 `false`인 경우 기존 데이터를 덮어쓰지 않습니다.|  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 `uint32` 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  