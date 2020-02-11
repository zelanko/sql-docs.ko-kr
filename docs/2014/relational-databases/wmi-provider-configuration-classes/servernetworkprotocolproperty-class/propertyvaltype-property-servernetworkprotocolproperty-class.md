---
title: PropertyValType 속성 (ServerNetworkProtocolProperty 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4a69cb8f0817c086537381a87b96dfb237b8d59c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62643191"
---
# <a name="propertyvaltype-property-servernetworkprotocolproperty-class"></a>PropertyValType 속성(ServerNetworkProtocolProperty 클래스)
  참조된 속성에 저장된 값의 데이터 형식을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.PropertyValType [= value]  
```  
  
## <a name="parts"></a>부분  
 *개체가*  
 인스턴스의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]네트워크 프로토콜 특성을 나타내는 [servernetworkprotocolproperty 클래스](servernetworkprotocolproperty-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 속성 값의 데이터 형식을 지정하는 `uint32` 값입니다. 문자열 값인 경우 0을 반환하고 숫자 형식인 경우 1을 반환합니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
