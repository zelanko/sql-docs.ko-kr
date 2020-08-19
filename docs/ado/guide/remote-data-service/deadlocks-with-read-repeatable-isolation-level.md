---
description: 읽기 반복 가능 격리 수준으로 인한 교착 상태
title: 반복 읽기 격리 수준을 사용한 교착 상태 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 398fd636c7e7ebfce448d5b7ebfae7a62d7c1a2b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452215"
---
# <a name="deadlocks-with-read-repeatable-isolation-level"></a>읽기 반복 가능 격리 수준으로 인한 교착 상태
사용자 지정 비즈니스 개체에서 반복 읽기의 격리 수준을 사용 하 여 SQL Server에 액세스 하 고, 동일한 트랜잭션에서 쿼리 및 업데이트를 전송 하는 두 클라이언트에서 비즈니스 개체를 동시에 호출 하는 경우 교착 상태가 발생할 수 있습니다. 원격 데이터 서비스는 프로세스 중 하나가 시간 초과 되어 교착 상태를 해제할 수 있도록 설계 되었지만 해당 클라이언트에 대 한 업데이트는 실패 합니다.  
  
 [Cursor Service](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) **Command time out** 동적 속성을 사용 하 여 시간 제한의 길이를 수정할 수 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)



