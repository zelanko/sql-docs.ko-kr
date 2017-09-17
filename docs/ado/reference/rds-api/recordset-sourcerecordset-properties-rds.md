---
title: "레코드 집합 SourceRecordset 속성 (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2c5ce9fc2ef297c44f4bcfb3868168d0cb1dda15
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="recordset-sourcerecordset-properties-rds"></a>SourceRecordset 속성 (RDS) 레코드 집합
나타냅니다는 **레코드 집합** 사용자 지정 비즈니스 개체에서 반환 된 개체입니다.  
  
 **적용 대상:** [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 개체 변수를 나타내는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 *레코드 집합*  
 개체 변수를 나타내는 **레코드 집합** 개체입니다.  
  
## <a name="remarks"></a>주의  
 설정할 수 있습니다는 **SourceRecordset** 속성을 한 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 에서 사용자 지정 비즈니스 개체를 반환 합니다.  
  
 이러한 속성 사용자 지정 프로세스를 사용 하 여 바인딩 프로세스를 처리 하는 응용 프로그램을 사용 합니다. 에 래핑된 행 집합을 받게는 **레코드 집합** 와 직접 상호 작용할 수 있도록는 **레코드 집합**, 속성 설정 등의 작업을 수행 하거나을 반복 하는 **레코드 집합 **.  
  
 설정할 수 있습니다는 **SourceRecordset** 속성 또는 읽기는 **레코드 집합** 스크립트 코드에서 런타임 시 속성입니다.  
  
 **SourceRecordset** 달리은 쓰기 전용 속성은 **레코드 집합** 속성은 읽기 전용 속성입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목:  
 [레코드 집합 및 SourceRecordset 속성 예 (VBScript)](../../../ado/reference/rds-api/recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [CreateRecordset 메서드 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [Query 메서드(RDS)](../../../ado/reference/rds-api/query-method-rds.md)



