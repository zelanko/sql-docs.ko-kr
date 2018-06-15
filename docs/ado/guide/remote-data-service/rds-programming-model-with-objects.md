---
title: RDS 프로그래밍 모델 개체와 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9501b819e664e4b0841140f6b3d835773d2e2ed
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274082"
---
# <a name="rds-programming-model-with-objects"></a>RDS 프로그래밍 모델 개체와 사용
RDS의 목표 액세스 하 고 IIS와 같은 매개 자를 통해 데이터 소스를 업데이트 하는 것입니다. 프로그래밍 모델은이 목표를 달성 하는 데 필요한 작업 순서를 지정 합니다. 개체 모델 메서드와 속성이 프로그래밍 모델에 영향을 줄 개체를 지정 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 RDS에는 다음과 같은 일련의 동작을 수행 하는 방법을 제공 합니다.  
  
-   서버에서 호출할 프로그램을 지정 하 고 클라이언트에서 참조 하는 방법 (프록시) ([.rds입니다 DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)).  
  
-   서버 프로그램을 호출 합니다. 데이터 원본과를 식별 하는 서버 프로그램 매개 변수 전달 (프록시 또는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)).  
  
-   서버를 얻기는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) ADO를 사용 하 여 일반적으로 데이터 원본의 개체입니다. 필요에 따라는 **레코드 집합** 서버에서 개체를 처리 하는 ([업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)).  
  
-   서버 프로그램 최종 반환 **레코드 집합** 클라이언트 응용 프로그램 (프록시)에 개체입니다.  
  
-   클라이언트에서의 **레코드 집합** 개체 시각적 컨트롤에서 쉽게 사용할 수 있는 형식으로 변환 됩니다 (시각적 컨트롤 및 **.rds입니다 DataControl**).  
  
-   변경 된 **레코드 집합** 개체는 서버에 다시 전송 되 고 데이터 소스를 업데이트 하는 데 사용 됩니다 (**.rds입니다 DataControl** 또는 **업데이트할**).  
  
## <a name="see-also"></a>관련 항목  
 [RDS 개체 모델 요약](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory 개체 (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [데이터 공간 개체 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS 시나리오](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 자습서](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [RDS 사용량 및 보안](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


