---
description: DataFactory 개체(RDSServer)
title: DataFactory 개체 (RDSServer) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a27d7911b00e5172941245ef5dcd587345aa1fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439105"
---
# <a name="datafactory-object-rdsserver"></a>DataFactory 개체(RDSServer)
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 이 기본 서버측 비즈니스 개체는 클라이언트 쪽 응용 프로그램에 대해 지정 된 데이터 원본에 대 한 읽기/쓰기 데이터 액세스를 제공 하는 메서드를 구현 합니다.  
  
 DataFactory 개체는 클라이언트 요청을 수신 하는 서버 쪽 자동화 개체로 설계 **RDSServer.** 인터넷 구현에서이는 웹 서버에 상주 하며 ADISAPI 구성 요소에 의해 인스턴스화됩니다. **RDSServer** 개체는 지정 된 데이터 원본에 대 한 읽기 및 쓰기 권한을 제공 하지만 유효성 검사 또는 비즈니스 규칙 논리를 포함 하지 않습니다.  
  
 DataFactory와 RDS 모두에서 사용할 수 있는 메서드를 사용 하는 경우 **RDSServer** . [ DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체, 원격 데이터 서비스는 RDS를 사용 합니다 **. ** 기본적으로는 DataControl 버전이 있습니다. 기본값은 기본 프로그래밍 시나리오를 가정 합니다. 여기서 **RDSServer는 DataFactory** 가 일반 서버 쪽 비즈니스 개체로 사용 됩니다.  
  
 웹 응용 프로그램에서 작업 관련 서버 쪽 처리를 처리 하 게 하려면 DataFactory를 사용자 지정 비즈니스 개체로 **RDSServer.**  
  
 [Query](../../../ado/reference/rds-api/query-method-rds.md) 및 [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)와 같은 **RDSServer DataFactory** 메서드를 호출 하는 서버 쪽 비즈니스 개체를 만들 수 있습니다. 이는 비즈니스 개체에 기능을 추가 하지만 기존 원격 데이터 서비스 기술을 활용 하려는 경우에 유용 합니다.  
  
 **DataFactory** 개체는 클라이언트 쪽에서 실행 되는 스크립트에는 안전 하지 않습니다.  
  
 **DataFactory** 개체의 클래스 ID는 9381D8F5-0288-11D0-9501-00AA00B911A5입니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [DataFactory 개체(RDSServer) 속성, 메서드 및 이벤트](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [DataFactory 개체, Query 메서드 및 CreateObject 메서드 예제(VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


