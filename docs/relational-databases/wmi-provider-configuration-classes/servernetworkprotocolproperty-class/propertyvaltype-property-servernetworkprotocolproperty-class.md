---
title: PropertyValType 속성 (ServerNetworkProtocolProperty)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyValType Property (ServerNetworkProtocolProperty
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyValType property
ms.assetid: fbd42e8e-0642-4a19-b3c8-6ce88345145f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b2a74e515d2dddd58242e4760e3dd33c2c5031f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73659936"
---
# <a name="propertyvaltype-property-servernetworkprotocolproperty-class"></a>PropertyValType 속성(ServerNetworkProtocolProperty 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  참조된 속성에 저장된 값의 데이터 형식을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.PropertyValType [= value]  
```  
  
## <a name="parts"></a>부분  
 *개체가*  
 인스턴스의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]네트워크 프로토콜 특성을 나타내는 [servernetworkprotocolproperty 클래스](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 속성 값의 데이터 형식을 지정 하는 **uint32** 값입니다. 문자열 값인 경우 0을 반환하고 숫자 형식인 경우 1을 반환합니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
