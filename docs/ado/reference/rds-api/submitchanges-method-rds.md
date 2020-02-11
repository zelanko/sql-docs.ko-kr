---
title: SubmitChanges 메서드 (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SubmitChanges method [ADO]
ms.assetid: 250062a4-13c4-4bed-807d-8b9ad81536d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 783ad55a2355759f7625d536272f5243cd1c61c4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67963284"
---
# <a name="submitchanges-method-rds"></a>SubmitChanges 메서드(RDS)
로컬에서 캐시 하 고 업데이트할 수 있는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 의 보류 중인 변경 내용을 [Connect](../../../ado/reference/rds-api/connect-property-rds.md) 속성 또는 [URL](../../../ado/reference/rds-api/url-property-rds.md) 속성에 지정 된 데이터 원본에 전송 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 [. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 *DataFactory*  
 DataFactory 개체를 나타내는 개체 변수 [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) .  
  
 *연결*  
 RDS를 사용 하 여 만든 연결을 나타내는 **문자열** 값입니다 **. DataControl** 개체의 [Connect](../../../ado/reference/rds-api/connect-property-rds.md) 속성입니다.  
  
 *레코드 집합*  
 **레코드 집합** 개체를 나타내는 개체 변수입니다.  
  
## <a name="remarks"></a>설명  
 RDS와 함께 **SubmitChanges** 메서드를 사용 하려면 먼저 [Connect](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md)및 [SQL](../../../ado/reference/rds-api/sql-property.md) 속성을 설정 해야 합니다 **. DataControl** 개체입니다.  
  
 동일한 **레코드 집합** 개체에 대해 **SubmitChanges** 를 호출한 후에 [cancelupdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) 메서드를 호출 하면 변경 내용이 이미 커밋 되었으므로 **cancelupdate** 호출이 실패 합니다.  
  
 변경 된 레코드만 수정 하기 위해 전송 되 고 모든 변경 내용이 성공 하거나 모든 변경 내용이 함께 실패 합니다.  
  
 **SubmitChanges** 는 기본 **RDSServer DataFactory** 개체에만 사용할 수 있습니다. 사용자 지정 비즈니스 개체는이 메서드를 사용할 수 없습니다.  
  
 **Url** 속성이 설정 된 경우 **SubmitChanges** 는 url로 지정 된 위치에 변경 내용을 전송 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>참고 항목  
 [SubmitChanges 메서드 예제 (VBScript)](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [주소록 명령 단추](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate 메서드 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh 메서드(RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)



