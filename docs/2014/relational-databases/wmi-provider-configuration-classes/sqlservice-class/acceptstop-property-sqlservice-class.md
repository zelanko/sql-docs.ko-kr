---
title: AcceptStop 속성 (SqlService 클래스) | Microsoft Docs
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
- AcceptStop Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 19197db0e6d2679d0ad13bcb43472be4448fccb7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093023"
---
# <a name="acceptstop-property-sqlservice-class"></a>AcceptStop 속성(SqlService 클래스)
  서비스를 중지할 수 있는지 여부를 지정하는 부울 속성 값을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.AcceptStop [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 A [SqlService 클래스](sqlservice-class.md) 서비스를 나타내는 개체  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서비스를 중지할 수 있는지 여부를 지정하는 부울 값입니다. `true`는 서비스를 중지할 수 있음을 나타내고 `false`는 서비스를 일시 중지할 수 없음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [서비스 시작 및 중지](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  