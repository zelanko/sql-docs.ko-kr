---
title: RDS 개체 모델 요약 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS objects [ADO], object model summary
- RDS object model [ADO]
ms.assetid: 909f9af7-31db-4eec-ad52-650ce74dac2f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 434c27f5e2da0208ba5141664ccc69accfc2fbb2
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704238"
---
# <a name="rds-object-model-summary"></a>RDS 개체 모델 요약
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
|Object|설명|  
|------------|-----------------|  
|[RDS.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)|이 개체는 서버 프록시를 얻을 수 있는 메서드가 포함 됩니다. 프록시는 기본 또는 사용자 지정 서버 프로그램 (비즈니스 개체) 수 있습니다. 서버 프로그램 인터넷, 인트라넷, 로컬 영역 네트워크에서 호출할 수 있습니다 또는 로컬 동적 연결 라이브러리를 수 있습니다.<br /><br /> 합니다 **DataSpace** 개체가 스크립팅 작업에 안전 합니다.|  
|[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|이 개체는 기본 서버 프로그램을 나타냅니다. 기본 RDS 데이터 검색 및 업데이트 동작을 실행합니다.<br /><br /> 합니다 **DataFactory** 개체가 스크립팅 작업에 안전 합니다.|  
|[RDS.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|이 개체를 자동으로 호출할 수는 **rds. DataSpace** 하 고 **업데이트할** 개체입니다.<br /><br /> 이 개체를 사용 하 여 기본 RDS 데이터 검색 또는 업데이트 동작을 호출 합니다.<br /><br /> 또한이 개체는 시각적 컨트롤이 반환 된 액세스를 제공 **레코드 집합** 개체입니다.<br /><br /> 합니다 **DataControl** 개체가 스크립팅 작업에 안전 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 시나리오](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 사용량 및 보안](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


