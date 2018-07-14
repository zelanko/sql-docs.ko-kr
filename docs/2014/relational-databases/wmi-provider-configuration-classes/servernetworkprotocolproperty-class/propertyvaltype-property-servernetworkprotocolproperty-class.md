---
title: PropertyValType 속성 (ServerNetworkProtocolProperty 클래스) | Microsoft Docs
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
- PropertyValType Property (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- PropertyValType property
ms.assetid: fbd42e8e-0642-4a19-b3c8-6ce88345145f
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 52331d787707fbd4882055023ba289a60b2dc250
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201123"
---
# <a name="propertyvaltype-property-servernetworkprotocolproperty-class"></a>PropertyValType 속성(ServerNetworkProtocolProperty 클래스)
  참조된 속성에 저장된 값의 데이터 형식을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.PropertyValType [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 A [ServerNetworkProtocolProperty 클래스](servernetworkprotocolproperty-class.md) 인스턴스의 네트워크 프로토콜의 특성을 나타내는 개체입니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 속성 값의 데이터 형식을 지정하는 `uint32` 값입니다. 문자열 값인 경우 0을 반환하고 숫자 형식인 경우 1을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
