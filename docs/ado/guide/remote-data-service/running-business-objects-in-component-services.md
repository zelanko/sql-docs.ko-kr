---
description: 구성 요소 서비스에서 비즈니스 개체 실행
title: 구성 요소 서비스에서 비즈니스 개체 실행 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- component services in RDS [ADO]
ms.assetid: 3077d0b6-42d6-4f10-8e5d-42e6204f1109
author: rothja
ms.author: jroth
ms.openlocfilehash: 4343d8e1bd04d7e8044fa7f3f1b5de6184466d3f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977724"
---
# <a name="running-business-objects-in-component-services"></a>구성 요소 서비스에서 비즈니스 개체 실행
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 비즈니스 개체는 실행 파일 (.exe) 또는 동적 연결 라이브러리 (.dll) 일 수 있습니다. 비즈니스 개체를 실행 하는 데 사용 하는 구성은 개체가 .dll 또는 .exe 파일 인지 여부에 따라 달라 집니다.  
  
-   .Exe 파일로 만든 비즈니스 개체는 DCOM을 통해 호출할 수 있습니다. 이러한 비즈니스 개체를 인터넷 정보 서비스 (IIS)를 통해 사용 하는 경우 추가 데이터 마샬링이 적용 되므로 클라이언트 성능이 저하 됩니다.  
  
-   .Dll 파일로 만든 비즈니스 개체를 IIS를 통해 사용할 수 있으므로 HTTP를 통해서도 사용할 수 있습니다. 또한 Windows NT를 사용 하는 경우에는 구성 요소 서비스 또는 Microsoft 트랜잭션 서버를 통해서만 DCOM을 통해 사용할 수 있습니다. Iis를 통해 액세스 하려면 비즈니스 개체 Dll을 IIS 서버 컴퓨터에 등록 해야 합니다. DCOM에서 실행 되도록 DLL을 구성 하는 방법에 대 한 자세한 내용은 [dcom에서 Dll 실행을 활성화](./enabling-a-dll-to-run-on-dcom.md)하는 섹션을 참조 하세요.  
  
> [!NOTE]
>  중간 계층의 비즈니스 개체가 **Getobjectcontext**, **Setcomplete**및 **SetAbort**를 사용 하 여 구성 요소 서비스 구성 요소로 구현 되는 경우 비즈니스 개체는 구성 요소 서비스 (또는 Windows NT를 사용 하는 경우 MTS)를 사용 하 여 여러 클라이언트 호출에서 상태를 유지할 수 있습니다. 이 시나리오는 일반적으로 신뢰할 수 있는 클라이언트와 인트라넷의 서버 간에 구현 되는 DCOM에서 가능 합니다. 이 경우 [RDS. ](../../reference/rds-api/dataspace-object-rds.md)클라이언트 쪽의 공간 개체 및 [CreateObject](../../reference/rds-api/createobject-method-rds.md) 메서드는 **ITransactionContext** 인터페이스에서 제공 되 고 구성 요소 서비스에 의해 구현 되는 트랜잭션 컨텍스트 개체 및 **CreateInstance** 메서드로 대체 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [RDS 기본 사항](./rds-fundamentals.md)