---
description: Refresh 메서드(RDS)
title: Refresh 메서드 (RDS) | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
author: rothja
ms.author: jroth
ms.openlocfilehash: bf89101c070b883fe33cf1b4065f732f2c305943
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88981324"
---
# <a name="refresh-method-rds"></a>Refresh 메서드(RDS)
[Connect](./connect-property-rds.md) 속성에 지정 된 데이터 원본을 쿼리하고 쿼리 결과를 업데이트 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>매개 변수  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 [. DataControl](./datacontrol-object-rds.md) 개체입니다.  
  
## <a name="remarks"></a>설명  
 **Refresh** 메서드를 사용 하기 전에 [Connect](./connect-property-rds.md), [Server](./server-property-rds.md)및 [SQL](./sql-property.md) 속성을 설정 해야 합니다. RDS와 연결 된 폼의 모든 데이터 바인딩된 컨트롤 **입니다. DataControl** 개체는 새 레코드 집합을 반영 합니다. 기존의 모든 [레코드 집합](../ado-api/recordset-object-ado.md) 개체는 해제 되 고 저장 되지 않은 변경 내용은 모두 삭제 됩니다. **Refresh** 메서드는 첫 번째 레코드를 현재 레코드로 자동으로 만듭니다.  
  
 데이터를 사용할 때 **Refresh** 메서드를 주기적으로 호출 하는 것이 좋습니다. 데이터를 검색 한 후 클라이언트 컴퓨터에 저장 하는 경우 최신 상태가 아닐 수 있습니다. 다른 사용자가 레코드를 변경 하 고 변경 내용을 제출 했을 수 있으므로 변경한 내용이 실패할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [Refresh 메서드 예제 (VB)](../ado-api/refresh-method-example-vb.md)   
 [Refresh 메서드 예제 (VBScript)](./refresh-method-example-vbscript.md)   
 [주소록 명령 단추](../../guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate 메서드 (RDS)](./cancelupdate-method-rds.md)   
 [Refresh 메서드 (ADO)](../ado-api/refresh-method-ado.md)   
 [SubmitChanges 메서드(RDS)](./submitchanges-method-rds.md)