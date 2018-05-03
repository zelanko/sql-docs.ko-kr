---
title: InvokeService (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InvokeService [RDS]
ms.assetid: ad45c676-ec7e-4a3a-9a6b-a54f75eb3012
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 875c2635c196df61dd087240603ae339c08c7b2b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="invokeservice-rds"></a>InvokeService (RDS)
기능이 더 많은 버전의 개체에 요청된 된 인터페이스에 대 한 포인터를 반환합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>매개 변수  
 *riid*  
  
 [in] 요청 된 인터페이스의 식별자입니다.  
  
 *punkNotSoFunctionalInterface*  
  
 [in] 기능이 적은 소스 개체입니다.  
  
 *ppunkMoreFunctionalInterface*  
  
 [out] 요청 된 인터페이스 포인터를 받는 포인터 변수의 주소 *riid*합니다. 성공적으로 반환 되는 *ppunkMoreFunctionalInterface* 매개 변수 개체에는 요청 된 인터페이스 포인터를 포함 합니다. 개체에 지정 된 인터페이스를 지원 하지 않는 경우 *riid*, *ppunkMoreFunctionalInterface* NULL로 설정 됩니다.  
  
## <a name="return-value"></a>반환 값  
 여부를 나타내는 HRESULT 값에 대 한 호출에서 **InvokeService** 메서드 성공 했습니다.  
  
## <a name="remarks"></a>주의  
 RDS 커서 엔진 구현 **InvokeService** 입력된 행 집합 (또는 여러 결과 개체)는 입력된 행 집합에서 커서 엔진 채우고 다음 자신에 대 한 포인터를 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [IRDSService 인터페이스(RDS)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>관련 항목:  
 [RDS 메서드](../../../ado/reference/rds-api/rds-methods.md)


