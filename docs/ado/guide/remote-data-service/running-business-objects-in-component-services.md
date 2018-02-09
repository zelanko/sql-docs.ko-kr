---
title: "구성 요소 서비스에서 비즈니스 개체 실행 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: abb4f5b48c17c720c94ced62139c534acebf2e05
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="running-business-objects-in-component-services"></a>구성 요소 서비스에서 비즈니스 개체를 실행합니다.
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 비즈니스 개체는 실행 파일 (.exe) 또는 동적 연결 라이브러리 (.dll) 일 수 있습니다. 비즈니스 개체를 실행할 사용 하는 구성 개체는.dll 또는.exe 파일 인지에 따라 달라 집니다.  
  
-   DCOM을 통해.exe 파일로 만든 비즈니스 개체를 호출할 수 있습니다. 이러한 비즈니스 개체를 통해 인터넷 정보 서비스 (IIS)를 사용 하는 클라이언트 성능이 저하 될 수 있는 데이터의 추가 마샬링 적용 됩니다.  
  
-   비즈니스 개체를 만들 IIS를 통해.dll 파일을 사용할 수 있으므로 HTTP로도 합니다. 있습니다 사용할 수도 있습니다 Microsoft Transaction Server 또는 구성 요소 서비스를 통해만 DCOM을 통해 Windows NT를 사용 하는 경우. 비즈니스 개체 Dll IIS를 통해 액세스 하는 데 IIS 서버 컴퓨터에 등록 해야 합니다. DCOM에서 실행 하는 DLL을 구성 하는 방법에 대 한 내용은 섹션을 참조 [DCOM 실행 되도록 DLL을 사용 하도록 설정](../../../ado/guide/remote-data-service/enabling-a-dll-to-run-on-dcom.md)합니다.  
  
> [!NOTE]
>  구성 요소 서비스 구성 요소로 사용 하 여 중간 계층 비즈니스 개체는 구현 하는 경우 **GetObjectContext**, **SetComplete**, 및 **SetAbort**, 비즈니스 개체가 구성 요소 서비스 (또는 Windows NT를 사용 하는 경우에 MTS)를 사용할 수 컨텍스트 개체 클라이언트에 대 한 여러 호출에서 해당 상태를 유지 합니다. 이 시나리오는 일반적으로 신뢰할 수 있는 클라이언트와 서버의 인트라넷에서 구현 되는 DCOM으로 이전에 가능 합니다. 이 경우에 [.rds입니다 DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) 개체 및 [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) 메서드 클라이언트 쪽에서 트랜잭션 컨텍스트 개체에 의해 대체 됩니다 및 **CreateInstance** 는 에서제공하는메서드를**ITransactionContext** 인터페이스 및 구성 요소 서비스에 의해 구현 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)


