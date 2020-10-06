---
description: SQL 속성
title: SQL 속성 | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
author: rothja
ms.author: jroth
ms.openlocfilehash: 325f739e55bcb2b7d3e7440e9906fad341c01078
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724199"
---
# <a name="sql-property"></a>SQL 속성
[레코드 집합](../ado-api/recordset-object-ado.md)을 검색 하는 데 사용 되는 쿼리 문자열을 나타냅니다.  
  
 RDS에서 디자인 타임에 **SQL** 속성을 설정할 수 있습니다 [. DataControl](./datacontrol-object-rds.md) 개체의 개체 태그 또는 런타임 시 스크립팅 코드  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>매개 변수  
 *문자열*  
 유효한 SQL 데이터 요청을 포함 하는 **문자열** 값입니다.  
  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 **. DataControl** 개체입니다.  
  
## <a name="remarks"></a>설명  
 일반적으로이는와 같은 SQL 문입니다 (데이터베이스 서버 언어 사용) `"Select * from NewTitles"` . 레코드가 일치 하 고 정확 하 게 업데이트 되도록 하려면 긴 이진 필드 또는 계산 필드 이외의 필드를 업데이트할 수 있는 쿼리에 포함 해야 합니다.  
  
 사용자 지정 서버 쪽 비즈니스 개체가 클라이언트의 데이터를 검색 하는 경우 **SQL** 속성은 선택 사항입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL 속성 예제 (VBScript)](./sql-property-example-vbscript.md)   
 [Connect 속성 (RDS)](./connect-property-rds.md)   
 [Query 메서드 (RDS)](./query-method-rds.md)   
 [Refresh 메서드 (RDS)](./refresh-method-rds.md)   
 [SubmitChanges 메서드(RDS)](./submitchanges-method-rds.md)