---
description: RDS 개체 모델 요약
title: RDS 개체 모델 요약 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS objects [ADO], object model summary
- RDS object model [ADO]
ms.assetid: 909f9af7-31db-4eec-ad52-650ce74dac2f
author: rothja
ms.author: jroth
ms.openlocfilehash: e2650f9a80c56856133d1e694a5ea0eb807251f0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977984"
---
# <a name="rds-object-model-summary"></a>RDS 개체 모델 요약
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
|Object|설명|  
|------------|-----------------|  
|[RDS. 스페이스가](../../reference/rds-api/dataspace-object-rds.md)|이 개체에는 서버 프록시를 얻기 위한 메서드가 포함 되어 있습니다. 프록시는 기본 또는 사용자 지정 서버 프로그램 (비즈니스 개체) 일 수 있습니다. 서버 프로그램은 인터넷, 인트라넷 또는 로컬 영역 네트워크에서 호출 되거나 로컬 동적 연결 라이브러리 일 수 있습니다.<br /><br /> **스페이스** 개체는 스크립팅에 안전 합니다.|  
|[RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md)|이 개체는 기본 서버 프로그램을 나타냅니다. 기본 RDS 데이터 검색 및 업데이트 동작을 실행 합니다.<br /><br /> **DataFactory** 개체는 스크립팅에 안전 하지 않습니다.|  
|[RDS. DataControl](../../reference/rds-api/datacontrol-object-rds.md)|이 개체는 RDS를 자동으로 호출할 수 있습니다 **. ** RDSServer 및 **DataFactory** 개체<br /><br /> 이 개체를 사용 하 여 기본 RDS 데이터 검색 또는 업데이트 동작을 호출 합니다.<br /><br /> 또한이 개체는 visual 컨트롤에서 반환 된 **레코드 집합** 개체에 액세스할 수 있는 방법을 제공 합니다.<br /><br /> **DataControl** 개체는 스크립팅에 안전 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [RDS 기본 사항](./rds-fundamentals.md)   
 [RDS 시나리오](./rds-scenario.md)   
 [RDS 자습서](./rds-tutorial.md)   
 [RDS 사용량 및 보안](./rds-usage-and-security.md)