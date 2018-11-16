---
title: 반복 읽기 격리 수준으로 교착 상태 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deadlocks in RDS [ADO]
- read repeatable in RDS [ADO]
ms.assetid: 29f3683f-12f3-4304-8a54-fe133c25a423
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a063bfa08ee0c405b52c123f0af03397751a2289
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558441"
---
# <a name="deadlocks-with-read-repeatable-isolation-level"></a>읽기 반복 가능 격리 수준으로 인한 교착 상태
사용자 지정 비즈니스 개체를 격리 수준을 반복 읽기를 사용 하 여 SQL Server에 액세스 하 고 비즈니스 개체는 쿼리를 보내고 동일한 트랜잭션에서 업데이트 하는 두 명의 클라이언트에서 동시에 호출 됩니다, 경우에 교착 상태가 발생 가능성이 있습니다. 원격 데이터 서비스는 교착 상태를 해제 하려면 시간 초과 프로세스 중 하나를 허용 하도록 만들어졌지만 해당 클라이언트에 대 한 업데이트가 실패 합니다.  
  
 사용 된 [커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) **명령 제한 시간** 제한의 길이 수정 하려면 동적 속성입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)



