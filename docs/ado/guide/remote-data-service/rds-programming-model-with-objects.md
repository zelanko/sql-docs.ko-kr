---
description: 개체에서 RDS 프로그래밍 모델
title: 개체를 사용 하는 RDS 프로그래밍 모델 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
author: rothja
ms.author: jroth
ms.openlocfilehash: 2658b8b7591284f1624f3649e3980db6e2022726
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977954"
---
# <a name="rds-programming-model-with-objects"></a>개체에서 RDS 프로그래밍 모델
RDS의 목표는 IIS와 같은 중개자를 통해 데이터 원본에 액세스 하 고 업데이트 하는 것입니다. 프로그래밍 모델은이 목표를 달성 하는 데 필요한 활동의 시퀀스를 지정 합니다. 개체 모델은 메서드 및 속성이 프로그래밍 모델에 영향을 주는 개체를 지정 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 RDS는 다음과 같은 일련의 작업을 수행할 수 있는 방법을 제공 합니다.  
  
-   서버에서 호출할 프로그램을 지정 하 고 클라이언트 (RDS)에서 참조 하는 방법 (프록시)을 가져옵니다[. 공간](../../reference/rds-api/dataspace-object-rds.md)).  
  
-   서버 프로그램을 호출 합니다. 데이터 원본 및 실행할 명령 (프록시 또는 RDS)을 식별 하는 서버 프로그램에 매개 변수를 전달 [합니다. DataControl](../../reference/rds-api/datacontrol-object-rds.md)).  
  
-   서버 프로그램은 일반적으로 ADO를 사용 하 여 데이터 원본에서 [레코드 집합](../../reference/ado-api/recordset-object-ado.md) 개체를 가져옵니다. 필요에 따라 **레코드 집합** 개체가 서버 ([RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md))에서 처리 됩니다.  
  
-   서버 프로그램은 최종 **레코드 집합** 개체를 클라이언트 응용 프로그램 (프록시)에 반환 합니다.  
  
-   클라이언트에서 **레코드 집합** 개체는 시각적 컨트롤 (시각적 컨트롤 및 RDS)에서 쉽게 사용할 수 있는 폼에 저장 됩니다 **. DataControl**).  
  
-   **레코드 집합** 개체에 대 한 변경 내용은 서버로 다시 전송 되어 데이터 원본 (RDS)을 업데이트 하는 데 사용 됩니다 **. DataControl** 또는 **RDSServer. DataFactory**).  
  
## <a name="see-also"></a>참고 항목  
 [RDS 개체 모델 요약](./rds-object-model-summary.md)   
 [DataControl 개체 (RDS)](../../reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 개체 (RDSServer)](../../reference/rds-api/datafactory-object-rdsserver.md)   
 [스페이스 개체 (RDS)](../../reference/rds-api/dataspace-object-rds.md)   
 [RDS 시나리오](./rds-scenario.md)   
 [RDS 자습서](./rds-tutorial.md)   
 [레코드 집합 개체 (ADO)](../../reference/ado-api/recordset-object-ado.md)   
 [RDS 사용량 및 보안](./rds-usage-and-security.md)