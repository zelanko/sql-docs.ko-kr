---
title: "연결 속성 (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb6a9a33267b70f83eb9a3c559ec24e5e1427af7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="connect-property-rds"></a>속성 (RDS) 연결
쿼리 및 업데이트 작업은 실행 하는 데이터베이스 이름을 나타냅니다.  
  
 설정할 수 있습니다는 **연결** 에서 디자인 타임에 속성의 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 개체 태그 또는 런타임에 코드 (예를 들어 VBScript) 스크립트를 작성할 수 있습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>매개 변수  
 *연결 문자열*  
 유효한 연결 문자열입니다. 연결 문자열에 대 한 자세한 내용은 참조는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성 또는 공급자 설명서입니다.  
  
> [!NOTE]
>  에 대 한 공급자도 MS 원격을 지정 하는 **.rds입니다 DataControl** 4 계층 시나리오를 만듭니다. 시나리오 3 단계 이상의 테스트 하지 않은 및 필요 하지 않습니다.  
  
 *DataControl*  
 개체 변수를 나타내는 **.rds입니다 DataControl** 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목:  
 [연결 속성 (VBScript) 예제](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [Query 메서드 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh (RDS) 메서드](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 메서드(RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


