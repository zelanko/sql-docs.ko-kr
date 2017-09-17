---
title: "반복 읽기 격리 수준으로 교착 상태 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deadlocks in RDS [ADO]
- read repeatable in RDS [ADO]
ms.assetid: 29f3683f-12f3-4304-8a54-fe133c25a423
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 02e8b890b7973626676b8439471a782d6fba3f27
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="deadlocks-with-read-repeatable-isolation-level"></a>반복 읽기 격리 수준으로 교착 상태
사용자 지정 비즈니스 개체는 격리 수준을 반복 읽기를 사용 하 여 SQL Server에 액세스 하 고 비즈니스 개체는 동시에 쿼리를 보내고 동일한 트랜잭션 내에서 업데이트 하는 두 명의 클라이언트에서 호출 되 면 교착 상태가 가능 합니다. 원격 데이터 서비스는 교착 상태를 해제 하기 위해 제한 시간이 초과 프로세스 중 하나를 허용 하도록 만들어졌지만 해당 클라이언트에 대 한 업데이트가 실패 합니다.  
  
 사용 하 여는 [커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) **명령 제한 시간** 동적 속성을 제한 시간 길이 수정 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)




