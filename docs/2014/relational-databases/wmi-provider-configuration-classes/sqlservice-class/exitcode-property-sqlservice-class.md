---
title: ExitCode 속성 (SqlService 클래스) | Microsoft Docs
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
- ExitCode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c1866ced05724a95f17ebcd8e73af60412c5289e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184000"
---
# <a name="exitcode-property-sqlservice-class"></a>ExitCode 속성(SqlService 클래스)
  서비스를 시작하거나 중지할 때 발생하는 문제를 정의하는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win32 오류 코드를 가져오거나 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.ExitCode [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서비스를 나타내는 [SqlService 클래스](sqlservice-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 종료 코드를 지정하는 `uint32` 값입니다.  
  
## <a name="remarks"></a>Remarks  
 오류가 이 클래스가 나타내는 서비스에 고유한 것이면 이 속성은 ERROR_SERVICE_SPECIFIC_ERROR(1066)로 설정됩니다. 서비스는 실행 중일 때와 정상 종료 시 이 값을 다시 NO_ERROR로 설정합니다.  
  
## <a name="see-also"></a>관련 항목  
 [서비스 시작 및 중지](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  