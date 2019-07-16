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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964560"
---
# <a name="connect-property-rds"></a>Connect 속성(RDS)
쿼리 및 업데이트 작업을 실행할 데이터베이스 이름을 나타냅니다.  
  
 설정할 수 있습니다 합니다 **Connect** 에서 디자인 타임에 속성을 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 OBJECT 태그 또는 코드 (예: VBScript) 스크립트에서 런타임 시.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectionString*  
 유효한 연결 문자열입니다. 연결 문자열에 대 한 자세한 내용은 참조는 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) 속성 또는 공급자 설명서.  
  
> [!NOTE]
>  MS 원격에 대 한 공급자를 지정 하는 **rds. DataControl** 는 4 계층 시나리오를 만듭니다. 시나리오 3 계층 보다 큰 테스트 하지 않은 하 고 필요 하지 않습니다.  
  
 *DataControl*  
 나타내는 개체 변수는 **rds. DataControl** 개체입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [Connect 속성 예제 (VBScript)](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [Query 메서드 (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh 메서드 (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges 메서드(RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


