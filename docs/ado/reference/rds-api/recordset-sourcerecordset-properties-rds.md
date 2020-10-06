---
description: Recordset, SourceRecordset 속성(RDS)
title: 레코드 집합, SourceRecordset 속성 (RDS) | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
author: rothja
ms.author: jroth
ms.openlocfilehash: cdf8a894341343fee7576daed45c75a46857b909
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724300"
---
# <a name="recordset-sourcerecordset-properties-rds"></a>Recordset, SourceRecordset 속성(RDS)
사용자 지정 비즈니스 개체에서 반환 된 **레코드 집합** 개체를 나타냅니다.  
  
 **적용 대상:** [DATACONTROL 개체 (RDS)](./datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 [. DataControl](./datacontrol-object-rds.md) 개체입니다.  
  
 *레코드 집합*  
 **레코드 집합** 개체를 나타내는 개체 변수입니다.  
  
## <a name="remarks"></a>설명  
 사용자 지정 비즈니스 개체에서 반환 된 [레코드 집합](../ado-api/recordset-object-ado.md) 으로 **SourceRecordset** 속성을 설정할 수 있습니다.  
  
 이러한 속성을 통해 응용 프로그램은 사용자 지정 프로세스를 통해 바인딩 프로세스를 처리할 수 있습니다. 레코드 집합에 래핑된 행 집합을 받습니다 **. 그러면 레코드** 집합과 직접 상호 작용 하 여 속성 **설정,** **레코드 집합**반복 등의 작업을 수행할 수 있습니다.  
  
 **SourceRecordset** 속성을 설정 하거나 런타임에 스크립트 코드에서 **레코드 집합** 속성을 읽을 수 있습니다.  
  
 **SourceRecordset** 는 읽기 전용 속성인 **레코드 집합** 속성과 달리 쓰기 전용 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [레코드 집합 및 SourceRecordset 속성 예제 (VBScript)](./recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [CreateRecordset 메서드 (RDS)](./createrecordset-method-rds.md)   
 [Query 메서드(RDS)](./query-method-rds.md)