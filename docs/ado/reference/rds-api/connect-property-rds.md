---
title: Connect 속성 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba8b5aa1f59fbb161da878f5930f83d2f6ff0bdd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964560"
---
# <a name="connect-property-rds"></a>Connect 속성(RDS)
쿼리 및 업데이트 작업이 실행 되는 데이터베이스 이름을 나타냅니다.  
  
 RDS에서 디자인 타임에 **연결** 속성을 설정할 수 있습니다 [. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 개체 태그 또는 런타임에 스크립팅 코드에서 (예를 들어 VBScript)  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectionString*  
 올바른 연결 문자열입니다. 연결 문자열에 대 한 일반적인 정보는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성 또는 공급자 설명서를 참조 하세요.  
  
> [!NOTE]
>  MS 원격을 RDS 공급자로 지정 **합니다. DataControl** 은 4 계층 시나리오를 만듭니다. 3 계층 이상으로 이루어진 시나리오는 테스트 되지 않았으므로 필요 하지 않습니다.  
  
 *DataControl*  
 RDS를 나타내는 개체 변수입니다 **. DataControl** 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>참고 항목  
 [Connect 속성 예제 (VBScript)](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [Query 메서드 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh 메서드 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 메서드(RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


