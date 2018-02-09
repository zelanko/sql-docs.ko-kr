---
title: "DataFactory 개체 (RDSServer) | Microsoft Docs"
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
apitype: COM
helpviewer_keywords:
- DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db11cc8488b2ca2d3083ca95ac124cbe15b5313c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="datafactory-object-rdsserver"></a>DataFactory 개체 (RDSServer)
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 이 기본 서버 쪽 비즈니스 개체는 클라이언트 쪽 응용 프로그램에 대 한 지정 된 데이터 원본 데이터 읽기/쓰기 권한을 제공 하는 메서드를 구현 합니다.  
  
 **업데이트할** 개체는 클라이언트 요청을 수신 하는 서버 쪽 자동화 개체도 설계 되었습니다. 인터넷 구현에서이 클래스는 웹 서버에 상주 하며 ADISAPI 구성 요소에 의해 인스턴스화됩니다. **업데이트할** 개체 읽기를 제공 하 고 지정 된 데이터에 대 한 쓰기 원본, 하지만 모든 유효성 검사 또는 비즈니스 규칙 논리를 포함 하지 않습니다.  
  
 둘 다에서 사용할 수 있는 메서드를 사용 하는 경우는 **업데이트할** 및 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체를 사용 하 여 원격 데이터 서비스는 **.rds입니다 DataControl** 기본적으로 버전입니다. 기본값에는 기본 프로그래밍 시나리오에서 가정 여기서는 **업데이트할** 일반적인 서버 쪽 비즈니스 개체 역할을 합니다.  
  
 작업별 서버 쪽 처리를 처리 하도록 웹 응용 프로그램을 원하는 경우 교체할 수 있습니다는 **업데이트할** 사용자 지정 비즈니스 개체를 사용 합니다.  
  
 호출 하는 서버 쪽 비즈니스 개체를 만들 수는 **업데이트할** 메서드 같은 [쿼리](../../../ado/reference/rds-api/query-method-rds.md) 및 [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)합니다. 이렇게 하면 비즈니스 개체에 기능을 추가 하지만 기존 원격 데이터 서비스 기술을 활용 하려는 경우에 유용 합니다.  
  
 **DataFactory** 개체 클라이언트 쪽에서 실행 되는 스크립트에 안전 하지 않습니다.  
  
 에 대 한 클래스 ID는 **업데이트할** 개체는 9381D8F5-0288-11 D 0-9501-00AA00B911A5 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [DataFactory 개체(RDSServer) 속성, 메서드 및 이벤트](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [DataFactory 개체, Query 메서드 및 CreateObject 메서드 예제(VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


