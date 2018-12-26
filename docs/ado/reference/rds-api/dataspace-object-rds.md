---
title: DataSpace 개체 (RDS) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d75a5dcd8a09388c031e4e01c8bb8b9c1d62bb80
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600563"
---
# <a name="dataspace-object-rds"></a>DataSpace 개체(RDS)
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 클라이언트 쪽 프록시 중간 계층에 있는 사용자 지정 비즈니스 개체를 만듭니다.  
  
 원격 데이터 서비스 클라이언트 쪽 구성 요소는 중간 계층에 있는 비즈니스 개체를 사용 하 여 통신할 수 있도록 비즈니스 개체 프록시가 필요 합니다. 패키징, 패키징하고 및 전송 (마샬링) 응용 프로그램의 프록시 용이 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 프로세스 또는 컴퓨터 경계를 넘어 데이터입니다.  
  
 원격 데이터 서비스에서 사용 하 여 **rds. DataSpace** 개체의 [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) 비즈니스 개체 프록시를 만드는 방법. 중간 계층 비즈니스 개체의 인스턴스를 만들 때마다 해당 비즈니스 개체 프록시 동적으로 만들어집니다. 원격 데이터 서비스는 다음 프로토콜을 지원 합니다: HTTP, HTTPS (HTTP Secure Sockets), DCOM 및 in-process (클라이언트 구성 요소와 동일한 컴퓨터에 있는 비즈니스 개체).  
  
> [!NOTE]
>  RDS "상태 비저장" 방식으로 동작 하는 경우를 **rds. DataSpace** 개체는 HTTP 또는 HTTPS 프로토콜을 사용 합니다. 즉, 클라이언트 요청에 대 한 내부 정보는 서버 응답을 반환 된 후 삭제 됩니다.  
  
> [!NOTE]
>  비즈니스 개체는 비즈니스 개체 프록시의 수명 동안 존재으로 나타나지만, 비즈니스 개체 요청에 응답을 전송 될 때까지만 실제로 존재 합니다. 요청이 실행 되는 경우 (즉,는 메서드가 호출 되는 비즈니스 개체에서) 프록시 서버에 새 연결을 열고 서버 비즈니스 개체의 새 인스턴스를 만듭니다. 비즈니스 개체는 요청에 응답 한 후 서버는 비즈니스 개체를 제거 하 고 연결을 닫습니다.  
  
> [!NOTE]
>  이 동작은 데이터 요청에서을 사용 하 여 다른 비즈니스 개체 속성 또는 변수를 전달할 수 없습니다. 상태 데이터를 유지 하는 메서드 인수를 파일 등의 다른 메커니즘을 사용 해야 합니다.  
  
 에 대 한 클래스 ID를 **rds. DataSpace** 개체가 BD96C556-65A3-11 D 0 983A 00C04FC29E36 합니다.  
  
 합니다 **DataSpace** 개체가 스크립팅 작업에 안전 합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [DataSpace 개체(RDS) 속성, 메서드 및 이벤트](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [DataSpace 개체 및 CreateObject 메서드 예제(VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


