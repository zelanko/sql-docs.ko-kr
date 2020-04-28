---
title: InvokeService (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InvokeService [RDS]
ms.assetid: ad45c676-ec7e-4a3a-9a6b-a54f75eb3012
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86ebb27ebdc5de5a045304afe45cd8653e491827
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963869"
---
# <a name="invokeservice-rds"></a>InvokeService(RDS)
개체의 지원 되는 버전에서 요청 된 인터페이스에 대 한 포인터를 반환 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>매개 변수  
 *riid*  
  
 진행 요청 되는 인터페이스의 식별자입니다.  
  
 *punkNotSoFunctionalInterface*  
  
 진행 지원 되지 않는 소스 개체입니다.  
  
 *ppunkMoreFunctionalInterface*  
  
 제한이 *Riid*에서 요청 된 인터페이스 포인터를 받는 포인터 변수의 주소입니다. 반환이 성공적 이면 *ppunkMoreFunctionalInterface* 매개 변수는 개체에 대 한 요청 된 인터페이스 포인터를 포함 합니다. 개체에서 *riid*에 지정 된 인터페이스를 지원 하지 않는 경우 *ppunkMoreFunctionalInterface* 가 NULL로 설정 됩니다.  
  
## <a name="return-value"></a>Return Value  
 **InvokeService** 메서드에 대 한 호출이 성공 했는지 여부를 나타내는 HRESULT 값입니다.  
  
## <a name="remarks"></a>설명  
 **InvokeService** 의 RDS 커서 엔진 구현에서는 입력 행 집합 (또는 여러 결과 개체)을 사용 하 여 입력 행 집합에서 커서 엔진을 채운 다음 자체에 대 한 포인터를 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [IRDSService 인터페이스(RDS)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [RDS 메서드](../../../ado/reference/rds-api/rds-methods.md)


