---
title: 번호 Off지연과 지연 속성 (SInstance)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- NumberOfFlags Property (SInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- NumberOfFlags property
ms.assetid: b62005f8-9af3-4fc8-9344-a1ccdb713053
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 053a53cff621cedc29e8583ebca354c9c067774a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73659070"
---
# <a name="numberofflags-property-sinstance-class"></a>NumberOfFlags 속성(SInstance 클래스)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  인스턴스의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]플래그 수를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.NumberOfFlags [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 서버 인스턴스를 나타내는 [Sinstance 클래스](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md) 개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 인스턴스의 플래그 수를 지정 하는 **uint32** 값입니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
