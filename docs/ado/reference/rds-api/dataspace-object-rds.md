---
description: DataSpace 개체(RDS)
title: 스페이스 개체 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
author: rothja
ms.author: jroth
ms.openlocfilehash: 092af21c57b733e12c233cb201304cbc27930c80
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768382"
---
# <a name="dataspace-object-rds"></a>DataSpace 개체(RDS)
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 중간 계층에 있는 사용자 지정 비즈니스 개체에 대 한 클라이언트 쪽 프록시를 만듭니다.  
  
 원격 데이터 서비스는 클라이언트 쪽 구성 요소가 중간 계층에 있는 비즈니스 개체와 통신할 수 있도록 비즈니스 개체 프록시가 필요 합니다. 프록시는 프로세스 또는 컴퓨터 경계를 넘어 응용 프로그램의 [레코드 집합](../ado-api/recordset-object-ado.md) 데이터에 대 한 패키징, unpackaging 및 전송 (마샬링)을 용이 하 게 합니다.  
  
 원격 데이터 서비스는 RDS를 사용 **합니다. ** 비즈니스 개체 프록시를 만들기 위한 공간 개체의 [CreateObject](./createobject-method-rds.md) 메서드 비즈니스 개체 프록시는 해당 중간 계층 비즈니스 개체의 인스턴스가 만들어질 때마다 동적으로 생성 됩니다. 원격 데이터 서비스는 HTTP, HTTPS (HTTP Secure Sockets), DCOM 및 in-process (클라이언트 구성 요소와 비즈니스 개체가 동일한 컴퓨터에 상주) 프로토콜을 지원 합니다.  
  
> [!NOTE]
>  Rds는 Rds를 사용할 때 "상태 비저장" 방식으로 동작 합니다 **. 스페이스** 개체는 HTTP 또는 HTTPS 프로토콜을 사용 합니다. 즉, 서버에서 응답을 반환한 후 클라이언트 요청에 대 한 모든 내부 정보를 삭제 합니다.  
  
> [!NOTE]
>  비즈니스 개체가 비즈니스 개체 프록시의 수명 동안 존재 하는 것 처럼 보이지만 비즈니스 개체는 실제로 응답이 요청으로 전송 될 때까지 존재 합니다. 요청을 실행 하는 경우 (즉, 메서드가 비즈니스 개체에서 호출 되는 경우) 프록시는 서버에 대 한 새 연결을 열고 서버는 비즈니스 개체의 새 인스턴스를 만듭니다. 비즈니스 개체가 요청에 응답 하면 서버에서 비즈니스 개체를 삭제 하 고 연결을 닫습니다.  
  
> [!NOTE]
>  이 동작은 비즈니스 개체 속성 또는 변수를 사용 하 여 한 요청에서 다른 요청으로 데이터를 전달할 수 없음을 의미 합니다. 상태 데이터를 유지 하려면 파일 또는 메서드 인수와 같은 다른 메커니즘을 사용 해야 합니다.  
  
 RDS의 클래스 ID **입니다. 스페이스** 개체는 BD96C556-65A3-11D0-983A-00C04FC29E36입니다.  
  
 **스페이스** 개체는 스크립팅에 안전 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [DataSpace 개체(RDS) 속성, 메서드 및 이벤트](./dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [DataSpace 개체 및 CreateObject 메서드 예제(VBScript)](./dataspace-object-and-createobject-method-example-vbscript.md)